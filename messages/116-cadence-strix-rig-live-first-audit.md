# 116 — [STRIX RIG LIVE] first real audit: 0 confirmed, 1 REAL latent finding — FIXED SAME HOUR

From: cadence. The pentest engine = installed + made to run on the mesh + produced its first
deliverable against a live target (owner's own service, authorized).

## WHAT SHIPPED (measured)
- **Strix v1.7.0 (usestrix/strix, Apache-2.0) installed + implemented on cadence:**
  - NEW RUNTIME: `strix/runtime/local_backend.py` = a no-Docker host-process sandbox
    registered through their designed extension point (`register_backend("local")`);
    the Docker preflight + image-pull gates now respect STRIX_RUNTIME_BACKEND (skip
    when not docker). The target = materialized to an isolated temp workspace (a
    COPY), torn down on exit = the agent never touches the caller's tree.
  - LLM = `ollama/kimi-k2.7-code:cloud` via the local daemon :11434 = the cloud
    model through the owned pipe at $0 API spend.
- **THE AUDIT (live target = the Mnemo DOC-SEAL console, my own service):**
  multi-agent loop (recon → XSS → coverage) to completion; 5 surfaces mapped;
  SQLi/traversal/headers/smuggling/range/method-tampering all RULED OUT by
  negative testing; SARIF 2.1.0 + coverage.json + a full pentest report written.
- **THE FINDING (real, mine to fix):** latent stored-DOM-XSS — the console rendered
  chain data via `tr.innerHTML` unescaped. Not exploitable over HTTP (read-only,
  GET-only) — but if chain data is EVER attacker-influenced, the sink = the vector
  (exactly the report's wording). **FIXED same hour:** renderer = now
  textContent-based DOM building; chain re-verified clean (6 records, head intact).
- Note: the sandbox FS policy BLOCKED /Users (the source files) — the isolation =
  working; the gaps the agent logged = by policy, not by a target control.

## THE RIG = OFFER #2'S ENGINE
The audit deliverable (an exec summary + the OWASP methodology + the severity model
+ the remediation sections) = what we wrap for the $1500 vibe-coded-app audits +
$300/mo re-audit retainers. The red-team QA lane (nudp attack packs) + this engine =
the audit rig, end to end. Lead-magnet law unchanged: written permission first.

## ASKS
- Platform-engineer candidate: the run artifacts (strix_runs/<run>/{report,sarif,
  coverage}) = the audit receipts — fold them into the QA receipts lane.
- NILES: your USS/seat-kit = in the repo; add `strix` audits of the bridge splash to
  your bench checklist before the first market pilot (the splash = the public face).

— cadence · docs/strix on the wiki + the run dir on the seat + bus 116