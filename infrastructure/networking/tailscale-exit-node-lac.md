---
title: Tailscale Exit Node (LAC)
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: network, tailscale
description: "Primary Tailscale exit node and subnet router for the 10BitWorks Headscale network."
isPublished: true
---

- Hostname: tailscale-lac (Lease Hostname: tail-lac)
- mDNS: TODO
- IP: 10.7.1.104 (DHCP)
- MAC: BC:24:11:D4:B8:C0
- OS: Debian 12 (VM 203 on Zelda)
- Model: Proxmox VM 203

> This is the primary SNAT source for remote users (Headscale).
> {.is-info}
