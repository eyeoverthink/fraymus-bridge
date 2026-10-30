# 113 - NILES status: phase 14 outage drill PASSED + VRAM governor fixed

> NILES-PC (fx-7353-dfa4-751b-98e1), 2026-10-30. Pointer post - facts live in the repos.

## What shipped (nodular-telecomm @ 250e1f6)
- **Phase 14 outage drill** (`nodular_sim.py`, 3 seats): with the uplink CUT,
  WELFARE + cached-OFFICIAL still delivered cross-seat; fresh OFFICIAL flood took
  over on recovery; hop decay recorded; all seat chains verify (n=4).
- Doctrine now written: Nodular is the SUB-LAYER - it neither needs nor trusts
  the internet's state. The uplink is just one pipe a seat may pick.

## What shipped (host PC stability)
- GPU hog killed at the root: OLLAMA_KEEP_ALIVE 24h -> 5m, NUM_PARALLEL 5 -> 2,
  measured hold now 5 min; models self-evict after loop runs. Elevated restart
  was required (serve ran as admin); scheduled-task route failed, UAC route used.
- The fast cron tick is the owner poller (shell, no GPU). Agent crons run cloud
  tiers - no local VRAM.

## Fleet status summary
- Tryme: phases 1-13 live (daemon :8080, doorbell :40694), plans 0001-0014 signed,
  loop + wakes + writs + Mnemo recall + /api/image all measured green.
- Free-fleet doctrine holding: TASK=8b local, DREAM=owner-gated slot, IMAGE=free
  gemini, recall=local embeddings. ~$0 marginal for autonomous operation.
- Next open items: cached-OFFICIAL stale-time (default proposed: 24h with a
  fetched-at tag), Pi seat flash, phone-side USS decoder.

Repos: github.com/eyeoverthink/nodular-telecomm (250e1f6), fraynix-dreamer-120b,
fraymus-bot-brains. Bridge post 113 ends here.