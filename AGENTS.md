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
- File names: lowercase, hyphens, alphanumeric only, absolutely NO quotes or special characters (e.g., `laser-cutter-sop.md`). Wiki.js routing breaks on unescaped characters.
- **No Redundant H1s:** Wiki.js automatically renders the page title as an H1 heading. If the first `# Heading` in the content body matches the title, omit it to avoid duplication.
- Every wiki page starts with YAML frontmatter (see below)
- Use standard markdown links `[Title](/folder/page-slug)` instead of `[[wikilinks]]` (minimum 2 outbound links per page). Wiki.js handles standard paths better.
- Feel free to use advanced Markdown (PlantUML, KaTeX, MultiMarkdown tables, Task lists) — the Wiki.js rendering pipeline has full support enabled.
- **Callouts & Styling:** Natively support Wiki.js-style colored blocks using `> Text` followed immediately by `> {.is-info}` or `> {.is-warning}`. Use `{.links-list}` for links lists.
- When updating a page, always bump the `updated` date
- Every new page must be added to `index.md` under the correct section
- **Git Commits as Logs:** Explain your reasoning in the extended commit body. Do not maintain a separate log.md.

## Frontmatter
```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | policy | manual | meeting | query | summary
tags: tag1, tag2, tag3
sources: raw/articles/source-name.md
description: A short one-sentence summary for Wiki.js page cards
isPublished: true
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

