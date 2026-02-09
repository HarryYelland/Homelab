## Foundations & Server Hardening
These foundational steps were taken prior to any software installation in order to build with security, not bolt it on as an afterthought.

### Objective
Establish a secure baseline for the DietPi homelab by hardening access controls, reducing attack surface, enforcing network filtering and implementing basic intrusion prevention prior to deploying any monitoring and detection tooling or further security stack.

---

### Access Control & Identity Hardening
A non-root administrative user was created and granted `sudo` privileges to eliminate direct root usage. This reduced the blast radius of potential compromise and enabled proper privilege separation for administrative actions.
SSH was enabled and validated before any hardening steps were applied to ensure continuity of access. Initial password-based SSH access was used temporarily to bootstrap key/fingerprint based authentication.

---

### Secure Remote Access Configuration

SSH key-based authentication was implemented using modern ED25519 keys, public keys were deployed to the server and validated before disabling basic password authentication.

The SSH daemon was hardened with the following controls:
- Root login disabled
- Password authentication disabled
- Explicit user allow-list enforced
- Authentication attempts limited
- Login timeouts reduced
- Unnecessary forwarding features disabled
- Non-standard SSH port configured

---

### Network Security & Firewall Enforcement

UFW was deployed as the primary host-based firewall with a default-deny inbound policy and explicit allow rules were only created for:
- SSH access over the ZeroTier network
- ZeroTier control traffic
- Required internal service ports

Outbound traffic was permitted by default to avoid disrupting system operations.
Firewall rules were verified post-deployment to ensure continued SSH and service availability and logging was (later) enabled to support SIEM ingestion and intrusion detection.

---

### Intrusion Prevention with Fail2ban

Fail2ban was implemented to provide automated response to brute-force authentication attempts, protecting the SSH using both standard and aggressive jails with:
- Low retry thresholds
- Time-bound bans
- UFW-based enforcement

---

### Outcome
Phase 1 successfully transitioned the server from an exposed, convenience-driven setup to a hardened baseline with:
- Principle-of-least-privilege (PoLP) access
- Encrypted, key-only remote administration
- Reduced external attack surface
- Enforced network filtering
- Automated intrusion prevention
