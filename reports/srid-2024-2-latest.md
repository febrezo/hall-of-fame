Security Report ID: SRID-2024-2
=========================================================

- Reported by: Parth Narula 
- Report date: 2024-08-07
- Last modification date: 2024-11-02
- Report version: 1.1
- Impact: Low (1/3)
- Probability: Low (1/3)
- Status: `fixed`
- Recognition: Apart from the publication of this report, inclusion in the [Hall of Fame](https://felixbrezo.com/hall-of-fame.txt) and explicit mention in personal social network's @ Mastodon (pending of confirmation by the reporter).

Changelog:

- **v1.1** (latest) @ 2024-11-02. Add reporter name.
- **v1.0** (latest) @ 2024-08-18. First response to the expert.

Report description
---------------------------------------------------------

A potential information disclosure vulnerability has been identified at https://felixbrezo.com/invalid. The server response might include a banner revealing details about the server software, such as:

### Server Software

Name and version of the web server software (nginx/1.14.2 )

### Impact

While the disclosed information might seem trivial, it can be used by attackers in the following ways:

- Targeted Attacks: Knowing the specific server software version can help attackers identify potential vulnerabilities associated with that particular version. They can then exploit those vulnerabilities to launch targeted attacks.
- Planning and Reconnaissance: The disclosed information can aid attackers in planning and reconnaissance activities. They can use it to gather information about the server's environment and potentially discover other vulnerabilities.

### Remediation

The security team should address this information disclosure to minimize potential risks:

- Disable Server Banners**: If possible, disable server banners in the server configuration. This prevents the server from disclosing any unnecessary information in the response headers.
- Security Updates: Maintain up-to-date server software and operating systems to minimize the risk of known vulnerabilities being exploited.
- Waf Consideration (Optional): Consider implementing a Web Application Firewall (WAF) to monitor incoming requests and filter out malicious traffic.

Technical discussion
---------------------------------------------------------

The information disclosure vulnerability could be confirmed as of 2024-08-18 02:35 UTC+2.

```
$ curl -I https://felixbrezo.com/invalid
HTTP/1.1 404 Not Found
Server: nginx/1.14.2
Date: Sun, 18 Aug 2024 01:08:48 GMT
Content-Type: text/html
Content-Length: 169
Connection: keep-alive

$ curl https://felixbrezo.com/invalid
<html>
<head><title>404 Not Found</title></head>
<body bgcolor="white">
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.14.2</center>
</body>
</html>
```

The version of the information disclosure in the `Server` header was fixed by setting the `server_tokens off` directive in the Nginx configuration. 

```
server_tokens off
```

The information disclosure vulnerability was then fixed avoiding revealing information about the software version:

```
$ curl -I https://felixbrezo.com/invalid
HTTP/1.1 404 Not Found
Server: nginx
Date: Sun, 18 Aug 2024 01:11:31 GMT
Content-Type: text/html
Content-Length: 162
Connection: keep-alive

$ curl https://felixbrezo.com/invalid
<html>
<head><title>404 Not Found</title></head>
<body bgcolor="white">
<center><h1>404 Not Found</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

Additionally, to avoid showing even that it is an Nginx server in the headers, the `nginx-extras` package was installed to allow the `more_clear_headers` to be used.

```
more_clear_headers 'Server';
```

This removes the `Server` header.

```
$ curl -I https://felixbrezo.com/invalid
HTTP/1.1 404 Not Found
Date: Sun, 18 Aug 2024 01:12:51 GMT
Content-Type: text/html
Content-Length: 162
Connection: keep-alive
```

However, the fact that the server was an Nginx was also disclosed, so a specific `/404.html` page was created and set in Nginx instead of the default one.

```
        error_page 404 /404.html;
```

Thus:

```
$ curl -I https://felixbrezo.com/invalid
HTTP/1.1 404 Not Found
Date: Sun, 18 Aug 2024 01:34:48 GMT
Content-Type: text/html
Content-Length: 1647
Connection: keep-alive
ETag: "66c14efa-66f"

$ curl https://felixbrezo.com/invalid
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>404 Not Found</title>
...
```

Final remarks
---------------------------------------------------------

Although Nginx was updated to the latest version, it's true that revealing software versions can be used in future scenarios where Nginx has some vulnerabilities.
By masking the information, the server tries not to be the low-hanging-fruit and somewhat hiding potential misconfigurations from being exploited. 
Taking this into account, additional measures have been taken for a more elegant error handling.

Considering the remediations proposed:

- **Disable server banners**. Removed from the Nginx configuration.  ✅ 
- **Security updates**. The software in the server is updated periodically to the latest safe version.  ✅ 
- **Waf consideration**. Not implemented considering the size of the website, but security and error logs are periodically archived for recurrent investigation. 

Additional steps taken:

- Creating a specific 404.html page not to reveal even the type of software used.
