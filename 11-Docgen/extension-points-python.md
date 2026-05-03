# Extension Points Python

[← Home](../00-Home.md) | [↑ README](../README.md)

Source: `/a0/usr/projects/agentzero/a0/extensions/python`

- `.gitkeep` (0 bytes) — Placeholder to preserve empty directory in git
- `_functions/` (2 items) — Implicit @extensible decorator hooks organised by module/qualname/start|end
- `agent_init/` (3 items) — Fires when an agent instance is initialized (setup, state, config)
- `banners/` (3 items) — Controls banner display on agent startup and chat load
- `before_main_llm_call/` (2 items) — Fires immediately before the main LLM inference call
- `error_format/` (2 items) — Fires when formatting error messages for agent consumption
- `hist_add_before/` (2 items) — Fires before a message is added to conversation history (filter/transform)
- `hist_add_tool_result/` (2 items) — Fires after a tool result is added to history (log/audit)
- `job_loop/` (2 items) — Fires each iteration of the scheduled job execution loop
- `message_loop_end/` (3 items) — Fires at the end of each agent message loop iteration (teardown)
- `message_loop_prompts_after/` (6 items) — Fires after all prompts are assembled for the current loop iteration
- `message_loop_prompts_before/` (2 items) — Fires before prompt assembly begins for the current iteration
- `message_loop_start/` (2 items) — Fires at the start of each agent message loop iteration (setup)
- `monologue_end/` (2 items) — Fires at the end of the agent monologue phase (cleanup)
- `monologue_start/` (2 items) — Fires at the start of the agent monologue phase (setup)
- `process_chain_end/` (2 items) — Fires at the end of the message processing chain
- `reasoning_stream/` (2 items) — Fires when a reasoning stream begins from the LLM
- `reasoning_stream_chunk/` (2 items) — Fires for each chunk in a reasoning stream
- `reasoning_stream_end/` (2 items) — Fires when a reasoning stream completes
- `response_stream/` (4 items) — Fires when the LLM response stream begins
- `response_stream_chunk/` (2 items) — Fires for each chunk in the LLM response stream
- `response_stream_end/` (3 items) — Fires when the LLM response stream completes
- `startup_migration/` (1 items) — Fires during startup for database/schema migration tasks
- `system_prompt/` (7 items) — Fires during system prompt assembly (inject custom instructions)
- `tool_execute_after/` (2 items) — Fires after a tool is executed (auditing, post-processing)
- `tool_execute_before/` (3 items) — Fires before a tool is executed (validation, transformation)
- `user_message_ui/` (2 items) — Fires when processing a user message from the WebUI
- `util_model_call_before/` (2 items) — Fires before a utility model call (e.g., embedding, quick tasks)
- `webui_ws_connect/` (1 items) — Fires when a WebSocket client connects to the WebUI
- `webui_ws_disconnect/` (1 items) — Fires when a WebSocket client disconnects from the WebUI
- `webui_ws_event/` (1 items) — Fires on WebSocket events between frontend and backend
