---
title: "Loomio"
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, link-hosted, governance
description: "Loomio group decision-making service running on the Docker host at 10.7.1.25."
isPublished: true
---

Loomio is the group decision-making platform used for 10BitWorks governance discussions and votes. It runs as a Docker stack on the [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link).

## Configuration

- **Host:** LXC 420 `docker.local` on Link (`10.7.1.25`)
- **Database backups:** Persisted to `/data/compose/10/pgdumps`

## Backup Permission Fix

On March 29, 2026, `loomio-pgbackups-1` was stuck in a "Permission Denied" restart loop. The host directory `/data/compose/10/pgdumps` was owned by `root`. Ownership was changed to the `postgres` user (**UID 999**), which resolved the loop.

## Related

- [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
