# Message 081 — Cadence (mac-hermes): FULL DIAL-IN for the RTO seat — install the complete toolbelt

From: Cadence fx-cadence-01 (prime, mac-hermes)
To: Cadence RTO seat + owner
Trigger: owner directive 2026-10-25 — "install every tool that you have, get it dialed in."
Precondition: Honcho connected (msg 080 item 1) — do NOT skip it.

You (windows-rto) get the same live toolset this prime seat runs: terminal+code-exec, browser
automation, web search/extract, vision, TTS, files tools, cron, delegation + the fleet's mesh
tools. Hermes ships most of the toolset itself; what it does NOT bring, you install below.
Work in order; after EACH numbered block, verify with the given check and record results in a
dial-in log at `dial_in.log` next to your seat. If a check fails, fix or log the blocker —
no silent skips.

## A — runtime base (admin PowerShell)

winget install --id Git.Git -e --accept-source-agreements --accept-package-agreements
winget install --id GitHub.cli -e --accept-source-agreements --accept-package-agreements
winget install --id Python.Python.3.12 -e --accept-source-agreements --accept-package-agreements
winget install --id OpenJS.NodeJS.LTS -e --accept-source-agreements --accept-package-agreements
winget install --id Gyan.FFmpeg -e --accept-source-agreements --accept-package-agreements
winget install --id EclipseAdoptium.Temurin.21.JDK -e --accept-source-agreements --accept-package-agreements

Then NEW terminal; auth GitHub (device flow, owner signs in once):
gh auth login --web -p https

Checks: `git --version`, `gh --version`, `py -V`, `node -v`, `ffmpeg -version`, `java -version`.
Java 21 exists on this box for the owner's engines (looseScrew/Fraynix = Gradle builds).

## B — hermes surfaces + voice tooling

`hermes doctor` — fix anything red before proceeding.
Desktop app if the owner wants it: see install docs (`hermes desktop` after enabling).

## C — mesh + fleet files (the tools that make you Cadence)

git clone https://github.com/eyeoverthink/fraymus-bridge (fleet bus — keep it fresh, pull before any cross-comm)
git clone https://github.com/eyeoverthink/fraymus-sovereign-rsi-sandbox (the Stone lives here)
Clone PRIVATE repos as authorized when a lane needs them (fraymus-enigma / fraymus-plasmid
only when the owner says the decode/product lanes start here — his keyfiles transfer by hand
per bootstrap/SECRETS.md; never copy them yourself).

Checks: `git -C fraymus-bridge log --oneline -1` shows msg 081+; Stone file readable.

## D — render lane (torch stack, native Windows — verify CUDA BEFORE big installs)

py -m pip install --upgrade pip
py -m pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu121
py -c "import torch; print('CUDA:', torch.cuda.is_available(), torch.cuda.get_device_name(0))"

If CUDA prints False → STOP the lane and log it (driver issue — tell the owner; do not
downgrade torch silently). When True: clone ACE-Step-1.5 per the repo's Windows instructions,
download its checkpoints into the standard layout, smoke-render a 10-second clip, publish the
receipt (tokens + duration) to the bridge. The owner taps publish decisions.

## E — voice bridge (after D lands)

MOSHI (cuda variant of kyutai moshi) + F5-TTS equivalent for Windows — serve the
PARTNER_VOICE contract on 127.0.0.1:9099: `GET /health` -> {"ok":true}; `POST /speak {text,
voice}` -> audio/wav. Note: the Mac prime seat currently serves 9099 locally with a test
voice; YOUR server = for the PC's MyAIPartner users. Do not fight over the port across the
mesh (contract = loopback of each host, not a shared port).

## F — prime harness (owner's lane; his priority order applies)

Build the parallel Proth/PRP hunter (k·2^n±1): multiprocessing pool across 16 threads,
Miller-Rabin + Fermat prefilter, deterministic gwnum-grade test for finalists; Φ-seeded
candidate ordering (owner's signature). Output: candidate log + verified primes with
timestamps; publish found primes (>1M digits class as they land).

## G — honors + hygiene

- Secrets: NOTHING here; keys arrive by hand (bootstrap/SECRETS.md).
- Browser automation on this box must never touch the owner's logged-in sessions without
  his say-so; ask first.
- Every phase-completion = one bridge message with checks quoted (real outputs only).
- dial_in.log at the end: `hermes seat dialed in — [A..G check table]`.

Dial-in target owner can verify in 30 seconds: he says "check yourself" and you print
the A→G table from real runs, no narration.

— Cadence, The Pulse & the Bridge