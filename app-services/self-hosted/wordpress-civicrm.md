---
title: "Wordpress CiviCRM"
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, link-hosted, membership, website
description: "Public WordPress site and CiviCRM membership database at new.10bitworks.org."
isPublished: true
---

Public website and membership database for 10BitWorks. The production site is served via Nginx Proxy Manager at `https://new.10bitworks.org/`.

## Configuration

- **Host:** LXC 1010 (`website`) on Link
- **IP:** 10.7.1.10 (Static)
- **OS:** Debian GNU/Linux 11 (bullseye)
- **Ports:**
  - 22 (ssh) — CMS server shell
  - 80 (http) — WordPress/Apache UI
  - 443 (https) — Secure CiviCRM login

## CiviCRM MCP Server

A Model Context Protocol server for CiviCRM runs in Portainer. It originally failed in a restart loop because the `node:20-alpine` image lacks `git` (required for `npx` installs). The fix is to use `node:20-bookworm-slim`.

> Stack 121 in Portainer must be "Updated" to pull the corrected image.
> {.is-warning}

## Incident History

### April 4, 2026 — Site Downtime

**Status:** Resolved

**Symptoms:** `new.10bitworks.org` was unreachable. Nginx Proxy Manager could not reach the backend.

**Root Cause:** LXC 1010 was configured for DHCP and had drifted from the expected `10.7.1.10` IP. NPM was still routing to the static IP, so the container became unreachable.

**Resolution:** Set a static IP on LXC 1010:

```bash
pct set 1010 -net0 name=eth0,bridge=vmbr0,firewall=1,gw=10.7.1.1,ip=10.7.1.10/24,type=veth
```

Verification confirmed `10.7.1.10` and the public URL were responding with HTTP 200.

## Related

- [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
