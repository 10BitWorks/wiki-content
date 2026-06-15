---
title: AGENTS
description: "Rules and structure for the 10BitWorks knowledge base"
isPublished: true
---

# 10BitWorks Knowledge Base — Agent Rules

## Core Philosophy

**Page vs Row Rule** (strict):
- A **page** is something with meaningful operational depth (config, troubleshooting, history, procedures, relationships).
- A **row** is just metadata (MAC, IP, last seen, generic model). These belong in inventory tables, never as their own page.

**Test**: "Can I write several useful sections about this, or is it just a line in a spreadsheet?"

## Folder Structure & Index Pages

We use Wiki.js's folder-index behavior. A page named after its folder becomes the automatic index for that folder.

```
infrastructure/
  network-inventory.md          ← master device table (always at this path)
  servers/
    servers.md                  ← index for /infrastructure/servers
    zelda-server-proxmox.md
    link-server-proxmox.md
    oracle-cloud.md
  networking/
    networking.md
    pfsense.md
    headscale.md
    tailscale.md

services/
  hosted/
    hosted.md                   ← index for /services/hosted
    kanidm.md
    n8n.md
    civicrm.md
    zammad.md
    ...

operations/
  front-door-access.md
  cameras-frigate.md
  digital-signage.md

equipment/
  equipment.md                  ← index for /equipment
  laser-cutter.md
  3d-printer-murderbot.md
  ...

devices/
  personal/                     ← member devices (usually just tables)
  iot/

concepts/
governance/
```

### Naming Rules
- All folder and file names: **lowercase**, hyphens, alphanumeric only.
- No quotes or special characters in filenames.
- Index pages are always named after their parent folder (`servers.md`, `hosted.md`, `equipment.md`).

## Tags — Host-Based Tagging

Use **host-based** tags for anything that runs on a specific machine:

- `zelda-hosted`
- `link-hosted`
- `oracle-hosted`
- `pfsense-hosted`

Additional required tags:
- Every real page gets at least one domain tag from the taxonomy below.
- Services also get the tag `service`.
- Equipment also gets the tag `equipment`.
- The master inventory page gets the tag `network-inventory`.

## Updated Tag Taxonomy

**Infrastructure**
- `proxmox`, `kanidm`, `tailscale`, `coolify`, `pfsense`, `headscale`
- `servers`, `networking`, `zelda-hosted`, `link-hosted`, `oracle-hosted`

**Services**
- `service`, `hosted`

**Operations**
- `operations`, `access-control`, `cameras`, `digital-signage`

**Equipment**
- `equipment`, `laser-cutter`, `3d-printer`, `woodshop`, `metalshop`

**Governance & People**
- `governance`, `board`, `membership`

**Concepts**
- `concepts`, `sso`, `passkeys`, `posix`

**Meta**
- `network-inventory`, `meeting-notes`, `policy`

## Frontmatter (updated)

```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: server | service | equipment | policy | concept | governance | reference
tags: zelda-hosted, service, proxmox
description: One-sentence summary for Wiki.js cards and search
isPublished: true
---
```

## Workflow for New Content

1. **Is it just attributes?** → Add a row to `network-inventory.md` (or the appropriate category table).
2. **Does it have real depth?** → Create a page in the correct folder.
3. **Always** add the appropriate `*-hosted` tag when relevant.
4. **Always** link from the relevant inventory table.

## Git & Commits

- All edits go through the Git repository at `~/wiki`.
- Use descriptive commit messages. Put reasoning in the extended body.
- Never maintain a separate `log.md`.

## Special Pages

- `network-inventory.md` is the single source of truth for IP/MAC lookup. It may contain multiple tables (Core, Cameras, IoT, Workshop). Only link to pages that actually exist.

This structure is designed to be:
- Extremely predictable for agents
- Still pleasant for human browsing via Wiki.js folder indexes
- Resistant to the "thousands of empty stubs" problem

---
*Last updated: 2026-06-15 — Major restructure to separate infrastructure, services, and equipment with host-based tagging.*