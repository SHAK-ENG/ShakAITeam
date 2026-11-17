# Ledger, cost units and team learning

All of this lives in the user's data folder, never inside the plugin, so plugin updates never erase it:
```
<user home>/.claude/shakaiteam/
  ledger/tasks.csv          one row per task          (the tracker)
  ledger/steps.csv          one row per agent step    (who spent what)
  playbooks/<role>.md       lessons each role has learned (≤25 lines each)
  routing-overrides.md      tuned routing that beats reference/routing.md
  cost-weights.md           relative model cost weights (user may edit)
```
Create missing files with just their header line.

## Where token numbers come from
Every Agent tool result ends with a usage block (total tokens, tool uses, duration). Record those numbers exactly — never estimate an agent's tokens. The front desk's own tokens are not visible to it; log them as `n/a` (the user can see the session total in the app's usage view).

## steps.csv
`task_id,date,step,role,level,model,tokens,tool_uses,duration_s,result`
- `result`: done | escalated | revised | failed
- `task_id`: `YYYYMMDD-HHMM-<task-type>`

## tasks.csv
`task_id,date,entity,task_type,complexity,polish,team,questions_asked,agent_tokens,cost_units,baseline_units,saved_pct,revisions,escalations,rating`
- `team`: roles joined by `>`, e.g. `creative-director>video-producer>reviewer`
- `rating`: good | fixes | redo | skipped (the user's one-click verdict)

## Cost units (so tokens on different models compare fairly)
`cost_units = Σ step tokens × weight(model)`, weights from `cost-weights.md`.
Default file content (relative, input+output blended; the user should update it from the current Anthropic pricing page):
```
haiku: 1
sonnet: 3
opus: 5
fable: 8
```

## Baseline (what "saved" means)
`baseline_units` = the same agent tokens as if every step had run on the session's top model (opus, or fable if it was used anywhere) = `agent_tokens × weight(top model)`.
`saved_pct = 1 − cost_units / baseline_units`.
This measures savings from **routing** only. Savings from fewer questions, saved memory and fewer retries show up as **falling agent_tokens per task type over time**, which /shakaiteam:stats reports as the trend. Say this plainly whenever reporting savings; never claim more.

## Lessons (how the team learns)
Agents may end their return with lines `LESSON: <one reusable sentence>` (e.g. "LESSON: in this repo run tests with `npm test -- <path>`, the full suite takes 4 min").
Front desk handling:
1. Keep lessons that would help a future task of the same role; drop one-offs and anything containing secrets or personal data.
2. Entity-specific lessons → that entity's `learnings.md`; general craft lessons → `playbooks/<role>.md` as `YYYY-MM-DD | lesson`.
3. Replace an older contradicting lesson instead of appending. Keep each playbook ≤25 lines (merge or drop the weakest).
When briefing a role, include at most 5 playbook lines relevant to this task under "Team lessons".
