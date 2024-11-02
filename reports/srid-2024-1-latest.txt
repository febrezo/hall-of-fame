Security Report ID: SRID-2024-1
===============================

- Reported by: Parth Narula
- Report date: 2024-08-07
- Last modification date: 2024-11-02
- Version: 1.0
- Impact: Negligible (0/3)
- Probability: Negligible (0/3)
- Status: `wont-fix`

Changelog:

- **v1.1** (latest) @ 2024-11-02. Add reporter name.
- **v1.0** (latest) @ 2024-08-18. First response to the expert.

Report description
---------------------------------------------------------

Upon examining the DNS (Domain Name System) records for the domain felixbrezo.com, it has come to my attention that the MTA-STS record is not properly configured. The MTA-STS mechanism is designed to enforce secure email communication by requiring the use of TLS (Transport Layer Security) encryption. However, in this case, the misconfiguration of the MTA-STS record exposes the email infrastructure to potential security vulnerabilities.

Technical discussion
---------------------------------------------------------

Below you can check the current configuration of the domain as of 2024-08-18 02:00 UTC+2.

```
$ dig felixbrezo.com MX

; <<>> DiG 9.20.0 <<>> felixbrezo.com MX
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14759
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 89d59c3fca159f1b0100000066c139943ca500e9d33602f4 (good)
;; QUESTION SECTION:
;felixbrezo.com. IN MX

;; ANSWER SECTION:
felixbrezo.com. 60 IN MX 10 mail.protonmail.ch.
felixbrezo.com. 60 IN MX 20 mailsec.protonmail.ch.

;; Query time: 30 msec
;; SERVER: 192.168.90.1#53(192.168.90.1) (UDP)
;; WHEN: Sun Aug 18 02:00:08 CEST 2024
;; MSG SIZE  rcvd: 129
```

Based on the output of the `dig` command, it shows that the domain `felixbrezo.com` is correctly configured to use ProtonMail’s mail servers. Here’s a breakdown of the relevant information:

MX Records:
- mail.protonmail.ch with a priority of 10.
- mailsec.protonmail.ch with a priority of 20.

As these MX (Mail Exchange) records indicate the domain’s email is handled by ProtonMail’s servers which is as expected.
The priority values (10 and 20) show the order in which email servers should be used, with the lower number being the primary server.

What this means from a security perspective?

- **Email security**. Since ProtonMail manages these servers, they already enforce the necessary security measures, including TLS encryption, for all incoming and outgoing emails.
- **No immediate need for MTA-STS**. ProtonMail's infrastructure already includes strong security protocols. Therefore, configuring MTA-STS on your domain isn’t necessary because ProtonMail handles these aspects.

Final remarks
---------------------------------------------------------

The current configuration looks correct and secure, given that I'm delegating in ProtonMail for email management. I rely on ProtonMail’s built-in security features without needing to make additional configurations like MTA-STS on the domain.  More information about how Proton deals with this information can be found here.
