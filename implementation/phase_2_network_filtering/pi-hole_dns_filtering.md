## DNS Filtering with Pi-hole

### Purpose
Pi-hole was implemented as the primary DNS resolver to provide pre-connection threat prevention and centralised visibility into domain-level activity.

### Objective
Block malicious sites *before* any TCP or TLS session is established, reducing exposure and noise for downstream security controls, as well as adding to defense-in-depth.

---

### Deployment Context

Pi-hole was deployed on the DietPi host and designated as the authoritative DNS server for all ZeroTier-connected devices to ensure consistent enforcement regardless of client operating system, with DNS enforcement applied at the network level rather than per-device to avoid reliance on endpoint configuration or user behaviour.

---

### Blocklist Strategy

Security-focused blocklists were selected to prioritise threat prevention over ad-blocking aesthetics. Lists covered:

- Known malware command-and-control domains
- Phishing infrastructure
- Ransomware distribution hosts
- Cryptomining pools
- Tracker and telemetry endpoints

Gravity updates were executed after list ingestion to build a blocking database exceeding hundreds of thousands of domains, ensuring fast, deterministic blocking with minimal false positives.

---

### Network Enforcement

DNS resolution for the network was explicitly configured to use Pi-hole, preventing bypass via alternate resolvers and ensures all queries logged centrally.

Firewall rules were applied to:
- Allow DNS queries from trusted network ranges
- Restrict access to the Pi-hole administrative interface

This ensured DNS was both enforced and observable without exposing management services unnecessarily.

---

### Logging & Telemetry

Pi-hole query logging was left fully enabled to maximise visibility. Logs captured:
- Source IP
- Queried domain
- Block/allow decision
- Timestamp

These logs form a high-value data source for later SIEM correlation, particularly for detecting:
- Beaconing behaviour
- Newly observed malicious domains
- Compromised clients repeatedly querying blocked infrastructure

---

### Outcome

Pi-hole successfully introduced a low-latency, high-signal filtering layer that:
- Blocked malicious destinations before connection
- Reduced load on downstream inspection layers
- Generated structured DNS telemetry for security monitoring
