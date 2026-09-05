---
type: security-plan
status: proposed-not-verified
updated: 2026-09-05
tags: [security, privacy]
---
# Security and Privacy

Security requirements and verification plan, not a certification or compliance claim. No scanners have run and no controls are implemented yet. See [[Architecture]], [[Implementation Roadmap]], and [[Sources]].

## Frameworks

- Use OWASP ASVS 5.0 Level 2 as the proposed application verification baseline, with API authorization/object access coverage. Map individual applicable requirements to tests/evidence as implementation proceeds.
- Use NIST SSDF practices for development, review, dependency provenance, vulnerability handling, and release evidence. Recheck the current final publication before recording a formal version baseline.
- Use ISO/IEC 27001:2022 as an organizational risk-management reference. Certification involves a scoped management system, not a passing application scan.
- GDPR is a legal regime, not a scanner category. Determine applicability and controller/processor responsibilities before broader launch. Implement minimization, purpose limitation, access/export/deletion, retention, vendor review, and breach procedures as product requirements. Do not presume consent is the correct legal basis for all processing.
- SAST, SCA, DAST and IAST are testing approaches. Semgrep and dependency scanners do not cover all of them.

## Threats and required evidence

| Risk | Planned control | Required verification |
|---|---|---|
| Cross-tenant object access | Backend membership + RLS + composite FKs | Tenant A cannot read/write/export/scan tenant B, even with known IDs |
| Pooled connection leakage | Transaction-local context, scoped client | Alternating/concurrent A/B requests and absent context deny leakage |
| RLS bypass | Non-owner, non-superuser runtime role, FORCE RLS | Query actual role flags and run negative DB tests |
| OAuth account substitution | Bound single-use state and provider asset validation | Replayed/expired/wrong-user/wrong-tenant state rejected |
| Token theft | Authenticated encryption, restricted secrets, redaction | No tokens in responses/logs; rotation/decryption failures tested |
| Scan abuse | Separate scheduler auth, member role checks, limits | Anonymous/viewer/cross-tenant triggers denied; overlap/replay controlled |
| Worker crash or duplicate requests | Durable jobs, leases, idempotency | Restart recovery and no duplicate observations |
| External content injection | Text rendering, CSP, input limits | Stored XSS payload remains inert |
| Server-side request forgery | Fixed provider hosts; bounded redirects | User URLs cannot reach LAN/metadata targets |
| Deletion races | Disable connection, cancel jobs, recheck before commit | Deleted account cannot be repopulated by in-flight scan |
| Backup disclosure | Encrypted backups, separate key access | Restore tested; no secrets in source/vault |

Rate-limit auth-adjacent, OAuth, manual scan, export and deletion endpoints. Use narrow CORS/allowed origins, security headers, body limits, and CSRF protection appropriate to the chosen credential transport. Never place bearer credentials in query strings. Tenant-aware audit events record actor/action/target/result without payload secrets. Restrict write access to audit events; retention/deletion rights still require a documented policy.

## Verification pipeline

Proposed PR gates: locked dependency install, lint/type checks, meaningful tests, PostgreSQL migration/RLS tests, Semgrep SAST, Gitleaks secret detection, and dependency SCA. Configure Dependabot updates and Snyk with documented ownership and severity triage. Missing Snyk credentials must be reported as not run, not passed. Pin reviewed CI actions, grant minimal workflow permissions, and never expose secrets to untrusted fork code. No GitHub repository/remote exists yet; do not claim Actions or Dependabot are active.

DAST: add OWASP ZAP against a disposable test deployment, including authenticated access and two-tenant cases. Do not active-scan Meta, Clerk, or production data. Baseline scanning alone does not verify business authorization.

IAST: evaluate a Node/Nest-compatible instrumented test runtime before selecting a product. It is an explicit open requirement, not covered by Semgrep/Snyk/ZAP. Keep the coverage gap visible until implemented or consciously deferred with rationale.

Capture scan date, tool/version, commit, result, triage and remediation evidence. Define an exception process with owner/expiry; passing tools alone is not release approval. Deployment should be gated separately from CI, with migration/backup/rollback procedures.

## Privacy and lifecycle

Initially collect aggregate metrics, account identifiers, post metadata and manual tags; avoid audience identities, comment bodies, DMs, and mirrored creative assets. Account-level data can still be personal data. Inventory Clerk, Meta, hosting, backup, and any model providers and their data flows. Document agent access agreement and keep it revocable.

Define retention by data class before real ingestion, including permitted raw response duration, normalized history, audit logs, OAuth state, and backups. On disconnect stop collection and revoke/delete credentials as appropriate; make history retention a separate explicit choice consistent with provider rules. On deletion, stop jobs, purge permitted live data and address backup expiry/restoration replay. Implement provider-required deauthorization/data deletion handling. Test workspace exports and deletion under real RLS.

Runtime secrets must live outside the OneDrive-synced project on the host, though the development convention remains gitignored .env. Gitignore prevents Git commits; it does not prevent OneDrive synchronization. .env.example must contain placeholders only.
