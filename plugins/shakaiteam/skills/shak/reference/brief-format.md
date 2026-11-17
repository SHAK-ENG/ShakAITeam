# Brief format (what every agent receives)

Keep it under ~40 lines. Agents start with zero context, so the brief must be complete — but only with what THIS step needs.

```
## Brief — <task type> for <Entity> — step <n>/<total>: <role>
Goal: <one sentence, outcome not activity>
Deliverable: <exact file(s) / format / length>
Polish: Draft | Balanced | Polished

Context (from entity memory):
- What <Entity> is: <1 line>
- Audience: <1 line>
- Brand/voice: <colors, fonts, tone — only if relevant to this step>
- Do: <learnings that apply>   Don't: <rejected things that apply>

Team lessons (from playbooks/<role>.md, ≤5 lines, only if relevant):
- <lesson>

Inputs:
- <file paths, reference video path, previous step's summary + paths>

Parameters:
- <param>: <value>  (from template; mark "Assumed" where defaulted)

Acceptance criteria:
1. <testable criterion>
2. ...

Constraints: <budget e.g. "max 3 web searches">, <files you may touch>, <no deploys/sends without approval>
Return: ≤N lines — files, what was verified, open questions. If the task is bigger than described, return "ESCALATE: <reason>".
        If you learned something reusable for future tasks of your role, add up to 2 lines "LESSON: <one sentence>".
```
