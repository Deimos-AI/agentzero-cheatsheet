# Agent Zero Developer Knowledge Base — Vault Audit Report

> **Generated:** 2026-04-27 | **Scan Level:** Deep | **Auditor:** Mary 📊 (BMAD Business Analyst)
> **Vault Version:** Community-maintained, tracking Agent Zero v1.3+

---

## Executive Summary

The agentzero-dev-knowledgebase vault is a well-structured Obsidian-compatible markdown knowledgebase documenting the Agent Zero framework. It covers the full lifecycle from architecture to deployment, targeting both operators and developers.

**Overall Quality Rating: B (Good, with notable gaps)**

| Dimension | Rating | Notes |
|-----------|--------|-------|
| Structure & Navigation | A | Excellent numbered-section convention, consistent breadcrumbs |
| Formatting & Markdown | A- | Clean tables, code blocks, callouts; no wikilinks (by design) |
| Content Completeness | C+ | 6+ sections truncated or stub; critical gaps in tools, plugins |
| Accuracy | B+ | Technically accurate where content exists; v1.3 alignment is good |
| Obsidian Compatibility | B | Frontmatter + tags present; wikilinks deliberately absent |
| Cross-Referencing | B- | Navigation links strong; conceptual cross-links weak |
| Docgen Section | C | File-size catalogs with minimal descriptions; low utility |

**Critical Finding:** The vault has a solid skeleton but multiple sections are incomplete — headers exist with `----` placeholder content. This suggests the vault was scaffolded but not fully populated.

---

## 1. Vault Structure Assessment

### 1.1 Directory Layout

```
agentzero-dev-knowledgebase/
├── 00-Home.md                    ✅ Hub page with full navigation table
├── 01-Architecture/              ✅ 4 pages — core concepts
│   ├── Agent-Loop.md             ⚠️ Context Assembly section empty
│   ├── Directory-Map.md          ✅ Complete
│   ├── Multi-Agent-Hierarchy.md  ✅ Complete
│   └── Project-Context.md        ✅ Complete
├── 02-Agent-Profiles/            ✅ 2 pages — profile system
│   ├── Profile-Guide.md          ✅ Complete
│   └── Per-Agent-Model-Config.md ✅ Complete
├── 03-Plugins/                   ⚠️ 3 pages — gaps present
│   ├── Plugin-Architecture.md    ⚠️ Directory Structure + Discovery sections empty
│   ├── hooks-py.md               ✅ Complete
│   └── Extension-Points.md       ⚠️ LLM Interaction section empty
├── 04-Prompts/                   ✅ 1 page
│   └── Prompt-System.md          ✅ Complete
├── 05-Memory-and-Knowledge/      ⚠️ 2 pages — minor gaps
│   ├── Memory-System.md          ⚠️ memory_forget warning section empty
│   └── Knowledge-System.md       ⚠️ Supported Formats (first instance) empty
├── 06-Tools/                     ⚠️ 1 page — significant gap
│   └── Tools-Reference.md        ⚠️ code_execution_tool body is empty (----)
├── 07-Configuration/             ✅ 1 page
│   └── Settings.md               ✅ Complete
├── 08-Deployment/                ✅ 1 page
│   └── Docker-Setup.md           ✅ Complete
├── 09-Troubleshooting/           ✅ 1 page
│   └── Common-Issues.md          ✅ Complete
├── 10-Contributing/              ✅ 1 page
│   └── Contributing-Guide.md     ✅ Complete
├── 11-Docgen/                    📋 10 auto-generated catalogs
│   ├── README.md                 ✅ Explains purpose
│   ├── agents.md                 📋 File listing
│   ├── api-routes.md             📋 File listing
│   ├── conf.md                   📋 File listing
│   ├── extension-points-python.md 📋 File listing
│   ├── extension-points-webui.md  📋 File listing
│   ├── prompts.md                📋 File listing
│   ├── python-helpers.md         📋 File listing (largest: 168 lines)
│   ├── skills.md                 📋 File listing
│   └── tools.md                  📋 File listing
├── README.md                     ✅ Strong landing page
└── LICENSE                       ✅ Present
```

### 1.2 Section Balance

| Section | Pages | Lines | Status |
|---------|-------|-------|--------|
| 00 Home | 1 | 72 | ✅ Complete |
| 01 Architecture | 4 | 270 | ⚠️ 1 gap |
| 02 Agent Profiles | 2 | 147 | ✅ Complete |
| 03 Plugins | 3 | 350 | ⚠️ 2 gaps |
| 04 Prompts | 1 | 100 | ✅ Complete |
| 05 Memory & Knowledge | 2 | 160 | ⚠️ 2 minor gaps |
| 06 Tools | 1 | 233 | ⚠️ Major gap |
| 07 Configuration | 1 | 108 | ✅ Complete |
| 08 Deployment | 1 | 123 | ✅ Complete |
| 09 Troubleshooting | 1 | 80 | ✅ Complete |
| 10 Contributing | 1 | 103 | ✅ Complete |
| 11 Docgen | 10 | 344 | 📋 Auto-generated |

---

## 2. Content Quality Assessment

### 2.1 Complete & High-Quality Pages (10 pages)

These pages are well-structured, accurate, and substantive:

1. **00-Home.md** — Excellent hub with navigation table, golden rules, resource links
2. **01-Architecture/Directory-Map.md** — Clear persistence vs ephemeral file mapping
3. **01-Architecture/Multi-Agent-Hierarchy.md** — Thorough delegation tree documentation
4. **01-Architecture/Project-Context.md** — Good .a0proj workspace explanation
5. **02-Agent-Profiles/Profile-Guide.md** — Complete agent.yaml schema with examples
6. **02-Agent-Profiles/Per-Agent-Model-Config.md** — Clear _model_config override docs
7. **04-Prompts/Prompt-System.md** — Thorough resolution chain and override documentation
8. **07-Configuration/Settings.md** — Complete settings reference with migration notes
9. **08-Deployment/Docker-Setup.md** — Practical Docker deployment guide
10. **10-Contributing/Contributing-Guide.md** — Clear contribution standards and checklist

### 2.2 Pages With Gaps (6 pages)

| Page | Missing Section | Severity | Impact |
|------|----------------|----------|--------|
| Agent-Loop.md | Context Assembly | Medium | Users won't understand how system prompt is assembled |
| Plugin-Architecture.md | Directory Structure | High | Critical for plugin developers |
| Plugin-Architecture.md | Plugin Discovery | High | Critical for plugin developers |
| Extension-Points.md | LLM Interaction | Medium | Incomplete extension point catalog |
| Tools-Reference.md | code_execution_tool body | High | Most-used tool undocumented |
| Memory-System.md | memory_forget Warning | Low | Important safety note missing |
| Knowledge-System.md | Supported Formats (duplicate header) | Low | Formatting issue |

### 2.3 Accuracy Assessment

- **Technical accuracy:** High where content exists. FAISS references, monologue JSON structure, resolution hierarchies, and Docker commands are correct.
- **Version alignment:** Good — references v1.3+ features (plugin-based config, .a0proj workspaces, _model_config).
- **Legacy migration:** Properly documented with clear deprecation notes.
- **Date consistency:** One potential issue — "v1.3 upstream sync (2026-03-20)" may need verification.

---

## 3. Formatting & Obsidian Compatibility

### 3.1 Strengths
- ✅ Consistent YAML frontmatter with `tags` arrays across all content pages
- ✅ Clean Markdown tables for schemas, configurations, and comparisons
- ✅ Properly fenced code blocks (json, yaml, bash, python)
- ✅ Callout-style notes for critical warnings
- ✅ Consistent breadcrumb navigation (`[← Home]`, `[↑ README]`)

### 3.2 Issues
- ❌ **No Obsidian wikilinks** — Uses `[text](../path/file.md)` instead of `[[file]]`. This is **by design** for Gitea/GitHub compatibility, but reduces Obsidian graph connectivity.
- ⚠️ **`----` placeholder convention** — Horizontal rules used as content placeholders rather than thematic breaks. This is ambiguous and should be replaced with explicit TODO/FIXME markers.
- ⚠️ **Duplicate headers** — "Supported Formats" and "Knowledge vs Memory" appear twice in Knowledge-System.md due to formatting issues.

### 3.3 Recommendation

Consider adopting a **dual-linking strategy**: maintain relative Markdown links for Gitea/GitHub rendering, but add Obsidian `[[wikilinks]]` as inline references for graph connectivity. Obsidian renders both formats; Gitea/GitHub ignore wikilinks gracefully.

---

## 4. Gap Analysis

### 4.1 Missing Content (Content That Should Exist But Doesn't)

| Gap | Priority | Audience | Notes |
|-----|----------|----------|-------|
| **code_execution_tool documentation** | 🔴 Critical | Both | Most-used tool; only entry with empty body |
| **Plugin Directory Structure** | 🔴 Critical | Developers | Plugin devs need the full directory tree |
| **Plugin Discovery Mechanism** | 🔴 Critical | Developers | How plugins are found and loaded |
| **Context Assembly (Agent Loop)** | 🟡 High | Both | How system prompt is built from parts |
| **LLM Interaction Extension Points** | 🟡 High | Developers | Incomplete extension point catalog |
| **memory_forget Safety Warning** | 🟢 Medium | Both | Important operational safety note |
| **Skills System** | 🟡 High | Both | Referenced in docgen but no content page |
| **WebUI Navigation & Features** | 🟡 High | Operators | No dedicated page for the web interface |
| **Scheduler Tool** | 🟡 High | Both | Listed in tools but no documentation |
| **A2A / Multi-Agent Communication** | 🟢 Medium | Developers | No page on remote agent protocol |

### 4.2 Missing Sections (Entire Topics Without Pages)

| Proposed Section | Priority | Suggested Location |
|------------------|----------|-------------------|
| Skills System | 🟡 High | `04a-Skills/` or add to `04-Prompts/` |
| WebUI Guide | 🟡 High | `12-WebUI/` |
| Scheduler & Tasks | 🟡 High | `06a-Scheduler/` or expand `06-Tools/` |
| A2A Protocol | 🟢 Medium | `01-Architecture/` or new section |
| Security Model | 🟢 Medium | `07a-Security/` or expand `07-Configuration/` |
| Upgrading Guide | 🟢 Medium | Expand `08-Deployment/` |
| MCP Integration | 🟡 High | New section or expand `03-Plugins/` |
| Browser Tool | 🟢 Medium | Expand `06-Tools/` |

### 4.3 Docgen Section Assessment

The `11-Docgen/` section contains 10 auto-generated file catalogs. Assessment:

| Aspect | Rating | Detail |
|--------|--------|--------|
| File coverage | B+ | Lists most source files with byte counts |
| Descriptions | D | Almost no functional descriptions — just file names and sizes |
| Maintenance | C | Auto-generated but no docgen script in repo to regenerate |
| Usefulness | C- | Good for finding files; poor for understanding what they do |

**Recommendation:** Either enrich the docgen catalogs with functional descriptions (even 1-line summaries), or clearly label them as "source file indexes" rather than documentation.

---

## 5. Structural Issues

### 5.1 Content Organization

- **Strength:** Numbered section convention (00–11) provides clear reading order
- **Strength:** Section names are descriptive and follow Title-Case
- **Issue:** Section 06 (Tools) is a single large page (233 lines) that could benefit from splitting
- **Issue:** No page covers the Skills system despite Skills being a major Agent Zero feature

### 5.2 Navigation

- **Strength:** Breadcrumb navigation on every page (`← Home`, `↑ README`)
- **Strength:** Home page has complete navigation table
- **Issue:** No forward navigation (→ Next page) or section-level TOC
- **Issue:** README and Home have overlapping navigation roles

### 5.3 Cross-Referencing

- **Strength:** Concepts reference each other in prose
- **Issue:** No backlinks or "Related pages" sections
- **Issue:** No inline links when mentioning concepts covered in other sections

---

## 6. Improvement Recommendations

### 6.1 Critical (Do First)

1. **Fill `code_execution_tool` documentation** — This is the most-used tool and its entry is empty
2. **Complete Plugin Architecture** — Directory Structure and Discovery sections are critical for developers
3. **Add Skills System page** — Major feature with no coverage

### 6.2 High Priority

4. **Complete Context Assembly section** in Agent-Loop.md
5. **Complete LLM Interaction extension points** in Extension-Points.md
6. **Add WebUI Guide page** — Operators need to understand the web interface
7. **Add Scheduler documentation** — Expanding the Tools-Reference or new page
8. **Add MCP Integration documentation** — Model Context Protocol is increasingly important

### 6.3 Medium Priority

9. **Replace `----` placeholders** with explicit `> ⚠️ **TODO:** This section needs content.` callouts
10. **Enrich docgen catalogs** with 1-line functional descriptions per file
11. **Add forward navigation** (`→ Next`) alongside existing breadcrumbs
12. **Add "Related Pages" sections** at the bottom of each page
13. **Split Tools-Reference.md** into per-tool pages if it grows further

### 6.4 Nice to Have

14. **Add Obsidian wikilinks** alongside Markdown links for graph connectivity
15. **Add Mermaid diagrams** for Agent Loop, Multi-Agent Hierarchy, Plugin Discovery
16. **Add search tags** for Obsidian search (e.g., `#tool/code-execution`, `#config/docker`)
17. **Create a docgen script** to auto-regenerate Section 11 from source

---

## 7. Content Quality Matrix

| Page | Complete | Accurate | Formatted | Linked | Overall |
|------|----------|----------|-----------|--------|---------|
| 00-Home | ✅ | ✅ | ✅ | ✅ | A |
| Agent-Loop | ⚠️ | ✅ | ✅ | ✅ | B |
| Directory-Map | ✅ | ✅ | ✅ | ✅ | A |
| Multi-Agent-Hierarchy | ✅ | ✅ | ✅ | ✅ | A |
| Project-Context | ✅ | ✅ | ✅ | ✅ | A |
| Profile-Guide | ✅ | ✅ | ✅ | ✅ | A |
| Per-Agent-Model-Config | ✅ | ✅ | ✅ | ✅ | A |
| Plugin-Architecture | ⚠️ | ✅ | ✅ | ✅ | B- |
| hooks-py | ✅ | ✅ | ✅ | ✅ | A |
| Extension-Points | ⚠️ | ✅ | ✅ | ✅ | B |
| Prompt-System | ✅ | ✅ | ✅ | ✅ | A |
| Memory-System | ⚠️ | ✅ | ✅ | ✅ | B+ |
| Knowledge-System | ⚠️ | ✅ | ⚠️ | ✅ | B |
| Tools-Reference | ⚠️ | ✅ | ✅ | ✅ | B- |
| Settings | ✅ | ✅ | ✅ | ✅ | A |
| Docker-Setup | ✅ | ✅ | ✅ | ✅ | A |
| Common-Issues | ✅ | ✅ | ✅ | ✅ | A- |
| Contributing-Guide | ✅ | ✅ | ✅ | ✅ | A |
| README | ✅ | ✅ | ✅ | ✅ | A |

---

## 8. Repository Health

| Aspect | Status | Detail |
|--------|--------|--------|
| Gitea (primary) | ✅ | https://gitea.deimos.local/deimosAI/agentzero-dev-knowledgebase |
| GitHub (mirror) | ✅ | https://github.com/Deimos-AI/agentzero-dev-knowledgebase |
| Upstream tracking | ✅ | https://github.com/sleepinginrlyeh/agentzero-dev-knowledgebase |
| LICENSE | ✅ | Present |
| README | ✅ | Strong landing page |
| Contributing guide | ✅ | Present with quality checklist |
| Branch strategy | ✅ | PRs to `development` branch |
| Docgen automation | ❌ | No docgen script in repo |

---

## 9. Metrics Summary

| Metric | Value |
|--------|-------|
| Total files | 28 |
| Content pages (Sections 00-10) | 18 |
| Docgen catalogs (Section 11) | 10 |
| Total lines | 2,305 |
| Pages complete | 12 (67%) |
| Pages with gaps | 6 (33%) |
| Empty/truncated sections | 8 |
| Missing topic areas | 5+ |
| Overall quality grade | B |

---

*Audit completed by Mary 📊 (BMAD Business Analyst) — 2026-04-27*
