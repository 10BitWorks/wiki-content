---
title: Headscale Coordination Server
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: network, tailscale, headscale, zelda-hosted
description: "Headscale control plane for the 10BitWorks overlay mesh VPN."
isPublished: true
---

- Hostname: headscale
- mDNS: Unsupported
- IP: 10.7.1.242 (DHCP)
- MAC: BC:24:11:27:00:29
- OS: Debian 12 (VM 200 on Zelda)
- Model: Proxmox VM 200
- Port: 8080 (http) - Headscale Control Plane

## Tailnet Architecture

Headscale provides the coordination server for the 10BitWorks hosted Tailnet. Two exit nodes/subnet routers handle traffic:

- [Tailscale Exit Node (LAC)](/infrastructure/networking/tailscale-exit-node-lac) — Primary exit node and subnet router for the `10.7.1.0/24` subnet. SNATs traffic so it appears to originate from `10.7.1.104`.
- [Tailscale Exit Node (Kudu)](/infrastructure/networking/tailscale-exit-node-kudu) — Exit node bridging the hosted network to Eric's personal tailnet.

## Critical Constraint: Do Not Accept Routes on Physical Hosts

Never run `tailscale up --accept-routes` or `tailscale set --accept-routes=true` on any host already physically connected to `10.7.1.0/24` (such as Zelda or Link).

**Reason:** These hosts already have a direct route to the subnet. Accepting the same route via Tailscale creates an asymmetric routing loop: traffic arrives via the physical interface, but the response is forced into the Tailscale tunnel (policy routing / Table 52) and blackholed.

**Symptoms:** Node reachable via Layer 2 (ARP/IPv6 Link-Local) but Layer 3 (IPv4/ping/SSH) times out.

**Recovery:** Access the node via Link-Local IPv6 from a neighbor and disable route acceptance:

```bash
ssh -A -6 root@fe80::...%interface
sudo tailscale set --accept-routes=false
```

## Related

- [Tailscale Exit Node (LAC)](/infrastructure/networking/tailscale-exit-node-lac)
- [Tailscale Exit Node (Kudu)](/infrastructure/networking/tailscale-exit-node-kudu)
- [Network Inventory](/infrastructure/network-inventory)
