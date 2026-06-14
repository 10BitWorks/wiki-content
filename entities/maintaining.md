---
title: Maintaining
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: [network]
description: "Network details and configuration for Maintaining"
isPublished: true
---

# Maintaining

- **Scanning**: Rather than slow network sweep, SSH into the DNS servers (Pihole 1 and 2) to get the latest list, and the `extrawall` pfsense firewall, and into the Proxmox servers (Zelda and Link) to get the latest list of containers and their IPs.
- **Installing public key**: If I have to provide a password for first access, install the public key after login so it's not required next time.
- **.local addresses**: We shall make every device natively broadcast its own mDNS address, excet where it's confirmed to be impossible.
--
Physical servers, routers, and out-of-band management.

