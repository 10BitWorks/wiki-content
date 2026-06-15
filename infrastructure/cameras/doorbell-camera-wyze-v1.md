---
title: Doorbell Camera (Wyze v1)
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: cameras, infrastructure, thingino
description: "Wyze Video Doorbell v1 running Thingino firmware."
isPublished: true
---

- Hostname: doorbell-wyze1
- mDNS: doorbell-wyze1.local
- IP: 10.7.1.121 (DHCP)
- MAC: 02:74:51:53:96:e8
- OS: Thingino Linux (Build 2026.x)
- Model: Wyze Video Doorbell v1
- Port: 80 (http) - Thingino Web Interface
- Port: 554 (rtsp) - RTSP Camera Stream
- Port: 8080 (admin) - Thingino Admin/Debug UI

## Doorbell-Specific Hardware

- **Sensor Orientation:** The SC4236 sensor is native portrait (3:4). Use `stream0.rotation=2` and `stream1.rotation=2` to orient correctly.
- **Button GPIO:** The front doorbell button is on GPIO 7.
- **Speaker Amp:** GPIO 63 must be set HIGH to enable the speaker.
- **Greeting Logic:** A custom script `/usr/sbin/doorbell-greeting` plays `greeting.wav` while suppressing status LEDs via `/run/greeting_active`.
- **Button Config:** `/etc/thingino-button.conf` maps `KEY_0 PRESS` to the greeting script.
- **Floodlight:** GPIO 60. Automatically triggered by `scripts/motion` when `ircut read` is "on" (Night Vision active) and motion is detected.

## Firmware Details

- **OS**: Thingino Linux (Build 2026.x)
- **Primary Ports**: 80 (Web), 554 (RTSP), 8080 (Admin)
- **Optimization**: H.264 @ 1000kbps for outdoor.
- **Transport Requirement**: UDP mandatory for stability.

## Related

- [Frigate NVR](/app-services/self-hosted/frigate)
- [Cameras](/infrastructure/cameras)
