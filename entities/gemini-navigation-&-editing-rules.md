---
title: Gemini Navigation & Editing Rules
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: [misc, network]
description: "Network details and configuration for Gemini Navigation & Editing Rules"
---

# Gemini Navigation & Editing Rules

- **Hierarchy**: Use `# Project Category` (H1) and `## Brief Description` (H2).
- **Separate Bullets**: Every Hostname, mDNS address, IP address, Port, MAC address, OS, and Machine Model must be its own bullet point.
- **Hostname First**: The first bullet for every host MUST be the hostname.
- **mDNS Second**: The second bullet MUST be the mDNS address (`.local`). If `.local` is not supported or unverified, leave it as **Unknown**.
- **Port Descriptions**: Every port bullet MUST describe the service running there.
- **DO NOT ASSUME**: If data is missing (mDNS, OS, Model), leave it as **Unknown** or **TODO**. Never invent placeholders. Don't trust hostnames to be informative.
- **Standard Access**: Unless otherwise specified, the SSH user is `root` and authentication is handled automatically via authorized public key.
- **Monitoring**: Netdata is used for real-time monitoring. The **Parent Node** is `link.local` (10.7.1.7). Children stream to the parent using the key `c38f3006-3e1d-4c29-ac41-fb77fc59578a`.
- **Scope-Locked Details**: Niche metadata (Credentials, logic paths, troubleshooting) belong in the `GEMINI.md` file within the respective project subfolder.
- **Guardrails**: Do NOT remove, rename, or modify these rules without explicit user permission.
- **Keep Updated**: When you notice something in this list needs updating, update it. Non-static IPs may move, so use mac addresses to track these changes.

