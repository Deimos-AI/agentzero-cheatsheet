---
aliases: [home, index]
tags: [agentzero, developer knowledgebase]
---

# 🧭 Agent Zero Developer Knowledge Base

> A comprehensive reference for **operators** and **developers** working with [Agent Zero](https://www.agent-zero.ai/).

---

## 🚀 Start Here

**New to Agent Zero?** Read these first:

| # | Start With | Why |
|---|-----------|-----|
| 1 | [Directory Map](01-Architecture/Directory-Map.md) | Understand where everything lives — and what gets wiped on update |
| 2 | [Docker Setup](08-Deployment/Docker-Setup.md) | Get it running with persistent storage |
| 3 | [Settings](07-Configuration/Settings.md) | Configure API keys, models, and providers |

---

## 📚 Full Reference

| Topic | Description |
|-------|-------------|
| [Agent Loop](01-Architecture/Agent-Loop.md) | How the monologue cycle works |
| [Multi-Agent Hierarchy](01-Architecture/Multi-Agent-Hierarchy.md) | Superior/subordinate delegation tree |
| [Project Context](01-Architecture/Project-Context.md) | The `.a0proj/` project system |
| [WebUI Guide](01-Architecture/WebUI-Guide.md) | Web interface, message rendering, plugin UI |
| [Profile Guide](02-Agent-Profiles/Profile-Guide.md) | Creating and managing agent profiles |
| [Per-Agent Model Config](02-Agent-Profiles/Per-Agent-Model-Config.md) | Per-profile model overrides |
| [Plugin Architecture](03-Plugins/Plugin-Architecture.md) | Plugin directory structure and manifest |
| [hooks.py](03-Plugins/hooks-py.md) | The `hooks.py` config hook system |
| [Extension Points](03-Plugins/Extension-Points.md) | Full catalog of Python + WebUI extension points |
| [Prompt System](04-Prompts/Prompt-System.md) | Prompt assembly and override mechanism |
| [Memory System](05-Memory-and-Knowledge/Memory-System.md) | Memory tools and FAISS vector store |
| [Knowledge System](05-Memory-and-Knowledge/Knowledge-System.md) | Knowledge files and indexing |
| [Tools Reference](06-Tools/Tools-Reference.md) | Every tool, its args, and usage |
| [Skills System](06-Tools/Skills-System.md) | Skills workflow packages |
| [Scheduler](06-Tools/Scheduler.md) | Scheduled, planned, and adhoc tasks |
| [MCP Integration](06-Tools/MCP-Integration.md) | Model Context Protocol tool servers |
| [Common Issues](09-Troubleshooting/Common-Issues.md) | Symptoms and fixes |
| [Contributing Guide](10-Contributing/Contributing-Guide.md) | How to improve this knowledgebase |

---

## 🔍 Codebase Catalogs (Auto-Generated)

| Catalog | Content |
|---------|---------|
| [Prompts](11-Docgen/prompts.md) | All prompt files in the codebase |
| [API Routes](11-Docgen/api-routes.md) | All API endpoint files |
| [Extension Points (Python)](11-Docgen/extension-points-python.md) | Python extension point listing |
| [Extension Points (WebUI)](11-Docgen/extension-points-webui.md) | WebUI extension point listing |
| [Tools](11-Docgen/tools.md) | Tool file catalog |
| [Skills](11-Docgen/skills.md) | Skill directory catalog |
| [Agents](11-Docgen/agents.md) | Agent profile catalog |

---

## Help Resources

- [Agent Zero Discord](https://discord.gg/dpSzUPnX)
- [Agent Zero Homepage](https://www.agent-zero.ai/)
- [Agent Zero DeepWiki](https://deepwiki.com/agent0ai/agent-zero)
- [Agent Zero Docs](https://www.agent-zero.ai/p/docs/)

## Golden Rules

1. **Never edit outside `/a0/usr/`** — anything outside gets blown away on update
2. **Plugins rule all** — if you need new behaviour, write a plugin
3. **Submit PRs to `development` branch** — not `main`
4. **`memory_forget` is destructive** — use sparingly, prefer `memory_delete` by ID
5. **Prompt changes go in `usr/agents/` or `usr/prompts/`** — never edit `/a0/prompts/` directly
