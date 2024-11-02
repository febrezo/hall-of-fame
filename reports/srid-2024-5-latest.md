Security Report ID: SRID-2024-5
===============================

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

The author sent an email using the standard procedures confirming that DNSSEC was not activated for the domain.
This information was confirmed using third party tools (such as https://mxtoolbox.com/SuperTool.aspx), prior to this report.

Technical discussion
---------------------------------------------------------

DNSSEC was configured with the domain provider after this report.
The activation can be confirmed using third party tools by filtering for `dnskey:felixbrezo.com` (https://mxtoolbox.com/SuperTool.aspx).

Final remarks
---------------------------------------------------------

Although DNSSEC is recommended for all domains, the impact of the report is very limited considering that the website under felixbrezo.com is only a static website used as a landing page, so the scenarios in which an attacker may compromise the DNS to tirgger further actions is limited.
In any case, I strongly agree with the reporter that implementing DNSSEC is a desirable action to be taken.
The reporter has acknowledged to be mentioned in this report and this will trigger a mention in the `README.md`.
