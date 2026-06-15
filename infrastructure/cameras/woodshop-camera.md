---
title: Woodshop Camera
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: cameras, infrastructure, thingino
description: "Wyze Cam v3 running Thingino firmware, monitoring the woodshop."
isPublished: true
---

- Hostname: cam-wood
- mDNS: 10bit-wyze3-wood.local (Legacy: cam-wyze3-woodworking)
- IP: 10.7.1.143 (DHCP)
- MAC: 02:96:3E:67:F6:CC
- OS: Thingino Linux (Build 2026.x)
- Model: Wyze Camera v3
- Port: 80 (http) - Thingino Web Interface
- Port: 554 (rtsp) - RTSP Camera Stream
- Port: 8080 (admin) - Thingino Admin/Debug UI

## Firmware Details

- **OS**: Thingino Linux (Build 2026.x)
- **Primary Ports**: 80 (Web), 554 (RTSP), 8080 (Admin)
- **Optimization**: H.265 for indoor.
- **Transport Requirement**: UDP mandatory for stability.

## Related

- [Frigate NVR](/app-services/self-hosted/frigate)
- [Cameras](/infrastructure/cameras)
