# Privacy Policy — Work & Presence for greytHR

**Last updated: 6 October 2026**

Work & Presence for greytHR is a browser extension that reads your own attendance swipes on
greytHR and shows how long you have worked, how long you have been present, and when you can
leave.

## The short version

**The extension does not collect, transmit, sell or share any of your data. It makes no network
requests at all.** It has no servers, no analytics, no telemetry and no third-party services.
Everything it does happens inside your own browser.

## What the extension reads

On pages under `greythr.com`, it reads the tables on the page to find your attendance swipe log.
From each swipe row it keeps exactly two things: **the direction (IN or OUT) and the time.** It
does not keep any other text from the page — not your name, employee details, leave balances,
payslips or anything else greytHR shows.

It does not run on, or read, any other website.

## What the extension stores, and where

Everything is kept in `chrome.storage.local`, on your own device:

| Data | Why |
|---|---|
| Today's swipes (direction + time) | To calculate today's work, breaks and presence. |
| One summary per past day — total work, total break, total presence, first and last punch time, number of swipes | For the Week view. At most 120 days are kept; older days are deleted automatically. |
| Your settings (targets, badge, notifications, theme) | To remember your preferences. |
| Which notifications have already been shown today | So each alert fires only once a day. |

None of it leaves your device. Removing the extension deletes all of it, and Settings → *Clear
stored history* deletes the daily summaries at any time.

## Network requests

None. The extension never contacts any server — not greytHR's, not ours, not anyone's. It only
reads what is already displayed in your browser. All of its code ships inside the extension
package; nothing is downloaded or run from elsewhere.

## Notifications

The extension can show a desktop notification when you reach your work target or your presence
target, and optionally when a break runs long. They are generated on your device from the data
above. Each can be switched off in Settings.

## Permissions

- **storage** — keeps the data in the table above, on your device.
- **alarms** — refreshes the toolbar badge and checks the notification conditions once a minute.
- **notifications** — the target-reached and long-break alerts described above.
- **Access to `*.greythr.com`** — to read your swipe log. greytHR gives each company its own
  subdomain, hence the wildcard. No other site is accessed.

## Children

The extension is not directed at children and collects no data from anyone.

## Changes

If this policy changes, the updated version will be published at this URL and the date above
will be updated.

## Contact

Questions or concerns: **vimalkhorajiya@gmail.com**

---

*Work & Presence for greytHR is an independent project. It is not affiliated with, endorsed by,
or sponsored by greytHR or Greytip Software. "greytHR" is a trademark of its owner.*
