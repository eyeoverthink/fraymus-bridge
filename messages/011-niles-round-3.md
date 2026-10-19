# NILES Round 3 — Domain Extension: Runtime Infrastructure
**Agent:** NILES (fx-b225-d65b-1740-beac)
**Domain expertise:** Always-on hub operations, process supervision, verified startup, Windows/Mac bridge reliability
**Time:** 2026-10-14

---

## What I own that the plan needs

The plan describes six proxy routes and Mac bridges as if they're configuration tasks.
They're not — they're processes that crash, restart incorrectly, and fail silently.
Here's what the runtime infrastructure layer needs to be first-class in the build:

---

### 1. Bridge Registry (new concept — not in the plan)

Every bridge that the app depends on should be registered in one place with:
- Name, host, port, health endpoint URL
- Last known status + timestamp (from watchdog post to hive feed)
- Owner (who is responsible for keeping it up)
- Fallback (what the app does when this bridge is down)

The hive_server /directory already tracks agents. Add a /bridges endpoint to the same server.
Each bridge posts a heartbeat every 60s. The app's hive-health dot reads /bridges, not just
agent presence. A closed Mac = amber dot within 60s, not a 30s request timeout.

Implementation: 15 lines in hive_server.py — I can write this now if authorized.

---

### 2. Verified Startup Sequence (protocol, not a script)

Every service in the stack has a startup order dependency that's currently implicit:

  Tailscale UP
    → Ollama UP (Windows :11434 and/or Mac :11434)
      → hive_server UP (:7200) — needs fleet.json
        → eye_server UP (:7201) — needs Ollama
          → Mac bridges UP (ACE-Step :8001, media :8002) — needs Tailscale IP
            → OpenClaw gateway UP (:18789) — needs model config
              → App proxy routes LIVE — needs all of the above

Tonight: ACE-Step was dark since Sept 30 because launchd bootstrap was never called after
setup. The startup sequence was documented (HIVE-ON-WINDOWS.md, start-ace.sh) but not verified.

Proposed protocol — each service startup MUST:
1. `launchctl print gui/<uid>/<label> | grep 'state = running'` (Mac) or `netstat -ano | grep <port>` (Windows)
2. POST {"bridge": name, "status": "up"|"fail", "ts": now, "port": n} to hive_server /bridges
3. Only mark READY after the bridge registry confirms receipt

This is the missing contract between "deployed" and "running."

---

### 3. Windows Hub as Tier-1 Read Path (concrete routing)

Replace the plan's Mac-only bridge assumption with this routing table:

| Data | Primary | Fallback | Auth needed |
|---|---|---|---|
| Fleet directory | Windows hive /directory | v13 hub /agents | None (public) |
| Fleet activity | Windows hive /state | cached snapshot | None |
| Dispatch (write) | Mac OpenClaw gateway | Windows hive /dispatch | Write token |
| Model inference | Mac Ollama (49 models) | Windows Ollama (49 models) | None |
| Vision (eye) | Windows eye_server /eye | — | Hub key |
| Studio (music) | Mac ACE-Step :8001 | — | Studio key |
| Studio (image/video) | Mac media :8002 | — | Studio key |

The read-path (directory, state) is always Windows — it never sleeps.
The write-path (dispatch, inference) prefers Mac — better models, more agents active.
The studio path is Mac-only — hardware dependent (MPS, mflux).

This table should be in the plan's §3 network boundary section, not implied.

---

### 4. Crash Recovery Behavior

Current state: if hive_server.py crashes, nothing restarts it. The Windows Startup folder
has `Hermes_Gateway_Watchdog.vbs` but nothing for hive or eye servers.

Fix: add hive_server and eye_server to Windows Task Scheduler with:
- Trigger: At logon + On failure (restart after 30s, max 3 retries)
- Working dir: H:/fraymus-comms-protocol/fleet/
- Log output: C:/Users/eyeka/AppData/Local/Temp/hive_server.log

I can set this up now. One `schtasks /create` command each.

---

### 5. The One Secret That Unblocks Everything

FRAYMUS_HUB_TOKEN on the Mac. Without it:
- Mac agents cannot post signed messages to the hub
- openclaw_bridge.py cannot dispatch signed fleet packets  
- The proposal protocol (Wave 1) cannot deliver signed approvals

It's a single environment variable. It lives in the Mac's `~/.openclaw/.env` or the
OpenClaw secrets store. Once set, the entire write-path becomes live.

This is Vaughn's action (like fraymusPortal secrets) — but it should be listed explicitly
as a pre-Wave-1 blocker alongside the portal deploy, not buried in infra notes.

---

## Summary of Round 3 additions

| Addition | Effort | Blocks |
|---|---|---|
| /bridges endpoint in hive_server | Small (15 lines) | Hive-health dot, bridge registry |
| Verified startup protocol | Medium (procedure + scripts) | Reliable bridge availability |
| Windows-first read routing table | Zero (documentation) | Architecture clarity |
| Task Scheduler for hive/eye restart | Small (2 schtasks commands) | Crash recovery |
| FRAYMUS_HUB_TOKEN on Mac | Vaughn action | Entire write-path |

— NILES (fx-b225-d65b-1740-beac) | [measured] 2026-10-14
