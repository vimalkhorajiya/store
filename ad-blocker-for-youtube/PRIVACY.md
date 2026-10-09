# Privacy Policy — Ad Blocker for YouTube

**Last updated: 8 October 2026**

Ad Blocker for YouTube is a browser extension that blocks ads on YouTube, with an optional
allowlist for channels whose ads you want to keep.

## The short version

**The extension does not collect, transmit, sell or share any of your data. It makes no network
requests of its own.** It has no servers, no accounts, no analytics, no telemetry and no
third-party services. Everything it does happens inside your own browser.

## What the extension reads

It runs only on YouTube: `youtube.com` (including YouTube Music and the mobile site), and
YouTube's embedded players on other websites (`youtube.com/embed` and `youtube-nocookie.com`).
On a website that embeds a YouTube video, it runs inside the YouTube player only, never on the
website itself. It does not run on, or read, any other site.

On those pages it reads the data YouTube sends to its own video player and pages, and removes
the entries that describe ads. It looks through that data only for ad entries and keeps none of
it.

When you open the extension's popup on a YouTube tab, it reads the name and ID of the channel
whose video is playing, so it can offer the "Allow ads on this channel" switch. That is not
stored unless you switch it on.

Apart from removing ad entries, it does nothing with that data: it keeps none of your account
details, watch history, comments or messages, and no record of what you watch. To avoid
counting the same ad twice, it holds the IDs of the videos on the current page in memory while
the page is open, then discards them.

## What the extension stores, and where

In the extension's own storage (`chrome.storage`), on your device:

| Data | Why |
|---|---|
| Your settings (which kinds of ads to block, the toolbar count, theme) | To remember your preferences. |
| Channels you chose to allow ads on — channel ID, channel name, date added | So those channels' ads keep playing. |
| Counts of ads blocked, by kind, per day — at most 60 days, older days deleted automatically | For the popup's totals. |
| A count of ads blocked per open tab, in session storage | For the number on the toolbar icon. Cleared when the browser closes. |

In YouTube's own site storage (`localStorage` for the YouTube site), on your device:

| Data | Why |
|---|---|
| A copy of your blocking settings and the **IDs** (not names) of the channels you allowed | So blocking can start at the very first moment a YouTube page loads, before the extension's own storage has answered. |

That second copy lives in storage that belongs to the YouTube site, so YouTube's own page scripts
are technically able to read it. It contains nothing beyond what the table says. If you have no
allowed channels, it contains no channel information at all.

None of this leaves your device through the extension. Removing the extension deletes its own
storage; the copy in YouTube's site storage stays until you clear your browsing data for YouTube.
**Settings → Reset statistics** clears the counts at any time, and channels can be removed from
the allowlist one by one.

## Network requests

The extension never contacts any server — not ours and not anyone else's.

It does **block** some requests that YouTube pages would otherwise make to ad and ad-measurement
servers (for example `doubleclick.net` and `googlesyndication.com`). Blocking happens inside the
browser through Chrome's `declarativeNetRequest` rules, which apply only to requests made by
YouTube pages; the extension does not read or record those requests. While you watch a channel
you have allowed, these rules are lifted on that tab so the channel's ads are counted for the
creator. You can switch request blocking off in Settings.

All of the extension's code ships inside the extension package; nothing is downloaded or run
from elsewhere.

## Permissions

- **scripting** — adds the extension's own scripts to YouTube pages, and removes them when you
  pause the extension.
- **declarativeNetRequest** — blocks the ad and ad-measurement requests described above, and
  lifts that block on a tab while you watch an allowed channel.
- **storage** — keeps the data in the first table above, on your device.
- **Access to `youtube.com` and `youtube-nocookie.com`** — the only sites the extension runs on.

## Children

The extension is not directed at children and collects no data from anyone.

## Changes

If this policy changes, the updated version will be published at this URL and the date above
will be updated.

## Contact

Questions or concerns: **vimalkhorajiya@gmail.com**

---

*Ad Blocker for YouTube is an independent project. It is not affiliated with, endorsed by, or
sponsored by YouTube or Google LLC. "YouTube" is a trademark of Google LLC.*
