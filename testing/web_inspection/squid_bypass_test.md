# Squid Proxy Bypass Test

## Objective

Demonstrate that Squid only operates as a proxy when enabled and that traffic is only inspected when the client is configured to use it.
This test validates that Squid does not intercept traffic out of scope and proxy enforcement depends on client configuration and that the loss of proxy configuration results in loss of application-layer visibility.

---

## Test Environment

- **Client:** Firefox on MacOS
- **Proxy Extension:** FoxyProxy
- **Test Domain:** `https://example.com`

---

## Step 1 – Disable Proxy Configuration

The FoxyProxy extension was disabled to remove the explicit proxy configuration from the browser.
<img src="/img/squid_foxy_proxy_config_disabled.png" width=30% />

---

## Step 2 – Generate HTTPS Traffic

The client navigated to: https://example.com
<img src="/img/squid_example_connection.png" />

The page loaded successfully, which confirms that, regardless of the proxy being disabled, direct internet access remains available.

## Step 3 – Inspect Squid Logs

On the DietPi server, Squid logs showed no inspection (via):

```bash
sudo tail -n 50 /var/log/squid/access.log
```

No new log entries corresponding to the request were logged, indicating that the request bypassed Squid entirely.

---

## Related MITRE Techniques To This Test:

| Technique | ID | Tactic |
|------------|-----|--------|
| Impair Defenses | T1562 | Defense Evasion |
| Modify Configuration | T1112 | Defense Evasion |
