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
│   └── architecture-map.md
│
├── implementation/
│
├── troubleshooting/
│
├── testing/
│
└── misc/
```

## Future Enhancements & Considerations

- **SOAR Integration**: For automated response workflows
- **Threat Intelligence**: For IOC correlation
- **Network Traffic Analysis**: Via IDS/IPS deployment
- **Honeypot**: For attacker profiling

*Last Updated: February 2026*
