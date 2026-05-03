---
tags: [agentzero, plugins, architecture]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Plugin Architecture

## Overview

**Plugins rule all.** If you need new behaviour in Agent Zero, write a plugin. If you need a new extension point, submit a PR to the `development` branch.

The plugin system was established by PR #998 (merged 2026-02-19) and provides convention-over-configuration runtime capability discovery.

## Directory Structure

```
plugins/<plugin_id>/
├── plugin.yaml              # Manifest (title, description, version, etc.)
├── default_config.yaml      # Default plugin configuration
├── initialize.py            # Optional init script (runs on startup)
├── hooks.py                 # Config get/save hooks
├── README.md                # Optional docs
├── LICENSE                  # Required for Plugin Index submission
├── api/                     # API handlers (auto-registered at /api/<plugin>/<endpoint>)
│   └── <endpoint>.py
├── extensions/
│   ├── python/              # Backend lifecycle hooks
│   │   └── <extension_point>/
│   │       └── _NN_hook.py  # Numbered for execution order
│   └── webui/               # Frontend hook contributions
│       └── <extension_point>/
│           └── component.html|.js
├── webui/                   # Full plugin pages/components
├── helpers/                 # Shared Python logic
├── prompts/                 # Prompt templates
├── tools/                   # Agent tools
├── agents/                  # Plugin-provided agent profiles
│   └── <agent_name>/
│       ├── agent.yaml
│       └── prompts/
└── conf/                    # Config files (e.g. model_providers.yaml)
```

## Naming Conventions

> **All plugin folder names, sub-folder names, and file names must use `snake_case`.**

| Item | Convention | Example |
|------|------------|--------|
| Plugin root directory | `snake_case` | `deimos_openbao_secrets/` |
| Sub-directories (`helpers/`, `api/`, etc.) | `snake_case` | `my_helper_lib/` |
| Python files | `snake_case` | `credential_resolver.py` |
| YAML / config files | `snake_case` | `default_config.yaml` |

**Why:** A0 imports plugin helpers as `from plugins.<plugin_id>.helpers.<module> import …`. Python cannot import hyphenated module names — using dashes will cause silent import failures at runtime.


## Manifest (plugin.yaml)

```yaml
title: My Plugin              # Human-readable name (REQUIRED)
description: What it does     # REQUIRED
version: 1.0.0                # Semantic versioning
per_agent_config: false       # Enable per-agent config scoping
per_project_config: false     # Enable per-project config scoping
always_enabled: false         # Cannot be disabled by user
settings_sections: []         # UI settings sections definition
```

### Key Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `title` | string | — | Display name in UI |
| `description` | string | — | Brief description |
| `version` | string | `"0.1.0"` | Semantic version |
| `per_agent_config` | bool | `false` | Enables per-agent settings UI |
| `per_project_config` | bool | `false` | Enables per-project settings UI |
| `always_enabled` | bool | `false` | Plugin cannot be toggled off |

## Plugin Discovery

Agent Zero uses a **3-level discovery mechanism** to find and load plugins at startup. The plugin scanner (`_plugin_scan`) traverses known directories looking for valid plugin manifests.

### Discovery Order

1. **Built-in plugins** — `plugins/_<name>/`
   - Ship with Agent Zero itself (in the repository under `plugins/`)
   - Use the `_` prefix convention to distinguish them from user plugins
   - Scanned on every startup — always available
   - Examples: `_memory`, `_skills`, `_code_execution`, `_text_editor`, `_browser_agent`

2. **User plugins** — `usr/plugins/<name>/`
   - Installed by the user into the `usr/plugins/` directory
   - Also scanned on every startup
   - No `_` prefix — plain `snake_case` directory names
   - This is where community, custom, and third-party plugins live

3. **Plugin install** — via Plugin Installer UI or manual placement
   - The `_plugin_installer` built-in plugin provides a UI to browse and install plugins from the Plugin Hub
   - Alternatively, manually place a plugin directory into `usr/plugins/<name>/`
   - Installed plugins are discovered on the next startup

### The `_` Prefix Convention

The **underscore prefix** (`_`) is reserved for built-in plugins. This convention:

- Distinguishes core-shipped plugins from user-installed ones at a glance
- Prevents naming collisions between built-in and user plugins
- Signals that the plugin is maintained as part of the Agent Zero codebase
- User plugins must **not** use the `_` prefix

### How Directories Are Recognized as Plugins

A directory is recognized as a plugin **only if it contains a `plugin.yaml` manifest file**. The scanner:

1. Iterates over `plugins/` and `usr/plugins/` directories
2. For each subdirectory, checks for the presence of `plugin.yaml`
3. If found, parses the manifest (title, description, version, etc.)
4. Registers the plugin and its capabilities (tools, extensions, API routes, etc.)

Without a `plugin.yaml`, a directory is **silently ignored** — it will not appear in the UI or expose any functionality.

### Plugin Scan Sequence

```
Startup → scan plugins/_*/ → scan usr/plugins/*/ → register all with valid plugin.yaml → run initialize.py (if present)
```

Built-in plugins are scanned first, then user plugins. If both have a tool or extension with the same name, the user plugin takes precedence (last-writer-wins for extension hooks).

## Extension File Naming

- **Named lifecycle hooks:** `extensions/python/<point>/_NN_hook.py` — numbered for deterministic execution order
- **Implicit @extensible hooks:** `extensions/python/_functions/<module>/<qualname>/<start|end>/_NN_hook.py`
- **WebUI breakpoints:** `extensions/webui/<point>/component.html` or `.js`

> Do NOT use the retired flattened `python/<module>_<qualname>_<start|end>/` form.

## API Auto-Registration

Files in `api/` are automatically registered as API endpoints:

```
api/v1/my_endpoint.py  →  /api/<plugin_id>/v1/my_endpoint
```

## Built-in Plugins

| Plugin | Purpose |
|--------|---------|
| `_memory` | Memory recall, embedding, FAISS management |
| `_skills` | Skill loading, search, and discovery |
| `_model_config` | Model selection and configuration |
| `_code_execution` | Terminal/Python/Node execution |
| `_text_editor` | File read/write/patch operations |
| `_browser_agent` | Browser automation |
| `_chat_branching` | Chat forking and branching |
| `_chat_compaction` | Context window compaction |
| `_promptinclude` | `.promptinclude.md` injection |
| `_discovery` | Onboarding and banner display |
| `_error_retry` | Automatic error recovery |
| `_infection_check` | Security scanning |
| `_email_integration` | Email polling and sending |
| `_telegram_integration` | Telegram bot integration |
| `_whatsapp_integration` | WhatsApp integration |
| `_plugin_installer` | Plugin Hub install/uninstall |
| `_plugin_scan` | Plugin directory scanner |
| `_plugin_validator` | Plugin compliance checker |
| `_onboarding` | First-run experience |
| `_a0_connector` | CLI connector support |

## Related Pages
- [Extension Points](../03-Plugins/Extension-Points.md) — Lifecycle hooks provided by plugins
- [hooks.py](../03-Plugins/hooks-py.md) — Plugin config get/save hooks
- [Directory Map](../01-Architecture/Directory-Map.md) — Where plugins live on disk
- [Settings](../07-Configuration/Settings.md) — Plugin settings resolution and scopes
