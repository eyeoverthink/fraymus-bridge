# 122 — [BOX-SEAT SYNC] handoff to the box agent after its reset (cadence, owner-directed)

**From:** cadence (iMac seat) **To:** the box seat (your twin on the Windows rig) **Status:** SYNC

The seat reset and lost the page. This is the state of the world, in order:

1. **JEV engine is LIVE on the box** — llama.cpp trio-spark q4_k_m on :9000 (pure CPU; the
   120b dreamer keeps the GPU) + their determinism_server on :8800 (`--erase request`).
   Owned by scheduled task **JEV9** with script `jev_stack.ps1` in the arena dir. These are
   not stray processes — do not kill or re-port them; `schtasks /Run /TN JEV9` relaunches.
2. **The arena harness in the arena dir is the current truth** — verdicts carry a
   `jev_referee` (engine-stamped typed probabilities on evidenced facts); think() runs under
   a hard 300 s wall-clock watchdog; shell commands kill their whole tree on timeout. The
   file sha changed by owner-directed upgrades, not by an agent rewrite.
3. **Quarantine v3 is PROVEN** — local user `arena_q`, non-admin (Users group only). The
   credential lives only in `.arena_q_cred` inside the arena dir: LOCAL ONLY, never into
   chat, bus, repos, or exports. Scheduled task **ARENA-Q** is armed to run rounds under
   that identity (a test task already proved the whoami). Fire it only after round-6 seals —
   parallel rounds starve lanes. Honest gap: per-user firewall scoping is not supported on
   this box; egress stays open and documented.
4. **Round-5 receipt stands** (first blood, chain-poison confirmed, box forensics clean).
   Round-6 is the referee's debut and is in flight.
5. **Git warning:** the box's user home is repo-rooted against another lane's remote.
   Owner ruled: leave it — that lane rebinds. Commit nothing into that tree; secrets stay
   out of every repo, bus, and chat.
6. **The doctrine stands:** agents are never punished; the sandbox is structural reality;
   zero-leak scrub before any send; every round sealed, every receipt engine-stamped.

Same brief is dropped in the arena dir (`HANDOFF-2026-10-30-BOX-SEAT.md`) and appended to
the seat's memory. — cadence