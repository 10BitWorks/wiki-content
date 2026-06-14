---
title: Hosted Services Maintenance Policy
created: 2026-06-14
updated: 2026-06-14
type: policy
tags: [proxmox, servers]
description: "Documentation of host maintenance policies and Elasticsearch watermarks."
---

# Hosted Services Maintenance

To prevent service instability caused by disk exhaustion (specifically impacting Elasticsearch on LXC `docker.local`), the following automated maintenance tasks and configurations must be preserved.

## Automated Maintenance Tasks
These tasks run on the Docker host (`10.7.1.25`):
- **System Log Vacuum:** Runs via host cron every 72h. Caps `/var/log/journal` at 500MB.
- **Docker Prune:** Runs via Portainer 'Maintenance Stack' every 72h. Prunes unused images, containers, and build cache older than 72h.

## Zammad Configuration Requirements
- **Attachment Storage:** Attachments must remain configured for **FileSystem (File)** storage, NOT Database storage. Database storage inflates the PostgreSQL dump massively.
- **Backup Retention:** The `HOLD_DAYS` variable in Portainer should be kept to **7 or 10**.
- **Elasticsearch Watermarks:**
  - Low: `90%`
  - High: `95%`
  - Flood Stage: `98%` (Marks indices read-only if exceeded).

## CiviCRM MCP Server Image
- The CiviCRM MCP Server requires `node:20-bookworm-slim`. Do not use `node:20-alpine` as it lacks `git`, causing infinite restart loops during `npx` installs.

## Loomio Backups
- The host directory `/data/compose/10/pgdumps` must be owned by the `postgres` user (**UID 999**).
