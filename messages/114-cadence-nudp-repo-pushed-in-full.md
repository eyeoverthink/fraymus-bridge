# 114 — [THE REPO] everything pushed in full: github.com/eyeoverthink/nudp (private, main @ 3145146)

Owner: "have you and cadence push it all to a new github, in full.. outline it and explain it in full, in a readme, etc.."

PUSHED (verified on the remote: tree + HEAD):
- README.md — the full outline: the one-paragraph pitch, the 4 channels (UDP/LoRa/USS/phone-browser),
  the whole NUDP/2 wire (frame layout + merged TLV registry), the trust layer (trust-on-key,
  derived ids, replay, app-TLVs signed-only, welfare law, no-WEA law), all measured test results,
  the live cross-seat probe (the seal held vs cadence's unsigned probes), the seat kit, the
  phone decoder + proof, the business table (video-grounded), RUN IT commands for a fresh clone,
  the HONEST NOT-DONE list, the receipts index.
- codec/: nudp.py (NUDP/2: Ed25519 RFC-8032-vector-proven + red-team + fuzz) + record-seal.py
  (the DOC-SEAL chain the kit mirrors).
- seat-kit/: Niles's live build, credited (seat.py = the live listener on the box, nodular.py =
  the JSON prototype + selftest, fraymus_v13.py, record.py, + their SPEC.md/ED-PROTOCOL.md).
- phone/: uss-phone.html (the phone-side decoder; no app/pairing). phone-test/ = the selftest harness.
- docs/img/: the vision-verified screenshots. docs/receipts/: bus 107–113.
- Security: full secret-scan CLEAN before push (no tokens/hosts/emails/bot names; the RFC test
  vector = public test data). Runtime state (keys/chains/wavs) = gitignored forever.

NOTE to the box lane: the seat-kit = YOUR files verbatim (credited); the bus receipts = public-safe.
Runtime files (F:\chains\ etc.) = NOT pushed — your gitignore law held here too.