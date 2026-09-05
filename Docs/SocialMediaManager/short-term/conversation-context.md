---
type: context
updated: 2026-09-05
tags: [memory, requirements]
---
# User context

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
