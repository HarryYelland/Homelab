# Cybersecurity Home Lab

[![SIEM](https://img.shields.io/badge/SIEM-Wazuh-005571?style=for-the-badge&logo=wazuh&logoColor=white)](https://wazuh.com/)
[![Firewall](https://img.shields.io/badge/Firewall-UFW-EF5233?style=for-the-badge&logo=ubuntu&logoColor=white)](https://help.ubuntu.com/community/UFW)
[![IPS](https://img.shields.io/badge/IPS-Fail2ban-D32F2F?style=for-the-badge&logo=security&logoColor=white)](https://github.com/fail2ban/fail2ban)
[![DNS Security](https://img.shields.io/badge/DNS%20Security-Pi--hole-96060C?style=for-the-badge&logo=pihole&logoColor=white)](https://pi-hole.net/)
[![Proxy](https://img.shields.io/badge/Proxy-Squid-000000?style=for-the-badge&logo=squid&logoColor=white)](https://www.squid-cache.org/)
[![Antivirus](https://img.shields.io/badge/Antivirus-ClamAV-FF6B35?style=for-the-badge&logo=clamav&logoColor=white)](https://www.clamav.net/)
[![Vuln Scanning](https://img.shields.io/badge/Vuln%20Scanning-OpenVAS-7FBA00?style=for-the-badge&logo=greenbone&logoColor=white)](https://openvas.org/)
[![Hardening](https://img.shields.io/badge/Hardening-Lynis-4B32C3?style=for-the-badge&logo=linux&logoColor=white)](https://cisofy.com/lynis/)
[![Platform](https://img.shields.io/badge/Platform-DietPi-A80030?style=for-the-badge&logo=linux&logoColor=white)](https://dietpi.com/)
[![Containers](https://img.shields.io/badge/Containers-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![VPN](https://img.shields.io/badge/VPN-ZeroTier-FFB441?style=for-the-badge&logo=zerotier&logoColor=black)](https://www.zerotier.com/)

My Cybersecurity Homelab Documentation &amp; Testing on a single server utilising open-source tools to emulate basic SOC activities (such as security monitoring, threat detection and incident response).

## Project Overview
This home lab has turned a previously media, file-hosting and game hosting server machine into a cybersecurity piece for me to build my practical skills, implementing defense-in-depth architecture across network, application and endpoint layers.

**Primary Goal**: Develop hands-on security skills aligned with SOC and enterprise-level security practices, whilst creating a portfolio-worthy demonstration of enterprise security capabilities.

### What This Lab Is (and Isn’t)

This lab is:
- A (somewhat) realistic SOC-style security environment
- Focused on detection, visibility and response
- Built incrementally with real trade-offs

This lab is not:
- A penetration testing playground
- A simulated enterprise network

## Technology Stack

| Layer | Tool | Purpose |
|-------|------|---------|
| **SIEM** | Wazuh | Centralised log management, correlation, alerting |
| **Firewall** | UFW | Network-layer packet filtering |
| **IPS** | Fail2ban | Adaptive intrusion prevention |
| **DNS Security** | Pi-hole | Malicious domain blocking, DNS filtering |
| **Proxy** | Squid | SSL/TLS inspection, web filtering |
| **Antivirus** | ClamAV + C-ICAP | Inline malware scanning |
| **Vuln Scanning** | OpenVAS | Network vulnerability assessment |
| **Hardening** | Lynis | System security auditing |
| **Platform** | DietPi + Docker | Minimal Linux + container management |
| **VPN** | ZeroTier | Secure remote access |

## Documentation Structure
```
docs/
├── architecture/
│   ├── architecture_map.txt
│   └── data_flow_diagram.md
│   └── security_stack_overview.md
│
│
├── implementation/
│   ├── phase_1_foundations_and_server_hardening/
│   │   └── server_hardening.md
│   │
│   ├── phase_2_network_filtering/
│   │   ├── clamav_icap_malware_detection.md
│   │   ├── pi-hole_dns_filtering.md
│   │   ├── squid_proxy_https_inspection.md
│   │   └── yara_pattern_detection.md
│   │
│   ├── phase_3_siem/
│   │   └── wazuh_siem.md
│   │
│   ├── phase_4_endpoint_protection/
│   │   └── wazuh_agent_endpoint_protection.md
│   │
│   └── phase_5_vulnerability_scanning/
│       ├── lynis_findings_and_improvements.md
│       ├── lynis_hardening_audits.md
│       └── openvas_network_vulnerability_scanning.md
│
│
├── testing/
│   ├── auth/
│   │   └── ssh_test.md
│   │
│   ├── malware/
│   │    └── eicar_test.md
│   │
│   ├── siem/
│   │    └── privilege_escalation_user_creation_test.md
│   │
│   └── web_inspection/
│       ├── squid_bypass_test.md
│       ├── squid_proxy_connectivity_test.md
│       └── squid_ssl_inspection_test.md
│
│
├── troubleshooting/
│   ├── caddy/
│   │   └── caddy_reverse_proxy_ssl_certificate_configuration.md
│   │
│   ├── ufw/
│   │   └── network_scanning_detection.md
│   │
│   └── wazuh/
│       └── agent_event_queue_flooding.md
│
│
└── misc/
    ├── why_casaos_and_docker.md
    └── why_dietpi_os.md
    └── why_wazuh_over_splunk.md
```

## Future Enhancements & Considerations

- **SOAR Integration**: For automated response workflows
- **Threat Intelligence**: For IOC correlation
- **Network Traffic Analysis**: Via IDS/IPS deployment
- **Honeypot**: For attacker profiling

*Last Updated: February 2026*
