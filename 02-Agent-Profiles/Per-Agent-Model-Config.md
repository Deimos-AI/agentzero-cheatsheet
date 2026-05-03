---
tags: [agentzero, agents, model-config, configuration]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Per-Agent Model Configuration

## Overview

Since v1.3, model configuration is managed by the **`_model_config`** built-in plugin (`plugins/_model_config/`, `always_enabled: true`). This replaces the legacy `settings.json` model fields.

## Configuration Methods

### 1. Per-Agent Override (via Plugin Settings UI)

The `_model_config` plugin supports `per_agent_config: true`, enabling agent profiles to override model selection.

Configure via the **Plugin Settings UI** under the relevant agent profile.

### 2. Agent Profile `settings.json`

Agent profiles can include a `settings.json` file to control model selection and hyperparameters:

```
usr/agents/my_specialist/
├── agent.yaml
├── settings.json       # Model/hyperparameter overrides
└── prompts/
```

### 3. Environment Variables

Set `A0_SET_` prefixed environment variables for model overrides.

## Extension Hooks

The `_model_config` plugin intercepts model resolution at these extension points:

| Hook Point | Intercept |
|-----------|-----------|
| `agent.get_chat_model/start` | Chat model resolution |
| `agent.get_utility_model/start` | Utility model resolution |
| `agent.get_embedding_model/start` | Embedding model resolution |

## Migration from Legacy

- **Top-level** `tmp/settings.json` model fields (e.g. `chat_model_name`, `util_model_name`) were removed from `helpers/settings.py` in v1.3 — model selection is now managed by the `_model_config` plugin
- **Agent-level** `agents/<profile>/settings.json` files remain **fully valid** and are used by `_model_config` for per-agent hyperparameter overrides
- Auto-migration from legacy top-level fields runs on first startup
- See plugin settings UI for current configuration

## Related Pages
- [Profile Guide](../02-Agent-Profiles/Profile-Guide.md) — Agent profile definition and structure
- [Settings](../07-Configuration/Settings.md) — Global model and API key configuration
- [Extension Points](../03-Plugins/Extension-Points.md) — Model resolution extension hooks
- [Agent Loop](../01-Architecture/Agent-Loop.md) — Where model calls happen
