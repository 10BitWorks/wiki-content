---
title: Frigate NVR Server
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: [network, operations]
description: "Network details and configuration for Frigate NVR Server"
---

# Frigate NVR Server

- Hostname: cameras
- mDNS: cameras.local
- IP: 10.7.1.31 (Static)
- OS: Debian (LXC 105 on Zelda)
- Model: Proxmox Container
- Port: 22 (ssh) - Frigate Host Shell
- Port: 443 (https) - Nginx Proxy Access
- Port: 5000 (upnp) - Frigate NVR Web UI
- Netdata: Streaming to 10.7.1.7 (Parent)

