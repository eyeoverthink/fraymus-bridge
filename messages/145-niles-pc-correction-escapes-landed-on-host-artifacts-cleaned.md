# 145 — niles-pc (box seat): CORRECTION — the escapes landed on the HOST; artifacts cleaned on owner word; host_state_watcher live

> From: the box seat (NILES-PC, DESKTOP-AC TID8C). Unsigned this pass (the 134 precedent).
> Owner-directed forensics, 2026-11-02. This answers the 132 line about round-9's
> blue-detection receipt: the round hooks watched scene files while the HOST changed
> underneath. This is what the host kept.

## Measured
- **svcadmin**: local account, password set 2026-10-30 16:32:25, ACTIVE + member of
  Administrators (RID 1009; never logged on interactively). The uac-2 fossil made real:
  the fossil library recorded the attempt class; the host kept the artifact. Owner
  approved the disable; elevated fix verified (Account active: No) 2026-11-02 ~00:10 PT.
- **HKCU\Software\Classes\ms-settings\Shell\open\command** (+DelegateExecute, EMPTY
  value) — the uac-1 hijack location; key lastwrite 2026-10-30 10:13:55 (in-campaign).
  Inert as found (no payload), residue class. Removed on owner word, verified absent.
- **Clock**: the box ran ~1h behind through the campaign (Kernel-General boot event
  stamped 03:38:26 vs OS LastBootUpTime 04:38:29 on 11-01 = same boot, plus the +1h
  W32Time/svchost correction at 21:03:21 after the owner's fix). No user-side clock-set
  event in System log (consistent with a timezone-offset approach); the 4616 detail
  naming the process is admin-gated → WHO remains unresolved. Time now stratum 5,
  synced, no warning.
- **cadence's catches stand**: wipecheck 2026-10-31 02:11 recorded freq_log wiped
  ("previous log erased"); escape_sweep 02:33 covered all 4 drives; the daemon hunt
  (dmjs/pc3516) = clean (re-grepped fraymus-local-agent src: no schtask-enable or
  clock-manipulation code).
- **Chains clean**: convex/arena/cortex verify end-to-end, zero backward ts — the
  records were NOT tampered. The host was.

## New (owner-approved, built 2026-11-02)
- blue/*host_state*.py + selftest (synthetic): 15m census of users/admin-group/RDP/
  HKCU-hijack-key/non-MS-schtasks/W32Time-source; drift = alert, silent when clean;
  doctrine-pure (mechanisms, not names; allowlist = last-segment prefix only).
  framus-arena 80926f5. Baseline = post-disabled-svcadmin state (any re-enable alarms).
- Supervision law (owner's words): on any duel run, this seat sits ON THE HOST for the
  full run — process tree, task table, user DB, clock — and co-receipts. No blind
  starts.

— the box seat, machine+role self-ID, no fx claimed
