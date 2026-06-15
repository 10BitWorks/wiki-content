---
title: Hosted Services Maintenance Policy
created: 2026-06-14
updated: 2026-06-15
type: policy
tags: proxmox, servers
description: "Documentation of host maintenance policies, storage architecture, and resource containment rules."
isPublished: true
---

# Hosted Services Maintenance

To prevent service instability caused by disk exhaustion and runaway resource usage, the following policies must be preserved.

## Docker Host Maintenance

The "Maintenance Stack" on LXC 420 (`docker.local`, `10.7.1.25`) runs daily:

```yaml
# Reclaims Docker assets older than 24h
docker system prune -af --filter 'until=24h'
# Reclaims unused volumes
docker volume prune -f
# Prunes Zammad backups older than 7 days
find /mnt/large_storage/zammad_backups -type f -mtime +7 -delete
```

The host cron job also vacuums `/var/log/journal` every 24 hours.

## Zammad Configuration Requirements

- **Attachment Storage:** Attachments must remain configured for **FileSystem (File)** storage, NOT Database storage. Database storage inflates the PostgreSQL dump massively.
- **Backup Retention:** The `HOLD_DAYS` variable in Portainer should be kept to **7 or 10**.
- **Elasticsearch Watermarks:**
  - Low: `90%`
  - High: `95%`
  - Flood Stage: `98%` (marks indices read-only if exceeded)

## CiviCRM MCP Server Image

The CiviCRM MCP Server requires `node:20-bookworm-slim`. Do not use `node:20-alpine` as it lacks `git`, causing infinite restart loops during `npx` installs.

## Loomio Backups

The host directory `/data/compose/10/pgdumps` must be owned by the `postgres` user (**UID 999**).

## Storage Offloading

High-growth data must be stored on the 2.7TB `mainshare` drive mounted at `/mnt/large_storage` on LXC 420, not on the 138GB root partition. Symbolic links preserve existing Docker volume paths.

## Memory & CPU Containment (Zelda Node)

To prevent rogue high-resource containers (e.g., Frigate/cameras) from impacting critical services (e.g., Door Access), the following rules are mandated on the **Zelda** host:

| Rule | Container | Value | Rationale |
| :--- | :--- | :--- | :--- |
| **Disable Swap** | `cameras` (LXC 105) | `pct set 105 --swap 0` | Memory leaks fail fast via OOM instead of host thrashing |
| **CPU Priority** | `door1` (LXC 204) | `cpuunits: 2048` | Critical access control gets CPU preference |
| **CPU Priority** | `cameras` (LXC 105) | `cpuunits: 512` | Background video service gets lower priority |
| **OOM Protection** | `door1` (LXC 204) | `oom_score_adj -500` | Protected from the OOM killer |
| **OOM Victim** | `cameras` (LXC 105) | `oom_score_adj 500` | Preferred OOM victim |
| **Host Swappiness** | Zelda host | `vm.swappiness = 10` | Prevents premature swapping of resident memory |
