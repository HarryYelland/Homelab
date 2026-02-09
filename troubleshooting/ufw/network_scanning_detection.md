## Network Scanning Detection

**Problem:**  
Running `nmap` port scans against the DietPi server from external hosts did not trigger any Wazuh intrusion detection alerts, despite scans completing successfully.

### Investigation
- Confirmed `nmap` scans were completing successfully and detecting open ports.
- Checked the Wazuh dashboard for port scan detection rules (40000 series) but no alerts were generated.
- Reviewed Wazuh architecture and identified that it primarily monitors log files rather than raw network traffic.
- Checked firewall configuration for logging capabilities.

### Root Cause
Wazuh is a log-based SIEM and does not perform network packet inspection by default.  
Without firewall logs containing connection attempts, Wazuh had no data source to detect scanning activity.

### Solutions Implemented

**Enabled UFW logging to generate connection logs for Wazuh to analyse:**
```bash
sudo ufw logging on
sudo ufw logging high
```

**Configured Wazuh to monitor firewall logs:**
```xml
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/kern.log</location>
</localfile>
```
### Alternative Approach
For proper network-level intrusion detection, integration with tools such as Suricata IDS would be a better architectural solution. Suricata performs deep packet inspection and generates alerts that Wazuh can then correlate with other security events.

### Outcome
Whilst this troubleshooting highlighted an important architectural limitation, enabling high ufw logging mitigated many of the issues.
