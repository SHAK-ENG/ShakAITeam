# ShakAITeam

**An AI R&D company inside Claude Code.** Stop writing perfect prompts. Say what you want in plain words. ShakAITeam asks a few click-to-answer questions, remembers each brand or project you work on, lets you pick the team, and gives every step the cheapest model that can do it well.

```
/shakaiteam:shak make a 30s ad for ShakTalk, learn from the attached video
```

## Why

| Problem | What ShakAITeam does |
|---|---|
| Vague prompts lead to guessing, redoing work and wasted tokens | **Task templates** list exactly what each kind of job needs. Only the missing pieces are asked, as multiple choice. |
| Every new session starts from zero | **Memory per main character**: one profile for each brand, product, client or project (e.g. `shaktalk/`), loaded only when a task is about it |
| An expensive model gets used for everything | **Levelled team and model routing**: Haiku for finding and admin, Sonnet for making, Opus/Fable only for the one step that decides quality |
| You can't control cost vs. quality | **Polish levels**: Draft / Balanced / Polished, chosen per task and remembered |
| The AI picks how to staff the job | **You approve the team** before any work starts |

## How a task flows

```
your words ─► front desk (/shak)
              1. detect task type + main character
              2. load that character's memory (profile, brand, learnings)
              3. ask ≤4 click questions (only what's missing) + polish level
              4. propose a team → you pick (recommended / cheaper / stronger)
              5. brief each agent → dispatch (parallel where possible)
              6. quality gate (reviewer) according to polish level
              7. report + save history and learnings for next time
```

The second time you ask for a ShakTalk ad, it already knows the platform, length, voice and what you rejected last time, so it may ask nothing at all.

## The team (19 agents)

| Dept | Agents |
|---|---|
| Research | scout (L1), research-analyst (L2), data-scientist (L3) |
| Product & Ops | product-manager (L2), project-manager (L1), technical-writer (L1) |
| Design | ux-designer (L2), creative-director (L4) |
| Engineering | engineer-junior (L1), engineer-mid (L2), engineer-senior (L3), engineer-principal (L4), qa-engineer, devops-engineer, security-engineer |
| Marketing | content-marketer, growth-marketer, video-producer |
| Quality | reviewer |

Run `/shakaiteam:team` for the full chart with models. Lower-level engineers return `ESCALATE` when a task is bigger than it looked, and the front desk moves it up one level.

## Install

You need [Claude Code](https://docs.claude.com/en/docs/claude-code) installed.

**From GitHub:**
```bash
claude plugin marketplace add SHAK-ENG/ShakAITeam
```
```bash
claude plugin install shakaiteam@shakaiteam
```
Or, inside a Claude Code session: `/plugin marketplace add SHAK-ENG/ShakAITeam`, then `/plugin install shakaiteam@shakaiteam`.

> **Private repo:** testers must be added as collaborators, and Git on their machine must be signed in to GitHub (e.g. run `gh auth login` once, or use Git Credential Manager) so Claude Code can clone it.

**From a local folder** (for trying it out or development):
```bash
claude plugin marketplace add ./ShakAITeam
```
```bash
claude plugin install shakaiteam@shakaiteam
```
Or load it for a single session without installing:
```bash
claude --plugin-dir ./ShakAITeam/plugins/shakaiteam
```

Restart Claude Code after installing. Then check that `/shakaiteam:team` works.

**Update / remove:** `claude plugin marketplace update shakaiteam`, then `claude plugin update shakaiteam@shakaiteam`. To remove it: `claude plugin uninstall shakaiteam@shakaiteam`.

## Commands

| Command | What it does |
|---|---|
| `/shakaiteam:shak <request>` | Front desk: intake → questions → team → work → memory |
| `/shakaiteam:entity list \| show \| new \| update \| tidy <name>` | Manage main-character memory |
| `/shakaiteam:team` | Show the org chart |
| `/shakaiteam:stats [last N \| task-type \| entity]` | Token tracker: tokens per task, cost units, savings, trends |
| `/shakaiteam:retro [last N]` | Team retrospective: learns from ratings and the ledger, proposes tuning, applies what you approve |

## Token tracker and a team that learns

Every `/shak` task is logged. Agent token counts come from Claude Code's own usage report for each agent; nothing is estimated.

- `ledger/steps.csv` has one row per agent step: role, level, model, tokens, tool uses, result.
- `ledger/tasks.csv` has one row per task: team, total tokens, **cost units** (tokens weighted by model price), **baseline** (the same work all on the top model), **saved %**, revisions, escalations, and your one-click rating.

The team improves in the same ways real engineers do with experience:
1. **Lessons.** Agents report reusable `LESSON:` lines, such as "this repo's tests run with `npm test -- <path>`". They're kept in `playbooks/<role>.md` and passed to that role on later tasks.
2. **Feedback.** A "Needs fixes" or "Redo" rating becomes a lesson for the role that made the deliverable.
3. **Retros.** `/shakaiteam:retro` checks escalations, reviewer pass rates, token outliers and ratings. It then proposes changes, such as starting a task type at senior level, dropping a review that always passes, or making an answer you always give the default. It applies only what you approve, then checks at the next retro whether each change helped.

All of this data lives in `~/.claude/shakaiteam/`, outside the plugin, so updates never erase what the team has learned. Model cost weights are in `cost-weights.md`. Update them from Anthropic's current pricing page.

*Honest note:* "saved %" counts routing savings only. Savings from fewer questions and remembered context show up as **falling tokens per task type over time**, which `/stats` reports as the trend.

## Where memory lives

- **Personal** (default): `~/.claude/shakaiteam/entities/<name>/`. Works in every session and folder.
- **Shared with a team**: create `.shakaiteam/entities/` in a project and commit it. The project copy takes priority.

Each entity has `profile.md`, `brand.md`, `learnings.md` and `history.md`, all short with hard line limits so loading them stays cheap. Secrets and private personal data are never stored.

## Customising

- **New task type**: copy `skills/shak/templates/generic.md`, fill in the parameter table, and add one line to `templates/INDEX.md`.
- **Change models or teams**: edit `skills/shak/reference/routing.md`.
- **New role**: add `agents/<role>.md` (front-matter: `name`, `description`, `tools`, `model`), then add it to `routing.md` and the `team` skill.

## Repository layout

```
ShakAITeam/
├─ .claude-plugin/marketplace.json      ← makes this repo installable as a marketplace
└─ plugins/shakaiteam/
   ├─ .claude-plugin/plugin.json
   ├─ agents/                           ← 19 role agents
   └─ skills/
      ├─ shak/       SKILL.md, reference/(routing, brief-format), templates/(task types)
      ├─ entity/     SKILL.md, template/(profile, brand, learnings, history)
      ├─ team/       SKILL.md
      ├─ stats/      SKILL.md   ← token tracker report
      └─ retro/      SKILL.md   ← team learning loop
```

## Honest limits

- A plugin can't change a model's price per token. It saves money by using **fewer tokens** (no guessing, no repeated exploring) and **cheaper models for most steps**.
- Each handoff to an agent starts fresh, so tiny tasks are cheaper without `/shak`. Just ask directly.
- Results are only as good as the templates and the memory. Keep them up to date with `/shakaiteam:entity tidy`.

## License

MIT. See [LICENSE](LICENSE).
