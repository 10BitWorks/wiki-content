---
title: Cardmaker Pi
created: 2026-06-14
updated: 2026-06-15
type: reference
tags: access-control, infrastructure, pfsense-hosted
description: "Badge provisioning station for 10BitWorks access cards."
isPublished: true
---

The Cardmaker Pi provisions RFID access cards for 10BitWorks members.

- Hostname: cardPi
- mDNS: cardPi.local
- IP: 10.7.1.136 (DHCP)
- Model: Raspberry Pi
- Port: 22 (ssh) - Pi Management

> SSH user is `chale`, password `c@rdmaker`
> {.is-info}

## Software Stack

- Python 3 / Flask
- Flask-SocketIO
- SimpleMFRC522 (RFID)
- Squarespace API (`sq_mod.py`)

## Related

- [Access Card System](/infrastructure/access-control/access-card-system) — High-level overview
- [Front Door Pi Controllers](/infrastructure/access-control/front-door-pi-controllers) — Door controllers that read the cards
