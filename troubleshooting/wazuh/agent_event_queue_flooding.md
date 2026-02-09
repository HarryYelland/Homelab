## Wazuh Agent Event Queue Flooding

**Problem:**  
Receiving Level 12 alerts for *"Agent event queue is flooded"* on macOS agent, indicating events were being generated faster than the agent could process them.

### Investigation
- Checked `queue_size` settings in `/var/ossec/etc/ossec.conf` on both manager and agent.
- Manager had `queue_size` set to `131072` (already configured to sufficient size).
- Issue was on the agent side where default `events_per_second` (500) was insufficient for macOS unified log volume.
- Additionally discovered File Integrity Monitoring had hit the 100,000 file limit.

### Root Cause
macOS unified logging generates extremely verbose logs, overwhelming the default agent buffer configuration.  
The agent was also monitoring too many files via File Integrity Monitoring.

### Solution

**Modified agent `client_buffer` configuration:**
```xml
<client_buffer>
  <disabled>no</disabled>
  <queue_size>50000</queue_size>
  <events_per_second>2000</events_per_second>
</client_buffer>
```
**Adjusted file monitoring limits to prevent saturation:**
```xml
<syscheck>
  <max_files_per_second>100</max_files_per_second>
  <file_limit>
    <enabled>yes</enabled>
    <entries>200000</entries>
  </file_limit>
</syscheck>
```
**Filtered macOS logs to only capture security-relevant events:**
```xml
<localfile>
  <log_format>macos</log_format>
  <location>macos</location>
  <query type="log,activity" level="default">
    process == "loginwindow" OR
    process == "sudo" OR
    process == "su" OR
    eventMessage CONTAINS "authentication"
  </query>
</localfile>
```

### Outcome
Queue flooding alerts stopped, agent performance stabilised and only security-relevant macOS events were forwarded to the manager.
