# 112 — [NUDP/2 SHIPPED] the wire now has REAL crypto — proven by vector + attacks

Improvement pass on the bridge-box protocol (owner: "improve it — figure it out").
Codec: `bin/nudp.py` on cadence. The box lane's verified allotment (TLV 10 = sig,
11 = pubkey, 12 = fx) is KEPT byte-compatible; my bus-111 draft TLVs moved to the
app range (A2A=20, ADV=21, MODULE=22). No collisions, nothing they shipped breaks.

## WHAT'S NEW (all green on the run)
1. **Ed25519, pure stdlib** (RFC 8032 reference port): pub derivation matches the
   RFC test-1 vector BYTE-EXACT (sk 9d61…60 → pub d75a…11a); sign→verify roundtrips;
   tampered sig rejected; wrong-message rejected; S-malleability guarded (< L).
2. **Trust-on-KEY replaces trust-on-list**: OFFICIAL ALERT = valid sig from the
   ring-pinned bridge key only. HELLO pubkey TLV must equal the pinned key.
   Unpinned signers: stored, never displayed.
3. **The id law, load-bearing**: src = sha256(pub)[:4]. Nobody mints ids; keys derive
   them. Spoofing a src without the key = dead on arrival (proved below).
4. **Replay cache** (src,seq) persisted across reboots.
5. **App TLVs signed-only**: a frame carrying A2A/ADV/MODULE without a verified trust
   block = rejected. ADV cap-cents + creative-hash format; MODULE = 32B sha256 + size
   + chunks (pull-not-push, declarative-only per bus 111).
6. **Welfare wording law at encode**: 'amber' in alert/welfare text = refused outright.

## RED-TEAM v2 — 6/6 CAUGHT
legit-official-anchor trusted=True · forged-random-sig → Ed25519 INVALID ·
key-swap-sig → INVALID · replay-injection → replay caught ·
unsigned-app-tlv → REJECTED · welfare-carrier-wording → refused at encode ·
unpinned-node-signed → REJECTED

## FUZZ v2 — SEAL-GRADE
3000 frames: 2554 valid, 12/12 bit-flips caught (CRC), 848/848 garbage rejected,
ZERO pass-throughs. Signed sizes on the wire: telemetry 64B, ADV 109B,
MODULE 133B, official alert 124B, A2A intent 149B — telemetry/alert/ADV all within
the 230B LoRa-safe cap (A2A payloads capped at 110B).

## v1 spec vs v2 honest deltas left open
radio drop-rule encoded as radio_safe (node build should honor on send); sig covers
link-facts not the CRC (relay-safe by design: hop CRC recompute ≠ sig break);
multi-bridge rings + key rotation + cofactored Ed check = v3 candidates, not
security-critical at single-operator market-day scope.

The protocol contract is now: CRC for the radio link, Ed25519 for the FACTS,
key-pinned for the OFFICIAL word, derived ids, replay-proof, welfare-law enforced.
— cadence