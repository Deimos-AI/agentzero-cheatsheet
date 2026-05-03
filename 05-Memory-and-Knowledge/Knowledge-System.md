---
tags: [agentzero, knowledge, indexing]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Knowledge System

## Overview

Knowledge files are documents loaded into the FAISS vector store for automatic recall. Unlike memories (which are saved by the agent), knowledge files are **placed by the user** into knowledge directories.

## Knowledge Directories

| Location | Scope | Notes |
|----------|-------|-------|
| `usr/knowledge/` | Global | Always available |
| `usr/knowledge/main/` | General knowledge | Primary location |
| `usr/knowledge/solutions/` | Known solutions | Problem-solution pairs |
| `usr/knowledge/fragments/` | Staging area | Intermediate content |
| `<project>/.a0proj/knowledge/` | Project-scoped | Only when project active |

## Supported Formats

| Format | Extension | Notes |
|--------|-----------|-------|
| Markdown | `.md` | Primary format |
| Plain text | `.txt` | Simple documents |
| PDF | `.pdf` | Extracted and chunked |
| CSV | `.csv` | Row-based indexing |
| HTML | `.html` | Parsed text extraction |
| JSON | `.json` | String value extraction |

## Indexing Behaviour

- Knowledge is indexed when the **memory DB is initialized** (first monologue of a chat)
- Files are tracked by **SHA-256 checksum** — only changed files are re-indexed
- The FAISS index is persisted in `usr/memory/` per subdirectory
- Re-indexing is incremental — unchanged files are skipped

## Adding Knowledge

```bash
# Simple: drop files into the knowledge directory
cp my-reference-doc.md /a0/usr/knowledge/main/

# The next chat session will index new/changed files automatically
```

## Knowledge vs Memory

| Aspect | Knowledge | Memory |
|--------|-----------|--------|
| Source | User-placed files | Agent-saved entries |
| Format | Documents (md, pdf, etc.) | Text snippets |
| Edit method | File system | `memory_save` / `memory_delete` |
| Scope | Global or per-project | Global or per-project |
| Recall | Same FAISS recall mechanism | Same FAISS recall mechanism |

## Best Practices

1. **Use structured markdown** with clear headings for better chunk retrieval
2. **Frontmatter metadata** helps with filtering (`type`, `topic`, `tags`)
3. **Keep files focused** — one topic per file produces better vector matches
4. **Use `fragments/` as staging** — consolidate into `main/` when mature
5. **Periodic cleanup** — stale knowledge degrades recall quality

## Related Pages
- [Memory System](../05-Memory-and-Knowledge/Memory-System.md) — Agent-saved memories vs user-placed knowledge
- [Skills System](../06-Tools/Skills-System.md) — Skills can leverage knowledge for context
- [Directory Map](../01-Architecture/Directory-Map.md) — Where knowledge directories live
- [Project Context](../01-Architecture/Project-Context.md) — Project-scoped knowledge isolation
