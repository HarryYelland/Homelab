# Tool Integration Architecture – Data Flow & Visibility

This document explains how telemetry and enforcement signals flow through the homelab security stack and how those signals become actionable detections inside Wazuh.
The intent is to show **what each tool sees**, **why it sees it**, and **how Wazuh correlates it** into SOC-style alerts.

---

## 1) High-Level Architecture

### Control Planes
- **Enforcement / Prevention**
  - UFW (packet filtering)
  - Fail2ban (adaptive bans)
  - Pi-hole (DNS sinkhole)
  - Squid (proxy control & TLS inspection)
  - C-ICAP, ClamAV & YARA (inline malware scanning)

- **Detection / Visibility**
  - Wazuh SIEM (central log collection, parsing, correlation & alerting)
  - Endpoint agents (Windows/macOS) (host telemetry)

- **Assessment**
  - Lynis (host hardening audits)
  - OpenVAS (network vulnerability scanning)

---

## 2) Network Traffic Flow Through the Stack

### A) DNS Request Path (Pre-Connection Filtering)

1. Endpoint attempts to access a domain (e.g. `example.com`)
2. DNS query is sent to **Pi-hole**
3. Pi-hole filtering:
   - **Allowed** → resolves via upstream DNS and returns IP
   - **Blocked** → returns sinkhole response (connection fails)
This allows for DNS filtering to prevent contact with known malicious infrastructure *before* any TCP/TLS session exists.

---

### B) Web Traffic Path (Application-Layer Visibility)

When a domain is allowed, web traffic flows to Squid:
1. Endpoint sends HTTP/HTTPS traffic to **Squid** (explicit proxy)
2. For HTTPS, Squid performs **SSL/TLS inspection** (SSL bump) to decrypt and inspect content
3. Squid forwards response content to **C-ICAP**
4. C-ICAP passes content to **ClamAV** for scanning & **YARA rule matching** for detection beyond AV signatures:
   - **Clean** → content delivered to client
   - **Malicious** → content blocked and logged
This creates a *secure web gateway* with visibility and prevention for encrypted web traffic.

---

## 3) Log & Telemetry Flow Into Wazuh

Wazuh acts as the **central collection & correlation layer**, ingesting logs from each tool.

### Wazuh Ingestion Map (What feeds the SIEM)

| Data Source | What It Produces | Why It’s Useful | Ingested By Wazuh From |
|---|---|---|---|
| Pi-hole | DNS queries, blocks | Pre-connection threat prevention & beaconing visibility | `/var/log/pihole.log` |
| Squid | URL & request metadata | Full browsing visibility & download context | `/var/log/squid/access.log` |
| C-ICAP | ICAP transactions & blocks | Inline content scanning decisions | `/var/log/c-icap/access.log` |
| ClamAV | Malware detections | High-confidence malicious file indicators | `/var/log/clamav/clamav.log` |
| UFW | Blocked connections | Recon/bruteforce indicators, network enforcement telemetry | `/var/log/ufw.log` |
| Fail2ban | Ban events | Confirmed hostile auth behaviour & automated response signals | `/var/log/fail2ban.log` |
| OS auth | logins, sudo, failures | Account compromise & privilege escalation visibility | `/var/log/auth.log` |
| Endpoints | host telemetry | Process/activity & OS security logs | Agent telemetry via Wazuh |

---
