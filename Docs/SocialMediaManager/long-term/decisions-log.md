---
type: decisions
updated: 2026-09-05
tags: [memory, decision]
---
# Decisions

## 2026-09-05 — Final scope approved

Corey confirmed the consolidated MVP with "This sounds correct". [[MVP Scope]] is approved; readiness interview is complete. No further shared-understanding approval is needed. Implementation/session choice is next; no runtime work has been performed. Earlier pending-confirmation entries are historical.

## 2026-09-05 — Readiness interview, round 4 and consolidated MVP

User-confirmed, not implemented/verified: post list includes date/platform/caption or description/available thumbnail/tags/original link. Desktop downtime and missed observations are accepted local-host risks. Stop refreshing posts after age one year but retain history/tags; disconnect is separate from deletion. Keep history until explicit deletion, subject to the previously accepted provider requirements; the user's GDPR reference is not a compliance finding. Keep backups on the same system for now; off-system backup is explicitly deferred. Do not silently introduce cloud backup.

Consolidated accepted scope in [[MVP Scope]]. Final shared-understanding confirmation remains pending; this interview did not authorize implementation. Clerk Hobby is a billing plan, separate from development/production instances; paid upgrade alone does not perform production setup. LAN sign-in/session behavior and real provider account/metric access remain empirical acceptance gates.

## 2026-09-05 — Readiness interview, round 3

User-confirmed, not implemented/verified: first providers Facebook/Instagram; Clerk Hobby with authentication from the beginning and minimal future migration desired; API/web on personal PC exposed to LAN at fixed port/IP or optional router DNS name. This is the desired deployment, not evidence that exact Clerk/OAuth origins are supported. Hobby subscription and development/production instance configuration remain distinct.

Import last 90 days. Capture post measurements daily through age 30 days, then weekly through age one year; daily account follower/subscriber count, views and likes when available. Historical gaps are acceptable and must remain visible. Overrides prior age-based cadence proposal. Exact metric definitions/account eligibility and historical source access await live verification.

## 2026-09-05 — Readiness interview, round 2

User-confirmed, not implemented: core includes account connection, posts, measurement snapshots, manual tagging and basic comparisons; prioritize ingestion/history/tagging. Defer effort tracking and the entire AI experience from MVP. Preserve future AI possibility without implementing it now. Engagement targets/scoring are unnecessary; consolidate available raw engagement and follower measurements. Derived rates require validated source definitions.

User-confirmed tag behavior: any imported post can receive tags retrospectively. Keep similar tags distinct until explicit cleanup; allow rename and bulk normalization of selected variants to one label. Zero operating cost means no added costs; locally used third-party integrations must fit free usage. Exact network/deployment boundary remains open.

Research evidence (2026-09-05, not live integration verification): [Clerk pricing](https://clerk.com/pricing) offers a free Hobby plan; [environment guidance](https://clerk.com/docs/guides/development/managing-environments) says development is unsuitable for production and users do not transfer to production. [Production deployment](https://clerk.com/docs/guides/development/deployment/production) requires domain/DNS and HTTPS. [Local production-key troubleshooting](https://clerk.com/docs/guides/development/troubleshooting/using-production-keys-in-development) describes its hosts-file workaround as discouraged/unsupported; earlier private-DNS proposal is not established as a supported deployment. [Meta-owned Instagram documentation](https://www.postman.com/meta/instagram/folder/u4g5a2a/instagram-api-with-facebook-login) confirms professional IG plus linked Page for selected Facebook Login route. Actual account eligibility/metrics remain unverified.

## 2026-09-05 — Readiness interview, round 1

User-confirmed requirements, not implemented or verified: optimize content effort and posting schedule for engagement; both spouses can tag and analyze posts; wife uses manual UI and Corey may use AI analytics/synthesis and tag suggestions, with final human say on applied tags. No AI-generated content for social posting. MCP/browser agent interaction is allowed in principle; exact access and approval mechanics remain open.

Initial audience is private household use. Maintain product-capable tenancy and portable deployment with minimal future rework desired; this does not establish public-launch readiness. Zero local operating cost is required; precise cost scope remains unresolved. No fixed maintenance budget/deadline; agree the approach, then build/refine a core iteratively. Interview remains active; no implementation authorization in this exchange.

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
