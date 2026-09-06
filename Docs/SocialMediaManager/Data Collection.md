---
type: design
status: proposed
updated: 2026-09-05
tags: [data, collection]
---
# Data Collection

First prove authorized access to real account and post data. Keep each provider behind an adapter so direct Meta access can be replaced/supplemented with a vendor without changing the model. Custom software cannot expose metrics missing from the source.

## Data model

Tenant-scoped entities: workspace, membership, connection, social account, post, post tag, account observation, post observation, scan job/run, OAuth state, business event, audit event, retention policy. Principal-scoped identity rows follow the boundary described in [[Architecture]].

Observations preserve provider metric key, API version/definition, account/post identity, measurement period and aggregation type, observed_at, fetched_at, value, availability status, and source run. Distinguish lifetime post counts from daily account measurements. Missing, unsupported, and zero are distinct. Store UTC instants and source/reporting timezone; derive weekday in the chosen reporting timezone, including daylight-saving transitions.

Posts preserve stable provider IDs, publication time, permalink, format, and available metadata. Manual tags capture theme, presentation, purpose, color treatment, paid/organic status and book/campaign association. Preserve numeric duration and carousel count when available. Cross-posts remain separate platform records linked by an optional shared content ID.

Use append-only observations with deduplication for retries. Revised historical periods create revision-aware observations rather than silently erasing what was previously reported. If retaining raw responses is permitted, minimize/redact them and apply bounded retention. Never retain raw OAuth responses or authorization headers. Preview media URLs may expire; a permalink is the initial durable reference. Avoid mirroring media by default.

## Initial schedule

- User-confirmed readiness scope: initially import the last 90 days of Facebook/Instagram posts, subject to authorized availability. Older-post import remains an extension, not a promise of retrospective observations.
- Account metrics and post discovery daily at a fixed time. Desired account measurements include follower/subscriber count, views and likes where supported; preserve provider definitions and periods instead of assuming equivalent totals.
- User-confirmed post cadence: daily for the first 30 days of post life, then weekly through one year while supported. Stop scheduled refresh after one year and keep history/tags until explicit deletion, subject to provider requirements. Schedule is not implemented or verified.
- Re-fetch supported recent historical account periods for delayed reporting.
- Seven-day and 30-day post comparisons use actual age at observation. Daily polling only approximates exact 24-hour results.
- Stories, if included, require a separate capture policy because their availability can be short; exclude them from the first pilot until verified.

Provider limits and current API capabilities determine the final schedule. Never fill missing historical follower counts with fabricated values. After downtime, backfill only periods the source actually supplies.

## Health and evidence

Show last attempt, last complete success, next due time, connection expiry/reauthorization status, pages processed, posts discovered, observations stored, missing metrics, and partial/error reasons. Treat partial pagination or per-account failures as partial success, not a green complete scan. Log request identifiers without tokens or personal payloads.

Pilot availability matrix columns: platform, account type, metric, account/post scope, format, aggregation, permission, source endpoint/version, lookback, delay, paid/organic semantics, verified date, native comparison, status.

Post performance and account growth around publication are different measures. Do not assign the same follower increase to every overlapping post. Compare similar-age posts within platform, report sample size/variation, and label growth associations honestly. Business conversion outcomes can be added later.
