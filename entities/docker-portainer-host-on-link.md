---
title: Docker (Portainer) Host on Link
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: network, proxmox
description: "Network details and configuration for Docker (Portainer) Host on Link"
isPublished: true
---

- Hostname: docker
- mDNS: docker.local
- IP: 10.7.1.25 (Static)
- OS: Debian (LXC 420 on Link)
- Model: Proxmox Container
- Port: 22 (ssh) - Docker VM Shell
- Port: 80 (http) - Nginx Web UI
- Port: 3000 (grafana) - Loomio
- Port: 5000 (registry) - Local Docker Registry
- Port: 5432 (postgresql) - Shared Database Instance
- Port: 8000 (door-admin) - Portainer Stack Management
- Port: 8080 (n8n) - n8n Automation Engine
- Port: 9443 (portainer) - Portainer Admin Dashboard
- Netdata: Streaming to 10.7.1.7 (Parent)

