# Routing: complexity × polish → team and models

## 1. Score complexity (pick the highest that applies)
| Level | Signals |
|---|---|
| **C1 Simple** | One file/asset, clear cause or spec, copy/config change, short post, status update |
| **C2 Standard** | One area/module, a normal feature or bug, a landing page, one ad, a campaign brief |
| **C3 Complex** | Cross-module, unclear root cause, new integration, multi-asset campaign, research with conflicting sources |
| **C4 Critical** | Architecture/tech choice, security/data risk, brand-defining creative, production launch |

## 2. Polish level (user picks; you recommend)
| Polish | Meaning | Review |
|---|---|---|
| **Draft** | Fast and cheap; good enough to react to | none |
| **Balanced** | Production-ready for normal work (default) | 1 reviewer pass |
| **Polished** | Best possible; cost is secondary | review → revise → final review |

Recommend: C1→Draft, C2→Balanced, C3→Balanced, C4→Polished.

## 3. Engineer level by complexity
C1 → engineer-junior · C2 → engineer-mid · C3 → engineer-senior · C4 → engineer-principal designs, engineer-senior/mid implement.

## 4. Model per role and polish (pass as the Agent `model` override)
| Role tier | Draft | Balanced | Polished |
|---|---|---|---|
| Finders & admin (scout, project-manager, technical-writer, engineer-junior) | haiku | haiku | sonnet |
| Makers (engineer-mid/senior, ux-designer, content/growth-marketer, video-producer, research-analyst, data-scientist, product-manager, qa, devops) | haiku | sonnet | sonnet; the ONE most important making step → opus (or fable if available) |
| Judges & deciders (reviewer, security-engineer) | — | sonnet | opus |
| Leaders (engineer-principal, creative-director) | sonnet | opus | opus (or fable if available) |

Rule of thumb: spend the expensive model on **one** step — the decision or the hero deliverable — and keep everything around it cheap.

## 5. Typical teams
| Task type | Draft | Balanced | Polished |
|---|---|---|---|
| bug-fix | engineer-junior/mid | engineer-mid → qa | engineer-senior → qa → reviewer |
| feature | engineer-mid | product-manager(haiku) → engineer-mid → qa | product-manager → engineer-principal (design) → engineer-senior → qa → security → reviewer |
| landing-page | ux-designer + content-marketer | content-marketer → ux-designer → reviewer | creative-director → content-marketer → ux-designer → reviewer |
| ad-video | video-producer | creative-director(sonnet) → video-producer → reviewer | creative-director(opus) → content-marketer → video-producer → reviewer |
| campaign | growth-marketer | growth-marketer + content-marketer → reviewer | research-analyst → growth-marketer → content-marketer → creative-director review |
| research | scout/research-analyst(haiku) | research-analyst → reviewer | research-analyst ×2 (split sub-questions, parallel) → data-scientist → reviewer(opus) |
| plan | project-manager | product-manager → project-manager | product-manager → engineer-principal (estimates) → project-manager → reviewer |
| docs | technical-writer | technical-writer → reviewer(haiku) | technical-writer(sonnet) → reviewer |

## 6. Cost guards
- Never dispatch an agent for something you can answer in one line from the brief.
- Prefer one agent doing two small related steps over two handoffs.
- Pass summaries + file paths between agents, never full outputs.
