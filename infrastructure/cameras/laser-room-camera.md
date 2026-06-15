---
title: Laser Room Camera
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: cameras, infrastructure, thingino
description: "Wyze Cam v3 running Thingino firmware, monitoring the laser room."
isPublished: true
---

- Hostname: cam-laser
- mDNS: cam-wyze3-laser.local
- IP: 10.7.1.131 (DHCP)
- MAC: 02:F9:1F:5A:98:84
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
