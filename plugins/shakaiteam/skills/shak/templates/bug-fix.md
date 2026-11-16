# Task type: bug-fix
Deliverable: fix + regression test + one-line root cause.
Default complexity: C1 if cause is known and local; C2 typical; C3 if intermittent, cross-module or cause unknown.

| Parameter | Required | Default | Infer from |
|---|---|---|---|
| Symptom (what happens vs expected) | yes | — | message, error text |
| Where / how to reproduce | yes | — | message, logs, failing test |
| Error message / stack trace | no | — | attachments, terminal |
| Environment (local, staging, prod; OS/browser) | no | local | message |
| Since when / recent change | no | unknown | git log |
| Urgency | no | normal | message |

Acceptance criteria (base):
1. Root cause identified and stated in one line.
2. A test that failed before the fix passes after it.
3. Related tests pass; no unrelated changes.

Ask first (if unknown): expected vs actual behaviour, how to reproduce. Never ask for something visible in the error text or repo.
