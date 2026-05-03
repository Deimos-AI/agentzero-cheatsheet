---
aliases: [readme]
tags: [agentzero, developer knowledgebase]
---

# agentzero-dev-knowledgebase

A comprehensive, community-maintained reference for **Agent Zero** — covering operators and developers alike.

> **🌐 Browsing on Gitea or GitHub?** All links are relative markdown — just click through.
> Best experience: open as an **Obsidian vault** for graph view and search, or browse directly on Gitea/GitHub.

## Start Here

**👉 [00-Home.md](00-Home.md) — the navigation hub for the entire developer knowledgebase.**

## Structure

```
00-Home.md                    ← Navigation hub (start here!)
01-Architecture/              ← How Agent Zero works internally
  ├── Directory-Map.md        ← Where everything lives on disk
  ├── Agent-Loop.md           ← The monologue cycle
  ├── Multi-Agent-Hierarchy.md ← Superior/subordinate delegation
  └── Project-Context.md      ← The .a0proj/ project system
  └── WebUI-Guide.md         ← Web interface, rendering pipeline
02-Agent-Profiles/            ← Agent profiles and configuration
  ├── Profile-Guide.md        ← Creating and managing profiles
  └── Per-Agent-Model-Config.md ← Per-profile model overrides
03-Plugins/                   ← Plugin system (the extensibility layer)
  ├── Plugin-Architecture.md  ← Directory structure, manifest, discovery
  ├── hooks-py.md             ← Config lifecycle hooks
  └── Extension-Points.md     ← Full Python + WebUI extension catalog
04-Prompts/                   ← Prompt system (control the agent)
  └── Prompt-System.md        ← Assembly, override chain, .promptinclude
05-Memory-and-Knowledge/      ← Persistent memory and knowledge
  ├── Memory-System.md        ← FAISS, recall, memory tools
  └── Knowledge-System.md     ← Knowledge files and indexing
06-Tools/                     ← Every tool, its args, and usage
  └── Tools-Reference.md      ← Complete tool reference
  ├── Skills-System.md         ← Skills workflow packages
  ├── Scheduler.md             ← Scheduled, planned, adhoc tasks
  └── MCP-Integration.md       ← Model Context Protocol
07-Configuration/             ← Settings and configuration
  └── Settings.md             ← API keys, models, environment variables
08-Deployment/                ← Running Agent Zero
  └── Docker-Setup.md         ← Docker, volumes, updates, permissions
09-Troubleshooting/           ← Common issues and fixes
  └── Common-Issues.md        ← Symptom → cause → fix tables
10-Contributing/              ← Contributing to this developer knowledgebase
  └── Contributing-Guide.md   ← How to improve this knowledgebase
11-Docgen/                     ← Auto-generated codebase catalog
  ├── prompts.md              ← All prompt files
  ├── api-routes.md           ← All API route files
  ├── extension-points-*.md   ← Full Python + WebUI extension points
  ├── tools.md                ← Tool file catalog
  ├── skills.md               ← Skill directory catalog
  └── agents.md               ← Agent profile catalog
```

## Golden Rules

1. **Never edit outside `/a0/usr/`** — anything else gets blown away on update
2. **Plugins rule all** — if you need new behaviour, write a plugin
3. **Submit PRs to `development` branch** — not `main`
4. **`memory_forget` is destructive** — use sparingly, prefer `memory_delete` by ID
5. **Prompt overrides go in `usr/`** — never edit `/a0/prompts/` directly

## Help Resources

- [Agent Zero Discord](https://discord.gg/dpSzUPnX)
- [Agent Zero Homepage](https://www.agent-zero.ai/)
- [Agent Zero DeepWiki](https://deepwiki.com/agent0ai/agent-zero)
- [Agent Zero Docs](https://www.agent-zero.ai/p/docs/)

## Contributing to This Knowledge Base

Fork, edit, PR — see [Contributing Guide](10-Contributing/Contributing-Guide.md).

## Contributing to Agent Zero

To contribute to Agent Zero itself (plugins, core, extensions), see the contributing docs in the [agent-zero repository](https://github.com/agent0ai/agent-zero).

## License

See [LICENSE](LICENSE).
