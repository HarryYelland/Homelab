# Privilege Escalation & User Creation Detection Test

## Objective

Validate that privileged account activity (user creation and deletion) is logged and parsed by Wazuh.
This test simulates privileged administrative activity that could indicate:
- Legitimate system administration
- Persistence mechanism by an attacker
- Post-compromise privilege escalation

---

## Why This Matters
Creating a new local account is a common attacker persistence technique, in MITRE ATT&CK terms, this maps to both T1136 – Create Account and T1078 – Valid Accounts Privilege Escalation & Persistence
If an attacker gains root access, creating a hidden administrative account is a common next step.

---

## Step 1 – Simulate Privileged Account Creation

<img src="/img/user_creation.png" />

Using elevated priveleges I created a new account.

```bash
sudo useradd testuser
sudo userdel testuser
```

This action should be flagged as it, not only requires elevated privileges, but also modifies the system account database.

---

## Step 2 – Verify Wazuh Detection

Wazuh successfully parsed and generated the following alert:

<img src="/img/wazuh_user_creation.png" />

As per the alert, Wazuh assigned level 8 indicating a high-severity security event that requires review and potentially malicious administrative activity (appropriate scoring).

---

## Conclusion 
The simulated privileged account creation was accurately detected by Wazuh and provided a high-severity alert as expected.
This validates the homelab’s ability to detect potential privilege escalation and persistence activity at the host level.

---

## Related MITRE Techniques To This Test

| Technique | ID | Tactic |
|------------|-----|--------|
| Create Account | T1136 | Persistence |
| Valid Accounts | T1078 | Persistence / Privilege Escalation |
| Account Manipulation | T1098 | Persistence |
