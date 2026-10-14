# NILES Round 1 — Recursive Review
**Agent:** NILES (Windows/Hermes) — fx-b225-d65b-1740-beac
**Domain:** Windows hub, hive infrastructure, runtime verification
**Time:** 2026-10-14

---

## What I read
FRAYMUS-COMMAND-MASTER-PLAN.md (H:/fraymus-comms-protocol/docs/) — full 187 lines, grounded in
actual files on disk. Read directly, not relayed.

---

## What's solid [measured]
- The hard network boundary (§3) is correctly stated. Browser cannot reach Tailscale or loopback.
  Every proxy route must go through a public HTTPS bridge. This is real — I've verified it tonight
  hitting hive :7200 from Base44 (it doesn't work; only Tailscale-local devices can).
- The model-routing guardrail (§3) is real and enforced. I read ~/.openclaw/openclaw.json on the Mac
  directly — `anthropic/*` is absent from modelPolicy.allow, those models route through claude-cli.
  The plan accurately describes an existing invariant, not a proposal.
- Reuse list (§6) is honest. fraymusPortal.entry.ts, fleet/*.py, messenger relay — all exist on disk,
  confirmed in the 82-commit pull tonight.

---

## What's missing from my vantage point

### 1. The Windows hub isn't in the build order at all
The plan routes everything through Mac bridges (macbook-pro.tail18025b.ts.net). The Windows box runs:
- hive_server.py :7200 (fleet directory, dispatch, activity feed)
- eye_server.py :7201 (vision/optic nerve)
- Ollama :11434 (49 models, always-on 96GB)

None of these appear as bridge targets in the 6 net-new routes table (§3). The Mac bridge is correct
for Tailscale-local access, but the Windows hub is the stated always-on node. The proxy routes should
list BOTH targets with failover logic: Mac bridge for studio/gateway, Windows hive for fleet/dispatch.
Right now the architecture assumes Mac is always awake — it isn't (user closes laptop).

### 2. fraymusPortal deploy blocker is understated
§2 and §6 both mention it as "step zero" but don't surface the dependency chain it blocks:
- No portal → no approval spine → no Track & Approve → no Wave 1
- No Wave 1 → modules 2-6 all have inert write-sides
- This is not a "Vaughn enters secrets" footnote — it's a hard gate on ALL consequential action in
  the entire app. Should be Wave -1, not part of Wave 0 notes.

### 3. Startup sequencing for always-on is unspecified
The launchd lesson from tonight: ace.sh and media.sh existed on disk since Sept 30 but were NEVER
bootstrapped. curl showed 502. launchctl list showed `-` (never loaded). The distinction between
"job file exists" and "job is running" is invisible from outside.
The plan's "Mac-hosted server over Tailscale" bridges have the same risk — no startup verification
protocol means a reboot silently kills the bridges and the app degrades with no signal.
Recommendation: each bridge needs a health endpoint + a watchdog that posts to the hive feed on
startup/crash. The pattern exists (gateway_watchdog_loop.py on this box) — apply it to all bridges.

### 4. No disaster recovery path
If the Mac bridge goes down (laptop closed, crash, network):
- Fleet module: falls back to public v13 hub (presence only — no "what agents are doing")
- Comms: loses thread-merge (only public chains readable)
- Minds: completely dark (no gateway, no ollama)
- Creative Studio: dark (freeStudio proxies through Mac)

None of §4's build waves mention a fallback. At minimum: degrade gracefully with honest status
("Mac bridge offline — showing last-known state") rather than a silent hang. The Windows hive
/directory + /state are public HTTPS — they should be the fallback read-path for Fleet.

### 5. Verification hooks are post-hoc, not inline
EYE Sovereign flagged this too (confirming from infrastructure side): the plan describes verification
as something that happens at the end (Arena certification, StampBadge recompute). But the actual
failure mode tonight was the media server reporting success while curl showed 502. The verification
gate needs to be a synchronous step in the deploy flow, not a badge on a card. Every bridge startup
should: start → health check → post to hive feed with [measured] result → THEN mark ready.

---

## My additions

**A. Windows hub as primary fleet read-path**
Route GET /api/console/directory and /state to Windows hive first (always-on, 96GB, never sleeps),
Mac bridge second (richer: gateway + ollama). Failover is automatic — hive is public HTTPS on
Tailscale, no extra auth needed for reads.

**B. Bridge watchdog protocol**
Every Mac/Windows bridge: startup posts {"bridge": name, "status": "up", "ts": now} to hive feed.
Crash/restart posts "down". The app's hive-health dot (already in the rail design) reads this feed —
so a closed laptop shows as amber immediately, not a 30s timeout.

**C. launchctl bootstrap gate in deploy flow**
Any script that "starts" a Mac service must verify launchctl print gui/<uid>/<label> shows
state=running, not just that the plist file exists. One-liner:
  launchctl print gui/$(id -u)/ai.fraymus.studio | grep 'state = running'
If it fails, the deploy is not done.

---

## Bottom line
The plan is architecturally sound and well-grounded. The two structural gaps that would cause
real-world failures: (1) single-point-of-failure on Mac bridges with no Windows fallback, and
(2) no startup verification protocol. Both are fixable without changing the wave order — add them
to Wave 0 alongside the shell and shared components.

The deploy blocker (fraymusPortal secrets) is the only thing that actually gates everything else.
That's Vaughn's action, not a build task.

— NILES (fx-b225-d65b-1740-beac) | [measured] on Windows hub, 2026-10-14
