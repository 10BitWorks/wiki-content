---
title: AGENTS
description: 
published: true
date: 2026-06-14T10:42:18.944Z
tags: 
editor: markdown
dateCreated: 2026-06-14T09:51:38.498Z
---

# 10BitWorks Knowledge Base Schema

## Domain
10BitWorks Makerspace: IT infrastructure, physical space operations, machine manuals, governance, and organizational knowledge.

## Conventions
- File names: lowercase, hyphens, no spaces (e.g., `laser-cutter-sop.md`)
- Every wiki page starts with YAML frontmatter (see below)
- Use `[[wikilinks]]` to link between pages (minimum 2 outbound links per page)
- When updating a page, always bump the `updated` date
- Every new page must be added to `index.md` under the correct section
- Every action must be appended to `log.md`

## Frontmatter
```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | policy | manual | meeting | query | summary
tags: from taxonomy below
sources: [raw/articles/source-name.md]
# Optional quality signals:
confidence: high | medium | low
contested: true
---
```

## Tag Taxonomy
- Infrastructure: `proxmox`, `kanidm`, `tailscale`, `coolify`, `pfsense`, `network`, `servers`, `cameras`, `docker`
- Operations: `membership`, `onboarding`, `finance`, `governance`, `board`
- Machines: `laser-cutter`, `3d-printer`, `woodshop`, `metalshop`, `electronics`
- Identity: `sso`, `passkeys`, `posix`, `access-control`
- Meta: `meeting-notes`, `planning`, `brainstorming`

## Page Thresholds
- **Create a page** when an entity/concept is central to operations (e.g., Kanidm, Laser Cutter).
- **DON'T create a page** for passing mentions or temporary states.
- **Split a page** when it exceeds ~200 lines.
