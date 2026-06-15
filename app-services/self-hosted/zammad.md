---
title: Zammad
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, link-hosted, support
description: "Zammad support ticketing service running on the Docker host at 10.7.1.25."
isPublished: true
---

Zammad is the support ticketing system used by 10BitWorks. It runs as a Docker stack on the [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link).

## Configuration

- **Host:** LXC 420 `docker.local` on Link (`10.7.1.25`)
- **Stack:** Managed in Portainer
- **Attachment Storage:** Filesystem (Docker volume `zammad_zammad-storage`)
- **Backups:** Docker volume `zammad_zammad-backup`, symlinked to `/mnt/large_storage/zammad_backups`
- **Database:** PostgreSQL with Elasticsearch search backend

## Elasticsearch Watermarks

To prevent premature read-only lockouts on the 138GB root partition, the cluster watermarks were relaxed in March 2026:

| Level | Value |
| :--- | :--- |
| Low | 90% |
| High | 95% |
| Flood Stage | 98% |

Clearing a read-only block requires:

```bash
curl -X PUT 'localhost:9200/_all/_settings' -d '{"index.blocks.read_only_allow_delete": null}'
```

## Backup Retention

After database optimization, dumps dropped from ~700MB to ~150MB. `HOLD_DAYS` can safely be set to **7 or 10**.

## Incident History

### March 28, 2026 — Zammad Instability

**Status:** Resolved

**Symptoms:** Zammad UI was intermittently unresponsive and background jobs failed.

**Root Cause:** LXC 420 reached **99% disk usage**. Elasticsearch entered flood-stage read-only mode once disk usage exceeded 95%.

**Space Consumers:**

- Media files: ~25GB in `/mnt/media`
- Docker build cache: ~14GB
- Zammad attachments bloating PostgreSQL backups: ~700MB daily dump
- System logs: ~3.5GB over 28 days

**Resolution:**

- Vacuumed system journal (3.5GB reclaimed)
- Pruned Docker images/containers/build cache (~17GB reclaimed)
- Deleted 7 oldest Zammad backups (4.9GB reclaimed)
- Cleared Elasticsearch read-only block
- Migrated attachments from DB storage to Filesystem storage
- Ran `VACUUM FULL` on `store_provider_dbs`

**Result:** Database dump size reduced from ~700MB to ~150MB.

### April 11, 2026 — Docker Host Outage

**Status:** Resolved

**Symptoms:** Portainer, Zammad, and CiviCRM were down or blipping in Uptime Kuma.

**Root Cause:** LXC 420 reached **100% disk usage**. The 72-hour maintenance cycle was too infrequent.

**Resolution:**

- Reclaimed 7.1GB via manual log vacuum and `docker system prune`
- Tightened maintenance to run every **24 hours** with `until=24h` prune filter
- Offloaded high-growth data to the 2.7TB `mainshare` drive at `/mnt/large_storage`

### April 24, 2026 — System-Wide Storage Overhaul

**Status:** Implemented

**Actions:**

- Mounted `mainshare` into LXC 420 at `/mnt/large_storage`
- Moved `/mnt/media/downloads` (34GB) and `/mnt/media/media` (33GB)
- Moved Zammad backups and storage to `/mnt/large_storage/`
- Created symlinks to preserve Docker stack compatibility
- Deleted 81 malformed "Failed Emails" and a stuck "Data Privacy Task" from July 2025

## Related

- [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
