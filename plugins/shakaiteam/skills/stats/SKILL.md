---
name: stats
description: "ShakAITeam token tracker report — tokens and cost units per task, savings versus the all-top-model baseline, trends per task type, and which roles/models consume the most. Use when the user invokes /stats or asks how many tokens ShakAITeam used or saved."
argument-hint: "[last N | <task-type> | <entity>]"
---

# ShakAITeam stats

Data: `<user home>/.claude/shakaiteam/ledger/tasks.csv` and `steps.csv` (format: `../shak/reference/ledger-format.md`). If they don't exist yet, say "No tasks tracked yet — run `/shakaiteam:shak <task>` first." and stop.

Read the CSVs (only the rows needed: default the last 30 tasks; filter by the argument). Do the arithmetic yourself, carefully; if there are more than ~200 rows, compute with a short PowerShell or Python one-liner instead of by hand.

Report (≤25 lines, tables, no prose padding):

1. **Totals** — tasks, agent tokens, cost units, baseline units, overall saved % (routing).
2. **Per task type** — count, avg agent tokens, avg cost units, avg saved %, and the trend: average of the first half vs the second half of that type's tasks (↓ = the team got more efficient). Mark types with fewer than 4 tasks as "too few to trend".
3. **Per role** — total tokens and share of the total, escalation count, revision count. Top 3 most expensive roles first.
4. **Quality** — rating mix (good / fixes / redo) per task type. Cheap but redone is not a saving: flag any type with >25% fixes/redo.
5. **One recommendation** — the single change most likely to cut cost without hurting quality, and "run `/shakaiteam:retro` to apply it".

Always add this line under the totals: "Saved % counts routing only (cheaper models per step). Savings from fewer questions and remembered context show in the falling token trend."
Never invent numbers; anything missing shows as `n/a`.
