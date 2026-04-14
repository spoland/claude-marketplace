# context-advisor

Automatically prompts with context management recommendations after each task completes, helping reduce Claude Code token costs.

## What it does

- **Stop hook** — fires after every task, checks context usage, recommends `/clear`, `/compact`, or continue in one line
- **PreCompact hook** — reminds you to consider switching to a lighter model after compaction
- **Skill** — answers questions about context management and token costs on demand

## Install

```
/plugin marketplace add spoland/claude-marketplace
/plugin install context-advisor@claude-marketplace --scope user
```

## Usage

Automatic — the Stop hook fires after each task. You'll see a one-line recommendation like:

```
💡 Context: 45% used → Recommend: Continue (related tasks, context still light)
💡 Context: 72% used → Recommend: /compact (history useful but getting expensive)
```

You can also ask directly: "Should I clear my context?" or "How's my token usage?"

## Works well with

- `model-selector` — after a `/clear` or `/compact`, re-evaluate which model to use
