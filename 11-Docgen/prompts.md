# Prompts

[← Home](../00-Home.md) | [↑ README](../README.md)

Source: `/a0/usr/projects/agentzero/a0/prompts`

- `agent.context.extras.md` (19 bytes) — Placeholder for additional context injection into agent prompts
- `agent.extras.agent_info.md` (119 bytes) — Injects agent number, profile name, LLM model, and active preset
- `agent.extras.workdir_structure.md` (205 bytes) — Injects the working directory file tree into agent context
- `agent.system.behaviour.md` (32 bytes) — Behaviour adjustment instructions injected from persistent rules
- `agent.system.behaviour_default.md` (73 bytes) — Default behavioural rules applied when no adjustments exist
- `agent.system.datetime.md` (111 bytes) — Injects the current system date and time for temporal awareness
- `agent.system.main.communication.md` (846 bytes) — Defines the JSON response format with thoughts, headline, tool_name, tool_args
- `agent.system.main.communication_additions.md` (623 bytes) — Supplementary communication rules for response formatting
- `agent.system.main.environment.md` (169 bytes) — Runtime environment identification and container context
- `agent.system.main.md` (310 bytes) — Main system prompt that assembles all sub-prompts via dot-path hierarchy
- `agent.system.main.role.md` (221 bytes) — Defines the agent's role, identity, and mission statement
- `agent.system.main.solving.md` (689 bytes) — Problem-solving methodology and step-by-step reasoning instructions
- `agent.system.main.specifics.md` (0 bytes) — Placeholder for project-specific instructions (empty by default)
- `agent.system.main.tips.md` (660 bytes) — Operational tips and best practices for agent execution
- `agent.system.main.tips.py` (869 bytes) — Python logic that dynamically generates tips based on runtime state
- `agent.system.mcp_tools.md` (10 bytes) — Injects available MCP tool definitions into the system prompt
- `agent.system.projects.active.md` (346 bytes) — Project context injection when a project is currently active
- `agent.system.projects.inactive.md` (31 bytes) — Placeholder shown when no project is active
- `agent.system.projects.main.md` (30 bytes) — Project system prompt header that loads active/inactive sub-prompt
- `agent.system.response_tool_tips.md` (69 bytes) — Tips for using the response tool effectively
- `agent.system.secrets.md` (460 bytes) — Instructions for handling secrets and sensitive data in responses
- `agent.system.skills.loaded.md` (90 bytes) — Lists currently loaded skills available to the agent
- `agent.system.skills.md` (232 bytes) — Skill system overview and skill usage instructions
- `agent.system.skills.relevant.md` (190 bytes) — Injects contextually relevant skill suggestions based on current task
- `agent.system.tool.a2a_chat.md` (909 bytes) — Prompt documentation for the a2a_chat tool (remote agent communication)
- `agent.system.tool.behaviour.md` (179 bytes) — Prompt documentation for the behaviour_adjustment tool
- `agent.system.tool.call_sub.md` (848 bytes) — Prompt documentation for the call_subordinate tool (delegation)
- `agent.system.tool.call_sub.py` (1,121 bytes) — Python logic that builds the call_subordinate prompt with available profiles
- `agent.system.tool.document_query.md` (1,093 bytes) — Prompt documentation for the document_query tool
- `agent.system.tool.notify_user.md` (265 bytes) — Prompt documentation for the notify_user tool
- `agent.system.tool.response.md` (460 bytes) — Prompt documentation for the response tool (final answer)
- `agent.system.tool.scheduler.md` (1,402 bytes) — Prompt documentation for the scheduler tool with all methods
- `agent.system.tool.search_engine.md` (377 bytes) — Prompt documentation for the search_engine tool
- `agent.system.tool.skills.md` (684 bytes) — Prompt documentation for the skills_tool with search/list/load methods
