---
name: model-selector
description: >
  Advises on the most appropriate Claude model and effort level for the current
  task before work begins. Use this skill whenever a user starts a new task,
  asks "which model should I use", mentions Claude Code model selection, wants
  to optimise cost or speed vs quality, or begins any task where model choice
  could materially affect outcome or cost. Trigger at the start of sessions and
  when task scope becomes clear. Always use this skill before beginning complex
  or expensive operations.
effort: low
---

# Model Selector

Evaluate the incoming task and recommend the optimal Claude model and effort
level before proceeding. State the recommendation clearly, explain the
reasoning in one sentence, and provide the switch command.

---

## Model Tiers

| Model | Alias | Best For |
|---|---|---|
| Haiku | `haiku` | Simple edits, grep, formatting, docs, single-file changes |
| Sonnet | `sonnet` | Standard coding, debugging, moderate refactors, most daily work |
| Opus | `opus` | Complex architecture, deep multi-file reasoning, ambiguous specs, long agentic runs |

## Effort Levels

| Level | Flag | When |
|---|---|---|
| Low | `--effort low` | Routine tasks, clear requirements, simple edits |
| Medium | `--effort medium` | Standard feature work, debugging with stack trace |
| High | `--effort high` | Non-obvious design decisions, trade-off analysis |
| Max | `--effort max` | Architecting systems, deep bugs, security review |

> Note: effort is supported on Opus 4.6 and Sonnet 4.6 only.

---

## Classification Heuristics

**→ Haiku** if the task is:
- Single file, localised change (rename, reformat, add comment)
- Purely mechanical (find/replace, generate boilerplate from template)
- Documentation only
- Answering a narrow factual question about the codebase

**→ Sonnet** if the task is:
- Multi-file but well-scoped feature work
- Debugging with a clear error and stack trace
- Writing or updating tests
- Standard API integration or CRUD work
- Most day-to-day development tasks

**→ Opus** if the task is:
- Ambiguous or under-specified requirements needing refinement
- Architectural decisions spanning multiple services/systems
- Long agentic runs (>10 tool calls expected)
- Security-sensitive review or threat modelling
- Performance profiling with non-obvious root cause
- Migrating or refactoring large, complex codebases

**Elevate effort level** if:
- Multiple valid design approaches exist and trade-offs are non-trivial
- The task involves concurrency, distributed state, or security
- Previous attempts at this task failed unexpectedly

---

## Output Format

```
## Model Recommendation

**Model**: <Model Name> (`/model <alias>`)
**Effort**: <Low | Medium | High | Max> (`--effort <level>` or "default is fine")
**Reason**: <One sentence justification>

**To apply**:
  /model <alias>
```

If already on the correct model and effort, confirm and proceed immediately.

---

## Behaviour Notes

- Do not ask the user to classify their own task — infer from what they've said
- If task scope is genuinely unclear, ask one clarifying question before recommending
- Default to Sonnet when uncertain — it covers the widest range well
- Never recommend Opus for tasks that are clearly Haiku or Sonnet scope
- Models can be switched mid-session with `/model <alias>` — no restart needed
- After giving the recommendation, **stop and wait for the user to respond** before proceeding — do not continue with the task until the user confirms or replies
