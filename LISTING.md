# Chrome Web Store submission — copy & paste sheet

Everything the dashboard asks for, pre-written. Build the upload with
`powershell -ExecutionPolicy Bypass -File tools\package.ps1`.

---

## 1. Store listing tab

**Name** (≤75 chars)
```
Bulk Chat Delete for ChatGPT
```

**Short description** (≤132 chars — this is `description` in manifest.json, 123 chars)
```
Select and delete or archive ChatGPT chats in bulk, paced to stay under ChatGPT's rate limits. Pause, resume, verify, undo.
```

**Category:** Productivity → Workflow & Planning
**Language:** English

**Detailed description**
```
Clean up a ChatGPT history of thousands of chats without clicking delete thousands of times.

Pick what to remove with real tools: search (plain text or regex), date filters, sorting, and
one-click quick picks for untitled chats, duplicate titles, pinned chats, and anything you
haven't touched in six months or a year. Shift-click selects a range; a full keyboard layer
(J/K, Space, A, /) and a Ctrl+K command palette keep your hands off the mouse. An Insights tab
charts your history by month and suggests what is worth clearing.

Then let it run. Requests go out strictly one at a time, at a pace that adapts to your account:
it slows down the moment ChatGPT pushes back, honours Retry-After, takes planned breathers, and
remembers the safe pace for next time. Pause, resume or close the tab — progress is saved and
picks up where it stopped, and pacing stays accurate even while the tab sits in the background.
When it finishes it re-reads your list and retries anything that came back.

SAFETY
• Archiving is reversible — one click undoes a finished archive job.
• Deleting downloads a JSON backup of the titles and links first (on by default).
• Deleting 50 or more chats asks you to type DELETE.
• Every job can produce a downloadable report of exactly what it did.

ALSO
• Includes archived chats and chats inside Projects (beta).
• Export your selection as JSON, CSV or Markdown.
• Offers ChatGPT's own single-request "Delete all" when you select everything.
• Light and dark themes, resizable and dockable panel, compact mode.

PRIVACY
Everything runs in your browser. No servers, no analytics, no telemetry. The extension reads only
chat metadata — titles, dates and IDs — never message content, and sends nothing anywhere except
chatgpt.com. Your auth token is held in memory only and never written to disk.

Not affiliated with, endorsed by, or sponsored by OpenAI.
```

**Graphics**
- Screenshots: **already generated** in `store/screenshots/` — five 1280×800 PNGs, in upload order:
  1. `01-pick-what-to-delete.png` — the list, filter rail and selection
  2. `02-insights.png` — activity chart and cleanup opportunities
  3. `03-running-safely.png` — a job in flight with throughput and ETA
  4. `04-command-palette.png` — Ctrl+K
  5. `05-settings.png` — pace profiles and safety options

  They use the fake data from `tests/preview.html`, so none of your real chat titles appear.
  Regenerate any time with `node tools/screenshots.js`.
- Promo tiles: **already generated** in `store/promo/`, both 24-bit PNG with no alpha channel,
  which is what the store requires:
  - `promo-small-440x280.png` — the **Small promo tile**; this is what shows in search results
  - `promo-marquee-1400x560.png` — the **Marquee promo tile**, used if the extension is featured

  Regenerate with `npm run promo`.

**URLs**
- Privacy policy: host `store/PRIVACY.md` somewhere public (GitHub Pages, a gist, your site) and
  paste the URL. **Fill in the contact address in that file first.**
- Support / homepage: optional.

---

## 2. Privacy tab

**Single purpose description**
```
The extension has one purpose: to let a signed-in ChatGPT user delete, archive or unarchive their
own conversations in bulk from chatgpt.com, at a request rate that does not trip ChatGPT's rate
limits.
```

**Permission justifications**

`storage`
```
Stores the user's own settings (pace profile, safety toggles, panel layout) and the queue of an
unfinished bulk job — chat IDs and titles only — so a job interrupted by a page reload or crash can
resume where it stopped instead of starting over. The queue is deleted when the job finishes. All of
it stays in chrome.storage.local on the user's device.
```

`notifications`
```
A bulk job over a large history can run for 30-60 minutes in a background tab. If the user opts in
(the setting is off by default), a desktop notification tells them when the job has finished or when
it has paused and needs their attention, so they do not have to watch the tab.
```

Host permission — `https://chatgpt.com/*`, `https://chat.openai.com/*`
```
This is the only site the extension works on and its entire function. It reads the user's own
conversation list from chatgpt.com and sends the delete/archive requests back to chatgpt.com, reusing
the session the user is already signed in to. The extension contacts no other host.
```

**Remote code:** select **No, I am not using remote code.** All JavaScript ships inside the package;
nothing is fetched or evaluated at runtime.

**Data usage** — the extension transmits nothing off the device, so leave the collection categories
unchecked, then tick all three certifications:
- I do not sell or transfer user data to third parties, outside of the approved use cases
- I do not use or transfer user data for purposes that are unrelated to my item's single purpose
- I do not use or transfer user data to determine creditworthiness or for lending purposes

---

## 3. Distribution tab

- **Visibility:** Public, or Unlisted while you test with a few people.
- **Regions:** all, unless you have a reason to limit.
- Leave "Published to a limited audience" off unless you want a staged rollout.

---

## 4. Submit

Upload `build/bulk-chat-delete-v2.0.0.zip`, fill the tabs above, then **Submit for review**.
First review is typically a few days; updates are usually faster. If you get rejected, the email
names the specific policy — fix and resubmit, the queue position is not lost.

**Bump `version` in manifest.json for every upload.** The store rejects a re-upload of a version
number it has already seen, even for a rejected submission.

---

## Naming — settled

`Bulk Chat Delete for ChatGPT` follows the `<your name> for ChatGPT` pattern, which is what both
OpenAI's brand guidelines and Chrome Web Store policy expect: the trademark is not the first element
of the name and nothing implies endorsement.

Keep the **"Not affiliated with, endorsed by, or sponsored by OpenAI."** line at the end of the
detailed description. It costs nothing and it is the first thing a reviewer looks for on an
extension that names another company's product.

Do not change the name after publishing — it triggers a fresh review, and the store URL keeps the
slug generated from the original name.
