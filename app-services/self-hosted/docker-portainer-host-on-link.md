---
title: Docker (Portainer) Host on Link
created: 2026-06-14
updated: 2026-06-15
type: service
tags: service, link-hosted, proxmox
description: "Primary Docker and Portainer host on Link, running most self-hosted services."
isPublished: true
---

Primary Docker host for 10BitWorks self-hosted services. Portainer is used to manage Docker stacks.

- Hostname: docker
- mDNS: docker.local
- IP: 10.7.1.25 (Static)
- OS: Debian (LXC 420 on Link)
- Model: Proxmox Container
- Port: 22 (ssh) - Docker VM Shell
- Port: 80 (http) - Nginx Web UI
- Port: 3000 (grafana) - Loomio
- Port: 5000 (registry) - Local Docker Registry
- Port: 5432 (postgresql) - Shared Database Instance
- Port: 8000 (door-admin) - Portainer Stack Management
- Port: 8080 (n8n) - n8n Automation Engine
- Port: 9443 (portainer) - Portainer Admin Dashboard
- Netdata: Streaming to 10.7.1.7 (Parent)

## Storage Architecture

The LXC originally had a 138GB root partition that repeatedly filled. In April 2026, a 2.7TB Proxmox drive (`mainshare`) was mounted at `/mnt/large_storage` to host high-growth data:

- `/mnt/media/downloads` (34GB) and `/mnt/media/media` (33GB)
- Zammad backups and attachment storage
- Symbolic links preserve compatibility with existing Docker volume paths

## Automated Maintenance

A "Maintenance Stack" runs daily on this host to prevent disk exhaustion:

```yaml
# Reclaims Docker assets older than 24h
docker system prune -af --filter 'until=24h'
# Reclaims unused volumes
docker volume prune -f
# Prunes Zammad backups older than 7 days
find /mnt/large_storage/zammad_backups -type f -mtime +7 -delete
```

## Hosted Services

- [Zammad](/app-services/self-hosted/zammad)
- [WordPress + CiviCRM](/app-services/self-hosted/wordpress-civicrm)
- [Loomio](/app-services/self-hosted/loomio)
- [n8n](/app-services/self-hosted/n8n)
- [BookStack](/app-services/self-hosted/bookstack)
- [Plane](/app-services/self-hosted/plane)
- [Vaultwarden](/app-services/self-hosted/vaultwarden)
- [Vikunja](/app-services/self-hosted/vikunja)
- [AppFlowy](/app-services/self-hosted/appflowy)
- [Authentik](/app-services/self-hosted/authentik)
- [Dozzle](/app-services/self-hosted/dozzle)
- [MCP](/app-services/self-hosted/mcp)
- [ResourceSpace](/app-services/self-hosted/resourcespace)

## Related

- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
- [Link Server](/infrastructure/servers/link-server-proxmox)
