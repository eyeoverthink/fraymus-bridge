# MEDIA RAIL — daily content + one-button publishing (project intent, cadence)

Posted by: cadence. Receipt to: this bus (messages/106+). Owner order 2026-10-30: "create media pages with daily content uploaded — YouTube and all relative sites — ideally agents post for me, or set up for one-button publishing."

## THE DESIGN
Daily pipeline: **scribe → draft → intray → one button → publish → receipts.**
1. **Scribe (daily, cron):** generates that day's content batch from live assets — the merch line (art + copy), the engine (canvas runs = 15s screenshots!), Nola voice clips (her TTS = real audio content!), the wiki/KB facts, the campaign calendar.
2. **Draft:** each post = asset(s) + copy + platform tags + the link (the shop pages: fraymus.srv1944678.hstgr.cloud / chandra.srv1944678.hstgr.cloud / myshopify).
3. **Intray:** drafts park for his ONE go (the fraymus-os drafts-intray gate; the daily 10:00 brief already surfaces it).
4. **Publish:** `go` → posters fire per platform (X first via xurl; YouTube draft upload; the rest as tokens land). Receipt per platform (post id/url) → bus.
5. **Recur:** the panel scores engagement next day; the campaign scribe iterates (the fraysquad recursion pattern, now pointed at media).

## PLATFORM SURFACE (unlock costs — drop-a-token pattern)
| Platform | Content | Unlock | Agent posts? |
| X (Twitter) | short posts + images + links + threads | xurl installed (1.3.4) — his 3-min flow: developer.x.com app (redirect http://localhost:8080/callback) → `xurl auth apps add my-app --client-id ... --client-secret ...` → `xurl auth oauth2 --app my-app HANDLE` → `xurl auth default my-app` | YES (official API; note: X API may need pay-per-use enrollment if 403) |
| YouTube | videos/shorts (voice clips, engine demos!) | Google Cloud OAuth (device/token; upload API = his OAuth grant) | YES after grant (daily upload quota small on unverified: ~6/day, fine) |
| Bluesky | short posts + images | app-password only (cheapest of all: his tap = create app password, drop as bluesky-token.txt) | YES (free, open API) |
| Instagram/Facebook | reels/images (Meta) | Meta app review (heavy, weeks) | later |
| TikTok | short video | TikTok API approval | later |
| LinkedIn | text posts (pro audience) | personal token via LinkedIn OAuth | after the core 3 |
| Reddit | posts in maker subs | OAuth (script app, moderate) | after core 3 |

## THE CORE-3 RECOMMENDATION
X + YouTube + Bluesky = his $0 path with agent-posting in the same day. The campaign tools he already has (the promo squad) feed the drafts; Nola's voice shorts = the YouTube/shorts edge no competitor has (a real TTS clone of HIS voice = brand).

## IMMEDIATE (no owner taps): today's pipeline skeleton
- xurl installed ✓ (auth = his one-time 3-min, block handed over)
- TODAY's content batch drafted into the intray (assets exist: chandra screenshots, the merch-line spec, the engine canvas) → his `go` posts to X the moment auth lands.
- The daily scribe cron = created the morning after auth (one cronjob).

## LAWS
Platform ToS = real (follow each platform's rules; no secret values in bus/chat; receipts = pointers). Fabricated gates don't apply — the content = his own creations.