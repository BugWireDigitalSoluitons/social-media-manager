---
type: preferences
status: user-approved
updated: 2026-09-05
---
# Engineering Preferences

Everything should deliver Business, Performance, Security or User Experience value. Apply KISS: as little code as practical without sacrificing responsibility boundaries, clarity or correctness. Brevity is not code golf.

Prefer small cohesive files and reusable components. Split by responsibility, not arbitrary line counts. Keep features organized together; extract proven shared behavior. Avoid speculative abstractions, catch-all utilities, unnecessary wrappers and framework building. Modest duplication can be simpler than premature generalization.

Follow idiomatic supported practices for the selected stack. Components own presentation/interaction; feature hooks coordinate server state; Nest services own use cases; adapters own providers; scoped persistence owns database access. Avoid mechanically creating layers for trivial operations. TanStack Query owns server state, Zustand only shared client state, local state stays local. Architecture.md retains security requirements.

Use descriptive names and explicit contracts. Comments explain non-obvious intent and constraints. Reuse shared tokens and shadcn primitives without unnecessary wrappers.

## Tests protect value

Test important outcomes and consequential failure modes. Each test must have an identifiable Business, Performance, Security or UX purpose. Name the protected behavior or briefly explain why it matters; no mandatory test-tagging framework.

- Business: retries cannot inflate measurements.
- Security: knowing another tenant's account ID permits neither reading nor scanning it.
- UX: expired connections provide a reconnect path preserving workspace context.
- Performance: representative queries are bounded/paginated; avoid flaky wall-clock assertions without controlled benchmarks.

Unit-test meaningful pure rules; integration-test real boundaries, especially RLS/jobs; browser-test critical journeys. Mock providers at their boundary, not PostgreSQL when claiming RLS verification. Include negative cases where failure matters. Avoid tests for trivial getters, internal call order, JSX structure or coverage alone.

For each change ask: what outcome is protected, where does responsibility belong, what failure matters, and what is the smallest meaningful verification? Security/integrity tests are not optional simplifications. Report actual checks and unverified areas.
