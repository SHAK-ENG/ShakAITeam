# Task type: docs
Deliverable: the doc file(s), verified against the real repo.
Default complexity: C1; C2 for multi-page guides or API docs.

| Parameter | Required | Default | Infer from |
|---|---|---|---|
| Doc kind (README, guide, API, changelog, CLAUDE.md) | yes | — | message |
| Audience (users, contributors, AI agents) | yes | users | doc kind |
| Source of truth (code paths, specs) | no | current repo | scout |
| Length | no | as short as complete allows | — |

Acceptance criteria (base):
1. Every command/path mentioned exists.
2. Quick start works top-to-bottom.
3. CLAUDE.md ≤60 lines.

Ask first (if unknown): doc kind, audience.
