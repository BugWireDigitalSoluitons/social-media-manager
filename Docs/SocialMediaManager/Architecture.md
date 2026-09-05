---
type: design
status: proposed
updated: 2026-09-05
tags: [architecture, security]
---
# Architecture

Use the selected stack in [[short-term/conversation-context]]. Begin as a modular monolith with a separate durable worker process and one PostgreSQL database. No microservice fleet is needed. Proposed workspace: `apps/web`, `apps/api`, `apps/worker`, `packages/contracts`, `packages/database`, `infra`, and this vault. Pin compatible runtime and dependency versions during scaffolding; no versions have been tested yet.

## Identity and tenancy

Clerk owns user authentication. A tenant represents a business/workspace, not a login and not a social account. A workspace can have multiple members and multiple social accounts. Initially owner/admin/viewer: owners manage membership and deletion, owners/admins link accounts and trigger scans, viewers read permitted analytics. Start invitation-only for the private pilot; keep the model extensible to signup.

Validate Clerk session signature, issuer, expiration, token type, and authorized parties on the backend. A tenant ID from a route/header is a requested workspace, not authorization. Resolve the authenticated subject's active membership server-side before any tenant operation. Keep social OAuth separate from Clerk login.

All application tables receive RLS. All tenant-owned rows carry non-null `tenant_id`; social-account-owned rows also carry non-null `account_id`. Workspace-level memberships/tags do not get a fictitious social account. Identity/bootstrap records need principal-scoped policies; document those explicitly. Migration metadata is an infrastructure table, not tenant content, and must not be exposed to the runtime role.

Use composite unique constraints and foreign keys including tenant_id for relationships, so a row cannot refer to another tenant's account or post. Tenant context alone is insufficient if future roles have account-specific permissions; add explicit account grants when introduced.

## PostgreSQL and Prisma boundary

Version RLS SQL with Prisma migrations. Runtime roles must not be superuser, table owner, or BYPASSRLS. ENABLE and FORCE RLS; specify read/write policy expressions including WITH CHECK. Missing context denies access. Use separate migration credentials.

Set tenant/principal context transaction-locally with parameterized set_config calls inside a Prisma transaction and perform all protected queries on that transaction client. Never set session-scoped tenant context on pooled connections. Never fall back to the unscoped Prisma client. Keep remote API calls outside open database transactions.

Membership bootstrap must use a narrowly scoped principal policy/query; it must not recurse through its own RLS policy or allow clients to assign themselves owner. Workspace plus owner membership creation is atomic through a carefully reviewed provisioning path. Test actual runtime credentials, not migration credentials.

## Connections and credentials

Use Facebook Login OAuth as requested, validating actual eligible account types and scopes before committing to available metrics. The Facebook Login Instagram route requires a professional Instagram account linked to a Page. Use the official SDK behind a provider adapter; verify current SDK coverage and use documented Graph requests where necessary.

OAuth state is unpredictable, short-lived, single-use, stored server-side, and bound to user, workspace, provider, and allowed redirect. Consume atomically, recheck membership at callback, exchange codes server-side, and validate selected account IDs against provider-authorized assets. Request only needed scopes. Use PKCE where the selected provider flow supports it. Handle denied grants, partial access, reauthorization, revocation, and data-deletion requests.

Deployment secrets belong in restricted, gitignored .env files. Per-connection access/refresh tokens belong encrypted in PostgreSQL, with authenticated encryption, a unique nonce, key version, and tenant/connection binding. Encryption keys stay separate from the database in .env initially; design for later key management and rotation. Tokens never enter React state, logs, vault, analytics API responses, or agent tools. Do not store user passwords.

## Jobs and scheduling

Cron sends authenticated POST requests to enqueue due scans. UI POST requests enqueue authorized account scans. Return 202 plus a durable job ID; do not keep the HTTP request open during collection or start an untracked in-memory task.

Use PostgreSQL-backed jobs with atomic claiming, leases, retry limits, backoff/jitter, idempotency, per-account overlap prevention, and restart recovery. A narrow scheduler credential is distinct from Clerk tokens. Prefer per-tenant scheduler credentials for the pilot; a future global dispatcher requires a separate narrowly scoped mechanism, not general RLS bypass. The worker revalidates active connection/tenant state and writes under the claimed tenant context. Use bounded concurrency and provider rate budgets.

Proposed routes: POST /v1/workspaces, GET /v1/workspaces, GET /v1/workspaces/:id/accounts, POST /v1/workspaces/:id/connections/meta/start, GET /v1/connections/meta/callback, POST /v1/workspaces/:id/accounts/:accountId/scans, GET /v1/workspaces/:id/scans/:scanId, and a separate POST /internal/scans/due. Exact contracts remain to be implemented.

## Frontend and validation

First screens: Clerk login/setup; workspace/account settings; connection health; scan history and snapshot table. TanStack Query owns server state; Zustand only local interaction state. Namespace query caches by workspace and clear sensitive caches on logout/switch. No offline persistence of credentials. Render external captions as text.

Zod provides shared contracts. Nest DTO validation uses whitelist, forbidNonWhitelisted and explicit transformations. class-transformer is not an HTML sanitizer and class-validator does not establish authorization. Avoid implicit coercion of security identifiers; use contextual output encoding and parameterized queries. Add contract consistency checks to prevent Zod/DTO drift.

## Hosting

LAN deployment remains the goal. Production Clerk requires a configured domain and HTTPS; use a real hostname with private DNS resolving to the LAN host and a valid certificate, verifying the Clerk DNS requirements. Raw HTTP/private IP access is only a prototype assumption. Outbound access to Clerk and Meta is needed. OAuth redirects and provider lifecycle callbacks have separate reachability requirements; expose only narrowly required endpoints if necessary, not the database/admin dashboard.

The project is under OneDrive. Keep live PostgreSQL files, runtime .env secrets, and raw production dumps outside the synced source/vault tree on the deployment host. Choose that path during deployment rather than silently writing outside the project. Back up with database-aware tooling and test restores; do not treat live database file synchronization as backup.

Hermes reads a restricted analysis API or MCP wrapper later. It does not own the collection schedule or receive a database superuser connection.
