Security Report ID: SRID-2024-8
=========================================================

- Reported by: Shubham Deshmukh
- Report date: 2024-09-03
- Last modification date: 2024-11-02
- Version: 1.0
- Impact: Negligible (0/3)
- Probability: Negligible (0/3)
- Status: `upgrade`

Changelog:

- **v1.0** (latest) @ 2024-11-02. First response to the expert.

Report description
---------------------------------------------------------

The author notifies the deprecated optional usage of TLSv1.0 and TLSv1.1. This was confirmed due to old configuration that still maintaned that.

Technical discussion
---------------------------------------------------------

To mitigate the vulnerabilities, TLS was enforced to be TLSv1.2+:

- **Disabled TLS 1.0 and TLS 1.1**. Support for TLS 1.0 and 1.1 has been removed from the server configurations to prevent legacy protocol vulnerabilities, particularly those targeting predictable Initialization Vectors in CBC mode ciphers.
- **Enforced TLS 1.2 and TLS 1.3**. The server now only supports TLS 1.2 and 1.3 protocols, which provide improved security mechanisms, such as better encryption and integrity checks, effectively eliminating the risk posed by BEAST and similar attacks.

### Considerations

Given that felixbrezo.com functions solely as a landing page with static content and does not collect or process sensitive user data, the risk posed by the BEAST vulnerability was already low. However, disabling outdated protocols and updating cipher suites aligns the website with modern security standards and best practices, ensuring protection against cryptographic attacks regardless of the website’s current usage.

### Impact

These changes, while enhancing security, are expected to have minimal impact on website functionality due to its static nature.
The mitigations do not affect the content served and are compatible with the majority of modern web browsers. As a result, the security posture has been enhanced with negligible operational impact.

Final remarks
---------------------------------------------------------

The reported vulnerability in felixbrezo.com was promptly addressed by updating the TLS configurations to disable legacy protocols and enforcing secure cipher suites.
Although the website serves static content with no user interaction or sensitive data processing, these updates align it with best security practices and help protect against potential threats.
