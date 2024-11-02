Security Report ID: SRID-2024-3
===============================

- Reported by: Parth Narula
- Report date: 2024-08-07
- Last modification date: 2024-11-02
- Version: 1.1
- Impact: Low (1/3)
- Probability: Low (1/3)
- Status: `fixed`
- Recognition: Apart from the publication of this report, inclusion in the [Hall of Fame](https://felixbrezo.com/hall-of-fame.txt) and explicit mention in personal social network's @ Mastodon (pending of confirmation by the reporter).

Changelog:

- **v1.1** (latest) @ 2024-11-02. Add reporter name.
- **v1.0** (latest) @ 2024-08-18. First response to the expert.

Report description
---------------------------------------------------------

The website located at https://felixbrezo.com/ is vulnerable to clickjacking.
Additionally, the website lacks Content Security Policy (CSP) headers, which increases the risk of various attacks, including clickjacking.

### Steps to Reproduce:

1. Visit the URL https://felixbrezo.com/ in a web browser.

2. Load the vulnerable page in an iframe within a malicious website controlled by the attacker.

3. Overlay deceptive elements or transparent layers over the login form to trick users into clicking on unintended actions.

4. Capture the user's login credentials or perform unintended actions on their behalf.

### Impact:

- Clickjacking: Allows attackers to trick users into unknowingly performing actions they did not intend. Can lead to unauthorized access to user accounts, theft of sensitive information (such as login credentials), or manipulation of user interactions.
- Missing CSP: Increases the website's susceptibility to various attacks, including clickjacking, cross-site scripting (XSS), and data injection attacks. Fails to enforce security policies that mitigate the risks associated with loading content from untrusted sources or executing inline scripts.

### Remediation Steps:

1. Clickjacking Mitigation:
    - Implement the X-Frame-Options header with the value DENY or SAMEORIGIN to prevent the vulnerable page from being loaded within an iframe on other domains.
    - Consider implementing the Content-Security-Policy (CSP) frame-ancestors directive to further mitigate clickjacking risks.

2. Content Security Policy (CSP):
    - Develop and deploy a comprehensive CSP tailored to the website's specific requirements.
    - Include directives such as default-src, script-src, frame-src, and object-src to restrict the sources from which various types of content can be loaded.
    - Enforce strict policies to prevent inline scripts and evaluate the necessity of allowing unsafe inline styles.

Technical discussion
---------------------------------------------------------

Mitigation of the clickjacking has been implemented by adding a specific directive:

```
add_header X-Frame-Options "DENY";
```

Being true that a Content Security Policy helps mitigate a variety of attacks, including clickjacking, cross-site scripting (XSS), and data injection attacks, a basic CSP has been implemented with a new directive.

```
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none'; frame-ancestors 'self'; base-uri 'self';";
```

Final remarks
---------------------------------------------------------

Although clickjacking is not an issue in the fully static website that the website is right now, it's accepted that the policies were not properly configured. Both measures have been implemented in any way.
