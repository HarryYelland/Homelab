## HTTP/HTTPS Inspection with Squid Proxy

### Purpose
Squid was deployed as a forward proxy to provide application-layer visibility and control over outbound web traffic, including encrypted HTTPS sessions.

### Objective
Complements DNS filtering (Pi-Hole) by enabling URL-level inspection, request logging and integration with malware scanning services (ClamAV & C-ICAP).

---

### Proxy Architecture

Squid was configured as an explicit proxy for client devices on the ZeroTier network, as well as caching disabled to prioritise security fidelity over performance and prevent replay or cache poisoning scenarios.

---

### SSL Inspection (SSL Bump)

To enable HTTPS inspection, Squid was configured with SSL Bump using an internally generated certificate authority.
The proxy dynamically generated per-host certificates, allowing encrypted traffic to be decrypted, inspected and re-encrypted transparently to the client.
Modern TLS restrictions were enforced to disable legacy and weak protocols and ciphers.
Client trust was established by manually installing the Squid CA certificate on participating devices.

---

### Access Controls & Scope

Access control lists were defined to:
- Restrict proxy usage to trusted network ranges
- Enforce safe destination ports
- Block unauthorised CONNECT requests

This ensured Squid could not be abused as an open proxy and limited exposure to only intended clients.

---

### Logging & Visibility
Detailed access logging was enabled to capture:
- Client source address
- Requested URL
- HTTP method
- Response status
- User-Agent string
- Request timing

These logs provide insights into outbound web behaviour and form a core data source for detecting:
- Suspicious download activity
- Command-and-control over HTTPS
- Policy violations and anomalous browsing patterns

---

### Outcome

The Squid proxy introduced full application-layer visibility into outbound traffic, including encrypted sessions, creating a controlled inspection point that enabled deeper security controls whilst generating telemetry for later correlation and detection.
