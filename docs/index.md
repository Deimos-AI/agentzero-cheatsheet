# Agent Zero Developer Knowledge Base — Documentation Index

> **Generated:** 2026-04-27 | **Primary AI Retrieval Source**

---

## Project Overview

- **Type:** Monolithic documentation vault (Obsidian-compatible Markdown)
- **Purpose:** Community-maintained reference for the Agent Zero framework
- **Audience:** Operators + Developers
- **Framework Version:** v1.3+
- **Total Pages:** 28 files (18 content + 10 docgen catalogs)

---

## Generated Documentation

### Core Analysis

- [Vault Audit Report](./vault-audit-report.md) — **Key deliverable**: Quality, completeness, gap analysis
- [Project Overview](./project-overview.md) — What this vault is, audience, coverage summary
- [Source Tree Analysis](./source-tree-analysis.md) — Annotated vault structure with gap markers
- [Development Guide](./development-guide.md) — Conventions, contribution workflow, quality checklist

---

## Vault Content by Section

### Quick Reference

| # | Section | Pages | Status | Key Topics |
|---|---------|-------|--------|------------|
| 00 | Home | 1 | ✅ | Navigation hub, golden rules |
| 01 | Architecture | 4 | ⚠️ | Agent loop, hierarchy, context, directories |
| 02 | Agent Profiles | 2 | ✅ | agent.yaml, model config overrides |
| 03 | Plugins | 3 | ⚠️ | Architecture, hooks.py, extension points |
| 04 | Prompts | 1 | ✅ | Resolution chain, {{ include }}, overrides |
| 05 | Memory & Knowledge | 2 | ⚠️ | FAISS, file indexing, tools |
| 06 | Tools | 1 | ⚠️ | Tool reference (code_execution_tool gap) |
| 07 | Configuration | 1 | ✅ | settings.json, migration notes |
| 08 | Deployment | 1 | ✅ | Docker setup, volumes, permissions |
| 09 | Troubleshooting | 1 | ✅ | Issue/solution tables for 6 categories |
| 10 | Contributing | 1 | ✅ | PR process, quality checklist |
| 11 | Docgen | 10 | 📋 | Auto-generated source file catalogs |

### Critical Gaps Detected

> ⚠️ **8 sections** have missing content. See [Vault Audit Report](./vault-audit-report.md#4-gap-analysis) for full details.

**Critical (fill first):**
- `code_execution_tool` documentation (06-Tools) — body is empty
- Plugin Directory Structure + Discovery (03-Plugins) — sections empty

**High priority:**
- Context Assembly (01-Architecture/Agent-Loop) — section empty
- LLM Interaction Extension Points (03-Plugins) — section empty
- Skills System — entire topic missing (no page exists)

---

## Existing Vault Pages

### Architecture (01)
- [Agent Loop](../01-Architecture/Agent-Loop.md) — Monologue cycle, JSON output format
- [Directory Map](../01-Architecture/Directory-Map.md) — Persistence vs ephemeral paths
- [Multi-Agent Hierarchy](../01-Architecture/Multi-Agent-Hierarchy.md) — Delegation trees
- [Project Context](../01-Architecture/Project-Context.md) — .a0proj workspaces

### Agent Profiles (02)
- [Profile Guide](../02-Agent-Profiles/Profile-Guide.md) — agent.yaml schema
- [Per-Agent Model Config](../02-Agent-Profiles/Per-Agent-Model-Config.md) — Model overrides

### Plugins (03)
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin system overview
- [hooks.py](../03-Plugins/hooks-py.md) — Hook configuration
- [Extension Points](../03-Plugins/Extension-Points.md) — Full extension point catalog

### Prompts (04)
- [Prompt System](../04-Prompts/Prompt-System.md) — Resolution chain, overrides

### Memory & Knowledge (05)
- [Memory System](../05-Memory-and-Knowledge/Memory-System.md) — FAISS vector store
- [Knowledge System](../05-Memory-and-Knowledge/Knowledge-System.md) — File indexing

### Tools (06)
- [Tools Reference](../06-Tools/Tools-Reference.md) — Agent tool catalog

### Configuration (07)
- [Settings](../07-Configuration/Settings.md) — settings.json reference

### Deployment (08)
- [Docker Setup](../08-Deployment/Docker-Setup.md) — Container deployment guide

### Troubleshooting (09)
- [Common Issues](../09-Troubleshooting/Common-Issues.md) — Issue/solution tables

### Contributing (10)
- [Contributing Guide](../10-Contributing/Contributing-Guide.md) — PR process and standards

### Docgen (11)
- [Docgen README](../11-Docgen/README.md) — Auto-generated catalog explanation
- [Agents Catalog](../11-Docgen/agents.md) — Agent persona files
- [API Routes Catalog](../11-Docgen/api-routes.md) — API endpoint files
- [Config Catalog](../11-Docgen/conf.md) — Configuration files
- [Python Extension Points](../11-Docgen/extension-points-python.md) — Python hooks
- [WebUI Extension Points](../11-Docgen/extension-points-webui.md) — WebUI hooks
- [Prompts Catalog](../11-Docgen/prompts.md) — Prompt template files
- [Python Helpers](../11-Docgen/python-helpers.md) — Core Python modules
- [Skills Catalog](../11-Docgen/skills.md) — Skill files
- [Tools Catalog](../11-Docgen/tools.md) — Tool scripts

### Root Files
- [README](../README.md) — Repository landing page
- [Home](../00-Home.md) — Navigation hub

---

## Repositories

| Role | URL |
|------|-----|
| Primary (Gitea) | https://gitea.deimos.local/deimosAI/agentzero-dev-knowledgebase |
| Mirror (GitHub) | https://github.com/Deimos-AI/agentzero-dev-knowledgebase |
| Upstream | https://github.com/sleepinginrlyeh/agentzero-dev-knowledgebase |

---

## Getting Started

1. **Read the vault:** Start at [Home](../00-Home.md) for navigation
2. **Review quality:** See [Vault Audit Report](./vault-audit-report.md) for gap analysis
3. **Contribute:** Follow [Development Guide](./development-guide.md) for conventions
4. **Check gaps:** See [audit report §4](./vault-audit-report.md#4-gap-analysis) for priority list

---

*Generated by Mary 📊 (BMAD Business Analyst) — 2026-04-27*
