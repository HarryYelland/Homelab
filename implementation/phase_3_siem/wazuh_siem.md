## SIEM Deployment with Wazuh

### Objective
Deploy a centralised SIEM platform capable of ingesting, correlating and alerting on security telemetry generated across the homelab environment.
This phase consolidates logs and detections from the homelab, network filtering stack and security controls implemented in previous phases into a single analytical plane.

---

### SIEM Architecture Overview

The SIEM implementation is built using the Wazuh stack, consisting of three primary components:

- **Wazuh Manager** – log analysis, rule evaluation, correlation and alerting
- **Wazuh Indexer** – OpenSearch-based event storage and indexing
- **Wazuh Dashboard** – visualisation, investigation and alert review interface

All components were deployed in an all-in-one configuration suitable for a constrained homelab environment whilst preserving enterprise-style architecture.

This design provides:
- Real-time detection
- Historical event retention
- Searchable security telemetry
- Rule-based correlation

---

### Network & Access Controls

In phase 2 of implementation, UFW Firewall rules were explicitly defined to allow specified traffic only from trusted network ranges and logging was set to high to enable SIEM picking up on alerts.

This ensured:
- Agents and log sources could communicate reliably
- The dashboard and API were not publicly reachable

---

### Log Source Integration Strategy

Rather than relying solely on endpoint agents, Wazuh was configured to ingest logs directly from telemetry.

Integrated log sources included:
- DNS activity from Pi-hole
- HTTP/HTTPS access logs from Squid
- Malware detections from ClamAV
- Content inspection events from C-ICAP
- Firewall enforcement from UFW
- Intrusion prevention actions from Fail2ban
- Authentication and system activity from the host OS

---

### Detection Engineering

Custom Wazuh rules were created to elevate raw log data into actionable security alerts.

These rules focused on:
- Malware detections and blocked downloads
- Repeated firewall violations
- Brute-force authentication attempts
- Port scanning behaviour inferred from firewall logs
- Enforcement actions taken by security controls

---

### File Integrity Monitoring (FIM)

File Integrity Monitoring was enabled on critical system paths to detect unauthorised changes to binaries, configuration files and web content.

Monitoring scope was selected to balance coverage with noise reduction:
- System binaries and configuration directories were monitored aggressively
- Pseudo-filesystems and volatile paths were excluded
- Real-time monitoring was enabled where appropriate

---

### Validation

The SIEM deployment was validated through:
- Service health verification
- Log ingestion testing
- Controlled security events (blocked malware, firewall drops)

---

### Outcome

Successfully unified the security stack into a functioning SIEM, delivering:

- Centralised visibility across DNS, proxy, malware, firewall and host layers
- Real-time alerting
- Correlated security events rather than isolated logs
