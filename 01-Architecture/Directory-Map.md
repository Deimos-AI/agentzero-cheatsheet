---
aliases: [directories, file-map]
tags: [agentzero, architecture]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Directory Map

## Core Directories

| Path | Purpose | Persisted? |
|------|---------|:----------:|
| `/a0/` | Framework root | ❌ |
| `/a0/prompts/` | Default system prompts | ❌ |
| `/a0/agents/` | Default agent profiles | ❌ |
| `/a0/plugins/` | Built-in plugins | ❌ |
| `/a0/extensions/` | Core extension points | ❌ |
| `/a0/python/helpers/` | Core Python modules | ❌ |
| `/a0/skills/` | Built-in skills | ❌ |
| `/a0/tools/` | Built-in tool implementations | ❌ |
| `/a0/api/` | API routes | ❌ |
| `/a0/lib/` | Libraries (browser etc.) | ❌ |
| `/a0/docs/` | Documentation | ❌ |
| `/a0/docker/` | Docker configs | ❌ |
| `/a0/conf/` | Framework config | ❌ |

## User Directories (Persisted via Volume Mount)

| Path | Purpose | Notes |
|------|---------|-------|
| `/a0/usr/` | **All user data** — mount this! | Docker volume bind target |
| `/a0/usr/settings.json` | API keys, model config | Primary config file |
| `/a0/usr/memory/` | FAISS vector indexes | Auto-managed |
| `/a0/usr/knowledge/` | Knowledge files | `.md`, `.txt`, `.pdf`, `.csv`, `.html`, `.json` |
| `/a0/usr/agents/` | Custom agent profiles | Overrides `/a0/agents/` |
| `/a0/usr/plugins/` | User plugins | Highest priority |
| `/a0/usr/projects/` | Project workspaces | Each with `.a0proj/` |
| `/a0/usr/skills/` | User skills | |
| `/a0/usr/chats/` | Chat history | |
| `/a0/usr/scheduler/` | Scheduled tasks | |
| `/a0/usr/api/` | User API routes | |
| `/a0/usr/work/` | Default working directory | |
| `/a0/usr/downloads/` | Downloaded files | |

## ⚠️ Critical Convention

> **Never edit files outside `/a0/usr/` for customisation.** Everything outside is part of the framework and will be **destroyed on update**.
>
> - Override prompts in `usr/agents/<profile>/prompts/` or `usr/prompts/`
> - Add agents in `usr/agents/<profile>/`
> - Add plugins in `usr/plugins/<plugin>/`
> - Add knowledge in `usr/knowledge/`

## Related Pages
- [Project Context](../01-Architecture/Project-Context.md) — How projects override defaults
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin directory structure and discovery
- [Knowledge System](../05-Memory-and-Knowledge/Knowledge-System.md) — Knowledge directory layout
- [Settings](../07-Configuration/Settings.md) — Configuration file locations
