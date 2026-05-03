---
tags: [agentzero, plugins, extensions, reference]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Extension Points Catalog

## Overview

Extension points are named hooks in the Agent Zero lifecycle where plugins can inject behaviour. Plugins register for extension points by placing numbered Python files in the corresponding directory.

### Registration Pattern

```
plugins/<your_plugin>/extensions/python/<point>/_NN_hook.py
```

- `<point>` — the named extension point
- `_NN_` — two-digit number controlling execution order (00-99)
- Files are loaded and executed in alphabetical/numeric order

## Python Extension Points

### Agent Lifecycle

| Point | When | Common Use |
|-------|------|------------|
| `agent_init` | Agent context created | Initialisation, state setup |
| `monologue_start` | Monologue loop begins | Pre-loop setup |
| `monologue_end` | Monologue loop ends | Post-loop cleanup |
| `process_chain_end` | Full chain completes | Final processing |

### Message Loop

| Point | When | Common Use |
|-------|------|------------|
| `message_loop_start` | Loop iteration begins | Injection, state reset |
| `message_loop_prompts_before` | Before prompt assembly | Modify available prompts |
| `message_loop_prompts_after` | After prompt assembly | Inject additional context |
| `message_loop_end` | Loop iteration completes | Telemetry, logging |
| `hist_add_before` | Before adding to history | Filter, transform messages |
| `hist_add_tool_result` | After tool result generated | Log, audit tool calls |

### LLM Interaction

| Point | When | Common Use |
|-------|------|------------|
| `before_main_llm_call` | Before chat model API call | Inject system messages, modify params |
| `reasoning_stream` | Reasoning stream starts | Telemetry |
| `reasoning_stream_chunk` | Each reasoning chunk | Real-time processing |
| `reasoning_stream_end` | Reasoning stream completes | Post-reasoning analysis |
| `response_stream` | Response stream starts | Telemetry |
| `response_stream_chunk` | Each response chunk | Real-time processing |
| `response_stream_end` | Response stream completes | Post-response processing |
| `util_model_call_before` | Before utility model call | Modify utility model params |

### System

| Point | When | Common Use |
|-------|------|------------|
| `system_prompt` | During prompt assembly | Inject system-level instructions |
| `startup_migration` | On first startup | Data migration, config upgrades |
| `banners` | UI banner display | Version warnings, notifications |
| `error_format` | Error message formatting | Custom error presentation |
| `user_message_ui` | User message from UI | Pre-process user input |

### Tools

| Point | When | Common Use |
|-------|------|------------|
| `tool_execute_before` | Before tool execution | Validation, sandboxing, security |
| `tool_execute_after` | After tool execution | Auditing, result transformation |

### Embedding

| Point | When | Common Use |
|-------|------|------------|
| `embedding_model_changed` | Embedding model switches | Re-index memory/knowledge |

### WebSocket

| Point | When | Common Use |
|-------|------|------------|
| `webui_ws_connect` | WS client connects | Session tracking |
| `webui_ws_disconnect` | WS client disconnects | Cleanup |
| `webui_ws_event` | WS event received | Custom event handling |

### Job Loop (Integrations)

| Point | When | Common Use |
|-------|------|------------|
| `job_loop` | Integration job poll cycle | Email/Telegram/WhatsApp message polling |

## Implicit @extensible Hooks

Some core functions are decorated with `@extension.extensible`, creating implicit start/end hooks:

```
extensions/python/_functions/<module>/<qualname>/<start|end>/
```

Known implicit hooks:

| Module | Qualname | Point | Used By |
|--------|----------|-------|---------|
| `agent` | `Agent.handle_exception` | `end` | `_error_retry` |
| `__main__` | `init_a0` | `end` | Startup hooks |
| `agent` | `Agent.get_chat_model` | `start` | `_model_config` |
| `agent` | `Agent.get_utility_model` | `start` | `_model_config` |
| `agent` | `Agent.get_embedding_model` | `start` | `_model_config` |
| `agent` | `Agent.get_browser_model` | `start` | `_browser_agent` |

## WebUI Extension Points

| Point | When | Used By |
|-------|------|--------|
| `initFw_end` | Alpine init complete | `_skills` |
| `get_message_handler` | Message rendering | `_browser_agent`, `_code_execution` |
| `get_tool_message_handler` | Tool message rendering | `_browser_agent` |
| `set_messages_before_loop` | Before message loop display | WebUI core |
| `set_messages_after_loop` | After message loop display | `_chat_branching` |
| `json_api_call_before` | Before JSON API call | WebUI core |
| `json_api_call_after` | After JSON API call | WebUI core |
| `fetch_api_call_before` | Before fetch API call | WebUI core |
| `fetch_api_call_after` | After fetch API call | WebUI core |
| `webui_ws_push` | WebSocket push event | WebUI core |

### UI Slot Hooks

| Point | Purpose |
|-------|---------|
| `sidebar-quick-actions-dropdown-start` | Inject into sidebar dropdown |
| `_sidebar-quick-actions-main-start` | Inject into main sidebar actions |
| `chat-input-bottom-actions-start` | Inject below chat input |
| `chat-input-progress-start` | Inject into progress area |
| `plugins_list_after_load` | After plugins list renders |
| `plugins-list-dropdown-end` | End of plugins dropdown |
| `plugins-list-header-buttons` | Plugin list header buttons |
| `install-git-actions` | Install from git actions |
| `install-zip-actions` | Install from zip actions |
| `confirm_dialog_after_render` | After confirm dialog renders |
| `onboarding-success-end` | End of onboarding success |
| `welcome-actions-end` | End of welcome actions |

### Alpine Placement Directives

WebUI extensions use `x-move-*` directives in `initFw.js` for HTML injection:
- `x-move-before`, `x-move-after`, `x-move-inside-start`, `x-move-inside-end`

These relocate extension DOM elements to the correct UI position without manual JavaScript.

## Related Pages
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin system overview and discovery
- [Agent Loop](../01-Architecture/Agent-Loop.md) — Where extension points fire in the loop
- [hooks.py](../03-Plugins/hooks-py.md) — Config get/save hooks (alternative extension)
