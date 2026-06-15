---
title: Tailscale Exit Node (Kudu)
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: network, tailscale, headscale, zelda-hosted
description: "Tailscale exit node bridging the 10BitWorks hosted network to Eric's personal tailnet."
isPublished: true
---

- Hostname: tailscale-kudu (Lease Hostname: tail-kudu)
- mDNS: tail-kudu.local
- IP: 10.7.1.172 (DHCP)
- MAC: BC:24:11:BB:03:CB
- OS: Debian 12 (VM 205 on Zelda)
- Model: Proxmox VM 205

## Role

This exit node bridges the 10BitWorks hosted Headscale network to Eric's personal tailnet, allowing cross-tailnet access for trusted administrators.

## Related

- [Headscale Coordination Server](/infrastructure/networking/headscale-coordination-server)
- [Tailscale Exit Node (LAC)](/infrastructure/networking/tailscale-exit-node-lac)
- [Network Inventory](/infrastructure/network-inventory)
