Security Report ID: SRID-2024-10
=========================================================

- Reported by: AKHIL C.D.
- Report date: 2024-11-04
- Last modification date: 2024-11-13
- Version: 1.0
- Impact: Negligible (0/3)
- Probability: Negligible (0/3)
- Status: `fixed`

Changelog:

- **v1.0** (latest) @ 2024-11-13. First response to the expert.

Report description
---------------------------------------------------------

The reporter informed of the banner of the SSH service being shown by using

```
$ nmap -sT -sV -T4 -O -A -v --script vuln 51.38.32.251
```

SSH banner grabbing is a type of security vulnerability that occurs when an SSH server exposes sensitive information through its banner. This information can be exploited by attackers to gather intelligence about the server's configuration, software versions, and potential vulnerabilities.

Technical discussion
---------------------------------------------------------

In this case and according to RFC 4253, section 4.2 (http://www.openssh.com/txt/rfc4253.txt), this banner is part of the protocol version exchange when it has been exchanged.

> 4.2. Protocol Version Exchange

> When the connection has been established, both sides MUST send an
identification string. This identification string MUST be

> SSH-protoversion-softwareversion SP comments CR LF

Although the impact is in any case very limited and SSH version was up to date with the corresponding security fixes, it is a good recommendation to limit the access to Port 22 just in case apart from using fail2ban tools and so on.

Final remarks
---------------------------------------------------------

Additional measures have taken to hide and mask the software versions used as well as limiting the access of Port 22 to restricted locations.
