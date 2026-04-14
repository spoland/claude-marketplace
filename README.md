# spoland-claude-marketplace

Personal Claude Code plugin marketplace.

## Install

```
/plugin marketplace add YOUR_GITHUB_USERNAME/stephen-claude-marketplace
```

## Plugins

| Plugin | Description |
|---|---|
| `model-selector` | Recommends optimal Claude model and effort level per task |

## Adding to all projects automatically

Add to `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "stephen-claude-marketplace": {
      "source": {
        "source": "github",
        "repo": "spoland/spoland-claude-marketplace"
      }
    }
  }
}
```
