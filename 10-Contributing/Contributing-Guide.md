---
tags: [agentzero, contributing, knowledgebase, community]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Contributing to This Knowledge Base

## What This Is

This is a **community-maintained knowledgebase** for Agent Zero. It covers architecture, plugins, prompts, memory, tools, configuration, deployment, and troubleshooting for both operators and developers.

## How to Contribute

### Quick Path

1. **Fork** this repo on [GitHub](https://github.com/Deimos-AI/agentzero-dev-knowledgebase) or [Gitea](https://gitea.deimos.local/deimosAI/agentzero-dev-knowledgebase)
2. **Edit** — fix a typo, add a section, write a new page
3. **PR** — submit a pull request with a clear description

### Writing Guidelines

| Guideline | Rule |
|-----------|------|
| File naming | `Title-Case-with-dashes.md` |
| Section naming | Numbered folders (`01-Architecture/`, `03-Plugins/`) |
| Navigation | Use relative markdown links: `[text](../path/to/file.md)` |
| Breadcrumbs | Every page gets `[← Home](../00-Home.md) \| [↑ README](../README.md)` |
| Frontmatter | YAML block with `tags` array |
| Audience | Both operators AND developers — mark advanced sections clearly |

### Structure Convention

```
00-Home.md           ← Navigation hub
NN-Section/          ← Numbered sections
  └── Topic-Name.md  ← Individual pages
11-Docgen/           ← Auto-generated catalogs (don't hand-edit)
```

### Adding a New Page

1. Pick the right numbered section (or create a new `NN-Section/`)
2. Create `Topic-Name.md` with frontmatter, breadcrumb, and content
3. Add a link in [00-Home.md](../00-Home.md) under the appropriate table
4. Add a link in [README.md](../README.md) structure tree
5. Verify links work on Gitea/GitHub

### Quality Checklist

Before submitting a PR:

- [ ] All links are relative markdown (no `[[wikilinks]]`)
- [ ] Breadcrumb is present and correct
- [ ] Frontmatter has tags
- [ ] Content is accurate for current Agent Zero version
- [ ] Both operator and developer perspectives covered where relevant

## Repository Locations

| Instance | URL |
|----------|-----|
| Gitea (primary) | https://gitea.deimos.local/deimosAI/agentzero-dev-knowledgebase |
| GitHub (mirror) | https://github.com/Deimos-AI/agentzero-dev-knowledgebase |
| Upstream (original) | https://github.com/sleepinginrlyeh/agentzero-dev-knowledgebase |

Push to Gitea — changes auto-mirror to GitHub every 8 hours (or on every commit).

---

## Contributing to Agent Zero Itself

This developer knowledgebase documents Agent Zero — but to contribute to **Agent Zero itself** (plugins, core framework, extensions, tools):

| What | Where |
|------|-------|
| Agent Zero repo | [github.com/agent0ai/agent-zero](https://github.com/agent0ai/agent-zero) |
| Plugin Index | [github.com/agent0ai/a0-plugins](https://github.com/agent0ai/a0-plugins) |
| Discord | [discord.gg/dpSzUPnX](https://discord.gg/dpSzUPnX) |

### Agent Zero Contribution Rules

- **Plugin-first** — if you need new behaviour, write a plugin (not a core PR)
- **PR to `development` branch** — not `main`
- **One concern per PR** — especially for security fixes
- **Use `a0-contribute-plugin` skill** for Plugin Hub submissions
- **Review before submitting** — run `a0-review-plugin` first

### Key Branches

| Branch | Purpose |
|--------|---------|
| `main` | Stable releases |
| `development` | Active development, PRs target this |
| `hacking` | Experimental features |

### Key People

| Person | Role |
|--------|------|
| Alessandro (3clyp50) | Plugin architecture (PR #998) |
| Community | Discord contributors |

## Related Pages
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin contribution guidelines
- [Extension Points](../03-Plugins/Extension-Points.md) — Extension point contribution
- [Directory Map](../01-Architecture/Directory-Map.md) — Repository structure overview
- [Docker Setup](../08-Deployment/Docker-Setup.md) — Development environment setup
