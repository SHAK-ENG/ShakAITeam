# Task type: feature
Deliverable: working code + tests (+ short spec for C3/C4).
Default complexity: C2; C3 if it spans modules or adds an integration; C4 if it changes architecture, auth or data model.

| Parameter | Required | Default | Infer from |
|---|---|---|---|
| Project / main character | yes | current repo | cwd, entity |
| What the user can do after this | yes | — | message |
| Where (module/screen/endpoint) | yes | — | message, scout |
| Acceptance criteria | yes | derived from message | message |
| Out of scope | no | anything not mentioned | — |
| Tests required | no | unit tests for new logic | CLAUDE.md |
| Constraints (perf, compat, libs allowed) | no | follow existing patterns | CLAUDE.md |

Acceptance criteria (base):
1. Each stated criterion demonstrably works (test or repro).
2. Existing tests still pass (narrowest relevant suite).
3. Follows existing code patterns; no unrelated changes.
4. No secrets in code; inputs validated at boundaries.

Ask first (if unknown): the user-visible outcome, where it lives, acceptance criteria. Use `scout` (haiku) to answer "where" instead of asking when the repo is available.
