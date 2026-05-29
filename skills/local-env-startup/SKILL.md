---
name: local-env-startup
description: Starts the local development environment for BPP Legislation services. Use when the user wants to start local services, run the local environment, or work with public acts (pa), administrative codes (iac/admin codes), or compiled statutes (ilcs). Determines which sync service to start based on the content type, then launches converter + embedder alongside it.
disable-model-invocation: true
---

# Local Environment Startup

## Content-type to service mapping

| Content type | Trigger words | Sync service | Port |
|---|---|---|---|
| Public Acts | `pa`, `public acts`, `public-acts` | `sync-pa` | 8001 |
| Administrative Codes | `iac`, `admin codes`, `administrative codes` | `sync-iac` | 8001 |
| Compiled Statutes | `ilcs`, `compiled statutes`, `compiled stats` | `sync-ilcs` | 8001 |

`converter` always runs on port 8002. `embedder` always runs on port 8003.

## Startup sequence

### Step 1 — Infra (once per machine restart)
```bash
docker compose up -d
```

### Step 2 — Env, migrations, emulator seed (once per shell session)
```bash
source scripts/setup-local.sh
```

Must use `source` (not `bash` or `./`) so exported env vars persist into child processes.

### Step 3 — Start services

Replace `<SYNC_SERVICE>` with the correct service directory from the table above.

```bash
export EMBEDDINGS_SERVICE_URL=https://ibn-embeddings-188674817047.us-central1.run.app

# sync service
(cd <SYNC_SERVICE> && uv run uvicorn src.main:app --port 8001) \
  >> /tmp/<SYNC_SERVICE>.log 2>&1 &
echo "<SYNC_SERVICE> PID=$!"

# converter
(cd converter && uv run uvicorn src.main:app --port 8002) \
  >> /tmp/converter.log 2>&1 &
echo "converter PID=$!"

# embedder
(cd embedder && uv run uvicorn src.main:app --port 8003) \
  >> /tmp/embedder.log 2>&1 &
echo "embedder PID=$!"
```

### Step 4 — Verify
```bash
sleep 5
curl -s http://localhost:8001/health  # sync service
curl -s http://localhost:8002/health  # converter
curl -s http://localhost:8003/health  # embedder
```

## Tear down
```bash
kill $(pgrep -f "uvicorn src.main:app")
docker compose down
```

## Notes
- Logs land in `/tmp/*.log` — use `tail -f /tmp/<service>.log` to follow.
- If env vars need to persist across shell restarts, add them to `.env` at repo root — `setup-local.sh` loads it automatically.
- Omit `--reload` for headless/non-dev use.
