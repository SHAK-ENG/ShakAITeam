---
name: team
description: "Show the ShakAITeam org chart — every role, its seniority level, default model and what it is for — so the user can pick or request specific agents. Use when the user invokes /team or asks who is on ShakAITeam."
---

Print this table as-is (do not read any other files):

| Dept | Agent | Level | Default model | Use for |
|---|---|---|---|---|
| Research | scout | L1 | Haiku | Find files/facts cheaply |
| Research | research-analyst | L2 | Sonnet | Market, competitor, tech research |
| Research | data-scientist | L3 | Sonnet (high) | Data analysis, experiments |
| Product | product-manager | L2 | Sonnet | Specs, PRDs, prioritisation |
| Operations | project-manager | L1 | Haiku | Plans, sprints, status, notes |
| Operations | technical-writer | L1 | Haiku | Docs, READMEs, CLAUDE.md |
| Design | ux-designer | L2 | Sonnet | UX flows, UI, mockups |
| Design | creative-director | L4 | Opus | Concepts, brand, final creative review |
| Engineering | engineer-junior | L1 | Haiku | Small, clear, one-file changes |
| Engineering | engineer-mid | L2 | Sonnet | Standard features and fixes |
| Engineering | engineer-senior | L3 | Sonnet (high) | Cross-module, hard bugs, refactors |
| Engineering | engineer-principal | L4 | Opus | Architecture, tech decisions |
| Engineering | qa-engineer | L2 | Sonnet (low) | Tests and verification |
| Engineering | devops-engineer | L2 | Sonnet | CI/CD, deploy configs |
| Engineering | security-engineer | L3 | Sonnet (high) | Defensive security review |
| Marketing | content-marketer | L2 | Sonnet | Copy, posts, emails, scripts |
| Marketing | growth-marketer | L2 | Sonnet | GTM, campaigns, SEO plans |
| Marketing | video-producer | L2 | Sonnet | Storyboards, ad videos |
| Quality | reviewer | L3 | Sonnet → Opus at Polished | Quality gate for any deliverable |

Then add one line: "Start a task with `/shakaiteam:shak <what you want>` — the front desk asks a few questions, proposes a team, and you approve it. The model column is the default; `/shak` raises or lowers it by polish level. Track tokens with `/shakaiteam:stats`; tune the team with `/shakaiteam:retro`."
