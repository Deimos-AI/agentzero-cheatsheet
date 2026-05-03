# Python Helpers

[← Home](../00-Home.md) | [↑ README](../README.md)

Source: `/a0/helpers/` on devpod
Total: **87 modules**

## Core Modules

### Agent Core

| Module | Size | Description |
|--------|-----:|-------------|
| `context.py` | 1,269 bytes | Agent context management — current agent instance, conversation state, and pipeline data
| `context_utils.py` | 943 bytes | Utility functions for inspecting and manipulating agent context objects
| `defer.py` | 7,715 bytes | Deferred execution and coroutine scheduling for async agent operations
| `history.py` | 22,556 bytes | Conversation history management — storage, retrieval, truncation, and compaction
| `messages.py` | 2,472 bytes | Message formatting, parsing, and transformation between LLM and internal formats
| `process.py` | 690 bytes | Process management utilities for agent execution lifecycle
| `subagents.py` | 14,443 bytes | Subordinate agent orchestration — profile resolution, delegation, and result handling

### LLM & Models

| Module | Size | Description |
|--------|-----:|-------------|
| `call_llm.py` | 1,655 bytes | Core LLM invocation wrapper with streaming, retries, and error handling
| `dirty_json.py` | 12,107 bytes | Robust JSON extraction from LLM output that handles partial/malformed responses
| `extract_tools.py` | 2,427 bytes | Tool call extraction from LLM responses — parses JSON tool_name/tool_args pairs
| `providers.py` | 5,984 bytes | LLM provider registry and configuration (OpenAI, Anthropic, Google, etc.)
| `tokens.py` | 958 bytes | Token counting and context window size estimation for model selection

### Plugins & Extensions

| Module | Size | Description |
|--------|-----:|-------------|
| `extension.py` | 11,220 bytes | Extension point framework — @extensible decorator, hook discovery, and execution
| `modules.py` | 3,010 bytes | Dynamic module loading and hot-reload for plugin components
| `plugins.py` | 29,073 bytes | Plugin lifecycle management — discovery, loading, config, enable/disable, and validation
| `skills.py` | 16,963 bytes | Skill system — SKILL.md parsing, search, loading, and execution orchestration
| `skills_cli.py` | 11,815 bytes | CLI interface for skill management operations
| `skills_import.py` | 7,827 bytes | Skill import from external sources — URL download, validation, and installation

### Memory & Knowledge

| Module | Size | Description |
|--------|-----:|-------------|
| `cache.py` | 3,077 bytes | In-memory caching layer with TTL support for frequently accessed data
| `document_query.py` | 26,275 bytes | Document ingestion, chunking, embedding, and vector similarity search
| `faiss_monkey_patch.py` | 1,181 bytes | FAISS index optimizations — IndexIVFFlat configuration and metadata indexing
| `vector_db.py` | 4,965 bytes | FAISS vector database management — index creation, persistence, and query operations

### Files & I/O

| Module | Size | Description |
|--------|-----:|-------------|
| `attachment_manager.py` | 3,138 bytes | File attachment handling for chat messages — upload, storage, and retrieval
| `file_browser.py` | 14,063 bytes | File system browser with metadata, filtering, and directory traversal
| `file_tree.py` | 23,440 bytes | File tree generation and rendering for the working directory view
| `files.py` | 24,383 bytes | Core file operations — read, write, prompt loading, and path resolution
| `rfc.py` | 2,072 bytes | Request-for-comments workflow — create, review, and exchange collaborative documents
| `rfc_exchange.py` | 639 bytes | RFC exchange protocol for sharing documents between agents
| `rfc_files.py` | 18,039 bytes | RFC file management — storage, versioning, and status tracking

### Projects & Settings

| Module | Size | Description |
|--------|-----:|-------------|
| `kvp.py` | 2,918 bytes | Key-value pair persistence for lightweight state storage
| `migration.py` | 4,781 bytes | Database and settings schema migration between Agent Zero versions
| `projects.py` | 15,754 bytes | Project management — creation, switching, context loading, and isolation
| `settings.py` | 24,411 bytes | Settings resolution chain — global, per-agent, per-project, and plugin scoping
| `state_monitor.py` | 14,624 bytes | Real-time state monitoring and change detection for settings and config
| `state_monitor_integration.py` | 422 bytes | Integration glue connecting state monitor to the agent lifecycle
| `state_snapshot.py` | 10,847 bytes | State snapshot creation, diffing, and rollback for configuration changes

### Tools

| Module | Size | Description |
|--------|-----:|-------------|
| `functions.py` | 870 bytes | Tool function registration and discovery for the agent tool registry
| `job_loop.py` | 1,728 bytes | Scheduled job execution loop — tick processing and due-task dispatch
| `task_scheduler.py` | 49,209 bytes | Full task scheduler — CRUD, cron parsing, persistence, and execution management
| `tool.py` | 3,121 bytes | Base tool class and tool execution framework for all agent tools
| `watchdog.py` | 13,465 bytes | File system watchdog for detecting changes to knowledge, prompts, and config

### API & Server

| Module | Size | Description |
|--------|-----:|-------------|
| `api.py` | 8,244 bytes | API route auto-discovery and registration from the api/ directory
| `network.py` | 6,715 bytes | Network utilities — port detection, IP resolution, and connectivity checks
| `server_startup.py` | 13,461 bytes | Server initialization — plugin scanning, model loading, and service startup
| `ui_server.py` | 9,750 bytes | WebUI server configuration — static files, CORS, authentication middleware
| `ws.py` | 23,420 bytes | WebSocket endpoint — real-time message streaming between agent and frontend
| `ws_manager.py` | 54,128 bytes | WebSocket connection manager — session tracking, broadcasting, and event routing

### Communication

| Module | Size | Description |
|--------|-----:|-------------|
| `duckduckgo_search.py` | 1,063 bytes | DuckDuckGo search adapter (fallback when SearXNG unavailable)
| `email_client.py` | 22,333 bytes | Email integration — IMAP polling, SMTP sending, and message parsing
| `localization.py` | 7,892 bytes | Internationalization and localization framework for multi-language support
| `message_queue.py` | 5,876 bytes | Message queue management — enqueue, dequeue, and priority handling
| `notification.py` | 8,539 bytes | Notification system — create, deliver, and track user-facing alerts
| `perplexity_search.py` | 1,027 bytes | Perplexity AI search adapter for enhanced web search capabilities
| `searxng.py` | 395 bytes | SearXNG meta-search engine client configuration and query formatting

### Integrations

| Module | Size | Description |
|--------|-----:|-------------|
| `browser.py` | 13,988 bytes | Headless browser automation — page navigation, screenshot capture, and DOM interaction
| `docker.py` | 4,790 bytes | Docker container management for sandboxed code execution environments
| `fasta2a_client.py` | 8,027 bytes | FastA2A protocol client for inter-agent communication over HTTP
| `fasta2a_server.py` | 22,440 bytes | FastA2A protocol server — endpoint registration, context management, and routing
| `git.py` | 16,010 bytes | Git operations — clone, commit, branch management, and status checking
| `integration_commands.py` | 8,169 bytes | Integration command dispatcher for external service interactions
| `mcp_handler.py` | 46,684 bytes | MCP (Model Context Protocol) handler — server lifecycle, tool discovery, and invocation
| `mcp_server.py` | 17,091 bytes | MCP server configuration, connection management, and tool registration
| `tunnel_manager.py` | 4,570 bytes | Network tunnel management for exposing local services remotely

### Security

| Module | Size | Description |
|--------|-----:|-------------|
| `crypto.py` | 1,885 bytes | Cryptographic utilities — hashing, encryption, and key derivation
| `login.py` | 408 bytes | User authentication and session management
| `rate_limiter.py` | 1,909 bytes | API rate limiting with token bucket and sliding window algorithms
| `secrets.py` | 20,969 bytes | Secrets management — env file loading, key resolution, and provider integration
| `security.py` | 1,684 bytes | Security utilities — input sanitization, path traversal prevention, and access control

### UI & Display

| Module | Size | Description |
|--------|-----:|-------------|
| `images.py` | 1,179 bytes | Image processing — resize, encode, and format conversion for agent output
| `log.py` | 13,853 bytes | Logging framework — structured logging, console formatting, and file rotation
| `performance.py` | 1,615 bytes | Performance monitoring — timing decorators, memory tracking, and metrics collection
| `print_catch.py` | 1,006 bytes | stdout/stderr capture for routing print output into the logging system
| `print_style.py` | 8,705 bytes | Terminal styling — colors, formatting, and progress indicators for console output

### Voice & Audio

| Module | Size | Description |
|--------|-----:|-------------|
| `kokoro_tts.py` | 4,010 bytes | Kokoro text-to-speech synthesis for voice output
| `whisper.py` | 3,217 bytes | Whisper speech-to-text transcription for voice input

### Utilities

| Module | Size | Description |
|--------|-----:|-------------|
| `backup.py` | 37,480 bytes | Backup and restore system — full snapshots, selective restore, and migration
| `dotenv.py` | 1,163 bytes | .env file parser for environment variable loading
| `errors.py` | 3,131 bytes | Error classification, formatting, and user-friendly error message generation
| `guids.py` | 147 bytes | GUID/UUID generation utilities for unique identifiers
| `persist_chat.py` | 9,027 bytes | Chat persistence — save, load, and export conversation history
| `runtime.py` | 5,000 bytes | Runtime environment detection — platform, Python version, and capability checks
| `self_update.py` | 29,889 bytes | Self-update system — version checking, download, and atomic update installation
| `strings.py` | 6,491 bytes | String utilities — truncation, sanitization, template rendering, and matching
| `timed_input.py` | 301 bytes | Timed input prompt for interactive terminal sessions with timeout
| `update_check.py` | 598 bytes | Update availability check against the Agent Zero release channel
| `wait.py` | 2,092 bytes | Wait/sleep utilities with configurable duration and cancellation support
| `yaml.py` | 516 bytes | YAML loading and saving with safe parser defaults
