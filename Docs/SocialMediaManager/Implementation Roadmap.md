---
type: roadmap
updated: 2026-09-05
tags: [planning]
---
# Implementation Roadmap

Readiness interview steering: [[MVP Scope]] is the current product cut. Authentication remains first; post ingestion, snapshots and manual tagging are the first useful outcome. Basic comparisons belong in MVP. AI/agent access is entirely deferred. Await final shared-understanding confirmation/build instruction before starting implementation. Earlier milestone numbering is implementation sequencing, not authorization to postpone all user-facing tagging until optional agent work.

## 0 — Foundation (documentation complete)

Requirements, selected stack, tenancy boundaries, security plan and memory recorded. This does not implement any runtime control.

## 1 — Authenticated skeleton

Scaffold workspaces for React/Vite, NestJS, shared contracts and Prisma. Select compatible supported versions, install and lock dependencies, create placeholder-only .env.example and local PostgreSQL setup. Add Clerk login/setup and backend verification, tenant provisioning/membership and RLS migrations. First screens: login, workspace setup, account settings, scan history. Real provider credentials must be configured locally by the user. Development fixtures must be clearly labeled and isolated from production observations.

Acceptance: build/type checks pass; anonymous requests denied; two test tenants cannot cross boundaries via API or real runtime DB role; no-context RLS fails closed; unauthorized self-elevation rejected. Check role flags and pooled concurrency isolation.

## 2 — Meta connection pilot

Create/configure Meta app with the user, verify actual account types, permissions, app access mode/review requirements, callback URLs and SDK endpoints. Implement state-bound account linking, encrypted tokens, account selection, disconnect and reauthorization. Populate the metric availability matrix with actual responses and native comparisons. Do not assume private use waives Meta requirements.

Acceptance: replay/wrong-tenant OAuth rejected; selectable accounts come from authorized provider assets; unavailable metrics labeled; no credential leaks. Live proof requires user-owned Meta and Clerk configuration, not invented credentials.

## 3 — Durable scans

Implement authenticated manual and cron triggers into PostgreSQL-backed jobs, tenant-scoped worker, discovery, pagination, observations, retry and health reporting. Execute daily pilot for 7–14 days before declaring reliability. Time passage must be observed, not simulated and reported as live evidence.

Acceptance: manual and scheduled paths work; overlapping triggers do not duplicate runs; crash recovery works; partial scans surfaced; stale credentials visible; data can be backed up/restored. Retention policy implemented before real raw response storage.

## 4 — Security automation and hardening

Introduce CI early with first executable code. Configure Semgrep, Gitleaks, Dependabot and Snyk on the authorized GitHub repository; add authenticated DAST on an isolated target. Decide IAST tooling explicitly. Verify production hostname/TLS, backup restore, deletion/export and audit. No deployment or repository creation has been requested as a separate external action yet.

## 5 — Complete MVP analysis; future agent access deferred

Deliver manual tagging/post browsing alongside the first usable collection flow, including historical-post tagging and user-directed bulk tag normalization. Complete basic same-age comparisons by tag/format/weekday/time after collection is trustworthy. Richer timeline/heatmap/word-map views can follow as useful. All Hermes/MCP/AI interaction is outside MVP. Add other providers/business outcomes separately.

## Inputs to resolve during implementation

- Pi model/RAM/OS/storage and desktop runtime availability.
- Actual Facebook Page/profile and Instagram account status/linkage.
- Clerk and Meta app configuration; domain/TLS and callback approach.
- GitHub repository destination and security-tool access (when ready).
- Retention choices and agreed scope of hosted-model data access.

These do not block documentation or a credential-free scaffold. They block claiming live authentication/integration/deployment as working.
