---
title: "Wiki" VM on Zelda (includes NPM and Portainer)
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, zelda-hosted, proxmox, wiki
description: "Proxmox VM 300 on Zelda hosting Wiki.js, Nginx Proxy Manager, and Portainer."
isPublished: true
---

- Hostname: wiki
- mDNS: wiki.local
- IP: 10.7.1.241 (DHCP)
- MAC: BC:24:11:07:9C:2F
- OS: Debian 12 (VM 300 on Zelda)
- Model: Proxmox VM 300
- Port: 80 (http) - Wiki.js
- Port: 443 (https) - Nginx Proxy Manager
- Port: 9443 (https) - Portainer Admin Dashboard

## Services

- **Wiki.js**: The canonical knowledge base at `https://wiki.10bitworks.org`
- **Nginx Proxy Manager**: Reverse proxy and SSL termination for public services
- **Portainer**: Docker management UI for Zelda-hosted containers

## Memory Constraints

Zelda has only **8GB** physical RAM. VM 300 is capped at **2.5GB** to prevent host swapping. Total Zelda memory budgets:

| VM/LXC | Memory Limit |
| :--- | :--- |
| Cameras (105) | 4GB |
| Wiki/NPM (300) | 2.5GB |
| Bookstack (109) | 1GB |
| Pi-hole / Tailscale / Others | 512MB each |

## Related

- [Zelda Server](/infrastructure/servers/zelda-server-proxmox)
- [Network Inventory](/infrastructure/network-inventory)
