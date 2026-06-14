---
title: Passkeys
created: 2026-06-14
updated: 2026-06-14
type: concept
tags: access-control, passkeys, sso
isPublished: true
---

# Passkeys (WebAuthn)

Passkeys are the primary authentication mechanism for the 10BitWorks infrastructure, managed via [kanidm](/entities/kanidm).

## Overview
Moving away from legacy passwords and basic MFA, the infrastructure relies on WebAuthn to provide phishing-resistant, high-speed execution for member logins.

## Migration & Bridge Period
Because WebAuthn credentials (Passkeys) cannot be migrated from the legacy Authentik stack, members are subject to a 7-day "Bridge Period".
During this time, members log in via a Slack or Email backup method to register their new Kanidm Passkey.
