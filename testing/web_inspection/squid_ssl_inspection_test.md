# Squid SSL Inspection (Certificate Validation) Test

## Objective
Validate that Squid is performing HTTPS interception (SSL bump) correctly and that the client trusts the Squid Certificate Authority (CA).

---

## Test Environment

- **Client:** Firefox on MacOS
- **Proxy Extension:** FoxyProxy
- **Test Domain:** `https://example.com`

---

## Step 1 – Confirm Proxy Enabled

Ensure FoxyProxy is enabled and traffic is routed through Squid.

<img src="/img/squid_foxyproxy_config.png" width=30%/>

---

## Step 2 – Inspect Certificate in Browser

Host navigates to https://example.com and, as per the certificate information panel, the browser does **not** display a certificate warning.

<img src="/img/squid_ssl_bump.png" />

This confirms:
- Squid intercepted the TLS connection
- Squid generated a dynamic certificate for the requested domain
- The client trusts the Squid CA

## Conclusion
The Squid proxy successfully intercepts and re-signs HTTPS traffic using a trusted local Certificate Authority.

---

## Related MITRE Techniques To This Test:

| Technique | ID | Tactic |
|------------|-----|--------|
| Encrypted Channel | T1573 | Command & Control |
| Web Protocols | T1071.001 | Command & Control |
