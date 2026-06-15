---
title: Tailscale Exit Node (LAC)
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: network, tailscale, headscale, zelda-hosted
description: "Primary Tailscale exit node and subnet router for the 10BitWorks Headscale network."
isPublished: true
---

- Hostname: tailscale-lac (Lease Hostname: tail-lac)
- mDNS: tail-lac.local
- IP: 10.7.1.104 (DHCP)
- MAC: BC:24:11:D4:B8:C0
- OS: Debian 12 (VM 203 on Zelda)
- Model: Proxmox VM 203

## Role

This is the primary exit node and subnet router for the 10BitWorks hosted Headscale network. It advertises the `10.7.1.0/24` subnet and performs SNAT so remote Tailscale traffic appears to originate from `10.7.1.104` on the local network.

## Related

- [Headscale Coordination Server](/infrastructure/networking/headscale-coordination-server)
- [Tailscale Exit Node (Kudu)](/infrastructure/networking/tailscale-exit-node-kudu)
- [Network Inventory](/infrastructure/network-inventory)
