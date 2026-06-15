---
title: Network Inventory
created: 2026-06-15
updated: 2026-06-15
type: reference
tags: network-inventory
description: Master lookup table for all 10BitWorks network devices, IPs, and MAC addresses.
isPublished: true
---

# Network Inventory

**Single source of truth** for every device on the 10.7.1.0/24 network and related systems.  
Only entries with significant operational depth have their own wiki pages (hyperlinked).

---

## Core Infrastructure

| Hostname              | IP            | MAC                  | Role                          | Page |
|-----------------------|---------------|----------------------|-------------------------------|------|
| zelda                 | 10.7.1.240    | -                    | Proxmox Host (Dell Wyse 5070) | [Zelda Server](/infrastructure/servers/zelda-server-proxmox) |
| link                  | 10.7.1.7      | -                    | Proxmox Host                  | [Link Server](/infrastructure/servers/link-server-proxmox) |
| pfsense               | 10.7.1.1      | -                    | Firewall / Router             | [pfSense](/infrastructure/networking/pfsense) |
| headscale             | 10.7.1.3      | -                    | Tailscale Coordination        | [Headscale](/infrastructure/networking/headscale) |

## Oracle Cloud

| Hostname         | Public IP     | Role                     | Page |
|------------------|---------------|--------------------------|------|
| cloud-oracle     | -             | Main Coolify instance    | [Oracle Cloud](/infrastructure/servers/oracle-cloud) |

## Cameras & Vision

| Location          | IP            | Model / Notes                  | Page |
|-------------------|---------------|--------------------------------|------|
| Front of Shop     | 10.7.1.xxx    | Amcrest Turret (4MP)           | [Amcrest Turret](/infrastructure/operations/cameras-frigate) |
| Outside           | 10.7.1.xxx    | Wyze v3 (Thingino)             | [Outside Camera](/infrastructure/operations/cameras-frigate) |
| Kilns             | 10.7.1.xxx    | Wyze v3 (Thingino)             | [Kilns Camera](/infrastructure/operations/cameras-frigate) |
| Woodshop          | 10.7.1.xxx    | Wyze v3 (Thingino)             | [Woodshop Camera](/infrastructure/operations/cameras-frigate) |
| Laser             | 10.7.1.xxx    | Wyze v3 (Thingino)             | [Laser Camera](/infrastructure/operations/cameras-frigate) |
| Doorbell          | 10.7.1.121    | Wyze Doorbell v1 (Thingino)    | [Doorbell Camera](/infrastructure/operations/cameras-frigate) |

## IoT & Lighting

All Wyze and ESP-based lighting/switches are recorded here but do **not** have individual pages unless they develop significant custom logic or failure modes.

| Name                    | IP            | MAC                  | Type          | Notes |
|-------------------------|---------------|----------------------|---------------|-------|
| shop-east-light         | 10.7.1.xxx    | -                    | Wyze Switch   | - |
| shop-west-light         | 10.7.1.xxx    | -                    | Wyze Switch   | - |
| ... (add more as discovered) | ...       | ...                  | ...           | ... |

## Workshop Machines (non-IP or minimal)

These machines are documented under `/equipment/` when they have SOPs, maintenance history, or safety procedures.

| Name             | Type              | Network Notes          | Page |
|------------------|-------------------|------------------------|------|
| Murderbot        | Prusa MK4         | Minimal network        | [3D Printer (murderbot)](/equipment/3d-printer-murderbot) |
| Laser Cutter     | -                 | -                      | [Laser Cutter](/equipment/laser-cutter) |

---

**Notes**
- This page is intentionally kept relatively flat and tabular for fast lookup.
- Any device that develops meaningful documentation, failure modes, or procedures should be promoted to its own page under the appropriate folder and linked from here.
- Personal devices and one-off ESP projects generally stay in this table only.