# Chrome Web Store submission — Work & Presence for greytHR

Everything the dashboard asks for. For the Privacy tab, **[PRIVACY-TAB.txt](PRIVACY-TAB.txt)**
has the same answers as plain text, ready to paste.

Build the upload with `npm run package` →
`build/greythr-work-presence-v2.0.0.zip`.

---

## 1. Store listing tab

**Name** (27/75)
```
Work & Presence for greytHR
```

**Short description** (111/132 — this is `description` in manifest.json)
```
Live work, break and presence totals from your greytHR swipes, with a countdown badge and leave-time estimates.
```

**Category:** Productivity
**Language:** English

**Detailed description**
```
Stop doing clock maths in your head. Work & Presence reads your greytHR swipe log and tells you, live, how long you have worked, how long you have been in, and exactly when you can leave.

TODAY AT A GLANCE
• A live timer of the work you have done today, against your target
• "Leave at" — the time you reach your target, updated every second
• Your whole day on one timeline: work and breaks laid out, with "now" marked
• Work, break and presence kept separate, because they answer different questions
• Overtime counted from the moment you hit your target

WORKS FROM ANY TAB
Open your greytHR attendance page once and the figures keep updating — the popup and a countdown badge on the toolbar icon stay current even while greytHR sits in the background.

STAY ON TOP OF IT
• A notification when you reach your work target, and another at your presence target
• An optional nudge when a break runs long
• A week view with a daily chart, filled in from the days greytHR already shows

YOUR HOURS, YOUR RULES
Set your own work and presence targets (8h and 9h by default), choose what the badge shows, and pick light, dark or system theme.

PRIVATE BY DESIGN
The extension makes no network requests at all. It reads only your swipe directions and times from greytHR pages, keeps them on your device, and never reads any other site. No account, no servers, no analytics.

"Work" counts only time between IN and OUT. "Presence" counts from your first punch of the day, breaks included.

Not affiliated with, endorsed by, or sponsored by greytHR or Greytip Software.
```

**Graphics** — all generated, all 24-bit PNG with no alpha:

| Slot | File |
|---|---|
| Store icon (128×128) | taken from the package — `icons/icon128.png` |
| Screenshots (1280×800), in this order | `screenshots/01-when-you-can-leave.png` |
| | `screenshots/02-shape-of-your-day.png` |
| | `screenshots/03-target-met.png` |
| | `screenshots/04-week-history.png` |
| | `screenshots/05-settings.png` |
| Small promo tile (440×280) | `promo/promo-small-440x280.png` |
| Marquee promo tile (1400×560) | `promo/promo-marquee-1400x560.png` |

All of them use generated sample data — no real attendance records appear. Regenerate with
`npm run screenshots` then `npm run promo`.

**Privacy policy URL**
```
https://github.com/vimalkhorajiya/store/blob/main/work-presence/PRIVACY.md
```
(Live once the `store` repo is pushed and public — see START-HERE.)

---

## 2. Privacy tab

**Single purpose**
```
Shows a greytHR user how long they have worked and been present today, and when they can leave, calculated from their own attendance swipes on greytHR.
```

**Permission justifications** — four boxes, all required:

`storage`
```
Keeps the user's own data on their device: today's swipes (punch direction and time only), one summary per past day for the week view (capped at 120 days), the user's settings, and a record of which alerts were already shown today. Nothing is transmitted anywhere.
```

`alarms`
```
Refreshes the toolbar badge countdown and checks whether the work or presence target has been reached, once a minute. Manifest V3 service workers are suspended when idle, so a timer cannot be used; chrome.alarms is the supported way to run this periodic check.
```

`notifications`
```
Tells the user when they have reached their daily work target and their presence target, and optionally when a break has run longer than a limit they set. Each alert fires at most once a day and can be switched off in Settings.
```

Host permission — `https://*.greythr.com/*`
```
The extension's only function is reading the user's own attendance swipe log on greytHR. greytHR hosts each company on its own subdomain (company.greythr.com), hence the wildcard. From the page it keeps only the punch direction and time of each swipe. No other site is accessed, and the extension makes no network requests.
```

**Remote code:** **No, I am not using remote code.**

**Data usage:** leave **all** collection boxes unchecked, then tick the three certifications.

Why unchecked: Google ties the disclosure to data leaving the device or reaching the developer,
and this extension makes no network requests, so nothing can. If a reviewer asks about
*Website content* or *User activity*: it reads attendance tables on greytHR pages and keeps only
punch directions and times, locally. `PRIVACY.md` says the same, so the form and the policy agree.

---

## 3. Distribution tab

- Visibility: **Public** (or **Unlisted** to share a link with colleagues first)
- Regions: all — or just India, if greytHR's footprint is all you care about

---

## Naming

`Work & Presence for greytHR` puts the trademark last, which is the pattern reviewers expect.
Keep the "Not affiliated with…" line at the end of the description.

The original icon (a purple tile with a white "g") was replaced with an original stopwatch
mark, because it closely resembled greytHR's own app icon — the kind of resemblance reviewers
reject as impersonation. It is kept at `legacy/icon-original.png`.
