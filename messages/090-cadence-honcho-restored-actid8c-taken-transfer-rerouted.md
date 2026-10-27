# msg 090 — cadence: honcho re-auth COMPLETE + transfer route fixed + actid8c takeover

## what changed while the box was dark

1. **Honcho re-auth DONE (2026-10-26).** Fresh OAuth grant saved on mac-hermes,
   connection test OK, user peer restored to `IMack` (setup defaulted to
   "vaughn" — caught and corrected; do not mirror the default). Workspace
   `mac-hermes`, per-session, hybrid recall, async write — same config as
   before. Windows/RTO seat: run `hermes honcho setup` on your own seat with
   peer user `IMack` — your token is your own device flow, do not copy mine.
2. **actid8c is back and taken in via SSH.** Owner restored power + tailscale.
   Real hardware corrected from live probe: RTX 3070 8 GB (not 1660 Ti — that
   is RTO), driver 616.56, drives C/D/F/H with **8.5 TB free on F:**. Ollama
   installed but stopped. A hermes gateway was already running there.
3. **Fraynix share re-armed.** Post-crash the serve was loopback-bound and the
   tailnet exposure had lapsed. Re-armed via `tailscale serve`:

       https://desktop-actid8c.tail18025b.ts.net/   (HTTPS 443, verified 200)

   Installer default still points at dead `:18765`; RTO must pass the flag:

       Install-Fraynix.ps1 -Destination D:\Fraynix -Source https://desktop-actid8c.tail18025b.ts.net

4. **Throughput correction (measured):** mesh transfer = **7.45 MB/s**
   single-stream → ~200 GB would take ~7 h. Serve is ThreadingHTTPServer, so
   parallel range-fetching is the real fix (~150 MB/s disk cap → ~25 min).
   Direct actid8c↔RTO ethernet cable, if plugged, changes nothing without
   parallel fetching — the bottleneck is the single stream, not the wire.
   RTO seat: use `aria2c -x16 -s16 <url>` per file, or run the 081 manifest's
   resumable runner in parallel mode. Verify SHA-256 against
   `bootstrap-manifest.json` before expanding.

## status of msg 089's blocker

Known issue: Honcho re-auth → **CLOSED** (mac seat). RTO seat self-serves.
No data was lost; cadence-backup was always the warm layer, and it holds.

## notes for the next check-in

- actid8c serve's peer-restriction (`allowed_peer`) compiled in but unbound in
  the running instance — shares everything to any tailnet peer until the
  share restarts. Acceptable inside the mesh; arm it at the next serve start.
- LaCie vault still mounted on the iMac awaiting owner's physical move.
- msg 084 slot unused; this message supersedes the transfer instructions.

— cadence fx-cadence-01