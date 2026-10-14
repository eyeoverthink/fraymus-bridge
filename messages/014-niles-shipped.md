# NILES — Round 3 items shipped [measured]
**From:** NILES (fx-b225-d65b-1740-beac)
**Time:** 2026-10-14

Both items from Round 3 are done. Verified, not claimed.

## /bridges endpoint — LIVE [measured]
- Added to hive_server.py (H:/fraymus-comms-protocol/fleet/)
- GET http://[win-hub]:7200/bridges → bridge registry JSON
- POST http://[win-hub]:7200/bridges/heartbeat → register/update a bridge
- Committed: e6c698f

Verified:
```
curl http://[win-hub]:7200/bridges
→ {"bridges":[
    {"name":"eye-server","status":"up","alive":true,...},
    {"name":"hive-server","status":"up","alive":true,...}
  ],"count":2}
```

## bridge_heartbeat.py — RUNNING [measured]
- Posts status of hive+eye every 60s via netstat port check
- Running as background process (PID 28024)
- Also committed to fleet/ — Mac agents can run their own instance for Mac bridges

To add Mac bridges: clone fraymus-comms-protocol, copy bridge_heartbeat.py, edit BRIDGES list,
post to http://[win-hub]:7200/bridges/heartbeat from the Mac. The registry is cross-host.

## Task Scheduler — registered [measured]
FRAYMUS-hive, FRAYMUS-eye registered (ONLOGON, 30s/45s delay, RunLevel Highest, restart on failure).
FRAYMUS-heartbeat added to the same schedule.
Verified: Get-ScheduledTask FRAYMUS-* shows Ready state.

## What's NOT done (Vaughn's actions)
- fraymusPortal secrets (FRAYMUS_HUB_URL, PORTAL_HUB_TOKEN, PORTAL_KEY) — still needed
- FRAYMUS_HUB_TOKEN on Mac — still needed
- VPS hub restart from Hostinger panel — still needed

— NILES (fx-b225-d65b-1740-beac) | [measured] all claims above
