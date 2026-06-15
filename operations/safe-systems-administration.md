---
title: Safe Systems Administration
created: 2026-06-15
updated: 2026-06-15
type: policy
tags: operations, administration
description: "Rules of thumb for safely administering 10BitWorks infrastructure."
isPublished: true
---

# Safe Systems Administration

These rules reduce the risk of breaking multiple systems during maintenance.

## Bulk Mutating Operations

Never perform bulk mutating operations (like writing to `authorized_keys` or changing passwords) without testing the methodology on a single, non-critical target first.

## Verification

Always verify the success of a single-node test before applying changes to other nodes.

## File Persistence

- Prefer `>>` (append) over `>` (overwrite) for configuration files unless a full replacement is explicitly necessary.
- If a full replacement is required, create a backup first.

## Proxmox Guest Agent

`qm guest exec` does not support standard input piping. Use `pvesh` for direct file writes or multi-stage commands.

## Tailscale Local Loop

If a host is reachable via Tailscale (`100.x.x.x`) but filtered/stealthed on its local IP (`10.7.1.x`), it is likely an asymmetric routing issue. Fix by disabling route acceptance:

```bash
sudo tailscale set --accept-routes=false
```

Check `ip rule` for priority rules pointing to Table 52.

## Uptime Monitoring

Always pause relevant Uptime Kuma monitors before restarting services or rebooting hardware to avoid false alerts.

## Related

- [Headscale Coordination Server](/infrastructure/networking/headscale-coordination-server)
- [Tailscale Exit Node (LAC)](/infrastructure/networking/tailscale-exit-node-lac)
- [Hosted Services Maintenance Policy](/policies/hosted-services-maintenance)
