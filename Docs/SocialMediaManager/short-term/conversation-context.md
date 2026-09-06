---
type: context
updated: 2026-09-05
tags: [memory, requirements]
---
# User context

## Readiness interview — 2026-09-05 clarification

Round 4 user decisions: post library shows date, platform, caption/description, available thumbnail, tags and original link; accepted recommended date/untagged filters and original-platform full-video viewing for MVP. Desktop is almost always on, but downtime/missed data is an explicitly accepted local-hosting risk. Keep collected history and tags until user requests deletion, subject to the provider requirements already included in the recommendation; stopping refresh/disconnecting is distinct from deleting history. User mentioned GDPR as motivation; this is a retention preference, not evidence of legal compliance. Backups stay on the same system for now; remote/off-system backup is deferred by user. See [[MVP Scope]] for the consolidated scope. Interview decisions are settled; final shared-understanding confirmation is pending, and no build has been authorized in this interview.

Round 3 user decisions: Facebook and Instagram are the first platforms. Specific account type/linkage remains unverified; do not ask for secrets. Authentication must be present from the start using Clerk Hobby for local use. Corey expects later public-product deployment to need a subscription/configuration change and at most minor auth code changes, not retrofitted authentication. Hobby plan choice is distinct from Clerk development/production instance choice; exact LAN support is being checked.

Host API and React web on Corey's personal system with a fixed LAN port, accessible to both users via LAN IP and optionally a router-local DNS name. Remote public access is not requested. Import the last 90 days of posts. Desired post snapshots: daily during first 30 days of post life, then weekly through one year. Desired account snapshots: daily follower/subscriber count, total views and total likes where supported. Missing historical data is acceptable and must be shown honestly; never fabricate retrospective age snapshots. This cadence supersedes the earlier weekly-through-90-days/monthly-afterward proposal.

Latest steering (round 2, supersedes earlier MVP agent plans): AI experience is entirely outside the MVP. Preserve future extensibility without building MCP, agent tools, model integration or agent approval flows now. No effort tracking. Zero cost means no added costs; the base app must run locally and integrations such as Clerk must be free for localhost use. External-service/offline and LAN deployment boundaries still need clarification.

Accepted core: connect accounts, ingest posts, gather measurement snapshots, tag posts and provide basic comparisons. Highest priority is reliable post ingestion/history and tagging for later analysis. Consolidate available views, likes, comments, shares/reposts and account followers; targets and a universal best-post score are not required. Corey illustrated soft engagement as likes/views and hard engagement as other interactions/views; provider-specific definitions, overlap and availability must be validated before deriving rates. Do not attribute all account follower gains to an individual post.

Tagging: keep similar tags distinct until users clean them up. Either user can tag ANY imported post, including old posts when a new analytical factor is identified. Support keeping/renaming tags and selecting multiple variants to normalize their assignments to one chosen label (e.g. Book Promo/Promo/Promotional -> Promotion). Present this as normalization rather than merging. Detailed handling of duplicate assignments and historical comparisons remains implementation design, not a verified feature.

Corey requested a grilling interview before authorizing the core build. Continue in decision rounds; implementation has not been requested in this interview.

Confirmed purpose: help choose content worth creating and structure posting schedules for better engagement. Both spouses will review results and discuss strategy. His wife should browse recent posts every few days, tag posts from the last few weeks, and explore trends manually. Corey will also analyze and tag posts, using AI suggestions with his final approval over additions.

AI analytics and data synthesis are allowed, including MCP or browser interaction. The application must work without AI. AI-generated content intended for social posting is prohibited. This supersedes the earlier blanket no-ideation assumption where it conflicts with permitted analytical tag suggestions; exact agent read/write and hosted-data boundaries remain to be decided.

Outside users are not a near-term commitment. Preserve a product-capable architecture and portable deployment, with minimal later code changes desired for public launch. Public-launch prerequisites have not been verified or waived.

Local operating costs should be zero. Corey has no fixed development/maintenance time budget or deadline, wants useful core delivery as soon as the approach is jointly agreed, and expects iterative refinement/features/fixes. What counts as the core, cost boundary, and operational tradeoffs remain open.

Corey and his wife are the initial users. His wife writes contemporary romance, has four published books, has been full-time for two years, and is approaching break-even with expenses currently higher than revenue. She streams on Twitch and posts on Facebook and Instagram, avoids TikTok, and expects roughly one book fair per month with occasional skipped months.

She opposes generative AI because of its impact on authors. The application must be useful through ordinary manual analysis. Corey wants a separate Hermes/Jarvis experience, initially read-only, analyzing agreed metrics and manually entered tags. No posting automation or ideation is requested. Agree the scope of agent data access; local hosting does not mean hosted-model requests remain local.

Goal: preserve account and post measurements, tag themes/styles/formats, and investigate associations with growth. Future views include metric timelines with post markers, tag maps, comparison tables, and weekday/theme heatmaps. Future business modules may include ad spend, sales targets, newsletter conversion, and fair results. Association is not causation; comparable post age and adequate sample sizes matter.

Deployment: existing desktop and Raspberry Pi on the LAN; hardware details pending. Data collection precedes visual polish. User now explicitly requires scalability through authentication, credentials, multi-account connections, and tenant isolation.

Selected stack:
- React, TypeScript, Vite; TanStack Query; Zustand; Tailwind CSS; shadcn/ui; shared Zod schemas.
- Node.js, TypeScript, NestJS; facebook-nodejs-business-sdk; class-validator/class-transformer DTOs.
- PostgreSQL, Prisma, versioned migrations, RLS across tenant-owned tables.
- Portable cron calling an authenticated API endpoint; UI-triggered scans too.
- Clerk application login; Facebook OAuth for Facebook/Instagram linking.
- Gitignored .env files for deployment secrets.
- Semgrep, GitHub Dependabot, Snyk, Gitleaks, GitHub Actions. Consider OWASP, NIST, ISO, GDPR and SAST/SCA/DAST/IAST.

Do not ask for passwords or tokens in chat. Do not replace this stack without discussing a material incompatibility.
