---
tags: [agentzero, configuration, settings]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Configuration and Settings

## Settings Location

| File | Scope | Description |
|------|-------|-------------|
| `usr/settings.json` | Global | API keys, model config, all settings |
| `.a0proj/instructions/*.md` | Project | Auto-injected project instructions |
| `.promptinclude.md` | Directory | Auto-injected from working directory |
| `behaviour_adjustment` tool | Persistent | Runtime-adjusted behavioral rules |

## Key Settings Sections

### API Keys

Provider-specific sections in `settings.json`:

```json
{
  "api_keys": {
    "openai": "sk-...",
    "anthropic": "sk-ant-...",
    "google": "...",
    "openrouter": "sk-or-..."
  }
}
```

> Configure via WebUI Settings page or edit `usr/settings.json` directly.

### Model Configuration

Since v1.3, model configuration is managed by the **`_model_config`** plugin:

| Setting | Description | Configured Via |
|---------|-------------|---------------|
| Chat Model | Primary LLM for agent responses | Plugin Settings UI |
| Utility Model | Cheaper model for internal tasks | Plugin Settings UI |
| Embedding Model | Vector embedding model | Plugin Settings UI |

Per-agent and per-project overrides available via plugin config.

See [Per Agent Model Config](../02-Agent-Profiles/Per-Agent-Model-Config.md) for details.

### Model Providers

Agent Zero supports multiple providers via LiteLLM:

| Provider | Format | Notes |
|----------|--------|-------|
| OpenAI | `openai/gpt-4o` | Direct API |
| Anthropic | `anthropic/claude-3-sonnet` | Direct API |
| Google | `google/gemini-pro` | Direct API |
| OpenRouter | `openrouter/anthropic/claude-3` | Aggregator (needs provider prefix) |
| Local | `ollama/llama3` | Via Ollama |
| Custom | `openai/my-model` with base_url | Custom endpoints |

> **Common issue:** OpenRouter models require the full provider prefix (e.g., `anthropic/claude-3-sonnet-20240229`).

## Per-Project Configuration

Projects provide isolated configuration via `.a0proj/`:

| File | Purpose |
|------|---------|
| `project.json` | Project metadata |
| `agents.json` | Agent toggle state |
| `instructions/` | Auto-injected instructions |
| `prompts/` | Project-scoped prompt overrides |
| `agents/<profile>/` | Project-scoped agent profiles |
| `knowledge/` | Project-scoped knowledge files |
| `memory/` | Project-scoped FAISS indexes |
| `secrets_registry.yaml` | Project secrets |

## Environment Variables

| Variable | Purpose |
|----------|---------|
| `A0_SET_*` | Model override variables |
| `CHAT_MODEL` | Override chat model |
| `UTILITY_MODEL` | Override utility model |
| `EMBEDDING_MODEL` | Override embedding model |

## WebUI Configuration

Access via Settings page in the WebUI:
- API keys (provider sections)
- Model selection
- Plugin settings (per-plugin configuration panels)
- Agent management

## `.promptinclude.md` Persistence

Any `*.promptinclude.md` file in the working directory is auto-injected into the system prompt.
Use for:
- Environment context
- Development guidelines
- Project-specific rules
- Tool preferences

> **Critical:** Always persist preference changes to file before responding. Never just acknowledge verbally.

## Related Pages
- [Docker Setup](../08-Deployment/Docker-Setup.md) — Environment variables and Docker config
- [Profile Guide](../02-Agent-Profiles/Profile-Guide.md) — Per-agent settings scoping
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin settings resolution
- [Prompt System](../04-Prompts/Prompt-System.md) — `.promptinclude.md` injection mechanism
