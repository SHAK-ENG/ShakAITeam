---
name: entity
description: Create, view, update, list or clean up ShakAITeam "main character" memory — the saved context about a brand, product, client or project (e.g. ShakTalk) that every ShakAITeam task reuses across sessions. Use when the user invokes /entity, says "remember this about <name>", or wants to see/edit what ShakAITeam knows.
argument-hint: "[list | show <name> | new <name> | update <name> <fact> | tidy <name>]"
---

# Entity memory

Store location: `./.shakaiteam/entities/` in the current project if it exists (shareable with a team via git), otherwise `<user home>/.claude/shakaiteam/entities/` (personal, works in every session).

Layout:
```
entities/
  INDEX.md                 one line per entity: `slug — what it is — last used YYYY-MM-DD`
  <slug>/
    profile.md             what it is, audience, USPs, defaults per task type   (≤40 lines)
    brand.md               colors, fonts, logo/asset paths, voice, do/don't     (≤30 lines)
    learnings.md           durable preferences & lessons, one per line          (≤30 lines)
    history.md             one line per job                                      (≤40 lines, then compress)
```
Starter files are in `template/` next to this SKILL.md.

## Actions
- **list** — print `INDEX.md`.
- **show <name>** — print `profile.md` and `brand.md`; summarise `learnings.md` and the last 5 history lines. Don't dump everything.
- **new <name>** — copy the template files into `<slug>/`, then ask ONE AskUserQuestion round (≤4 questions: what it is, audience, default language/market, voice) offering best guesses from anything the user already said; fill the files; add an INDEX line.
- **update <name> <fact>** — put the fact in the right file (identity/audience → profile, visual/voice → brand, preference/lesson → learnings). Replace contradicting lines instead of appending.
- **tidy <name>** — dedupe learnings, compress history older than the last 10 entries into ≤5 summary lines, enforce the line limits.

Rules: keep files terse (facts, not prose). Never store passwords, API keys, tokens, payment data, or personal data about private individuals. Asset files (logos, videos) are referenced by path, never copied into memory.
