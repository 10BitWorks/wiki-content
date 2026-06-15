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

Wiki.js displays a folder's landing page when a user clicks on that folder. The landing page must be a file **at the same level as the folder** (sibling), named to match the folder. It is NOT placed inside the folder.

```
app-services.md                 ← landing page for /app-services (sibling of folder)
app-services/
  self-hosted.md                ← landing page for /app-services/self-hosted (sibling)
  self-hosted/
    kanidm.md
    n8n.md
    ...
  vendored.md                   ← landing page for /app-services/vendored (sibling)
  vendored/
    ...

equipment.md                    ← landing page for /equipment
equipment/
  3d-printer-murderbot.md
  ...

evaluations.md                  ← landing page for /evaluations
evaluations/
  frigate-hardware-eval.md

governance.md                   ← landing page for /governance
governance/
  board-2026.md
  ...

infrastructure/
  network-inventory.md          ← master device table (always at this path)
  iot.md                        ← landing page for /infrastructure/iot (sibling)
  iot/                          ← cameras, embedded systems, IoT devices
    frigate-nvr-server.md
    cardmaker-pi.md
    ...
  networking.md                 ← landing page for /infrastructure/networking (sibling)
  networking/
    pfsense.md
    headscale.md
    passkeys.md
    ...
  servers.md                    ← landing page for /infrastructure/servers (sibling)
  servers/
    zelda-server-proxmox.md
    link-server-proxmox.md
    ...

operations/                     ← physical access control and facility ops ONLY
  front-door-access-system.md

volunteers.md                   ← landing page for /volunteers
volunteers/
  connor.md                     ← notable member profiles
  ...
```

### Naming & Path Rules
- All folder and file names: **lowercase**, hyphens, alphanumeric only.
- No quotes or special characters in filenames.
- Index/landing pages are siblings of their folder, named to match it (e.g., `servers.md` sits next to `servers/`).
- **Standard Links:** Use standard markdown links `[Title](/folder/page-slug)` instead of Obsidian `[[wikilinks]]`. Wiki.js handles standard paths better.

## Formatting & Style Conventions

- **No Redundant H1s:** Wiki.js automatically renders the page title as an H1 heading. If the first `# Heading` in the content body matches the title, omit it to avoid double-headers in the Web UI.
- **Callouts:** Natively support Wiki.js colored callout blocks by putting `{.is-info}` (blue), `{.is-success}` (green), `{.is-warning}` (yellow), or `{.is-danger}` (red) immediately after a blockquote line.
- **Link Lists:** Format link grids using standard bullet lists followed immediately by `{.links-list}`.
- **Cross-linking:** Ensure every page has a minimum of 2 outbound links to keep the knowledge graph connected.
- **Git Commits as Logs:** Explain your reasoning in the extended commit body (`git commit -m "title" -m "reasoning"`). Never maintain a separate `log.md` file in the repository.

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
- `governance`, `board`, `membership`, `volunteer`

**Concepts & Evaluations**
- `evaluation`, `concepts`, `sso`, `passkeys`, `posix`

**Meta**
- `network-inventory`, `meeting-notes`, `policy`

## Frontmatter

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
- **Member Personal Devices** (phones, laptops) are strictly inventory rows in `network-inventory.md`. They never get dedicated pages.
- **IoT Devices** are considered infrastructure. Put them in `infrastructure/iot/` with a landing page at `infrastructure/iot.md`.
- **`operations/`**: Reserved strictly for physical access control and facility operations (e.g., front door system). Cameras, IoT devices, and embedded systems go in `infrastructure/iot/`.
- **`evaluations/`**: Research notes and hardware/software evaluations. Landing page at `evaluations.md`.
- **`volunteers/`**: Reserved for notable members (e.g., board members, project leads, or individuals with multiple significant non-financial contributions). Do not create pages for general members.
- **`.raw/`**: A hidden directory used strictly for agent memory (e.g. storing massive extracted text dumps from manuals or unparsed transcripts). Wiki.js ignores directories starting with `.` so these files will not clutter the human UI. Do not put polished content here.

---
*Last updated: 2026-06-15 — Corrected folder landing page convention (siblings not children); restructured operations/ to access-control only; moved IoT/cameras to infrastructure/iot/; renamed concepts/ to evaluations/.*
