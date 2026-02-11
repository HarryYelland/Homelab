# Squid Proxy Enforcement Test

## Objective

Validate that outbound web traffic from a client device is correctly routed through the Squid proxy and that requests are logged as expected.

This test confirms:
- Client proxy configuration is active
- Squid is handling HTTPS CONNECT requests
- Application-layer visibility is established & logging is functioning correctly
- Downstream inspection capabilities (C-ICAP / ClamAV / YARA) have a valid traffic path

---

## Test Environment

- **Client:** Firefox on MacOS
- **Proxy Extension:** FoxyProxy
- **Test Domain:** `https://example.com`

---

## Step 1 - Enable Proxy Configuration

By default I already have the FoxyProxy extension enabled on Firefox and configured to use the `DietPi-Squid` profile.

<img src="/img/squid_foxyproxy_config.png" width=30%/>

This ensures all browser traffic is forced through the proxy rather than directly to the internet.

---

## Step 2 – Generate HTTPS Traffic

The client browser navigated to: https://example.com
<img src="/img/squid_example_connection.png" />

The page loaded successfully, confirming proxy forwarding hasn't caused loading issues.

## Step 3 – Verify Squid Log Entries

On the DietPi server, Squid logs were inspected through looking at the tail of the access.log

```bash
sudo tail -n 50 /var/log/squid/access.log
```

<img src="/img/squid_test_logging.png" />

The log confirms Squid has visibility into:
- Client source IP
- Destination domain
- Full URL path
- HTTP method
- Response status
- Upstream IP address
- Content type

## Conclusion 
This test confirms that proxy enforcement is working, HTTPS traffic is correctly handled, full request metadata is logged for SIEM ingestion and the traffic path required for inline malware scanning is functioning correctly.

The Squid proxy is therefore successful in intercepting and logging outbound HTTPS traffic from the client, providing me with web inspection capabilities.

### Accepted Constraints
Due to the homelab not being 100% online/available (due to running costs etc.), I use the foxyproxy extension to provide quick proxy switching (between squid when the homelab is online and no proxy when offline).
In a more dedicated environment, the proxy would ideally be configured at the host's system level to avoid potential issues with human-error/bypassing.

