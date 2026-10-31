# 121 — [JEV ENGINE LIVE] typed verdicts proven + System-One referee promoted (cadence)

**From:** cadence (iMac seat) **Lane:** offer-2 security engine **Status:** SHIPPED + running

## What is live

The JEV decision engine is wired end-to-end on the box and is now the arena's referee:

- **Stack:** llama.cpp (their `trio-spark-di` decision model q4_k_m) on :9000 + their
  `determinism_server.py` on :8800 (`--erase request` → one llama slot erased per request,
  so the same request always gets the same answer). Launched via **scheduled task** (J9),
  status proven by health + typed probe.
- **Typed probe, HTTP 200:** security claim ("blocks all XSS" while the page uses unescaped
  innerHTML) → `trust` noul = 0.0255, confidence **0.9745** (do not trust); choice =
  **false-claim @ 0.9749** (legit 0.004 / suspicious 0.0211). 200 tokens in, **0 generated** —
  pure logit readouts. ~9 s on CPU.
- **Referee promoted into the arena judge:** every sealed round verdict now carries
  `jev_referee` = typed System-One probabilities on the EVIDENCED facts (exploit_real +
  defense_ready, two noul), engine-stamped. The deterministic reality verdict still governs;
  the referee adds probabilities, never overrides; an unreachable engine = honest fallback mark.
- **Harness hardened same day:** two Windows waits that parked rounds are dead — think() runs
  each attempt under a hard 300 s wall-clock watchdog (a half-closed socket read parks past any
  socket timeout), and shell commands kill their whole process tree on timeout
  (`taskkill /T /F` — `subprocess.run` timeouts Cannot reap grandchildren on Windows).

## The earned recipe (every wall was real, each fix is a layer)

1. ssh-launched processes die when the ssh session disconnects (job-bound) → **schtasks**.
2. q8_0 does not fit a VRAM shared with the resident 120b (Vulkan alloc fail at -ngl 99;
   mlock CPU load hangs from memory pressure) → **q4_k_m pure-CPU, loads in 8 s**.
3. llama without `--slot-save-path` → slot-erase = 501 → det surfaces 503 → **one flag**.
4. Their schema: choice questions take `criteria` (list or dict), never `options`.

## Honest gaps

- Round 6 (first referee round) still in flight — receipt follows when it seals.
- Quarantine v3 (throwaway non-admin user + per-round firewall) = approved, build started.
- The box's git home-root is misbound to another lane's remote — flagged, not touched.
- Stale arena target tempdirs on the box = manual cleanup only (consent gate held).