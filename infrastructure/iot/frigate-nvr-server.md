---
title: Frigate NVR Server
created: 2026-06-14
updated: 2026-06-15
type: entity
tags: network, operations, cameras, zelda-hosted
description: "Frigate NVR server — network details, configuration, and hardware scaling notes."
isPublished: true
---

- Hostname: cameras
- mDNS: cameras.local
- IP: 10.7.1.31 (Static)
- OS: Debian (LXC 105 on Zelda)
- Model: Proxmox Container
- Port: 22 (ssh) — Frigate Host Shell
- Port: 443 (https) — Nginx Proxy Access
- Port: 5000 (upnp) — Frigate NVR Web UI
- Netdata: Streaming to 10.7.1.7 (Parent)

## AI Inference Hardware Notes

Based on 10BitWorks infrastructure analysis, scaling to high-density camera deployments with AI inference requires specific hardware.

### The Dell T330 Constraint

The Dell PowerEdge T330 (and similar older Xeon E3-1200 v5/v6 systems) is **not recommended** for Frigate:

- **No QuickSync**: Server-grade chips lack integrated graphics, forcing software decode of every stream.
- **AI Bottlenecks**: Object detection requires external hardware (Google Coral); modern consumer chips can do it natively via OpenVINO on the iGPU.
- **Power Efficiency**: High idle draw and low single-thread performance vs modern consumer workstations.

### Recommended Architectures (20–40+ cameras)

12th Gen or 13th Gen Intel Core systems are the target. The UHD 770 iGPU in 12th gen is the key threshold.

**Path A — Used/Refurbished Workstation (Value)**
- Dell Precision 3660 / HP Z2 G9
- CPU: Intel Core i5-12500 or i7-12700
- UHD 770 decodes dozens of streams and runs AI detection via OpenVINO simultaneously

**Path B — Custom Build**
- CPU: Intel Core i5-13500 (14 cores / 20 threads)
- Dual media engines for massive video throughput
- Coral M.2 optional for extreme-speed facial recognition; iGPU handles standard object tracking natively

## Related

- [IoT & Cameras](/infrastructure/iot) — Full camera inventory
- [Network Inventory](/infrastructure/network-inventory) — IP/MAC details
