## Caddy Reverse Proxy SSL Certificate Configuration

**Problem:**  
Caddy serving blank pages when accessing services via `https://subdomain.harryyel.land`, despite successful certificate generation.

### Investigation
- Verified Cloudflare DNS API token was properly configured.
- Confirmed Let’s Encrypt certificates were being generated successfully via DNS-01 challenge.
- Checked that backend services (CasaOS, Immich, Wazuh) were responding on their respective ports.
- Tested DNS resolution and discovered inconsistent behaviour between devices.

### Root Causes Identified

**DNS Resolution**
- Some devices were using router DNS (`192.168.0.1`), which lacked custom entries for `harryyel.land`.
- Other devices were using Pi-hole (`192.168.0.27`), which *did* have the required entries.

**Reverse Proxy Protocol Mismatch**
- Initial configuration attempted HTTPS connections to backend services.
- Backend services were running HTTP only.

**Application-Specific Headers**
- Wazuh Dashboard required specific reverse proxy headers and WebSocket support.

### Solutions

**Configured Pi-hole as primary DNS** on all local devices to ensure consistent domain resolution.

**Corrected Caddyfile to use HTTP for backend connections** (SSL termination at Caddy):
```caddy
harryyel.land {
    tls {
        dns cloudflare {env.CF_API_TOKEN}
    }
    reverse_proxy http://10.244.144.89:90
}

photos.harryyel.land {
    tls {
        dns cloudflare {env.CF_API_TOKEN}
    }
    reverse_proxy http://10.244.144.89:2283
}
```

**Added required headers for Wazuh Dashboard:**
```caddy
wazuh.harryyel.land {
    tls {
        dns cloudflare {env.CF_API_TOKEN}
    }
    reverse_proxy http://10.244.144.89:443 {
        header_up Host {host}
        header_up X-Real-IP {remote_host}
        header_up X-Forwarded-For {remote_host}
        header_up X-Forwarded-Proto {scheme}
    }
}
```

### Outcome
All services accessible via HTTPS with valid certificates and proper SSL termination at the reverse proxy layer.
