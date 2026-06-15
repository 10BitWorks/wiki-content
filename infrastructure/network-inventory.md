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

## Core Infrastructure & Servers

| Device / Title | Hostname | IP | MAC | Model / OS | Ports / Notes |
|---|---|---|---|---|---|
| Zelda Proxmox Host | zelda | 10.7.1.240 | - | Proxmox Host (Dell Wyse 5070) | [Zelda Server](/infrastructure/servers/zelda-server-proxmox) |
| Link Proxmox Host | link | 10.7.1.7 | - | Proxmox Host | [Link Server](/infrastructure/servers/link-server-proxmox) |
| pfSense Firewall / Router | pfsense | 10.7.1.1 | - | Firewall / Router | [pfSense](/infrastructure/networking/pfsense) |
| Headscale Coordination | headscale | 10.7.1.3 | - | Tailscale Coordination | [Headscale](/infrastructure/networking/headscale-coordination-server) |
| Primary DNS & DHCP Server | dhcp1 | 10.7.1.9 (Static) | BC:24:11:96:44:00 (VM 209 on Zelda) | Proxmox VM 209 / Debian (bookworm) | [Primary DNS & DHCP](/infrastructure/networking/primary-dns-dhcp-server) |
| Secondary DNS Server | pihole1 | 10.7.1.8 (Static), 10.7.1.181 (DHCP) | B8:27:EB:68:F8:D1, B8:27:EB:3D:AD:84 | Raspberry Pi 3B+ / Debian (bookworm) | [Secondary DNS](/infrastructure/networking/secondary-dns-server) |
| Core Network Switch | coruscant | 10.7.1.1 (Static) | B4:A8:B9:F2:67:47 | Cisco Catalyst c3850-12x48u-s / IOS 16.06.09 | [Core Network Switch](/infrastructure/networking/core-network-switch) |
| Shared Oracle ARM Server | 10bitworks | 100.64.0.15 (Tailscale) | - | Oracle Cloud A1.Flex / Ubuntu 24.04 ARM | Shared Oracle ARM Server |
| New Door Access Controller | cobalt | 10.7.1.59 (Static) | - | Raspberry Pi 3B+ / Raspbian | [Front Door Access](/operations/front-door-access-system) |
| Old Door Access Controller | frontdoor | 10.7.1.6 (Static) | B8:27:EB:1B:CE:EF | Raspberry Pi 3B+ / Raspbian | [Front Door Access](/operations/front-door-access-system) |
| Door Admin Panel | door1 | 10.7.1.244 (Static) | - | Proxmox LXC 204 on Zelda / Debian | 8000 (http) - Door Admin Dashboard |
| Cardmaker Pi | cardPi | 10.7.1.136 (DHCP) | - | Raspberry Pi / Raspbian | 22 (ssh), user chale, pswd c@rdmaker |
| TP-Link AP | Archer_C7 | 10.7.1.152 (DHCP) | E4:C3:2A:DA:43:E0 | TP-Link Archer C7 / TP-Link Firmware | 80 (http) - Management UI |
| Wireless AP Nighthawk | rs70 | 10.7.1.252 (DHCP) | 54:07:7D:E4:0F:88 | Netgear Nighthawk R7000 / Netgear Genie | 80 (http) - Management UI |
| Upstream ISP Gateway | ATT-Fiber | 192.168.10.254 | - | AT&T BGW Series | 80 (http) - Gateway Web UI |
| Infrastructure Monitor | uptime | 10.7.1.89 (DHCP) | - | Proxmox LXC 120 on Zelda / Debian | 3001 (http) - Uptime Kuma |
| InvenTree Inventory System | inventree | - | BC:24:11:4D:21:F2 | Proxmox VM 331 on Zelda / Debian 12 | 80 (http) - InvenTree Dashboard |
| Invoice Ninja Server | invoice | 10.7.1.86 (DHCP) | - | Proxmox LXC 1031 on Link / Debian | 80 (http) - Invoice Ninja Web UI |
| Homebox Evaluation | cake | 10.7.1.88 (DHCP) | BC:24:11:0F:EB:01 | Proxmox LXC 205 on Link / Debian | 80 (http) - Homebox Dashboard |
| Label Printing Station | labelpi | 10.7.1.87 (DHCP) | B8:27:EB:46:E8:58 | Raspberry Pi 3B+ / Raspbian | - |
| Bookstack Documentation Site | bookstack | 10.7.1.13 (DHCP Lease) | - | Proxmox LXC 108 on Zelda / Debian | 80 (http) - Bookstack UI |
| Link Out-of-Band Management | idrac-electronics | 10.7.1.154 (DHCP) | 44:A8:42:44:70:B6 | iDRAC 8 (PowerEdge R430) | - |
| Machine Console | laser | 10.7.1.102 (DHCP) | 4C:03:4F:D4:C1:C8 | Machine Console / Unknown | - |
| General Purpose Device | eggo | 10.7.1.91 (DHCP) | A4:E8:8D:2F:C7:53 | TODO / Unknown | - |
| Generic Desktop Asset | DESKTOP-096JVUK | 10.7.1.101 (DHCP) | 30:89:4A:6E:D4:26 | Unknown / Windows | - |
| Unknown Workshop PC | MSI | DHCP (former .104) | 8C:55:4A:9D:2A:EC | MSI Desktop/Laptop / Windows 10/11 | - |
| Unknown Wi-Fi Asset | aa2 | 10.7.1.62 (DHCP) | D0:3F:27:50:84:FD | Unknown / Unknown | - |
| DHCP Sniffer (Stopped) | - | DHCP | BC:24:11:8F:0D:AB | Proxmox LXC 1101 on Zelda / Debian | - |
| Grocy Inventory (Stopped) | grocy | DHCP | BC:24:11:9E:B2:B7 | Proxmox LXC 102 on Zelda / Debian | - |
| Homepage Dashboard (Stopped)| homepage | DHCP | BC:24:11:ED:CB:EE | Proxmox LXC 100 on Zelda / Debian | - |
| Shared DB Instance (Stopped) | db-postgresql | DHCP | BC:24:11:A7:87:66 | Proxmox LXC 201 on Zelda / Debian | - |
| Legacy Support Desk (Stopped)| support | 10.7.1.22 | BC:24:11:32:08:76 | Proxmox LXC 104 on Zelda / Ubuntu | - |

---

## Cameras & Vision

| Device / Title | Hostname | IP | MAC | Model / OS | Ports / Notes |
|---|---|---|---|---|---|
| Front of Shop | - | - | - | Amcrest Turret (4MP) | [Amcrest Turret Camera](/infrastructure/iot/amcrest-turret-camera) |
| Outside Camera | - | - | - | Wyze v3 (Thingino) | [Outside Camera](/infrastructure/iot/outside-camera-wyze) |
| Kilns Camera | - | - | - | Wyze v3 (Thingino) | [Kilns Camera](/infrastructure/iot/kiln-area-camera) |
| Kiln Monitor | kiln-mon | 10.7.1.xxx | - | Raspberry Pi / Custom script | [Kiln Monitor](/infrastructure/iot/kiln-monitor) |
| Laser Room Camera | - | - | - | Wyze v3 (Thingino) | [Laser Room Camera](/infrastructure/iot/laser-room-camera) |
| Woodshop Camera | - | - | - | Wyze v3 (Thingino) | [Woodshop Camera](/infrastructure/iot/woodshop-camera) |
| Doorbell Camera | doorbell | 10.7.1.121 | - | Wyze Doorbell v1 (Thingino) | [Doorbell Camera](/infrastructure/iot/doorbell-camera-wyze-v1) |
| PTZ Camera (Glados) | Glados | 10.7.1.170 (DHCP) | F0:00:06:24:0C:4B | Jennov PTZ Camera | 554 (rtsp) - RTSP |

---

## IoT & Sensors

| Device / Title | Hostname | IP | MAC | Model / OS | Ports / Notes |
|---|---|---|---|---|---|
| Energy Monitor (Emporia) | Emporia | 10.7.1.127 (DHCP) | B8:F0:09:83:33:F4 | Emporia Vue Energy Monitor | - |
| Epson Network Printer | EPSONC7D47D | 10.7.1.185 (DHCP) | 9C:AE:D3:C7:D4:7D | Network Printer | - |
| Roku (Hisense Smart TV) | Bedroom | 10.7.1.147 (DHCP) | 1C:30:08:95:BC:1E | Hisense Smart TV | Roku OS |
| Generic IoT Module 1 | Unknown | 10.7.1.103 (DHCP) | 94:3C:C6:52:75:E0 | Espressif (ESP32/ESP8266) | - |
| Generic IoT Module 2 | Unknown | 10.7.1.192 (DHCP) | 08:A6:F7:0A:73:78 | Espressif (ESP32/ESP8266) | - |
| IoT Lighting Interface | Unknown | 10.7.1.128 (DHCP) | 1C:D6:BD:F5:29:89 | Leedarson / Zigbee Bridge | - |
| Wyze Light Switch 1 | - | 10.7.1.132 (DHCP) | 7C:78:B2:FD:85:E5 | Wyze Switch (Proprietary) | - |
| Wyze Light Switch 2 | - | 10.7.1.151 (DHCP) | 7C:78:B2:FE:25:48 | Wyze Switch (Proprietary) | - |
| Wyze Light Switch 3 | - | 10.7.1.198 (DHCP) | 7C:78:B2:FD:35:8C | Wyze Switch (Proprietary) | - |
| Wyze Light Switch 4 | - | 10.7.1.166 (DHCP) | D0:3F:27:11:7D:7E | Wyze Switch (Proprietary) | - |
| Wyze Sense Hub | wyzehub | 10.7.1.130 (DHCP) | 7E:78:B2:96:8C:70 | Wyze Sense Hub / Wyze Stock | - |

---

## Workshop Equipment

| Name | Type | IP | MAC | Page / Notes |
|---|---|---|---|---|
| Murderbot | Prusa MK4 | - | - | [3D Printer (murderbot)](/equipment/3d-printer-murderbot) |
| Sovol SV08 | 3D Printer | - | - | [Sovol SV08 (3D Printer)](/equipment/sovol-sv08-3d-printer) |
| Laser Cutter | - | - | - | Laser Cutter |

---

## Personal & Member Devices

| Device / Title | Hostname | IP | MAC | Model / OS | Ports / Notes |
|---|---|---|---|---|---|
| Connor's Laptop | lemur | 10.7.1.194 (DHCP) | 90:0F:0C:47:2B:15 | System76 Laptop / Linux (Guix System / Debian) | Current session host |
| Connor's Phone | Pixel-10-Pro-Fold | 10.7.1.149 (DHCP) | 82:FD:62:C8:6B:77 | Pixel 10 Pro Fold / Android | - |

---

**Notes**
- This page is the unified reference view of all network nodes.
- Devices with dedicated operational notes, SOPs, or guides are promoted to their own pages under servers, networking, hosted services, operations, or equipment folders.
- Any other device listed here remains a tabular record to avoid empty page clutter.
