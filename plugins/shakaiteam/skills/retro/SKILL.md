---
name: retro
description: "ShakAITeam retrospective — reviews the token ledger, ratings, escalations and lessons from recent tasks, then proposes and (after the user approves) applies tuning to routing, task-template defaults and role playbooks, so the team gets cheaper and better with experience. Use when the user invokes /retro, after every ~10 tasks, or when asked to make the team learn or improve."
argument-hint: "[last N tasks, default 10]"
---

# ShakAITeam retro — the team learns from its own work

Inputs (team data folder `<user home>/.claude/shakaiteam/`): `ledger/tasks.csv`, `ledger/steps.csv`, `playbooks/*.md`, `routing-overrides.md`. Rules for the data: `../shak/reference/ledger-format.md`. Fewer than 5 tracked tasks → say so and stop.

## 1. Find patterns (last N tasks; compare with the N before them when available)
Look for these, and only report what the data shows:
| Pattern in the data | Proposed change |
|---|---|
| A role at a level escalates ≥2 times for a task type | Start that task type one level higher |
| Reviewer says SHIP first time ≥80% for a task type, ratings mostly good | Downgrade the reviewer's model, or drop review at Balanced for that type |
| A step's tokens are far above the type's median (≥2×) more than once | Tighten that role's brief budget for the type (e.g. "max 3 files read", "max 2 searches") |
| Ratings "fixes/redo" ≥25% for a task type | Upgrade the making step's model or level, or add a required question to the template |
| The same answer is given to a question ≥3 times for an entity | Save it as that entity's default so the question is skipped |
| Two playbook lessons conflict or repeat | Merge them |
| A cheaper team got "good" ratings as often as the recommended one | Make the cheaper team the recommendation |

## 2. Propose
Show ≤6 proposed changes, each one line: change · evidence (numbers from the ledger) · expected effect on cost and quality. Ask with AskUserQuestion (multiSelect) which to apply.

## 3. Apply only what the user approved
- Routing changes → `routing-overrides.md` (never edit the plugin's own `reference/routing.md`; plugin updates would erase it). Format: `- <task-type>/<polish>: <rule> (since YYYY-MM-DD, evidence: …)`.
- Entity defaults → that entity's `profile.md` defaults line.
- Playbook merges → `playbooks/<role>.md` (≤25 lines each).
- Append one line to `ledger/retros.csv`: `date,tasks_reviewed,changes_applied,avg_cost_units_before`.

## 4. Close the loop
At the next retro, compare avg cost units and rating mix since each applied change. A change that made quality worse → propose reverting it. Report that comparison first.
