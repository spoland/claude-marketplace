---
name: context-advisor
description: >
  Advises on context window management to reduce token costs. Use this skill
  when a user asks about context, token usage, when to clear or compact,
  whether to start a fresh session, or how to reduce Claude Code costs.
  Also triggers automatically via Stop hook after task completion.
effort: low
---

# Context Advisor

Evaluate the current context window state and give a clear, actionable
recommendation. Keep responses brief — one line for routine checks,
a short paragraph only if the situation is complex.

---

## Decision Matrix

| Context Used | Next Task | Recommendation |
|---|---|---|
| < 30% | Related | Continue — no action needed |
| < 30% | Unrelated | `/clear` — fresh start is cheap |
| 30–60% | Related | Continue — monitor usage |
| 30–60% | Unrelated | `/clear` — avoid dragging irrelevant context |
| 60–80% | Any | `/compact` — preserve useful history, reduce tokens |
| > 80% | Any | `/compact` immediately, then consider `/clear` after |

---

## Key Commands

- `/cost` — show current token usage for the session
- `/clear` — wipe context entirely, start fresh (cheapest option)
- `/compact` — summarise conversation history, keep working (middle ground)
- `/model haiku` or `/model sonnet` — drop to cheaper model after compaction

---

## Cost Context

Token costs scale with context size — every message re-reads the full
conversation history. A 80% full context window on Opus costs roughly
19x more per turn than the same conversation on Haiku.

After `/compact` or at the start of a new unrelated task, always consider
whether the current model is appropriate using the model-selector skill.

---

## Behaviour Notes

- Be brief — this skill fires frequently via the Stop hook
- Never recommend `/clear` if the user is mid-task with unsaved state
- If unsure about next task relevance, ask one question before recommending
- Pair recommendations with the model-selector skill when context resets
