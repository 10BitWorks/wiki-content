---
title: Kiln Monitor
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: 3d-printer, network
description: "Network details and configuration for Kiln Monitor"
isPublished: true
---

# Kiln Monitor

- Hostname: kilnpi
- mDNS: kilnpi.local (DHCP Legacy: kiln)
- IP: 10.7.1.81 (Static)
- MAC: B8:27:EB:32:5F:65
- OS: Raspbian GNU/Linux 10 (buster)
- Model: Raspberry Pi 3B+
- Port: 22 (ssh) - Admin Shell
- Port: 80 (http) - Apache Web Server (Legacy UI)
- Port: 3000 (grafana) - Grafana Visualization
- Netdata: Streaming to 10.7.1.7 (Parent)
- Note: SSH user is `espehr` (see `./kiln pi/GEMINI.md`)

