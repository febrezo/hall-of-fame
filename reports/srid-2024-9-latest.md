Security Report ID: SRID-2024-9
=========================================================

- Reported by: Shubham Deshmukh
- Report date: 2024-09-03
- Last modification date: 2024-11-02
- Version: 1.0
- Impact: Negligible (0/3)
- Probability: Negligible (0/3)
- Status: `fixed`

Changelog:

- **v1.0** (latest) @ 2024-11-02. First response to the expert.

Report description
---------------------------------------------------------

The website felixbrezo.com has been evaluated and received a "D" security rating due to the absence of several critical HTTP security headers.
Missing headers include Content-Security-Policy, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, and Permissions-Policy.
Without these headers, the site is vulnerable to various web-based attacks, including cross-site scripting (XSS), clickjacking, MIME type misinterpretation, and information leakage.

Technical discussion
---------------------------------------------------------

HTTP security headers are essential for safeguarding web applications against common attacks. The lack of these headers on felixbrezo.com increases the risk of several known vulnerabilities. Below are the missing headers and their significance:

- Content-Security-Policy (CSP): Without a CSP, the website is exposed to potential XSS attacks since it lacks restrictions on which domains can load resources in the browser. A CSP defines trusted sources for scripts, images, styles, and other resources, preventing unauthorized domains from injecting malicious resources.
- X-Frame-Options: The absence of this header makes the site vulnerable to clickjacking attacks, where an attacker could embed the site within an iframe on another domain, tricking users into unintentionally interacting with hidden elements. Setting X-Frame-Options: DENY or SAMEORIGIN prevents the page from being rendered in iframes on other domains.
- X-Content-Type-Options: Without this header, browsers may perform MIME-type sniffing, potentially misinterpreting files as different MIME types than specified, which could lead to the execution of malicious content. The X-Content-Type-Options: nosniff header ensures that browsers respect the declared MIME type.
- Referrer-Policy: This header controls how much referrer information is shared with requests. Without it, sensitive data could be leaked in URLs, which could result in privacy concerns and information disclosure. Setting a policy such as Referrer-Policy: no-referrer limits the amount of information sent with referrer headers.
- Permissions-Policy: Without this header, browser features such as geolocation, camera, and microphone access are left unregulated. By defining a Permissions-Policy, you can specify which features the browser is allowed to use, reducing the risk of unauthorized access to these features by malicious actors.

Nginx configuration has been updated with:

```
# Security headers to mitigate srid-2024-9
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none';" always;
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "no-referrer" always;
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;
```
With this configuration, the website moved to a Grade A+ Security Headers [website](https://securityheaders.com/?q=felixbrezo.com&followRedirects=on).


Final remarks
---------------------------------------------------------

The addition of these HTTP security headers enhances the protection of felixbrezo.com against XSS, clickjacking, MIME type sniffing, information leakage, and other attacks.
Being a personal website with static content, the exploitable cases are still negligible, but the approrpiate of the headers is, definetely, a best practice.
