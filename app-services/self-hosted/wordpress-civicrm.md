---
title: "WordPress + CiviCRM"
created: 2026-06-14
updated: 2026-06-16
type: service
tags: service, oracle-hosted, coolify, membership, website
description: "Public WordPress site and CiviCRM membership database at 10bitworks.org."
isPublished: true
---

Public website and membership database for 10BitWorks. The production site is served at `https://10bitworks.org/` from a Coolify-managed Docker stack running on Oracle Cloud.

## Configuration

- **Deployment:** Coolify on Oracle Cloud ARM64 (Ampere A1)
- **Repository:** `10BitWorks/website-stack`
- **Main domain:** `10bitworks.org`
- **Stack:**
  - FrankenPHP (PHP 8.3) — web server + PHP runtime
  - MariaDB 10.11 — WordPress and CiviCRM schemas
  - Valkey — in-memory cache store (libre Redis fork)
- **Container:** `frankenphp-*` managed by Coolify; Traefik handles TLS termination and HTTP/3; FrankenPHP listens on plain HTTP internally.

## Caching Architecture

The site is optimized so anonymous visitors receive cached HTML without PHP execution, while logged-in users and dynamic endpoints still run through WordPress/CiviCRM.

### Why W3 Total Cache?

[W3 Total Cache](https://wordpress.org/plugins/w3-total-cache/) is the active caching plugin because it is the only one in the stack that provides all three required layers:

1. **Full-page cache** with static `.html` file generation (Disk: Enhanced mode).
2. **Database query cache** backed by Valkey.
3. **Object cache** backed by Valkey.

The database query cache was specifically required to prevent CiviCRM from exhausting PHP memory with large uncached query result sets.

### Page Cache: Disk Enhanced + Caddy

W3TC "Disk: Enhanced" writes static files such as:

```
wp-content/cache/page_enhanced/<host>/<path>/_index_slash_ssl.html
```

The FrankenPHP/Caddy configuration in the repo maps anonymous `GET`/`HEAD` requests to those files. When a cache file exists, Caddy serves it directly and PHP never starts. The response headers include:

```
X-Cache-Handler: w3tc-enhanced-file
Cache-Control: public, max-age=3600
```

Cached requests are skipped for:

- Logged-in users (`wordpress_logged_in*` cookie)
- Comment authors (`comment_author*` cookie)
- Password-protected posts (`wp-postpass*` cookie)
- `/wp-admin*`, `/wp-login.php`, `/wp-json*`, `/xmlrpc.php`
- Static assets under `/wp-content/uploads*`, `/wp-content/plugins*`, `/wp-content/themes*`, `/wp-includes*`

### DB and Object Cache

Both database query cache and object cache are handled by W3TC and stored in the in-stack Valkey container at `valkey:6379`. This keeps hot CiviCRM and WordPress data in memory instead of re-deriving it on every PHP request.

### Redis Object Cache Plugin

The `redis-cache` plugin is baked into the Docker image but kept **inactive**. It only implements WordPress object cache and cannot replace W3TC's page cache or database query cache. It is retained as an emergency fallback object-cache provider, but the active provider is W3TC.

### Auto-Healing

`docker-entrypoint.sh` enforces the following W3TC settings on every container start:

- `dbcache.engine` = `redis` (Valkey)
- `objectcache.engine` = `redis` (Valkey)
- `pgcache.engine` = `file` (Disk: Enhanced)
- Redis server = `valkey:6379`

### Verification

```bash
# Anonymous page (should show x-cache-handler: w3tc-enhanced-file)
curl -sS -D - https://10bitworks.org/ | grep -i x-cache

# Admin/dynamic endpoint (should show x-powered-by: PHP)
curl -sS -D - https://10bitworks.org/wp-admin/ | grep -i x-powered
```

## CiviCRM Configuration

- **Production CiviCRM**: WordPress plugin running inside the FrankenPHP container.
- **WordPress root**: `/var/www/html`
- **CiviCRM settings**: `/var/www/html/wp-content/uploads/civicrm/civicrm.settings.php`
- **Databases**: `wordpress` and `civicrm` schemas in MariaDB
- **Management tools**:
  - `wp` (WP-CLI) at `/usr/local/bin/wp`
  - `cv` (CiviCRM CLI) at `/usr/local/bin/cv`

## Constraints

- WordPress must host CiviCRM to maintain SSO integration with Kanidm.
- A standalone Docker CiviCRM deployment is unsuitable for production due to lack of SSO support.
- No third-party CDN (Cloudflare, etc.) is used; static-site speeds are achieved entirely within the stack.

## Incident History

### April 4, 2026 — Site Downtime (legacy Link-hosted deployment)

**Status:** Resolved

**Symptoms:** `new.10bitworks.org` was unreachable. Nginx Proxy Manager could not reach the backend.

**Root Cause:** LXC 1010 was configured for DHCP and had drifted from the expected `10.7.1.10` IP. NPM was still routing to the static IP, so the container became unreachable.

**Resolution:** Set a static IP on LXC 1010:

```bash
pct set 1010 -net0 name=eth0,bridge=vmbr0,firewall=1,gw=10.7.1.1,ip=10.7.1.10/24,type=veth
```

Verification confirmed `10.7.1.10` and the public URL were responding with HTTP 200.

## Related

- [10BitWorks Website Stack on GitHub](https://github.com/10BitWorks/website-stack)
- [Kanidm Identity Server](/app-services/self-hosted/kanidm)
- [Headscale Coordination Server](/infrastructure/networking/headscale-coordination-server)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
- [Docker (Portainer) Host on Link](/app-services/self-hosted/docker-portainer-host-on-link)