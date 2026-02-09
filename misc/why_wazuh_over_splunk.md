# Why Wazuh Over Splunk

This document explains the rationale for selecting **Wazuh** as the SIEM platform for this homelab instead of **Splunk**.

The goal was not to determine which product is *better* in absolute terms, but to select the platform that best aligned with:
- The project’s learning objectives
- Resource constraints of a single-server homelab
- Realistic SOC-style workflows
- Open, inspectable security tooling
- Maintaining zero costs

---

## Why Not Splunk

Splunk is an industry-leading SIEM and analytics platform. However, it was not selected for the following reasons:

- Splunk’s free tier imposes strict daily ingestion limits, which conflict with verbose security telemetry, continuous experimentation and testing and long-term log retention.
- Whilst Splunk supports advanced searches and detections, visibility into *how* detections are generated was prioritised over using black-box analytics.
- Splunk’s performance profile is better suited to more dedicated infrastructure, multi-node deployments and commercial environments.

## Why Wazuh Was Selected
Wazuh is fully open-source, allowing:
- Inspection of detection rules
- Custom rule creation and tuning

This aligns well with a learning-focused environment where understanding why an alert fired is as important as the alert itself.

---

### Integrated Security Capabilities

Wazuh combines multiple security functions natively, including:
- Log aggregation and analysis
- File integrity monitoring
- Vulnerability detection (optional)
- Rootkit and policy checks
- Active response

Wazuh integrates naturally with:
- auditd
- syslog / rsyslog
- Fail2ban
- Firewall logs
- Endpoint agents on Linux, Windows, and macOS

Wazuh can operate effectively in:
- Single-node deployments
- Low-to-moderate resource environments
- Containerised setups

## Trade-Offs Acknowledged

Choosing Wazuh does involve trade-offs:

- Less powerful ad-hoc analytics compared to Splunk
- Fewer third-party apps and integrations
- Smaller commercial ecosystem

These limitations were accepted in favour of greater control.
For a self-hosted, security-focused homelab intended as a learning and portfolio platform, Wazuh represents the most appropriate architectural choice.

