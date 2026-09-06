---
type: current-task
updated: 2026-09-05
tags: [memory, active]
---
# Current task

Current handoff: readiness interview rounds 1–4 are complete. [[MVP Scope]] consolidates accepted product scope. Await Corey's confirmation of shared understanding before implementing; prior next-task text below is historical context. Final decisions: post previews/date/platform/caption/tags/link; local-host downtime accepted; retain history/tags until explicit deletion subject to provider requirements; backups on this system only, off-system protection deferred. First implementation checks must prove Clerk-authenticated LAN access and actual FB/IG account eligibility/metric access. Do not promise public deployment is only a paid-plan upgrade or call local same-disk backups protection against host failure.

Round 3 settled: FB/IG first; auth-first Clerk Hobby; personal PC serves API/web on fixed LAN port/IP or optional router-local DNS; import 90 days; post snapshots daily for first 30 days then weekly through one year; daily account follower/views/likes where available; show gaps. Provider account eligibility remains unverified. Clerk Hobby versus environment configuration and exact LAN support are under factual review. Continue remaining operational/lifecycle decisions, then seek shared-understanding confirmation before implementation.

Latest interview steering: collection, snapshots and tagging are the MVP priority; basic comparisons remain accepted. No effort tracking or AI experience in MVP. Any imported post can be tagged retroactively; similar tags remain separate until user-directed bulk normalization. Zero cost means no added local-app/integration costs. Next resolve source accounts, connected-local versus offline operation, first access/hosting target and collection history. Clerk's free plan and dev/production distinction were researched; exact persistent LAN setup remains unverified. No build authorization yet.

Active work: readiness grilling requested by Corey. First round answered; user clarified engagement/content and posting-schedule decisions, shared manual/AI-assisted analysis with human-approved tags, no AI-generated social content, private initial users with future product portability, and zero local operating cost. Core build awaits agreement on approach. Continue the interview with scope, comparison definitions, tagging and agent boundaries; do not treat the prior milestone-1 next step as authorization to implement now. See [[short-term/conversation-context]] and [[long-term/decisions-log]].

Completed this session: initialized primary Obsidian memory, architecture, security/privacy plan, data collection design and implementation roadmap; added root AGENTS.md, README.md and .gitignore. Preserved existing vault configuration and Welcome.md.

Next implementation task: milestone 1 in [[Implementation Roadmap]] — scaffold selected stack and prove authentication/tenant isolation before live collection. No application source or dependencies installed yet. Do not confuse documented controls with implemented controls.

Known limits: Meta/Clerk credentials and account types unknown; no domain selected, no Git repository or CI exists; no scans/security tests run. User authorized filesystem write access to the project for this session. Future sessions must honor their actual permission boundaries.

Latest steering: follow [[Design Preferences]] and [[Engineering Preferences]]. Three project-local skills now reference these notes. Exact design tokens/reference page remain unapproved; actual reference artwork still needs inspection. Continue milestone 1 using these preferences.

Environment check (2026-09-05): Node.js v24.19.0, pnpm 11.22.0, Git 2.55.0 and VS Code are available. npm was updated and canonical npm.cmd reports 12.0.2. Snyk 1.1307.0 was installed globally and verified. Docker Desktop, PostgreSQL, GitHub CLI, Semgrep and Gitleaks remain user setup items; no application dependencies or manifests exist yet.

PostgreSQL follow-up (2026-09-05): PostgreSQL 18.6 is installed and the local server accepts connections on port 5432. The PostgreSQL bin directory is not yet on the current PowerShell PATH; direct executable path works.

Security tooling follow-up (2026-09-05): Semgrep 1.176.1 installed for the user with Python 3.14; its executable is present but startup currently fails in this agent environment while reading the Windows certificate store. Gitleaks 8.30.1 installed in the user-level tools directory and added to the user PATH. Chocolatey installation was blocked by non-administrator access. GitHub CLI is installed at `C:/Program Files/GitHub CLI/gh.exe`; current agent PATH has not refreshed. Docker CLI was not found in the current environment check and needs verification after restarting the shell/Docker Desktop.

Pre-development tooling (2026-09-05): Installed global CLI availability for ESLint 10.10.0, Prettier 3.9.6, TypeScript 7.0.2, Vitest 5.0.0 and Playwright 1.63.0. Project-local pinned versions and configuration remain required during scaffolding; global tools are only convenience commands.
