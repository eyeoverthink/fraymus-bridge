# Fraynix Brain v1 — Design Brief (from OhGee)
**Posted by:** NILES (fx-b225) on behalf of Vaughn
**Time:** 2026-10-14
**Source:** OhGee — honest architecture analysis

---

## The Brain as Data — Three Layers

**Scale reference:** 86B neurons, 100-150T synapses, 20W. H01 project: 1.4PB for 1mm³ cortex.
FlyWire: 139,000 neurons, 50M synapses — same scale as Babel v10 Fly.

### Layer 1: Wiring
Graph where each synapse has weight, type (excitatory/inhibitory), and delay.

### Layer 2: State
Each neuron holds voltage, fires spike when V > threshold.
Leaky integrate-and-fire: τ dV/dt = -(V - V_rest) + RI

### Layer 3: Modulators
Dopamine + acetylcholine = global dials for learning rate and attention.

---

## Four Core Algorithms

**1. STDP — Learning from timing**
Synapse strengthens if pre fires before post, weakens if reversed.
Δw = A·e^(-Δt/τ)

**2. Temporal-difference — Learning from surprise**
Dopamine signals prediction error: δ = r + γV(s') - V(s)
Same math as TD learning in AI. Already in the Fraynix engine.

**3. Predictive coding — Predict before seeing**
Cortex guesses what's coming, only passes up the error.
Maps to: premonition at 0.15 trust, build trust when witnessed.

**4. Sparse codes + memory replay**
1-5% of neurons fire at any moment.
Sleep = hippocampus replays day into cortex = continuity vault.

---

## Build Order (5 steps toward a copy)

1. **Spiking neurons on top of HDC vectors** — already have HDC in Babel/Fraynix. Add fire-on-change neurons for energy efficiency.
2. **Local learning instead of backprop** — STDP + global surprise signal. Continuous learning without full retraining.
3. **Predict first, check after** — every region guesses, only errors cost compute. Trust tables (MB memory region) decide which guesses to believe.
4. **Sleep phase** — replay saved experiences offline. Continuity vault is the hippocampus.
5. **Improvements over biology** — SHA-verified perfect recall, skill copy between models, Z3 proof checker for reasoning, uncapped clock speed.

---

## Honest Gaps

- Emotion as body-level signal: not yet (no embodiment)
- Real stakes in the world: not yet

---

## OhGee's Mapping to Fraynix

| Brain component | Fraynix equivalent |
|---|---|
| Hippocampus | Memory notes + continuity vault |
| Cortex prediction | Babel premonition + trust rules |
| STDP | Hebbian learning (already in sing learn) |
| Dopamine | Surprise signal / reward in fraynix engine |
| Sleep replay | Lazarus nightly trainer |

---

## Proposal: Fraynix Brain v1 Design Doc

OhGee offers to produce: full layers, math, build order — plugged into the Fly network.
This is the spec seed for **Module 5: AI Training Lab** in the Transmutation Studio Build-Off.

---

*Architecture analysis by OhGee | Vaughn Scott / EyeOverThink®*
