---
tags: [agentzero, tools, reference]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Tools Reference

## Core Tools

### `call_subordinate`

Delegate tasks to specialised agent instances.

| Arg | Type | Required | Description |
|-----|------|:--------:|-------------|
| `message` | string | ✅ | Task description with role, goal, steps, stop condition |
| `profile` | string | ❌ | Agent profile name (e.g. `developer`, `researcher`) |
| `reset` | bool | ❌ | `true` = fresh context, `false` = continue existing |

**Key behaviour:**
- Subordinate has **no access to parent history** — everything needed must be in `message`
- Subordinate can itself delegate further (no depth limit)
- Each subordinate runs in isolated `AgentContext`
- Use `§§include(path)` to reference long subordinate output

---

### `code_execution_tool`

Run terminal, Python, or Node.js commands.

| Arg | Type | Description |
|-----|------|-------------|
| `runtime` | string | `terminal`, `python`, `nodejs`, or `output` |
| `code` | string | Command or script |
| `session` | int | Session ID (default 0) |
| `reset` | bool | Kill session before running |

**Runtimes:**
- `terminal` — shell commands via persistent session
- `python` — Python snippets
- `nodejs` — JavaScript snippets
- `output` — poll running work (non-blocking)
- `input` — send keyboard input to interactive programs

---

### `text_editor`

Read, write, and patch files with numbered lines.

| Operation | Args | Description |
|-----------|------|-------------|
| `read` | `path`, `line_from?`, `line_to?` | Read file with line numbers (default first 200 lines) |
| `write` | `path`, `content` | Create/overwrite file (auto-creates dirs) |
| `patch` | `path`, `edits[{from,to,content}]` | Line-range edits (see below) |

**Patch operations:**
- `{from: 5, to: 5, content: "x
"}` — replace single line
- `{from: 1, to: 3, content: "x
"}` — replace range
- `{from: 2, to: 2}` — delete line (no content)
- `{from: 2, content: "x
"}` — insert before line (omit `to`)

**Critical:** For large files, use `patch` or `cat << 'EOF' >> file` — never `write` entire file (token limits).

---

### `document_query`

Read local or remote documents, or answer questions about them.

| Arg | Type | Description |
|-----|------|-------------|
| `document` | string or list | URL or path (accepts lists for cross-document comparison) |
| `query` | string | Single question |
| `queries` | list | Multiple questions |

Without `query`/`queries`, returns full document content.

---

### `response`

Final answer to user. **Ends task processing.**

| Arg | Type | Description |
|-----|------|-------------|
| `text` | string | Markdown-formatted response |

Only use when done or no task active. Supports `§§include(path)` for long content.

---

## Memory Tools

### `memory_save`

Save text to persistent memory. Returns memory ID.

| Arg | Type | Description |
|-----|------|-------------|
| `text` | string | Content to remember |

### `memory_load`

Query memories by similarity.

| Arg | Type | Default | Description |
|-----|------|---------|-------------|
| `query` | string | required | Search text |
| `threshold` | float | 0.7 | Similarity threshold (0=any, 1=exact) |
| `limit` | int | 5 | Max results |
| `filter` | string | — | Python filter expression on metadata |

### `memory_delete`

Delete specific memories by ID. **Safe, targeted removal.**

| Arg | Type | Description |
|-----|------|-------------|
| `ids` | string | Comma-separated memory IDs |

### `memory_forget`

> ⚠️ **DESTRUCTIVE — Use sparingly.**
> Removes memories matching query with fuzzy threshold.
> Can delete large swaths of related memories unintentionally.
> **Prefer `memory_delete` with specific IDs.**

| Arg | Type | Default | Description |
|-----|------|---------|-------------|
| `query` | string | required | Search text |
| `threshold` | float | 0.75 | Match threshold (higher = safer) |
| `filter` | string | — | Python filter expression |

---

## Search and Knowledge Tools

### `knowledge`

Web search (SearXNG) combined with memory search.

| Arg | Type | Description |
|-----|------|-------------|
| `query` | string | Search query |

### `search_engine`

Live web search for real-time data.

| Arg | Type | Description |
|-----|------|-------------|
| `query` | string | Search query |

---

## Utility Tools

### `behaviour_adjustment`

Update persistent behavioral rules (survives restart).

| Arg | Type | Description |
|-----|------|-------------|
| `adjustments` | string | What to add or remove from rules |

### `notify_user`

Send out-of-band notification without ending current task.

| Arg | Type | Description |
|-----|------|-------------|
| `message` | string | Notification text |
| `type` | string | `info`, `success`, `warning`, `error`, `progress` |
| `title` | string | Optional title |
| `priority` | string | Optional priority |

### `skills_tool`

Discover and load skills.

| Method | Description |
|--------|-------------|
| `skills_tool:search` | Find skills by keywords |
| `skills_tool:list` | List available skills |
| `skills_tool:load` | Load skill by name |

### `scheduler`

Manage scheduled and planned tasks.

| Method | Description |
|--------|-------------|
| `scheduler:list_tasks` | List tasks (filterable) |
| `scheduler:find_task_by_name` | Lookup by name |
| `scheduler:create_scheduled_task` | Cron-based task |
| `scheduler:create_adhoc_task` | One-time task |
| `scheduler:create_planned_task` | Scheduled at specific times |
| `scheduler:run_task` | Execute a task |
| `scheduler:delete_task` | Remove a task |
| `scheduler:show_task` | View task details |
| `scheduler:wait_for_task` | Wait for dedicated-context task |

### `wait`

Pause execution.

| Arg | Type | Description |
|-----|------|-------------|
| `seconds` | number | Duration to wait |
| `until` | string | ISO timestamp to wait until |

---

## Remote Tools (CLI Connector)

These tools operate on the **remote machine** where the CLI client is running.

### `code_execution_remote`

Same as `code_execution_tool` but on remote machine.

### `text_editor_remote`

Same as `text_editor` but on remote machine filesystem.

**Requirements:** CLI client connected with remote execution enabled.

## Related Pages
- [Agent Loop](../01-Architecture/Agent-Loop.md) — How tools are called in each iteration
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugins can provide custom tools
- [Skills System](../06-Tools/Skills-System.md) — Skills vs Tools distinction
- [MCP Integration](../06-Tools/MCP-Integration.md) — External tools via MCP
