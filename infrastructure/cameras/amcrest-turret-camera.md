---
title: Amcrest Turret Camera (front of shop)
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: cameras, infrastructure, amcrest
description: "Front-of-shop Amcrest turret camera connected to Frigate NVR."
isPublished: true
---

- Hostname: Amcrest1
- mDNS: Supported (10bit-amcrest-front.local)
- IP: 10.7.1.61 (Static)
- MAC: 30:DD:AA:80:9F:89
- OS: Amcrest/Dahua Firmware
- Model: IPC-T54IR-AS-S3 (2.5K Turret)
- Port: 80 (http) - Web UI
- Port: 554 (rtsp) - RTSP Camera Stream (Native AAC)
- Port: 37777 (dahua) - Private Management Port

> Supports AI SSA, WDR, and IR/White Light.
> {.is-info}

## Amcrest IPC-T54IR-AS-S3 Features

- **AI SSA (AI Scene Self-adaptation):** Automatically adjusts image parameters.
- **Support:** WDR, HLC, BLC, and 3D Noise Reduction.
- **Encoding:** Up to 2688x1520 (4MP) @ 30 FPS. Smart H.264+/H.265+.
- **AI Detection:** Smart Motion Detection (SMD) for Human and Motor Vehicle targets.
- **Protocols:** RTSP, ONVIF, CGI API control.
- **Audio:** Built-in Mic/Speaker (AAC support).

## Related

- [Frigate NVR](/app-services/self-hosted/frigate)
- [Cameras](/infrastructure/cameras)
