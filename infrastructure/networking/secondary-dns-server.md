---
title: "Secondary DNS Server"
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: networking, pihole
description: "Secondary Pi-hole DNS server and DHCP lease authority for 10BitWorks."
isPublished: true
---

- Hostname: pihole1
- mDNS: pihole1.local
- IP: 10.7.1.181 (WiFi - DHCP)
- IP: 10.7.1.8 (Ethernet - Static)
- MAC: B8:27:EB:3D:AD:84 (WiFi)
- MAC: B8:27:EB:68:F8:D1 (Ethernet)
- OS: Debian GNU/Linux 12 (bookworm)
- Model: Raspberry Pi 3B+
- Port: 22 (ssh) - Admin Shell
- Port: 53 (domain) - Pi-hole DNS Service
- Port: 80 (http) - Pi-hole Admin Web UI
- Port: 443 (https) - Secure Admin UI
- Port: 19999 (http) - Netdata Monitoring
- Netdata: Streaming to 10.7.1.7 (Parent)

## Role

This Pi-hole instance acts as a secondary DNS server and DHCP lease authority. It manages a separate DHCP pool from the primary DNS server (`dhcp1` at `10.7.1.9`). When verifying dynamic addresses, check leases on both:

```bash
ssh root@10.7.1.9 "cat /etc/pihole/dhcp.leases"
ssh root@10.7.1.8 "cat /etc/pihole/dhcp.leases"
```

## Related

- [Primary DNS & DHCP Server](/infrastructure/networking/primary-dns-dhcp-server)
- [Network Inventory](/infrastructure/network-inventory)
