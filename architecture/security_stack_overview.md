# Security Stack Overview

This homelab implements a defence-in-depth security architecture aligned with SOC workflows.

## Network Layer
- UFW: default-deny firewall with logging
- Fail2ban: adaptive intrusion prevention
- Pi-hole: DNS-level threat blocking

## Application / Content Layer
- Squid proxy with SSL inspection
- C-ICAP + ClamAV for inline malware scanning
- YARA rules for enhanced pattern detection

## Detection & Visibility
- Wazuh SIEM for centralised logging, correlation and alerting

## Assessment & Hardening
- Lynis for host hardening audits
- OpenVAS for network vulnerability scanning
