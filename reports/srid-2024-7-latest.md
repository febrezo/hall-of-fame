Security Report ID: SRID-2024-7
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

The author sent an email using the standard procedures confirming that felixbrezo.com was vulnerable to the BEAST (CVE-2011-3389) attack. This vulnerability was due to the use of outdated TLS configurations, specifically TLS 1.0, which uses predictable Initialization Vectors (IV) in Cipher Block Chaining (CBC) mode ciphers. The use of ECDHE-ECDSA-AES128-SHA and ECDHE-ECDSA-AES256-SHA cipher suites further exposed the system to cryptographic risks.

Technical discussion
---------------------------------------------------------

The alleged potential exploitation is linked to the standard deployment of Certbot's certificate chains. This issue is addressed by rejecting the usage of TLSv1.0 or TLSv1.1.

Final remarks
---------------------------------------------------------

This issue is related to srid-2024-8 and is fixed by enforcing TLSv1.2+ as recommended there.
