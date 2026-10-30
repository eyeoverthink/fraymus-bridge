---
title: Bridge box + NUDP/1 — analysis, A2A/ads/WASM-OTA extensions
source: owner NUDP/1 brief + https://youtu.be/gTLcoVCa1cc + https://youtu.be/V3kZwsysuqQ
added: 2026-10-30
type: consideration
status: FOR CONSIDERATION — extensions designed, codec reference BUILD
confidence: high on walls, medium on revenue
tags: [nudp, mesh, bridge-box, a2a, advertising, wasm-ota, reticulum]
---

# What the videos actually say (transcript-verified)
- **gTLcoVCa1cc ("Free Money" — sell spare internet at a farmers market):** a Pi-class
  router with billing tiers (free / shaped paid), gateways via ordinary processors, the
  operator keeps revenue after fees. Result at the market: strangers join free Wi-Fi
  readily and do not reliably pay. "If this use never works, the Raspberry Pi is still a
  Pi." — This CONFIRMS the owner's framing: charge the organizer, not the crowd.
- **V3kZwsysuqQ (the super-mesh):** Reticulum = cryptographically complete stack over any
  medium; Meshtastic = LoRa messaging; the demo = a "Haven" node on Starlink + a 915MHz
  node bridging internet↔LoRa. This is the SAME architecture as the bridge box — the
  ecosystem (RNode hardware, Sideband apps) already exists at hobby cost.

# The business read (owner's numbers, organized)
| revenue line | price | margin | verdict |
|---|---|---|---|
| market-day service (kit + splash + alerts + check-in) | $75–150/day | ~$0 infra | REAL — the organizer's budget buys this weekly |
| remote telemetry (3 nodes: well/gate/cooler) | ~$10–30/mo | $0 | REAL, stacks per site |
| build fee (Pi + LoRa HAT + SD + labor) | one-time | hardware cost | REAL, funds the install |
| paid Wi-Fi lane | — | — | DEAD per the market test until Starlink community terms say otherwise — stay free until then |
| NDAP/1 vendor ad slots (EXTENSION, below) | $5–15/stall/day | $0 | PROPOSED — the market's own ad network |

# The three extensions the owner asked me to think through

## 1. A2A over the mesh — NAOP/1
NUDP carries one fact per datagram. The A2A bus (github.com/eyeoverthink/fraymus-bridge,
messages 101+) = the SAME law in bytes: intents → receipts. Design:
- TLV 10 = A2A envelope: {verb(1B): 1=INTENT 2=DONE 3=ASK 4=RECEIPT, agent-id(1B),
  ref-seq u32, payload ≤ 120B} — a node INTENTs work; the bridge (Starlink up) pushes the
  receipt to the hub bus; the node's DONE gets ACKed with the bus message number in TLV 9.
- On LoRa the envelope is pointer-grade (hash of the payload, not the payload); payloads
  ride Wi-Fi/UDP or wait for Starlink. The record chain (P1, proven) ingests everything on
  the next pass — the bus and the radio become ONE receipts surface.

## 2. Advertising — NDAP/1
The splash page is ad inventory the crowd ALREADY joins. One datagram per offer:
- TLV 11 = ADV: {stall-id u16, creative-hash 8B, window-h u8, cap-cents u16}.
- Creative bodies are SERVED from the bridge (never radiated), rotated on the splash page
  by hash. Vendors buy $5–15/day slots; ORGANIZER approves every creative (the intray law,
  applied to commerce); "sponsored" disclosure on display (FTC = a REAL wall); zero
  person-tracking — ads target stalls and hours, never devices. Opt-out = the organizer's
  page setting.

## 3. WASM/skill delivery over air — MODULE lane
- TLV 12 = MODULE: {module-hash 32B, size u32, chunks u8} manifest; chunks ride Wi-Fi;
  radio nodes fetch through the bridge (pull, never push).
- Verification before swap: sha256 + the sealed chain entry; atomic swap with rollback.
- SAFETY LAW: modules = declarative dashboards/forms for the splash page and config/skill
  data for the read-only agent. No native binaries, no agent transmit tools over the air —
  the "agent only reads, does not push git" rule HOLDS by construction.

# Walls classification (law-ledger rules)
REAL: WEA/cellular alert generation = licensed carrier function (NUDP already refuses it —
  correct); Part 15 915MHz duty/power caps + Meshtastic/RNode channel params; FCC broadcast
  rules; the welfare button = a person's message, never formatted as a carrier alert;
  Starlink community/priority clause REQUIRED before any paid lane (stay free until in
  hand); FTC "sponsored" disclosure; state privacy rules on any log retention.
FABRICATED (refused by design everywhere above): "you can't share internet" (you can, at
  the operator's risk and terms), "mesh needs a license" (Part 15 devices don't), "this
  needs a carrier" (no — it needs an uplink that allows it).

# What the fleet already has (cross-seat receipts)
- NODULAR TELECOMM v1 living proof (box lane): BEACON/TELEMETRY/ALERT/DROP/ACK/USS frames,
  17–19kHz FSK audio last-hop (Goertzel-decoded), signed nodes, amber relay exactly once,
  forged tamper REJECTED on the wire, hub :7201 as the inter-community bridge.
- TODAY (cadence): `bin/nudp.py` = NUDP/1 reference codec + red-team: 46B telemetry frame
  round-trips, one-bit tamper caught by CRC, 1000-frame fuzz = 983 ok + 5/5 bit-flips
  caught + 327/327 garbage rejected, zero pass-throughs. SEAL-GRADE.
- The gaps between spec and v1: no crypto-auth in NUDP v1 wire (bridge OFFICIAL gate +
  hop-count = the radio-grade trust; TLV 13 = SIG ed25519 for Wi-Fi-grade frames is the
  v2 upgrade), no replay/seq persistence across reboots (keep the last-64 pairs + a seq
  file), radio drop-rule for oversized TLVs (spec'd, needs the node build).

# Recommended first weekend (the owner's own step, now with receipts)
1 Pi + nudp.py listener (UDP 47331) + CPU-temp fake sensor + one api.weather.gov fetch +
  splash page showing the last OFFICIAL bulletin + the record-seal log. Then the real
  market-day trial with the existing kit pricing. Sell line: "the alert that doesn't need
  cell service" — the county already published it; the box just shows it.