---
title: Access Card System
created: 2026-06-15
updated: 2026-06-15
type: reference
tags: access-control, infrastructure
description: "High-level overview of the 10BitWorks RFID member access card system."
isPublished: true
---

10BitWorks uses RFID cards for member access to the building. The system has three parts: card provisioning, door controllers, and the member database.

## Components

### Card Provisioning

New or replacement cards are written on the [Cardmaker Pi](/infrastructure/access-control/cardmaker-pi). The Pi runs a Flask application that reads a member's email via the Squarespace API, encodes it onto an RFID card, and writes the card.

### Door Controllers

Two Raspberry Pis read cards at the front door:

- [frontdoor](/infrastructure/access-control/front-door-pi-controllers) — Original monolithic controller
- [cobalt](/infrastructure/access-control/front-door-pi-controllers) — Current controller with status LEDs and sound effects

When a card is presented, the controller reads the obfuscated email, contacts the **Door Admin Panel** at `10.7.1.244:8000`, and unlocks the door if the member is active.

### Door Admin Panel

The Door Admin Panel runs in LXC 204 (`door1`) on Zelda. It hosts the Django database that maps cards to members and decides whether access is granted.

## Card Data Format

Stored card data is obfuscated with ROT13. The first 12 characters encode the member email prefix used for lookup. The full encoded string is sent to the admin panel for validation.

## Contributors

- [Ray Good](/contributors/ray) — Built the original frontdoor and cobalt Pi hardware/software
- [Connor Doherty](/contributors/connor) — Current improvements, including the chiptune sound effects and cobalt enhancements
