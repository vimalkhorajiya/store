# Publishing Bulk Chat Delete for ChatGPT to the Chrome Web Store

> **Want the short version?** Use **[START-HERE.md](START-HERE.md)** — 10 plain steps.
> This file is the same process with the reasoning and the edge cases spelled out; come here when a
> step in the short version goes wrong.

A start-to-finish runbook. Work top to bottom; each phase ends with something you can check.
The text to paste into the dashboard lives in **[LISTING.md](LISTING.md)** — this file is the
*procedure*, that file is the *content*.

Allow about 90 minutes for your first submission, most of it screenshots and the dashboard forms.

---

## Phase 0 — Name: done ✓

The extension is **Bulk Chat Delete for ChatGPT**. That follows the `<your name> for ChatGPT`
pattern both OpenAI's brand guidelines and Chrome Web Store policy expect, so the most common
rejection reason for an extension like this does not apply.

Do not change it after publishing — that means a fresh review, and the store URL keeps the slug
generated from the first name. If you ever do rename it, two places must move together: `name` in
`manifest.json`, and the `/Bulk Chat Delete/` regex in `tests/e2e.js:178` — Chrome names the content
script's isolated world after the extension, and the background-tab pacing test looks it up by name.

Go to Phase 1.

---

## Phase 1 — Verify the build (15 min)

### 1.1 Run the test suites

Needs Node, which is not installed on this machine — install it from <https://nodejs.org> first.

```bash
npm install
```

```bash
npm test
```

```bash
npm run test:e2e
```

`npm test` is fast and needs no browser. `npm run test:e2e` launches real Chromium against a mock
chatgpt.com and needs `openssl` on PATH (Git for Windows ships one). Do not ship a build with
failing tests.

### 1.2 Build the package

```bash
powershell -ExecutionPolicy Bypass -File tools\package.ps1
```

Produces `build/bulk-chat-delete-v<version>.zip` containing only `manifest.json`, `src/` and
`icons/`. It writes zip entry names with forward slashes on purpose — `Compress-Archive` uses
backslashes, and the store then reports *"Manifest file is missing or unreadable"*.

### 1.3 Smoke-test the exact zip you are about to upload

Do not skip this. It catches a broken package before a reviewer does.

1. Extract the zip to a scratch folder.
2. Open `chrome://extensions`, turn on **Developer mode**.
3. **Remove** any existing unpacked copy of this extension, so you are definitely testing the zip.
4. **Load unpacked** → select the extracted folder.
5. Open <https://chatgpt.com> and confirm: the trash tab appears, **Load my chats** works,
   `Ctrl+K` opens the palette, and archiving two chats then clicking **Undo** restores them.
6. Check `chrome://extensions` shows no errors for the extension.

---

## Phase 2 — Host the privacy policy (10 min)

The dashboard needs a **public URL**, not a file.

This is why there are two repositories: `vimalkhorajiya/Extensions` holds the source and stays
**private**, while `vimalkhorajiya/store` (this one) holds only the listing material and is made
**public**. Nothing of your code is exposed by publishing it.

1. `PRIVACY.md` already carries a real contact address. Change it first if you would rather not
   use that one — it becomes public in step 3.
2. Push this repo (GitHub Desktop → **Push origin**).
3. GitHub → `store` → **Settings** → **Danger Zone** → **Change visibility** → **Make public**.
4. Confirm in a private/incognito window that this loads without a login:
   `https://github.com/vimalkhorajiya/store/blob/main/PRIVACY.md`

Keep that URL handy — Phase 5 needs it.

*Alternative, if you would rather not make even this repo public:* paste `PRIVACY.md` into a public
gist at <https://gist.github.com> and use the gist URL instead. Either works.

---

## Phase 3 — Make the graphics (30 min)

Required: **at least one screenshot, 1280×800** (or 640×400), PNG or JPEG, no transparency.
Up to 5. Strongly recommended: a **440×280** small promo tile, which is what appears in search.

To shoot the UI without exposing your real chat titles, use the preview harness. It must be served
over HTTP — `file://` will not run the scripts:

```bash
npx serve .
```

Then open `http://localhost:3000/tests/preview.html` and use the buttons to reach each state.
Good screenshots, in order of usefulness:

1. The chat list with quick picks visible and a selection made
2. The Insights tab (activity chart + cleanup opportunities)
3. A job running — progress ring, stats, throughput
4. The command palette open
5. Settings

Crop or pad each to exactly 1280×800. Leave the browser chrome out.

---

## Phase 4 — Create the item (5 min)

1. Go to <https://chrome.google.com/webstore/devconsole>.
2. Confirm your **Account** page has a verified contact email — publishing is blocked without one.
3. **Add new item**.
4. Upload `build/bulk-chat-delete-v2.0.0.zip`.
5. Wait for the upload to parse. If it complains the manifest is missing, you zipped the parent
   folder instead of its contents, or used `Compress-Archive` — rebuild with `tools\package.ps1`.

The item is now a **draft**. Nothing is public until you submit and it is approved.

---

## Phase 5 — Fill the dashboard (25 min)

Four tabs down the left. Paste from [LISTING.md](LISTING.md).

### Store listing
- Name, short description, detailed description → LISTING.md §1
- Category: **Productivity** → Workflow & Planning
- Language: English
- Upload your screenshots and promo tile
- Privacy policy URL → the one from Phase 2

### Privacy
- **Single purpose** → LISTING.md §2
- **Permission justifications** — one box each for `storage`, `notifications`, and the host
  permission. Fill all three; a blank justification is an automatic rejection. → LISTING.md §2
- **Remote code:** select **"No, I am not using remote code."**
- **Data usage:** leave every collection category unchecked (the extension transmits nothing off
  the device), then tick all three certifications at the bottom.

### Distribution
- Visibility: **Public**, or **Unlisted** if you want to hand the link to a few people first.
  Unlisted still goes through full review, so it is a genuine dry run.
- Regions: all, unless you have a reason to limit.

### Payments
- Nothing to do; the extension is free.

**Save draft** as you go.

---

## Phase 6 — Submit (2 min)

1. Click **Submit for review**.
2. If a dialog offers "publish immediately once approved", accept it unless you want to control
   the launch moment yourself.

First review usually takes a few days. Extensions with broad host permissions can take longer.
You will get an email either way.

---

## Phase 7 — After submission

**If approved:** the listing goes live at `chrome.google.com/webstore/detail/<slug>/<id>`. Install
it yourself from the store and confirm it works as a store build, not just unpacked.

**If rejected:** the email names the exact policy clause. Fix it, then:

1. **Bump `version` in `manifest.json`** — the store permanently refuses a version number it has
   already seen, even from a rejected submission.
2. Rebuild: `powershell -ExecutionPolicy Bypass -File tools\package.ps1`
3. Upload the new zip to the same item and resubmit.

Most likely rejection reasons for this extension, in order:
- **Name implies affiliation with OpenAI** → rename per Phase 0.
- **Permission justification too vague** → the ones in LISTING.md are specific; use them verbatim.
- **Privacy policy URL unreachable** → check it in a private window.
- **Broad host permissions queried** → reply pointing out it is a single host and the extension's
  sole function; the detailed description already explains this.

### Shipping an update later

1. Make the change.
2. Bump `version` in `manifest.json` (e.g. `2.0.0` → `2.0.1`).
3. `powershell -ExecutionPolicy Bypass -File tools\package.ps1`
4. Dashboard → your item → **Package** → upload new zip → **Submit for review**.

Updates reach existing users automatically within a few hours of approval. Note that
`chrome.storage.local` survives updates — so if you ever rename the `cbd.*` storage keys, existing
users lose their settings and any unfinished job queue.
