# SSH Invalid Credentials Detection

## Overview
This document details a controlled invalid credentials test using one SSH to validate my DietPi homelab's ability to monitor through syslog and Wazuh SIEM alerting.

**Date:** January 28, 2026
**Test Objective:** Validate invalid credential detection through SIEM alerting.
**Status:** ✅ Pass

---

## Detection flow
1) User attempts to connect to the DietPi machine with invalid credentials via SSH
2) Attempt is noted in syslog
3) Wazuh picks up on log and event logged for SIEM analysis

---

## Incident Timeline

### 1. SSH Invalid Credentials Attempt

![SSH Invalid Attempt](img/SSH_Invalid_Credentials.png)

SSH attempts to connect to the DietPi machine using invalid details.

---

### 2. Wazuh SIEM Alert
**Alert Time:** 2026-01-28T18:46:46.725Z  
**Rule ID:** 5710  
**Severity Level:** 12

![Wazuh SIEM Alert](img/SSH_Invalid_Credentials_Wazuh.png)


---

## Detection Performance
- **Time to Detect:** Immediate (0 seconds)

### Areas for Improvement
N/A

---

## Conclusion

This controlled test successfully validated my home lab's SSH invalid login detection on Wazuh.
