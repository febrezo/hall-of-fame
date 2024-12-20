Security Report ID: SRID-2024-4
===============================

- Reported by: Parth Narula 
- Report date: 2024-08-07
- Last modification date: 2024-11-02
- Version: 1.1
- Impact: Negligible (0/3)
- Probability: Low (1/3)
- Status: `fixed`
- Recognition: Apart from the publication of this report, inclusion in the [Hall of Fame](https://felixbrezo.com/hall-of-fame.txt) and explicit mention in personal social network's @ Mastodon (pending of confirmation by the reporter).

Changelog:

- **v1.1** (latest) @ 2024-11-02. Add reporter name.
- **v1.0** @ 2024-08-18. First response to the expert.

Report description
---------------------------------------------------------

There was no "Strict-Transport-Security" header in the server response.

Remediation detail

A Strict-Transport-Security HTTP header should be sent with each HTTPS response. The syntax is as follows:

```
Strict-Transport-Security: max-age=<seconds>[; includeSubDomains]
```

The parameter `max-age` gives the time frame for the requirement of HTTPS in seconds and should be chosen quite high, e.g. several months. A value below 7776000 is considered as too low by this scanner check. The flag `includeSubDomains` defines that the policy applies also for sub domains of the sender of the response.


Technical discussion
---------------------------------------------------------

Confirming that as of 2024-08-18 there was no HSTS header, it has been set a new one for Strict Transport Security.

```
        add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
```

This can now be confirmed:

```
$ curl -I https://felixbrezo.com
HTTP/1.1 200 OK
Date: Sun, 18 Aug 2024 02:21:57 GMT
Content-Type: text/html
Content-Length: 1182
Last-Modified: Wed, 27 Sep 2023 22:16:34 GMT
Connection: keep-alive
ETag: "6514a9c2-49e"
X-Frame-Options: DENY
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'; frame-ancestors 'self'; base-uri 'self';
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Accept-Ranges: bytes
```

Final remarks
---------------------------------------------------------

By implementing HSTS, we can mitigate the risks associated with mixed content, protocol downgrade attacks, and potential man-in-the-middle attacks, thereby increasing the security posture of the website. Although the contents of the website are entirely public it is true that considering that HTTPS SHOULD be the current standard of HTTP connections way before 2024, the issue is considered relevant to be addressed.

Additionally, the website has also been added to the [HSTS preload list](https://hstspreload.org/?domain=felixbrezo.com), adjusting the corresponding Nginx configurations.
