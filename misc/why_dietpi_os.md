# DietPi on a Dell Optiplex???

This homelab is built on a **Dell Optiplex 7010 SFF Compact**, repurposed from a general-use Windows 10 server into a **home security lab** designed to emulate SOC tooling and workflows.

<img src="/img/dell_optiplex.jpeg" width=20% />
(My Dell Optiplex that the homelab runs on)

## Context
**Previous role:**
- Windows 10  
- 4 GB DDR3 RAM  (Full specs identical to this: https://www.hardware-corner.net/desktop-models/Dell-OptiPlex-7010-SFF/)
- File hosting, media sharing and game servers

**Current role:**
- DietPi (Debian-based)  
- 16 GB DDR3 RAM  
- Dockerised application stack  
- Security-first architecture

## Why Move Away from Windows 10
I was previously using Windows 10 Home and, whilst I could have implemented security measures, it fell short for what I wanted to achieve:
- Idle memory usage often exceeded **1.5 to 2 GB**, taking away resources that could otherwise be used by my security stack.
- GUI, telemetry and background services increase attack surface
- I wanted to 'brush up' on my linux skills having not used any distro in over a year.
- Finally, for a SOC-oriented environment, the operating system should be minimal, predictable and observable, with Windows often hiding elements wherever possible for easier UX.

---

## Ok, But Why DietPi?
DietPi is a minimal Debian-based distribution designed to maximise performance on constrained hardware.
Designed for being an even lesser-bloated alternative to raspbian for RaspberryPi PCs, DietPi is fully featured whilst utilising minimal system resources, meaning I would not find issues with missing software etc. but I could also maximise the potential resources for security.

### Key Advantages
- Idle RAM usage often under **150 MB** (sometimes even lower!)
- No desktop environment or unnecessary services, especially given I run the homelab in headless mode
- Reduced attack surface by default through only bare minimum services coming pre-installed
- Full control over installed components
- Stable Debian ecosystem with long-term security support

This allows system resources to be allocated to **security tooling**, not the operating system itself.

---

## But You Said You Upgraded The RAM To 16 GB Anyway?
Initially I ran with only 4GB of DDR3, adding system hardening and running C-ICAP analysis through Squid and ClamAV, however given the homelab server still ran personal (media, file, gaming) service hosting, it often started to utilise the majority of its resources still (something that would have still happened far quicker on a Windows 10 Home distro).
Furthermore, I knew I wanted to include more security tools and get a fully-functioning SIEM, therefore this larger security stack would introduce workloads that were fundamentally more memory-intensive than 4 GB could offer me.
One of the most intensive of these new security tools was OpenVAS, a vulnerability scanner that alone could use up to 4 GB of RAM, necessitating the upgrade.

For more information on the memory impact of different aspects see below:

| Component | Memory Impact |
|---------|---------------|
| **Wazuh (SIEM)** | Log indexing, correlation, and alerting rely on memory-heavy search engines |
| **OpenVAS** | Concurrent vulnerability checks require significant RAM during scans |
| **ClamAV + C-ICAP** | Inline malware scanning buffers content in memory |
| **Squid Proxy** | SSL/TLS inspection and caching increase memory pressure |
| **Docker Engine** | Multiple concurrent containers add orchestration overhead |

At 16 GB, the system can:
- Run scans without swapping
- Preserve SIEM responsiveness
- Prevent service disruption/degradation

---

## Security Posture Comparison

| Area | Windows 10 (Before) | DietPi + Docker (Now) |
|----|--------------------|----------------------|
| OS Overhead | High | Minimal |
| Attack Surface | Broad | Narrow |
| Visibility | Limited | Full |
| Update Disruption | Frequent | Controlled |

---

## Summary
Whilst some of the factors that determined my move to DietPi OS included getting more practice with Linux, the most important factors were:
- **building a defensible SOC-style environment on limited hardware**
- **getting the most performance out of a constrained environment**
- **ensuring I could implement a complete security stack that ran simultaneously, not just individual facets**
- **enabling the hosting of previous media-style services alongside the security stack**


This homelab is intentionally designed to prioritise **visibility, isolation, and defensive control** - the same principles expected in a production SOC environment.
