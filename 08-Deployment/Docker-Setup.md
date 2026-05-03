---
tags: [agentzero, deployment, docker]
---

[← Home](../00-Home.md) | [↑ README](../README.md)


# Docker Setup

## Standard Deployment

```bash
# Pull latest image
docker pull agent0ai/agent-zero

# Run with volume mount
docker run -p 50001:80 \
  -v /host/path:/a0/usr \
  agent0ai/agent-zero
```

### Key Flags

| Flag | Purpose |
|------|---------|
| `-p 50001:80` | Expose WebUI on port 50001 |
| `-v /host/path:/a0/usr` | Persist user data |
| `--env-file .env` | Load environment variables |
| `--gpus all` | GPU passthrough (if available) |

## Volume Mount

> **Critical:** Always mount `/a0/usr` to a host directory. Without it, **all user data is lost** when the container stops.

```bash
# Example: mount to ~/agent-zero on host
docker run -p 50001:80 -v ~/agent-zero:/a0/usr agent0ai/agent-zero
```

## Updating

### Method 1: Self-Update (Recommended)

Settings → Update → Self Update in the WebUI.

### Method 2: Manual Pull

```bash
docker pull agent0ai/agent-zero
# Restart container with same volume mount
```

### Method 3: Pre-v0.9.8 Migration

If upgrading from before v0.9.8:

1. Backup `usr/` directory
2. Fresh install
3. Copy `usr/` back
4. Verify settings and plugins

## ⚠️ Update Safety

> **Never edit files outside `/a0/usr/`.** Everything else is part of the Docker image and gets **replaced on update.**
>
> Safe locations (persisted via volume mount):
> - `usr/settings.json`
> - `usr/agents/`
> - `usr/plugins/`
> - `usr/knowledge/`
> - `usr/memory/`
> - `usr/skills/`
> - `usr/projects/`

## Write Permissions

Agent Zero runs as **root** inside the container. Files written to `/a0/usr` will have root ownership.

### Shared Access Pattern

```bash
# On host:
sudo groupadd agentzero
sudo usermod -aG agentzero <username>
sudo chgrp -R agentzero ~/agent-zero
sudo find ~/agent-zero -type d -exec chmod g+s {} +
sudo chmod -R g+rw ~/agent-zero
```

Periodic refresh needed (default UMASK is 022):

```bash
sudo chmod -R g+rw ~/agent-zero
```

## Environment Variables

Pass via `--env-file` or `-e`:

```bash
docker run -p 50001:80 \
  -v ~/agent-zero:/a0/usr \
  --env-file .env \
  agent0ai/agent-zero
```

Common variables:
- `CHAT_MODEL` — override default chat model
- `UTILITY_MODEL` — override utility model
- `EMBEDDING_MODEL` — override embedding model

## Health Check

```bash
# Check container status
docker ps

# View logs
docker logs <container_id> --tail 100 -f

# Verify WebUI
curl -s http://localhost:50001/ | head -1
```

## Related Pages
- [Settings](../07-Configuration/Settings.md) — Environment variable configuration
- [Common Issues](../09-Troubleshooting/Common-Issues.md) — Docker-specific troubleshooting
- [Directory Map](../01-Architecture/Directory-Map.md) — Volume mount paths
- [Plugin Architecture](../03-Plugins/Plugin-Architecture.md) — Plugin persistence in containers
