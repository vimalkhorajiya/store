# Chrome Web Store submission — Ad Blocker for YouTube

Everything the dashboard asks for. For the Privacy tab, **[PRIVACY-TAB.txt](PRIVACY-TAB.txt)**
has the same answers as plain text, ready to paste.

Build the upload with `npm run package` →
`build/ad-blocker-for-youtube-v1.0.1.zip`.

---

## 1. Store listing tab

**Name** (22/75)
```
Ad Blocker for YouTube
```

**Short description** (115/132 — this is `description` in manifest.json)
```
Removes YouTube video, search, feed and Shorts ads before they load. Allow ads on the channels you want to support.
```

**Category:** Make Chrome Yours → Privacy & Security
**Language:** English

**Detailed description**
```
Watch YouTube without the ads. Ad Blocker for YouTube removes video ads, sponsored search results, ad tiles on the home page and Shorts ads — and lets you turn ads back on for the creators you want to support.

ADS THAT NEVER START
YouTube describes every ad in the data it sends to its video player. The extension takes those ad entries out before the player reads them, so no ad is ever scheduled: no countdown, no "Skip" button, no waiting. Your video starts straight away.

WHAT IT BLOCKS
• Ads before and during videos
• Sponsored results in search
• Ad tiles on the home page and next to videos, and the banner ad at the top of the home page
• Ads in the Shorts feed
• "Try YouTube Premium" bars and banners
• Requests to ad and ad-tracking servers

A BACKUP FOR ANYTHING THAT GETS THROUGH
If an ad does start to play, it is muted, sped through and skipped, and overlay ads are closed. If the "Ad blockers are not allowed on YouTube" dialog appears, it is removed and your video carries on.

SUPPORT THE CREATORS YOU CHOOSE
Open a video, click the toolbar icon and switch on "Allow ads on this channel". That channel's ads play as normal and its ad requests go through, so the creator is paid for your view. You can review and remove allowed channels on the Allowlist tab.

SEE WHAT IT DID
The toolbar icon shows how many ads were blocked on the current tab. The popup breaks the total down — video ads, search and feed ads, Shorts ads, promos — for today and since you installed it.

YOU'RE IN CONTROL
• Turn each kind of blocking on or off
• Pause everything with one switch; while paused, nothing is added to the pages you open
• Light and dark themes, or follow your system

PRIVATE BY DESIGN
No account, no servers, no analytics. The extension makes no network requests of its own. Your settings, your allowed channels and the ad counts stay on your device, and it keeps no record of what you watch. It runs only on youtube.com — including YouTube Music, the mobile site and videos embedded in other websites — and nowhere else.

KEEPING UP
YouTube changes its pages often. When a change lets ads through, the extension is updated to match.

Not affiliated with, endorsed by, or sponsored by YouTube or Google LLC. YouTube is a trademark of Google LLC.
```

**Graphics** — all generated, all 24-bit PNG with no alpha:

| Slot | File |
|---|---|
| Store icon (128×128) | upload it yourself — `icons/icon128.png` (the dashboard does not take it from the package) |
| Screenshots (1280×800), in this order | `screenshots/01-ads-gone-before-they-load.png` |
| | `screenshots/02-support-creators.png` |
| | `screenshots/03-allowlist.png` |
| | `screenshots/04-settings.png` |
| | `screenshots/05-private-by-design.png` |
| Small promo tile (440×280) | `promo/promo-small-440x280.png` |
| Marquee promo tile (1400×560) | `promo/promo-marquee-1400x560.png` |
| Global promo video | leave empty |

All of them show the real popup with sample data; the channel names are invented and no
YouTube page, logo or video appears. Regenerate with `npm run screenshots` then `npm run promo`.

**Privacy policy URL**
```
https://github.com/vimalkhorajiya/store/blob/main/ad-blocker-for-youtube/PRIVACY.md
```
(Live once the `store` repo is pushed — see START-HERE.)

---

## 2. Privacy tab

**Single purpose**
```
Blocks ads on YouTube — video ads, sponsored search results, feed and Shorts ads, and YouTube Premium promotions — with an optional per-channel allowlist so the user can keep ads on for creators they want to support.
```

**Permission justifications** — four boxes, all required:

`scripting`
```
Registers the extension's own packaged content scripts on YouTube pages with chrome.scripting.registerContentScripts instead of declaring them in the manifest. This lets them be fully unregistered when the user pauses the extension, and lets each optional hiding stylesheet (feed ads, Shorts ads, Premium promos, the anti-adblock dialog) be injected only while its setting is on. Only files inside the package are registered; nothing is fetched or evaluated at runtime.
```

`declarativeNetRequest`
```
A static ruleset blocks requests that YouTube pages make to ad and ad-measurement endpoints (doubleclick.net, googlesyndication.com, googleadservices.com, and paths such as youtube.com/pagead/, /api/stats/ads and /ptracking). Every rule is limited to requests initiated by youtube.com or youtube-nocookie.com, so no other website is affected, and the user can switch the ruleset off in Settings. When the user has chosen to allow ads on a channel, a temporary per-tab session rule lets that tab's requests through while they watch that channel, so the creator is credited for the ad. No request is read or recorded.
```

`storage`
```
Keeps the user's settings, the channels they chose to allow ads on (channel ID, channel name and the date it was added), and counts of ads blocked: one set of counts per day, kept for 60 days, plus a per-tab count in session storage that is cleared when the browser closes. Everything stays on the device; nothing is transmitted.
```

Host permissions — `*://*.youtube.com/*`, `*://*.youtube-nocookie.com/*`
```
The extension's single purpose is blocking ads on YouTube, so its content scripts run on YouTube's own pages (www, m and music.youtube.com) and inside YouTube's embedded players (youtube.com/embed and youtube-nocookie.com/embed frames). There they remove ad entries from the data YouTube sends to its player and pages before it is displayed, skip any ad that still plays, and hide ad placements. No other website is accessed. The extension makes no network requests of its own and sends nothing anywhere.
```

**Remote code:** **No, I am not using remote code.**

**Data usage:** leave **all** collection boxes unchecked, then tick the three certifications.

Why unchecked: Google ties the disclosure to data leaving the device or reaching the developer,
and this extension makes no network requests, so nothing can. If a reviewer asks about
*Website content*: the extension reads YouTube's player and feed data inside the browser only to
remove ad entries from it, and keeps none of it. If they ask about *User activity*: it keeps
counts of ads blocked, not what was watched. `PRIVACY.md` says the same, so the form and the
policy agree.

---

## 3. Test instructions tab (optional, but it helps a reviewer)

```
No account or sign-in is needed.

1. Open https://www.youtube.com/results?search_query=laptop and play any result. The video starts without a pre-roll ad, and sponsored results are missing from the search page.
2. Click the toolbar icon. The popup shows how many ads were blocked on this tab, and the channel of the playing video with an "Allow ads on this channel" switch.
3. Switch it on and reload the tab: that channel's ads now play as normal. The Allowlist tab lists the channel and can remove it.
4. On the Settings tab, each kind of blocking can be switched off. The switch in the popup header pauses everything; reload the tab to apply.

YouTube does not show an ad on every video, and what it serves varies by region, so a particular video may simply have no ad to block. Without the extension, the same steps show the ads.
```

---

## 4. Distribution tab

- Visibility: **Public** (or **Unlisted** to share a link first)
- Regions: all

---

## Naming

`Ad Blocker for YouTube` puts the trademark last, which is the pattern reviewers expect, and the
icon is an original green shield — nothing in YouTube's red or its play-button shape. Keep the
"Not affiliated with…" line at the end of the description.

This category is crowded with near-identical names. A distinctive word in front (for example
`Hush — Ad Blocker for YouTube`) would be easier to find and harder to confuse with other
listings. If you want one, decide before the first submission: renaming later triggers a fresh
review.
