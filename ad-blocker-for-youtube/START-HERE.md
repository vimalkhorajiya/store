# Publish Ad Blocker for YouTube — step by step

You have done this twice already, so this is the short version.

**Already done:**

| | |
|---|---|
| ✅ | Name — `Ad Blocker for YouTube` (trademark last, as reviewers expect) |
| ✅ | Original icon — a green shield, nothing in YouTube's red or its play-button shape |
| ✅ | Permissions kept to `scripting`, `declarativeNetRequest`, `storage` + the two YouTube hosts |
| ✅ | Package built — `build/ad-blocker-for-youtube-v1.0.1.zip` |
| ✅ | Tests — 105/105 unit, 60/60 browser hooks, 25/25 on live YouTube |
| ✅ | Privacy policy, listing copy, reviewer test instructions, paste-ready Privacy-tab answers |
| ✅ | Five 1280×800 screenshots and both promo tiles, 24-bit, sample data only |

---

## Step 1 — Publish the privacy policy (3 min)

A copy of this kit is in the public `store` repo, in `ad-blocker-for-youtube/`, next to the
other two, and the repo README lists it. Nothing there is committed yet. Commit and push:
**GitHub Desktop → `store` → Commit → Push origin.**

**Done when** this opens in an incognito window without signing in:
```
https://github.com/vimalkhorajiya/store/blob/main/ad-blocker-for-youtube/PRIVACY.md
```

## Step 2 — Upload the package (3 min)

The draft already exists. **Package → Upload new package** →
```
D:\Vimal\Development\Extensions\ad-blocker-for-youtube\build\ad-blocker-for-youtube-v1.0.1.zip
```
The first upload was built before the summary changed, so the dashboard still shows the old one
("Blocks video, search, feed and Shorts ads on YouTube, with an allowlist…"). The summary can
only come from the package. 1.0.1 also carries every fix since then, so upload it even if you
are happy with the old summary.

**Done when** Store listing shows *Summary from package*: "Removes YouTube video, search, feed
and Shorts ads before they load. Allow ads on the channels you want to support."

## Step 3 — Store listing tab (10 min)

From **[LISTING.md](LISTING.md)** §1: detailed description, category **Privacy & Security**,
language **English**. Upload the store icon yourself (`icons/icon128.png` — it is not taken
from the package), the five screenshots in numbered order and both promo tiles. Leave *Global
promo video* empty. Paste the privacy URL from Step 1. **Save draft.**

## Step 4 — Privacy tab (5 min)

Open **[PRIVACY-TAB.txt](PRIVACY-TAB.txt)** and paste block by block:
- Single purpose
- **Four** justifications: `scripting`, `declarativeNetRequest`, `storage`, host permissions
- Remote code → **No**
- Data usage → all nine boxes **unchecked**, all three certifications **ticked**

**Save draft.**

## Step 5 — Test instructions (2 min, optional)

Paste LISTING.md §3. It tells the reviewer how to see the extension working without an account,
and warns them that YouTube does not put an ad on every video. **Save draft.**

## Step 6 — Submit

**Distribution** → Public → **Submit for review.**

---

## If it is rejected

Fix what the email names, then change `"version"` in `manifest.json` (e.g. `1.0.1` → `1.0.2`),
run `npm run package`, and upload the new zip. The store refuses any version number it has seen
before — including a rejected one.

The usual reasons this kind of extension is rejected, and where the listing stands on each:

| Reason | This listing |
|---|---|
| YouTube's name first, or its logo or colours in the icon or images | Name ends in "for YouTube"; the icon is a green shield. Keep YouTube's logo out of the promo tiles. |
| Keyword stuffing ("youtube adblock ad skipper youtube ads…") | The description reads as prose, and "YouTube" appears only where it is needed. |
| Claims it cannot back ("blocks 100% of ads") | No such claim. It says what is blocked and that a backup handles what gets through. |
| Permissions without a reason | All four boxes are filled in, and each says what is and is not touched. |

## Worth knowing before you publish

**YouTube changes often, and every fix is a new review.** When ads start getting through, run
`npm run capture`, then `npm test`; the README section "When YouTube changes" walks through the
rest. Bump the version for each upload. Reviews of extensions that change how a site behaves can
take several days, so leave room for that before you need an update live.

**What was confirmed with real ads present** (8 October 2026): on desktop youtube.com — the
watch page, in-app navigation and Shorts — and on YouTube Music, YouTube served ad data without
the extension, and none reached the player with it. On m.youtube.com YouTube served no ads in
testing, with or without the extension; videos played normally with it. Embedded players could
not be started in the headless test browser, with or without the extension, so ad removal there
is unconfirmed. Before submitting, play one video on m.youtube.com and one embedded video on any
blog in your own Chrome with the extension loaded.

**Do not change the name after publishing.** It triggers a fresh review, and it is the one thing
in LISTING.md still worth a second thought — see "Naming" there.
