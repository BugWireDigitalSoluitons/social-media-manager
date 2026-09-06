---
type: scope
status: user-approved-ready-for-implementation
updated: 2026-09-05
---
# MVP Scope

Consolidates Corey's answers in the readiness interview. Corey confirmed the complete scope with "This sounds correct" on 2026-09-05; the interview is complete and no further scope confirmation is required. No application behavior is implemented or verified. Corey is choosing whether to begin implementation in this task or a fresh project task.

## Purpose and users

Help Corey and his wife consolidate post performance, choose content and posting schedules, and tag posts for future analysis. Two users initially; both can tag and analyze in one business workspace. Preserve multi-workspace tenancy and portable deployment for a possible product without building public signup/billing now. Keep the selected stack in [[Architecture]] and [[short-term/conversation-context]].

## Core

- Auth-first Clerk integration within free Hobby capabilities. Application/API/database on Corey's personal system, web/API available on a fixed LAN port/IP or optional router DNS name. No added operating costs; network access to Clerk/Meta is permitted. Remote access is not requested.
- Facebook and Instagram account connection, encrypted credentials, reauthorization/disconnect, scheduled/manual durable collection and clear scan health.
- Import the last 90 days of accessible posts. Capture post snapshots daily during the first 30 days of post life, then weekly through one year. Stop scheduled post refresh afterward while keeping history and tags.
- Daily account follower/subscriber count, views and likes where supported. Preserve distinct provider definitions, periods and availability; do not promise that desired totals exist on every source.
- Preserve genuine observations and honestly show missing historical data, stale connections and partial failures. Recover supported history after downtime; never manufacture missing snapshots.
- Browse posts with date, platform, caption/description, available thumbnail, tags and original link. Filter by date and untagged status. Full video may open on the original platform.
- Either user can tag any imported post, including historical posts. Similar tags remain distinct until explicit cleanup. Rename tags or select variants and normalize assignments to a chosen label. Avoid duplicate assignments after normalization. Present the feature as normalization, not merging.
- Basic comparisons by tag, format, weekday and posting time remain in core; ingestion/snapshots/tagging are the highest priority. Show available raw engagement measures and account growth; no targets or opaque best-post score required. Rate formulas need source-definition validation. Compare like platforms and comparable post ages; do not claim causation or attribute account growth to an individual post without evidence.

## Lifecycle and operations

Desktop is almost always on; downtime and missed captures are accepted. Resume due collection safely after restart and expose gaps. Existing integrity/security requirements, including durable jobs, idempotency and tested tenant isolation, remain in force.

Retain normalized measurements and tags until explicit user deletion, subject to provider requirements. Disconnect stops collection/removes credentials separately from history deletion. User's GDPR reference is motivation for control over deletion, not evidence of compliance. Keep raw provider payload retention minimized; do not interpret history retention as permission for indefinite raw-response storage.

Backups stay on the host system for now. Use database-aware local backups outside the synced source tree and verify restore; exact runtime/backup locations are setup inputs. Same-system backup does not protect against loss of that system. Off-system/cloud backup is explicitly deferred. Keep runtime secrets/database files outside OneDrive source sync per [[Architecture]].

## Deferred

All AI experience, MCP/agent integration and approval workflows; effort tracking; sales/ads/newsletters/fairs; Twitch; public billing/onboarding; remote access; elaborate visualizations. Future AI analytics/synthesis may be allowed, but no AI-generated content for posting to social media.

## First implementation gates

1. Prove Clerk login, refresh/reload, logout and authorized API access on localhost and a second LAN device without an authentication bypass. Hobby pricing does not decide dev/production instance configuration. Exact LAN origin support is unverified; report any material incompatibility before changing the selected approach.
2. Verify intended Facebook account is an eligible Page and Instagram is an eligible professional account with the required linkage for the selected login route. Actual configuration is unknown. Validate available metrics, scopes and historical access with authorized accounts; no tokens in chat or memory.
3. Prove tenant boundaries with meaningful API and real PostgreSQL RLS tests using runtime roles, alongside collection integrity/restart handling. Run relevant checks and record actual evidence.
4. Demonstrate the useful journey: sign in, connect, import, inspect collection health, tag an old or new post, normalize selected tag variants, and inspect available measurements/basic comparisons. Exercise local backup restore.

Public release is a later readiness review. Clerk production needs appropriate domain/TLS/keys/callback configuration; development identities do not transfer automatically. Preserve a deliberate identity transition rather than promising a subscription upgrade alone. See linked primary-source research in [[long-term/decisions-log]].
