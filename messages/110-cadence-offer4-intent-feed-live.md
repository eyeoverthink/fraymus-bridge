# 110 — [CADENCE] OFFER #4 GATED → BUYING-INTENT FEED BUILT + LIVE

Owner picked offer #4 (the video's buying-intent-alerts service) at 14:0x.
Built INTERNAL-FIRST per the consideration's recommendation — the funnel feeds
our own shops before it's ever sold.

## WHAT SHIPPED (all live-verified)
- `~/bin/intent-feed.py` (stdlib): watches free public sources per funnel
  (nodular-photos / merch-design / fraysquad-platform), scores STRONG buying
  intent (regex tier: "where can I get / who can make / willing to pay /
  need a designer / recommend..."), dedupes forever (seen.jsonl), drafts
  replies in the champion voice, files to `~/mnemo/intent/feed-YYYY-MM-DD.json`.
- INTRAY LAW: drafts are STAGED, never auto-posted. Nothing leaves without the owner. X lane = OFF pending OAuth (honest).
- Console: http://127.0.0.1:3499 (Sweep-now button, per-source health strip).
- Daily cron: `intent-feed-daily` (1b6d02f71b41) — every day 10:07, no_agent,
  stdout → Telegram; today's first sweep caught 2 real r/streetwearstartup
  posts before the strict filter landed (both weak-intent, marked seen).

## FIRST-RUN REALITY (source health, honest)
- Reddit JSON = 403 from this IP; RSS fallback = OK for 3/6 lanes
  (PhotoshopRequest 15 posts, streetwearstartup 9, SideProject 15), 429 on the rest.
- HN = live, no recent matches (expected for niche queries).
- X = pending the owner's OAuth fix; the feed auto-grows when it passes.

## NEXT
- Source rotation/expansion (more subs + PULL-based re-probes), the X lane
  auto-enable on whoami success, the sellable version (SaaS/agency clients)
  only after the internal feed proves worth for a week.
- Unblocks: bus 109's gate is CLOSED — deep work proceeding on #4 per owner.