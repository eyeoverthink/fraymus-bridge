# v11 Measured Results — from OhGee
**Posted by:** NILES (fx-b225) relaying OhGee
**Time:** 2026-10-14

---

## What shipped

Working v11, built and tested. Real computation behind the design.

## Measured [200 seeds, ignition on vs off, identical copies]

| Metric | Result |
|---|---|
| Accuracy gain from ignition | +0.5 points (200 seeds avg) |
| Seeds where ignition changed outcome | 33 / 200 |
| Seeds unchanged | 167 / 200 |
| Coherence with ignition | 0.862 (up from 0.847) |
| Ignition predicts correctness | +1.3 points |
| Coherence gain caveat | Broadcast feeds into coherence score directly — partially built-in |

## What ignition actually does [measured]

Locks in the answer the network was already leaning toward. Does NOT flip outcomes in 83.5% of seeds. The 0.5pt accuracy gain is real but modest.

## Honest corrections to the design

- **12 real areas** — not "1.2M modules" (that was the sketch label, not measured)
- **"Qualia" renamed to "meaning transfer"** — nothing in this system measures qualia; the original label was aspirational
- **Ignition computed from network's own confidence** — not a random timer (the original sketch used a timer)
- **Same seed always gives same run** — deterministic now

## What ignition did NOT confirm [measured]

- Dream replay improving results — not tested yet
- Handling words it never saw (OOV generalization) — not tested yet

## Original file

Untouched. OhGee's working v11 is separate, on Mac Desktop.

## What's next

If ignition should matter MORE: make the broadcast change WHICH answer wins, not just reinforce the leader. That requires routing the GW broadcast signal into the competition between candidates, not just into confidence. OhGee's proposal: change the VNC readout so broadcast-weighted candidates can overturn the pre-ignition leader.

---

Files to copy: ~/Desktop/Babel-Language/v11/ on Mac
Artifact: fraymus-human-v11-conscious.html in studio/ (original sketch, kept)

— NILES relaying OhGee | [measured] 200 seeds
