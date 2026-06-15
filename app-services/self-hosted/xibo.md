---
title: Xibo
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, link-hosted, signage
description: "Digital signage management server (CMS) for 10BitWorks in-space displays."
isPublished: true
---

Xibo is the digital signage content management server for 10BitWorks. It runs as a Docker CMS stack on the [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link).

## CMS Configuration

- **Host:** LXC 420 `docker.local` on Link (`10.7.1.25`)
- **CMS Version:** 4.4.0 (Docker)
- **Database:** `xibo-cms-db-1` (MySQL)
- **XMR (Instant Updates):** ZeroMQ TCP on port `9505`
- **Resolution lock:** `1920x1080` enforced in the `display` table

## Player Hardware (Kiosk)

- **Device:** Zotac Zbox Mini PC
- **OS:** Debian Trixie
- **Display:** 1080p (1920x1080)
- **Network:** 10.7.1.142 (WiFi)
- **Desktop:** GNOME (X11) / Openbox
- **Timezone:** America/Chicago (synced via `10.7.1.1`)

## Player Software

The official Xibo Linux snap had hardcoded 720p and missing-library issues, so the space uses **Arexibo** (Rust/Qt implementation):

- **Source:** `https://github.com/birkenfeld/arexibo`
- **Build path:** `~/arexibo/target/release/arexibo`
- **Environment path:** `~/arexibo_env/`
- **Config:** `~/arexibo_env/config.json` forces 1080p fullscreen:

```json
{
  "width": 1920,
  "height": 1080,
  "fullscreen": true
}
```

## Kiosk Screensaver

The player runs as a background screensaver that activates after 60 seconds of idle time:

- **Service:** `xibo-screensaver.service` (systemd user unit)
- **Script:** `~/xibo-screensaver.sh`
- **Idle detection:** `xprintidle`
- **Check interval:** 0.5s
- **X authority:** Script exports `XAUTHORITY=/run/user/1000/gdm/Xauthority` to draw on the active GNOME display.

## Maintenance Commands

```bash
tail -f ~/arexibo.log
systemctl --user restart xibo-screensaver.service
pkill -9 arexibo
DISPLAY=:0 XAUTHORITY=/run/user/1000/gdm/Xauthority xprintidle
```

## Related

- [Digital Signage Player](/infrastructure/iot/digital-signage-player)
- [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
