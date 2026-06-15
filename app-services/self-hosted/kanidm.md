---
title: Kanidm
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: access-control, kanidm, passkeys, servers, sso
isPublished: true
---

# Kanidm at 10BitWorks

Kanidm serves as the Primary Identity Provider (IdP) and Directory Service for the 10BitWorks makerspace. It replaces the legacy Authentik stack to provide a high-performance, Rust-based, **Passkey-first** identity architecture.

## Deployment
- Hosted on Oracle Cloud (Ubuntu ARM) via Coolify.
- Bidirectional "Sync Partners" replicate identity state between the off-site Oracle Cloud instance and the Local Server (on-site).
- Deployed via GitOps from `10BitWorks-Makerspace/auth` repository.

## Features & Configuration
- **Authentication:** Native WebAuthn (Passkeys) is the default requirement.
- **POSIX Support:** Native Unix client (`kanidm-unixd`) provides centralized UID/GID management across all local servers via NSS/PAM without manual account creation.
- **SSO:** Provides OIDC authentication for internal services including Wiki.js and Nextcloud.

## Data Flow (Source of Truth)
1. **CiviCRM (Master):** All new members are created here first.
2. **Nextcloud (Secondary):** Accounts sync from CiviCRM.
3. **Kanidm (Tertiary):** SCIM pushes accounts from Nextcloud to Kanidm for authentication and physical access.

## Group Mapping & Access Control
Kanidm utilizes a single-axis status model to prevent stale permissions:
- `Good_Standing_Ever_Members` -> Parent group.
- `status_current` -> Active members. The ONLY valid parent for Admin Roles. Maps to Wiki.js "Members".
- `role_it_admins` -> Infrastructure and server access. Maps to Wiki.js "Administrators".

## Related Concepts
- [passkeys](/concepts/passkeys)
- [pfsense](/infrastructure/networking/pfsense) (Captive portal ties into identity)

