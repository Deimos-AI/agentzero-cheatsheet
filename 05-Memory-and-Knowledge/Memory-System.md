---
tags: [agentzero, memory, faiss, vector-store]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Memory System

## Overview

Agent Zero has persistent long-term memory powered by **FAISS** vector similarity search. Memories are embedded, indexed, and automatically recalled during conversations.

## Memory Tools

| Tool | Purpose | Safety |
|------|---------|--------|
| `memory_save` | Save a memory entry | ✅ Safe |
| `memory_load` | Query memories by similarity | ✅ Safe (read-only) |
| `memory_delete` | Delete specific memories by ID | ✅ Safe (targeted) |
| `memory_forget` | Remove memories by query/threshold | ⚠️ **DESTRUCTIVE** |

### ⚠️ `memory_forget` Warning

> **`memory_forget` is highly destructive.** It removes memories matching a query with a fuzzy threshold (default 0.75). It can delete large swaths of related memories unintentionally.
>
> **Prefer `memory_delete` with specific IDs** instead:
> 1. Use `memory_load` to find the memories you want to remove
> 2. Note their IDs from the result
> 3. Use `memory_delete` with those specific IDs
>
> Only use `memory_forget` when you genuinely need bulk removal and have verified the scope.

## Memory Areas

| Area | Purpose | Directory |
|------|---------|-----------|
| `main` | General knowledge and facts | `usr/memory/main/` |
| `solutions` | Known solutions to problems | `usr/memory/solutions/` |
| `fragments` | Partial/supplementary knowledge | `usr/memory/fragments/` |

## Storage Architecture

- **Backend:** FAISS vector index per memory subdirectory
- **Embedding:** Uses the configured embedding model
- **Tracking:** Files tracked by SHA-256 checksum; only changed files are re-indexed
- **Location:** `usr/memory/` (user volume)

## Recall Mechanism

The `RecallMemories` extension runs every N loop iterations (configurable):

1. Extracts search query from conversation context (or generates one via utility LLM)
2. Queries FAISS vector store across `main`, `fragments`, and `solutions` areas
3. Results are injected into `loop_data.extras_persistent`
4. Rendered into system prompt via `agent.context.extras.md` template

## Memory save Arguments

```json
{
    "tool_name": "memory_save",
    "tool_args": {
        "text": "Content to remember...",
        "area": "main"
    }
}
```

## Memory load Arguments

```json
{
    "tool_name": "memory_load",
    "tool_args": {
        "query": "search terms",
        "threshold": 0.7,
        "limit": 5,
        "filter": "area=='main'"
    }
}
```

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `query` | string | required | Search text |
| `threshold` | float | 0.7 | Similarity threshold (0=any, 1=exact) |
| `limit` | int | 5 | Max results |
| `filter` | string | — | Python filter expression on metadata keys |

## Per-Project Memory

When a project is active, `.a0proj/memory/` provides project-scoped FAISS indexes. Project memories are isolated from global memories.

## Related Pages
- [Knowledge System](../05-Memory-and-Knowledge/Knowledge-System.md) — User-placed documents vs agent-saved memories
- [Agent Loop](../01-Architecture/Agent-Loop.md) — Where memory recall happens in the loop
- [Tools Reference](../06-Tools/Tools-Reference.md) — memory_save, memory_load, memory_delete tools
- [Project Context](../01-Architecture/Project-Context.md) — Per-project memory isolation
