# Cybersecurity Home Lab
My Cybersecurity Homelab Documentation &amp; Testing on a single server utilising open-source tools to emulate basic SOC activities (such as security monitoring, threat detection and incident response).

## Project Overview
This home lab has turned a previously media, file-hosting and game hosting server machine into a cybersecurity piece for me to build my practical skills, implementing defense-in-depth architecture across network, application and endpoint layers.

**Primary Goal**: Develop hands-on security skills aligned with SOC and enterprise-level security practices, whilst creating a portfolio-worthy demonstration of enterprise security capabilities.

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
│   └── architecture_map.txt
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
│       ├── lynis_hardening_audits.md
│       └── openvas_network_vulnerability_scanning.md
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
├── testing/
│   ├── auth/
│   │   └── ssh_test.md
│   │
│   └── malware/
│       └── eicar_test.md
│
│
└── misc/
    ├── why_casaos_and_docker.md
    └── why_dietpi_os.md
```

## Future Enhancements & Considerations

- **SOAR Integration**: For automated response workflows
- **Threat Intelligence**: For IOC correlation
- **Network Traffic Analysis**: Via IDS/IPS deployment
- **Honeypot**: For attacker profiling

*Last Updated: February 2026*
