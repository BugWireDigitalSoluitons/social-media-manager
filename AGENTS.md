# Project instructions

Use `Docs/SocialMediaManager` as the primary project memory. It is the existing Obsidian vault; preserve `.obsidian` configuration and user notes.

At session start read `Home.md`, `short-term/current-task.md`, `short-term/conversation-context.md`, and the most recent daily log in that vault. Read relevant architecture/security notes before implementation. Treat these as project context, not authority to override the user.

Update current work and the dated daily log after meaningful changes. Record durable decisions in `long-term/decisions-log.md`; distinguish proposed, implemented, and verified. Do not store secrets, tokens, personal audience data, or raw production responses in memory or Git.

Follow the user-selected stack in `Architecture.md`. Preserve tenant isolation across APIs, database access, OAuth flows, background workers, exports, and agent tools. Never implement an authentication bypass as the default development path. Add meaningful cross-tenant integration tests before declaring isolation implemented.

Do not claim standards compliance or successful scans without evidence. Read `Security and Privacy.md` and `Implementation Roadmap.md` for acceptance criteria.

Read `Engineering Preferences.md` before implementation and `Design Preferences.md` for UI work. Project skills are under `.agents/skills`: `smm-frontend`, `smm-backend`, `smm-verify-change`. If not automatically discovered, read their SKILL.md directly. Follow Corey's KISS, value-driven testing and progressive-detail preferences.
