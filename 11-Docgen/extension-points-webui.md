# Extension Points Webui

[← Home](../00-Home.md) | [↑ README](../README.md)

Source: `/a0/usr/projects/agentzero/a0/extensions/webui`

- `.gitkeep` (0 bytes) — Placeholder to preserve empty directory in git
- `fetch_api_call_after/` (1 items) — Fires after a fetch() API call completes in the frontend
- `fetch_api_call_before/` (1 items) — Fires before a fetch() API call is sent from the frontend
- `get_message_handler/` (1 items) — Fires when processing incoming WebSocket messages in the UI
- `initFw_end/` (2 items) — Fires at the end of Alpine.js initFw initialization (post-DOM setup)
- `json_api_call_after/` (2 items) — Fires after a JSON API response is received in the frontend
- `json_api_call_before/` (1 items) — Fires before a JSON API request is sent from the frontend
- `set_messages_after_loop/` (1 items) — Fires after the message rendering loop completes
- `set_messages_before_loop/` (1 items) — Fires before the message rendering loop starts
- `webui_ws_push/` (1 items) — Fires when the backend pushes a WebSocket event to the frontend
