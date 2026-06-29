---
title: Primary DNS & DHCP Server
description: Network details and configuration for Primary DNS & DHCP Server
published: true
date: 2026-06-29T22:25:31.924Z
tags: network, networking, primary-dns-hosted
editor: markdown
dateCreated: 2026-06-14T11:12:09.903Z
---

# pihole2 (marked for replacement)
- Hostname: dhcp1
- mDNS: pihole2.local
- IP: 10.7.1.9 (Static)
- MAC: BC:24:11:96:44:00 (VM 209 on Zelda)
- OS: Debian GNU/Linux 12 (bookworm)
- Model: Proxmox VM 209
- Port: 22 (ssh) - Admin Shell
- Port: 53 (domain) - Primary DNS Service
- Port: 80 (http) - Pi-hole Admin Web UI
- Port: 443 (https) - Secure Admin UI
- Netdata: Streaming to 10.7.1.7 (Parent)
--
Tailscale/Headscale infrastructure for remote access.
# Retirement
Only providing DNS replies on 10.7.1.9
DHCP disabled
tech2 replacement designated machine for role of DNS secondary
