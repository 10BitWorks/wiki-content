---
title: Frigate NVR
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, hosted, link-hosted, cameras
description: "Frigate network video recorder service for 10BitWorks security cameras."
isPublished: true
---

Frigate is the network video recorder for all 10BitWorks security cameras.

- Hostname: cameras
- mDNS: cameras.local
- IP: 10.7.1.31 (Static)
- OS: Debian (LXC on Link)
- Model: Proxmox Container
- Port: 22 (ssh) — Frigate Host Shell
- Port: 443 (https) — Nginx Proxy Access
- Port: 5000 (http) — Frigate NVR Web UI
- Port: 1984 — go2rtc
- Netdata: Streaming to 10.7.1.7 (Parent)

## Active Cameras

- [Amcrest Turret Camera](/infrastructure/cameras/amcrest-turret-camera) — Front of shop
- [Outside Camera (Wyze)](/infrastructure/cameras/outside-camera-wyze)
- [Doorbell Camera (Wyze v1)](/infrastructure/cameras/doorbell-camera-wyze-v1)
- [Kiln Area Camera](/infrastructure/cameras/kiln-area-camera)
- [Laser Room Camera](/infrastructure/cameras/laser-room-camera)
- [Woodshop Camera](/infrastructure/cameras/woodshop-camera)

## Streaming Constraints

- **Thingino cameras must use UDP.** TCP causes camera-side memory exhaustion and crashes.
- **Do not use `#transport=tcp` or `#transport=udp` fragments** in go2rtc RTSP URLs.
- **H.265 preferred** for Thingino indoor cameras; H.264 @ 1000kbps for outdoor.
- **Use direct IP addresses** in Frigate config rather than `.local` mDNS during high-load events.

## Motion Offloading

Thingino cameras trigger events via JSON webhooks to `/api/events/...`. Frigate's internal pixel-based motion detection is disabled for these cameras to save CPU. `objects: track: motion` remains enabled so external events trigger recordings.

## mDNS Proxy

go2rtc is written in Go and cannot resolve `.local` addresses natively. The LXC host runs a `dnsmasq` proxy on `172.17.0.1` plus an `update-mdns.sh` script that resolves camera mDNS names and feeds them to dnsmasq. The Frigate container is configured to use `172.17.0.1` as its DNS server.

## Storage Architecture

Frigate uses a MergerFS pool combining a local NFS share and a Google Drive archive (Rclone):

- **Local Write Path**: `/mnt/frigate_recordings` (NFS on Link)
- **Cloud Archive**: `/mnt/gdrive` (Rclone)
- **Offload Policy**: `rclone move` with `--min-age 7d` preserves 7 days locally before archiving

> Snapshots and GenAI are disabled to prevent inode exhaustion.
> {.is-warning}

## Stability Hardening

A runaway `ffmpeg` incident on 2026-04-26 taught the following hardening rules:

1. **MergerFS policy** must isolate metadata/action operations to the local branch: `category.create=ff,category.search=ff,category.action=ff`.
2. **LXC 105 swap must remain 0** so a runaway `ffmpeg` is killed inside the container before host thrashing starts.
3. **Use JSMPEG** for live views; MSE can deadlock during stream instability.

## AI Inference Hardware Notes

The current Proxmox host (Intel Celeron J4105) supports VAAPI but lacks AVX, forcing CPU/TFLite detection. For scaling beyond a handful of cameras, a 12th Gen Intel Core system with UHD 770 iGPU is recommended. See the [Frigate Hardware Evaluation](/infrastructure/cameras/frigate-hardware-evaluation) for the full analysis.

## Related

- [Cameras](/infrastructure/cameras) — Full camera inventory
- [Network Inventory](/infrastructure/network-inventory) — IP/MAC details
- [Frigate Hardware Evaluation](/infrastructure/cameras/frigate-hardware-evaluation)
