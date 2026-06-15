---
title: pfSense
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: access-control, network, pfsense
isPublished: true
---

# pfSense Network Architecture

pfSense manages the core network routing, DHCP, and DNS for the 10BitWorks physical space.

## Strategy
Consolidating DHCP and DNS onto pfSense eliminates "split-brain" issues and enables identity-to-MAC mapping for physical space tracking.

### Subnets
- **Infrastructure (10.7.1.0/24):** Servers, Switches, Proxies. Static IPs; Can see all networks.
- **IoT / Cameras (10.7.2.0/24):** Cameras, untrusted IoT. Forever-lease DHCP; Local-only (Frigate).
- **Members (10.7.10.0/24):** Laptops, Phones, Tablets. Dynamic DHCP; Internet + 10.7.1.* access.

## Soft Captive Portal
We use a modern OIDC-backed Captive Portal (RFC 8908) to replace RADIUS/WPA2-Enterprise:
1. **Radio Layer:** WPA2-Personal (PSK) using the "wall password."
2. **Discovery:** pfSense broadcasts **DHCP Option 114** pointing to `https://id.10bitworks.org/api/capport`.
3. **Silent Auth:** Modern devices open a background window. If the member is already logged in to [kanidm](/services/hosted/kanidm), the portal auto-authorizes the MAC address instantly.
4. **Persistency:** Successful logins whitelist the MAC for 1 year, ensuring passive presence tracking for dashboards.

