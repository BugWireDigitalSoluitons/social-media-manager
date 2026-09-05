---
name: smm-backend
description: Implement Social Media Manager NestJS use cases, migrations, account connections and scan jobs with tenant isolation and collection integrity.
---
# smm-backend

Project-local skill. Resolve repository root three levels above this directory; the referenced notes live in Docs/SocialMediaManager. The vault owns preferences; do not create competing copies.

Read Architecture.md, Data Collection.md, Security and Privacy.md and Engineering Preferences.md as relevant. Identify the use case's Business, Performance, Security or UX value. Implement the smallest cohesive change. Keep provider calls outside DB transactions and protected persistence in authenticated transaction-local tenant context. Verify isolation with runtime credentials, never migration credentials. Test consequential boundary failures such as cross-tenant IDs, replay, retries, partial results or restart recovery. Distinguish mocks from live proof and keep credentials out of memory.
