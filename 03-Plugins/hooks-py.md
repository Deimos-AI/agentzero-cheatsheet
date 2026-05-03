---
tags: [agentzero, plugins, hooks, configuration]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# hooks.py — Plugin Configuration Hooks

## Overview

The optional `hooks.py` file in a plugin root provides **config lifecycle hooks** — functions that intercept plugin configuration reads and saves. This is how plugins transform, validate, or coerce settings between the UI and persistent storage.

## Hook Functions

### `get_plugin_config(default=None, **kwargs)`

Called when plugin settings are loaded. Receives the current config dict and returns the config that should be used.

**Use cases:**
- Inject computed defaults
- Coerce legacy config formats
- Merge environment variables into settings

### `save_plugin_config(settings=None, **kwargs)`

Called before plugin settings are persisted. Receives the settings dict and returns what should be saved.

**Use cases:**
- Strip transient UI-only fields
- Validate and sanitize values
- Transform between internal and storage formats

## Examples

### _skills plugin — Config coercion

```python
from __future__ import annotations
from plugins._skills.helpers.runtime import coerce_config

def get_plugin_config(default=None, **kwargs):
    return coerce_config(default)

def save_plugin_config(settings=None, **kwargs):
    return coerce_config(settings)
```

### _model_config plugin — Strip transient fields

```python
def save_plugin_config(result=None, settings=None, **kwargs):
    if settings and isinstance(settings, dict):
        for section in ("chat_model", "utility_model", "embedding_model"):
            if section in settings and isinstance(settings[section], dict):
                settings[section].pop("_kwargs_text", None)
                settings[section].pop("api_key", None)
    return settings
```

## Function Signature

Both hooks receive arbitrary keyword arguments. The framework passes:

| KWarg | Description |
|-------|-------------|
| `default` | Current config dict (for `get_plugin_config`) |
| `settings` | New settings dict from UI (for `save_plugin_config`) |
| `result` | Previous hook result (for chaining) |

## When to Use hooks.py

- You need to **transform** config between storage and runtime formats
- You need to **strip** UI-only fields before persisting
- You need to **merge** environment variables or external state
- You need to **validate** settings beyond what the UI schema provides

## When NOT to Use

- Simple static defaults → use `default_config.yaml`
- One-time init logic → use `initialize.py`
- Lifecycle hooks → use `extensions/python/<point>/`

## Related Pages
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin system overview and structure
- [Extension Points](../03-Plugins/Extension-Points.md) — Alternative lifecycle hook mechanism
- [Settings](../07-Configuration/Settings.md) — Plugin settings resolution chain
