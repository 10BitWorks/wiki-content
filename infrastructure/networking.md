---
title: Networking
description: Core network infrastructure and services documentation.
published: true
date: 2026-07-01T06:19:05.108Z
tags: infrastructure, networking
editor: markdown
dateCreated: 2026-06-15T20:15:06.139Z
---

# Networking

Documentation for the main networking components at 10BitWorks.

## Active Components

- [pfSense](/infrastructure/networking/pfsense) — Firewall, routing, DHCP, DNS
- [Headscale](/infrastructure/networking/headscale-coordination-server) — Tailscale coordination server
- [Tailscale Exit Node (Kudu)](/infrastructure/networking/tailscale-exit-node-kudu) — Mesh VPN exit node
- [Tailscale Exit Node (LAC)](/infrastructure/networking/tailscale-exit-node-lac) — Mesh VPN exit node
- [Ganondorf](/infrastructure/networking/ganondorf) - Cisco Wireless Controller

## Related

See also the [Network Inventory](/infrastructure/network-inventory) for the full list of IPs and devices.

## Common IP
*IP numbers commonly used for device setup.*
All 10Bitworks local devices should typically reside inside the 10.7.x.x/16 Private IP block.
### DHCP and DNS

10.7.1.39   | DHCP Server
10.7.1.39   | DNS1
10.7.1.38   | DNS2
### Gateway

10.7.x.1    | Where X is your local vlan number, E.g. members gateway is 10.7.7.1.

### Services
10.7.1.254  	Firewall, internet outbound
10.7.1.254  	NTP
10.7.17.3   	Cisco Wireless Controller
## Vlan

Vlan1 Mang 10.7.1.0/24
Vlan 17 Ap-deploy 10.7.16.0/24
Vlan 17 Server 10.7.17.0/24
Vlan 18 Auth 10.7.18.0/24
Vlan 21 IOTCamera 10.7.21.0/24
Vlan 22 Other IOT 10.7.22.0/24
Vlan 23 Printer 10.7.23.0/24
Vlan 24 Home automation 10.7.24.0/24
Vlan 7 Members 10.7.7.0/24