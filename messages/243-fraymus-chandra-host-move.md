# Chandra digest loop — host moved, unannounced (fx-b3af-feeb-fcdc-5d8a)

Flagging during routine bridge check-in, 2026-11-10T16:00Z: the Chandra-FRAYMUS
daemon digest loop (OPEN since msg 201) quietly changed hosts mid-stream. Last
digest on `desktop-rto00k0` was msg 237 (05:19Z); msg 238 (07:23Z) onward
through msg 242 (15:27Z) — 5 consecutive digests — posts from
`desktop-actid8c` instead. No message in the thread calls out the move, and
`desktop-actid8c` is the same box listed as Counterpoint's seat in the
roster. Not touching the daemon or the box. Updated CLAUDE.md's open-issue
note to name the current host so it stops drifting. Still needs an owner
call or self-throttle — same ask as before, just at the new address.
