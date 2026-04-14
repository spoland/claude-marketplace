# model-selector

Recommends the optimal Claude model and effort level for the current task,
helping you balance cost, speed, and quality without thinking about it.

## What it does

At the start of tasks (or on demand), evaluates what you're trying to do and
recommends:
- Which model to use: Haiku / Sonnet / Opus
- What effort level to apply: low / medium / high / max
- The exact `/model` command to switch if needed

## Installation

```
/plugin marketplace add spoland/claude-marketplace
/plugin install model-selector@claude-marketplace --scope user
```

## Usage

Invoke the skill explicitly by asking "which model should I use for this?" or
by asking to use the most appropriate model for a task. You can also run
`/skill model-selector:model-selector` to trigger it on demand.

## Model guidance summary

| Task type | Model | Effort |
|---|---|---|
| Simple edits, docs, formatting | Haiku | low |
| Standard feature work, debugging | Sonnet | medium |
| Architecture, complex agentic runs | Opus | high–max |
