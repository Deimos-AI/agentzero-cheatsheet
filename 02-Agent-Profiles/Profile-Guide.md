---
tags: [agentzero, agents, profiles]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Agent Profile Guide

## agent.yaml Schema

| Field | Type | Required | Default | Description |
|-------|------|:--------:|---------|-------------|
| `title` | string | No | folder name | Human-readable display name |
| `description` | string | No | `""` | Brief summary of specialisation (1-2 sentences) |
| `context` | string | No | `""` | Usage guidance for when to use this agent |
| `enabled` | boolean | No | `true` | Whether profile appears in available profiles |

> **Note:** The `name` field is derived from the folder name — do NOT include it in `agent.yaml`.

## Minimal Example

```yaml
title: My Specialist
description: Expert in domain X with capabilities Y and Z.
context: Use for tasks involving X, when you need Y, or for Z operations.
```

## Directory Structure

```
usr/agents/my_specialist/
├── agent.yaml          # Required metadata
├── prompts/            # Prompt overrides (optional)
│   └── agent.system.main.specifics.md
├── tools/              # Custom tools (optional)
│   └── my_tool.py
├── extensions/         # Agent lifecycle hooks (optional)
└── settings.json       # Per-agent model/hyperparameter overrides (optional)
```

## Profile Resolution Order

Profiles exist at three levels (highest wins):

1. **Project:** `<project>/.a0proj/agents/<profile>/`
2. **User:** `usr/agents/<profile>/`
3. **Framework:** `agents/<profile>/`
4. **Plugin:** `plugins/<plugin>/agents/<profile>/`

For `agent.yaml` fields: override values **replace** base values (no deep merge).
For `prompts/` directory: files merge by filename — override files **completely replace** base files of the same name.

## Creating a New Profile

```bash
# Step 1: Create directory
mkdir -p usr/agents/my_specialist

# Step 2: Create agent.yaml
cat > usr/agents/my_specialist/agent.yaml << 'EOF'
title: My Specialist
description: Expert in domain X.
context: Use for tasks involving X.
EOF

# Step 3 (optional): Add prompt overrides
mkdir -p usr/agents/my_specialist/prompts
cp agents/default/agent.system.main.specifics.md usr/agents/my_specialist/prompts/
# Edit the copy — never edit the original

# Step 4 (optional): Add custom tools
mkdir -p usr/agents/my_specialist/tools
# Create tool class extending Tool

# Step 5: Verify
curl http://localhost:80/api/subagents
```

## Naming Conventions

| Component | Convention | Example |
|-----------|-----------|---------|
| Folder name | lowercase, underscores | `my_specialist` |
| Title | Title Case | `"My Specialist"` |
| Tool files | lowercase, underscores | `my_tool.py` |
| Prompt files | dot-separated hierarchy | `agent.system.tool.my_tool.md` |

## Legacy Format Migration

| Legacy Format | Current | Auto-migration |
|--------------|---------|:-------------:|
| `_context.md` (context only) | `agent.yaml` | ✅ Fallback read |
| `agent.json` | `agent.yaml` | ✅ Auto-converts |

Migration happens transparently — no manual action required.

## Related Pages
- [Multi-Agent Hierarchy](../01-Architecture/Multi-Agent-Hierarchy.md) — How profiles define agent personas
- [Per-Agent Model Config](../02-Agent-Profiles/Per-Agent-Model-Config.md) — Per-profile model selection
- [Prompt System](../04-Prompts/Prompt-System.md) — How profile prompts are resolved
- [Settings](../07-Configuration/Settings.md) — Global settings that affect all profiles
