Security Report ID: SRID-2024-6
=========================================================

- Reported by: Shubham Deshmukh
- Report date: 2024-09-03
- Last modification date: 2024-11-02
- Version: 1.0
- Impact: Negligible (0/3)
- Probability: Negligible (0/3)
- Status: `duplicate`

Changelog:

- **v1.0** (latest) @ 2024-11-02. First response to the expert.

Report description
---------------------------------------------------------

The author sent an email using the standard procedures confirming that felixbrezo.com was vulnerable to LUCKY13 (CVE-2013-0169) attack. Findings include:

- Affected Protocols: The site felixbrezo.com supports TLS protocols with versions that do not sufficiently mitigate the LUCKY13 attack.
- Supported Protocols and Cipher Suites: TLSv1.0 and TLSv1.1 were found to be enabled, both of which are vulnerable to LUCKY13 in CBC mode. Disabling these older protocols in favor of TLSv1.2 and TLSv1.3 significantly reduces the risk of exposure to this vulnerability.

The LUCKY13 vulnerability poses a risk to data confidentiality and security, particularly for sessions requiring the highest levels of privacy.
Attackers leveraging this vulnerability can potentially decrypt session data and gain access to sensitive information exchanged over secure sessions.

Technical discussion
---------------------------------------------------------

The alleged potential exploitation is linked to the standard deployment of Certbot's certificate chains. This issue is addressed by rejecting the usage of TLSv1.0 or TLSv1.1.

Final remarks
---------------------------------------------------------

This issue is related to srid-2024-8 and is fixed by enforcing TLSv1.2+ as recommended there.
