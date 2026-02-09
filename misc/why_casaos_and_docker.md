# CasaOS + Docker: Balancing Accessibility and Security

This homelab is intentionally designed to serve **two very different user groups** on the same physical system:
1. **Non-technical household users** who need simple, reliable access to media and files  
2. **Security-focused workloads** that require strict control, visibility and isolation  

To achieve this, the system uses a **hybrid access model**:
- **CasaOS** for usability and accessibility  
- **Standard Docker (CLI-managed)** for controlled services  
- **Bare-metal (host-level) installations** for core security controls 

**Note** - *Given the SSH hardening (such as port changes and fingerprinting) that I have implemented, only my own machines can access the docker CLI-managed services, other users are purely restricted to the CasaOS dashboard*

---

## Design Principle: Tiered Access
The environment is structured around **tiered trust and access levels**:
| Tier | Audience | Characteristics |
|----|--------|----------------|
| Accessible Services | Household users | Simple UI, no system-level access |
| Restricted Services | Administrator only | CLI-managed, hidden from casual users |
| Core Security Controls | System-level | Host-integrated, non-containerised |

---

## CasaOS: Accessibility Without Privilege
CasaOS is used deliberately for services intended for other people in the home.

### Why CasaOS Is Appropriate Here

- **Web-based UI** removes the need for SSH, CLI knowledge or IP management  
- **Application abstraction** allows users to interact with services like media servers or file sharing without understanding Linux  
- **No root access exposure** reducing the risk of accidental misconfiguration  
- **Clear service boundaries** between user-facing apps and the underlying system  

This allows non-technical users to benefit from the homelab **without expanding the system’s threat surface**.

CasaOS is not treated as a security boundary, but as an **accessibility layer**.

---

## Standard Docker: Controlled and Hidden Services
Services that should not be visible or accessible to household users are deployed using **standard Docker via the command line**, not through CasaOS.

### Why These Containers Are Kept Separate

- **Not discoverable via the CasaOS dashboard**
- **No accidental restarts, configuration changes or deletions**
- **Explicit network, volume and resource control**
- **Clear administrative ownership**

## Bare-Metal Security Controls: Installed on the Host
Several security controls are installed **directly on the DietPi host** as this provides stronger guarantees than containerised equivalents.

### Why Some Tools Must Be Bare-Metal

| Tool | Reason for Host-Level Installation |
|----|----------------------------------|
| **UFW** | Firewalls must operate at the kernel level; containerised firewalls can be bypassed by Docker networking |
| **Fail2ban** | Requires direct access to host logs and firewall rule injection |
| **Lynis** | Audits the actual OS, kernel, and configuration - containers cannot see this context |
| **Wazuh Agent** | Needs host-level visibility for file integrity monitoring and rootkit detection |

## Security and Accessibility Trade-off:
By explicitly separating:
- **Who can see what**
- **Who can control what**
- **Which components enforce security**

---

## Summary

- **DietPi** provides a minimal, hardened foundation  
- **Bare-metal security controls** enforce system-wide protection  
- **Standard Docker** hosts restricted or sensitive services  
- **CasaOS** enables safe, user-friendly access for non-technical users  

The result is a single system that supports everyday use **without significantly weakening its defensive posture**, closely reflecting the compromises and design decisions encountered in SOC and infrastructure environments.
