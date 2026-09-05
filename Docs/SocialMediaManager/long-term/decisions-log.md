---
type: decisions
updated: 2026-09-05
tags: [memory, decision]
---
# Decisions

## 2026-09-05 — User-selected foundation

Accepted requirements: custom LAN-first application, collection before visual polish, selected stack in [[short-term/conversation-context]], Clerk login, multi-account Facebook OAuth, PostgreSQL RLS, portable cron/manual scans, security tooling, Obsidian primary memory. No runtime implementation yet.

## 2026-09-05 — Preserve actual vault

Observed `.obsidian` lives at `Docs/SocialMediaManager/.obsidian`. Use that vault; do not relocate it or overwrite Welcome.md. Root AGENTS.md points future sessions at it.

## 2026-09-05 — Proposed tenant and credential design

Tenant means business workspace; memberships support multiple users. Tenant rows get tenant_id and account rows also get account_id, with explicit principal/bootstrap policies. Per-connection credentials encrypted in DB; .env holds server configuration/keys. See [[Architecture]]. Proposed safeguards, not verified controls.

## 2026-09-05 — Durable scan endpoint design

Cron and UI enqueue durable jobs; HTTP does not run the whole scan. Database leases/idempotency allow recovery and later horizontal workers without a mandatory Redis dependency. Proposed implementation.

## 2026-09-05 — Deployment constraints

Clerk production requires domain/HTTPS, so raw HTTP LAN IP is not the production design. Source is under OneDrive; runtime database/secrets should be outside the sync tree. Hardware and final deployment paths pending.
