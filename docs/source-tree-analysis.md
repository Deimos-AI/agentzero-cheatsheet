# Source Tree Analysis — Agent Zero Developer Knowledge Base

> **Generated:** 2026-04-27 | **Scan Level:** Deep

---

## Vault Directory Structure

```
agentzero-dev-knowledgebase/                     # Root — Obsidian-compatible vault
│
├── README.md                              # 🏠 Landing page — project overview, golden rules, links
├── LICENSE                                 # 📄 Repository license
│
├── 00-Home.md                              # 🔑 Navigation hub — full section index table
│                                          #    Entry point for vault exploration
│
├── 01-Architecture/                        # 🏗️ Core Agent Zero architecture
│   ├── Agent-Loop.md                       #    ⚠️ Monologue cycle, JSON output format
│   │                                       #       GAP: Context Assembly section empty
│   ├── Directory-Map.md                    #    ✅ Persistence vs ephemeral file mapping
│   │                                       #       Critical: /a0/usr/ is the only persisted path
│   ├── Multi-Agent-Hierarchy.md            #    ✅ Delegation trees, subordinate isolation
│   └── Project-Context.md                  #    ✅ .a0proj isolated workspaces
│
├── 02-Agent-Profiles/                      # 🤖 Agent profile system
│   ├── Profile-Guide.md                    #    ✅ agent.yaml schema, naming, directory layout
│   └── Per-Agent-Model-Config.md           #    ✅ _model_config overrides per agent
│
├── 03-Plugins/                             # 🔌 Plugin system & extension points
│   ├── Plugin-Architecture.md              #    ⚠️ Plugin structure, API auto-registration
│   │                                       #       GAP: Directory Structure + Discovery empty
│   ├── hooks-py.md                         #    ✅ hooks.py configuration, get/save plugin config
│   └── Extension-Points.md                 #    ⚠️ Full extension point catalog
│                                           #       GAP: LLM Interaction section empty
├── 04-Prompts/                             # 📝 Prompt resolution system
│   └── Prompt-System.md                    #    ✅ Resolution chain, {{ include }}, overrides
│
├── 05-Memory-and-Knowledge/                # 🧠 Memory & knowledge subsystems
│   ├── Memory-System.md                    #    ⚠️ FAISS vector store, per-project isolation
│   │                                       #       GAP: memory_forget warning empty
│   └── Knowledge-System.md                 #    ⚠️ File indexing, SHA-256, supported formats
│                                           #       GAP: Duplicate "Supported Formats" header
├── 06-Tools/                               # 🛠️ Agent tool reference
│   └── Tools-Reference.md                  #    ⚠️ Tool argument schemas and usage
│                                           #       GAP: code_execution_tool body empty (----)
├── 07-Configuration/                       # ⚙️ Settings & configuration
│   └── Settings.md                         #    ✅ settings.json reference, migration notes
│
├── 08-Deployment/                          # 🚀 Deployment guides
│   └── Docker-Setup.md                     #    ✅ Docker pull, run, volumes, permissions
│
├── 09-Troubleshooting/                     # 🔧 Common issues & solutions
│   └── Common-Issues.md                    #    ✅ Issue/solution tables for 6 categories
│
├── 10-Contributing/                        # 🤝 Contribution guidelines
│   └── Contributing-Guide.md               #    ✅ Fork, branch, PR process, quality checklist
│
└── 11-Docgen/                              # 📋 Auto-generated source file catalogs
    ├── README.md                           #    ✅ Explains docgen purpose
    ├── agents.md                           #    📋 Agent persona file listing
    ├── api-routes.md                       #    📋 API endpoint file listing
    ├── conf.md                             #    📋 Configuration file listing
    ├── extension-points-python.md          #    📋 Python extension point listing
    ├── extension-points-webui.md           #    📋 WebUI extension point listing
    ├── prompts.md                          #    📋 Prompt template file listing
    ├── python-helpers.md                   #    📋 Python module listing (largest catalog)
    ├── skills.md                           #    📋 Skill file listing
    └── tools.md                            #    📋 Tool script listing
```

## Critical Paths

| Path | Purpose | Notes |
|------|---------|-------|
| `00-Home.md` | **Primary entry point** | Navigation hub for the entire vault |
| `README.md` | **Repository landing** | First file seen on Gitea/GitHub |
| `01-Architecture/` | **Core concepts** | Must-read for all users |
| `06-Tools/Tools-Reference.md` | **Operator reference** | Most consulted page (but has gap) |
| `03-Plugins/` | **Developer reference** | Plugin development documentation |
| `11-Docgen/` | **Source index** | Auto-generated; not human-authored docs |

## Entry Points

1. **For human readers:** Start at `README.md` → `00-Home.md` → section of interest
2. **For AI agents:** Use `00-Home.md` as the primary retrieval index; navigate via relative links
3. **For contributors:** Start at `10-Contributing/Contributing-Guide.md`

## Notable Absent Directories

| Expected Directory | Status | Notes |
|-------------------|--------|-------|
| `.obsidian/` | ❌ Missing | No Obsidian workspace config (by design — repo-only) |
| `12-WebUI/` | ❌ Missing | No WebUI guide page exists |
| `12-Skills/` | ❌ Missing | Skills system undocumented |
| `templates/` | ❌ Missing | No page templates for contributors |

---

*Generated by Mary 📊 (BMAD Business Analyst) — 2026-04-27*
