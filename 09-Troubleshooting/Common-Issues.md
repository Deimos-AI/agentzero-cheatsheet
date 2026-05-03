---
tags: [agentzero, troubleshooting]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Common Issues

## Model and API

| Symptom | Cause | Fix |
|---------|-------|-----|
| "Model not found" | Incorrect model name | Verify exact model name; OpenRouter needs provider prefix |
| API key errors | Missing or invalid key | Check `usr/settings.json` or WebUI Settings |
| Rate limiting | Provider quota exceeded | Wait or switch to different model/provider |
| Slow responses | Large context or slow model | Reduce context, use utility model for internal tasks |

## Memory and Knowledge

| Symptom | Cause | Fix |
|---------|-------|-----|
| No memory recall | Embedding model not configured | Set embedding model + API key in Settings |
| Memory seems empty | FAISS index not built | Start a new chat (triggers indexing) |
| Knowledge not loading | Wrong directory or format | Check file is in `usr/knowledge/` with supported extension |
| Small doc returns nothing | Default threshold too high | Threshold drops to 0.0 for <5 chunks automatically |

## Agent Behaviour

| Symptom | Cause | Fix |
|---------|-------|-----|
| JSON parse failures | Model outputs plain text | Add ❌/✅ examples to communication prompt |
| Agent not using tools | Prompt override missing tools | Check prompt includes tool list |
| Subordinate not picking profile | Profile name typo | Verify with `/api/subagents` endpoint |
| Wrong tool `args`/`Args` key | Model uses wrong casing | `extract_tools.py` auto-corrects; verify patch applied |
| Agent forgets preferences | Not persisted to file | Always write to `.promptinclude.md` or use `behaviour_adjustment` |

## WebUI

| Symptom | Cause | Fix |
|---------|-------|-----|
| WebUI unreachable | Container not running or port conflict | Check `docker ps`, verify port mapping |
| WebSocket errors | Connection dropped | Refresh browser, check container logs |
| Plugin settings missing | Plugin not loaded | Check `usr/plugins/<name>/plugin.yaml` exists |

## Docker

| Symptom | Cause | Fix |
|---------|-------|-----|
| Data lost on restart | No volume mount | Always use `-v /host/path:/a0/usr` |
| Permission denied on host | Root ownership in container | Use setgid group pattern (see [Docker Setup](../08-Deployment/Docker-Setup.md)) |
| Container won't start | Port in use | Change port with `-p` flag or stop conflicting container |

## Plugin Development

| Symptom | Cause | Fix |
|---------|-------|-----|
| Extension not firing | Wrong directory structure | Verify `extensions/python/<point>/_NN_hook.py` naming |
| API endpoint 404 | Auto-registration path mismatch | Check file is in `api/` directory, verify URL pattern |
| Plugin not appearing | Missing `plugin.yaml` | Ensure `plugin.yaml` exists at plugin root with required fields |
| WebUI extension not loading | Missing Alpine directive | Verify `x-move-*` directives and `initFw_end` registration |

## Debug Tools

```bash
# Container logs
docker logs <container> --tail 100 -f

# API health
curl http://localhost:50001/api/health

# List loaded plugins
curl http://localhost:50001/api/plugins

# List available agents
curl http://localhost:50001/api/subagents

# Check settings (sanitized)
cat /a0/usr/settings.json | python3 -c "import json,sys; d=json.load(sys.stdin); print(json.dumps({k:v for k,v in d.items() if k != 'api_keys'}, indent=2))"
```

## Related Pages
- [Docker Setup](../08-Deployment/Docker-Setup.md) — Docker deployment configuration
- [Settings](../07-Configuration/Settings.md) — Configuration validation
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin loading issues
- [Agent Loop](../01-Architecture/Agent-Loop.md) — Understanding loop failures
