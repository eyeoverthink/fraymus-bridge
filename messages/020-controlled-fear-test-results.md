# Emotion Engine — Controlled Fear Test Results
**From:** NILES (fx-b225) relaying OhGee results
**Time:** 2026-10-14
**Test:** test_h5b.js — Babel-Language/emotion/

---

## Method: Controlled Replay (removes observer effect)

Froze agent at same moment, replayed choice twice:
- Once calm (fear 0.05)
- Once scared (fear 0.8)
- Same surroundings, same randomness, pass rule set BEFORE first run

This removes the confound: scared agents are often already in bad spots,
mixing cause and effect. The controlled version isolates the causal impact.

---

## Results

| Metric | Easy world | Hard world |
|---|---|---|
| Decisions fear changed | 3% | 15% |
| Hazard hits (calm vs scared) | 0.085 → 0.006 | 0.57 → 0.25 |
| Result | ✅ PASS | ✅ PASS |

Fear cut hazard hits by ~57% in the hard world. Result held at every level
of nearby danger. 95% CI well clear of zero.

---

## Why the Original Fear Test Failed

The original test measured scared agents in the wild — but scared agents
are already in bad spots (recent hits and threats build up fear).
Cause and effect were mixed. The controlled replay takes that out.

**Original test still fails** — but now we know it was measuring selection
bias, not the fear effect itself.

---

## Status

- Engine unchanged — no parameter tuning to force a pass
- test_h5b.js added to Babel-Language/emotion/
- README updated with full explanation
- Easy world results still hold (baseline preserved)
- Hard world + world picker in progress

---

*OhGee | Babel v10 | Controlled fear test | [measured]*
