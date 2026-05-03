---
tags: [agentzero, scheduler, tools, tasks]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Scheduler

## Overview

The scheduler manages **persistent tasks** that can run on a schedule, at a specific time, or on-demand. Tasks survive restarts and run in isolated contexts.

```mermaid
graph LR
    A[Create Task] --> B{Type?}
    B -->|Scheduled| C[Cron-based repeat]
    B -->|Planned| D[Specific datetime(s)]
    B -->|Adhoc| E[On-demand execution]
    C --> F[Persisted to usr/scheduler/]
    D --> F
    E --> F
    F --> G[Agent executes task]

    style F fill:#2d8cf0,color:#fff
    style G fill:#67c23a,color:#fff
```

## Task Types

| Type | Method | Description |
|------|--------|-------------|
| Scheduled | `scheduler:create_scheduled_task` | Cron-based repeating tasks |
| Planned | `scheduler:create_planned_task` | One or more specific date/time executions |
| Adhoc | `scheduler:create_adhoc_task` | On-demand, no automatic schedule |

## Operations

| Method | Description |
|--------|-------------|
| `scheduler:list_tasks` | List all tasks (filterable by state, type, time) |
| `scheduler:find_task_by_name` | Lookup task by name |
| `scheduler:show_task` | View task details |
| `scheduler:run_task` | Execute a task immediately |
| `scheduler:delete_task` | Remove a task |
| `scheduler:wait_for_task` | Wait for dedicated-context task to complete |

## Task Parameters

| Param | Required | Description |
|-------|:--------:|-------------|
| `name` | ✅ | Unique task name |
| `system_prompt` | ✅ | System prompt for the task agent |
| `prompt` | ✅ | User prompt / task instructions |
| `attachments[]` | ❌ | File paths to attach |
| `schedule` | ❌ | Cron schedule (minute, hour, day, month, weekday) |
| `plan[]` | ❌ | Array of ISO datetime strings for planned tasks |
| `dedicated_context` | ❌ | Run in isolated chat context |

## Examples

### Scheduled Task (Daily Standup)

```json
{
    "tool_name": "scheduler",
    "tool_args": {
        "method": "create_scheduled_task",
        "name": "daily-standup",
        "system_prompt": "You are a project coordinator.",
        "prompt": "Review open issues and summarize status.",
        "schedule": {"minute": 0, "hour": 9}
    }
}
```

### Planned Task (Release Reminder)

```json
{
    "tool_name": "scheduler",
    "tool_args": {
        "method": "create_planned_task",
        "name": "release-check",
        "system_prompt": "You are a release manager.",
        "prompt": "Verify all PRs are merged for v2.0.",
        "plan": ["2026-05-01T09:00:00"]
    }
}
```

### Adhoc Task

```json
{
    "tool_name": "scheduler",
    "tool_args": {
        "method": "create_adhoc_task",
        "name": "security-scan",
        "system_prompt": "You are a security auditor.",
        "prompt": "Scan dependencies for known vulnerabilities."
    }
}
```

## Persistence

Tasks are persisted to `usr/scheduler/` and survive container restarts.

> **Important:** Always check for existing tasks before creating new ones using `scheduler:find_task_by_name` or `scheduler:list_tasks`.

## Related Pages
- [Tools Reference](../06-Tools/Tools-Reference.md) — Scheduler tool API reference
- [Skills System](../06-Tools/Skills-System.md) — Skills can be invoked by scheduled tasks
- [Agent Loop](../01-Architecture/Agent-Loop.md) — How scheduled tasks integrate with agent execution
- [Common Issues](../09-Troubleshooting/Common-Issues.md) — Debugging scheduler problems
