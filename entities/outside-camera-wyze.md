---
title: Outside Camera (Wyze)
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: network, operations
description: "Network details and configuration for Outside Camera (Wyze)"
isPublished: true
---

- Hostname: cam-wyze3-outside (Lease: cam-wyze3-outside)
- mDNS: cam-wyze3-outside.local (Legacy: cam-wyze3-front)
- IP: 10.7.1.100 (DHCP)
- MAC: 02:10:5D:64:85:38
- OS: Thingino Linux (Build 2026.x)
- Model: Wyze Camera v3
- Port: 80 (http) - Thingino Web Interface
- Port: 554 (rtsp) - RTSP Camera Stream
- Port: 8080 (admin) - Thingino Admin/Debug UI
> Configured as `outside` in Frigate NVR config.
> {.is-info}



## Firmware Details
- **OS**: Thingino Linux (Build 2026.x)
- **Primary Ports**: 80 (Web), 554 (RTSP), 8080 (Admin)
- **Optimization**: H.264 @ 1000kbps for outdoor, H.265 for indoor.
- **Transport Requirement**: UDP mandatory for stability.

