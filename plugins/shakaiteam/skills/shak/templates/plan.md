# Task type: plan
Deliverable: `PLAN.md` (+ `DECISIONS.md`) updated, or a status update / meeting notes.
Default complexity: C1 (status/notes), C2 (sprint/project plan), C3 (roadmap).

| Parameter | Required | Default | Infer from |
|---|---|---|---|
| Kind (roadmap, sprint, project plan, status update, notes) | yes | — | message |
| Goal / milestone | yes | — | message, entity |
| Horizon | no | sprint = 2 weeks, roadmap = 1 quarter | — |
| Team / capacity | no | ShakAITeam roles | — |
| Audience of the doc | no | the user | message |

Acceptance criteria (base):
1. Tasks are concrete, owned (role) and dated.
2. Dependencies and top 3 risks listed.
3. Fits on one screen; edited in place, not regenerated.

Ask first (if unknown): kind, goal, horizon.
