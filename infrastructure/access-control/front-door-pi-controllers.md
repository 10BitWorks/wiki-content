---
title: Front Door Pi Controllers
created: 2026-06-15
updated: 2026-06-15
type: reference
tags: access-control, infrastructure
description: "Raspberry Pi door controllers (frontdoor and cobalt) for 10BitWorks physical access."
isPublished: true
---

10BitWorks operates two Raspberry Pi implementations for controlling building door access. Both communicate with the **Door Admin Panel** at `http://10.7.1.244:8000` (running inside LXC 204 `door1` on Zelda) for member validation and use ROT13-based obfuscation for stored card email data.

See also the high-level [Access Card System](/infrastructure/access-control/access-card-system) overview and the [Cardmaker Pi](/infrastructure/access-control/cardmaker-pi) provisioning station.

## System Implementations

### frontdoor (10.7.1.6)

*   **Role**: Primary Door Controller.
*   **Hardware**: Raspberry Pi 3B+. Uses **Pin 12** (Board mode) for the door latch. No external LEDs.
*   **Software**: Monolithic `access_10Bit.py` path `/home/chale/latch_access/new_lock/access_10Bit.py`.
*   **Polling Behavior**: Uses blocking `rfid.read()`, resulting in ~100% CPU usage during polling.
*   **Access**: `[REDACTED]` via SSH (22) or XRDP (3389).

### cobalt (10.7.1.59)

*   **Role**: Secondary Door Controller.
*   **Hardware**: Raspberry Pi 3B+. Uses **Pin 16** (Board mode) for the door latch. Includes active support for status LEDs (Red, White, Blue) and a Piezo buzzer.
*   **Software**: Modular state machine `my_door.py` path `/home/pi/my_door/my_door.py` with non-blocking `rfid.read_no_block()`, reducing CPU usage to ~22%.
*   **Access**: `[REDACTED]` via SSH.
*   **Network Constraints**:
    *   Uses `bond0` (Linux Bonding active-backup via eth0 `B8:27:EB:B2:60:42` and wlan0 `B8:27:EB:E7:35:17`).
    *   Tailscale constraints: MUST NOT advertise routes (`--advertise-routes=""`) and MUST NOT accept routes (`--accept-routes=false`) to prevent local subnet hijacking.

## System LED & Sound States (Cobalt)

| System State | LED Behavior | Sound Effect |
| :--- | :--- | :--- |
| **Idle / Waiting for Card** | White: Slow Pulse (Breathing) | Silent |
| **Card Detected (Validating)** | Bouncing: W, R, W, B, W, R, W (200ms) | health_chirp every 3s (after first 3s) |
| **Access Granted** | Blue: Solid ON (5s) | Mario Coin |
| **Access Denied** | Red: Fast Flash (10 times) | access_denied |
| **RFID Read Error** | Red+White+Blue: Rapid Flash | hardware_error |
| **System Startup** | Cycling: R, W, B, R, W, B, R | |
| **Crash Recovery Detected** | White: Slow Pulse, Red: Solid ON | |
| **Low Disk / Low Voltage** | Red+White: Slow Pulse | Low Chirp (220Hz) every 1min |

## Troubleshooting & Hardware Quirks (Cobalt)

- **Power Throttling**: Throttling state `0x50005` was resolved by replacing high-resistance wiring with a high-current cable (status now `0x0`).
- **RFID RC522 Non-Standard Version**: The reader reports version `0xb2`.
- **Automated Recovery Watchdog**: An internal CRC self-test runs every 30s. If the chip hangs, it flashes Red/White/Blue (ERROR state). The system automatically reboots the Pi if unresponsive for 5 minutes.
- **Analog Latch-up**: If a software reboot fails to clear a hard latch-up, a **physical power cycle (Cold Boot)** is required.

## Contributors

- [Ray Good](/contributors/ray) — Original hardware and software for both controllers
- [Connor Doherty](/contributors/connor) — Cobalt improvements, chiptune audio, and automated recovery
