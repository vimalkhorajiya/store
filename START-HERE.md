# Publish to the Chrome Web Store — step by step

Everything that can be prepared is prepared. Below is only what needs your accounts.

**Already done:**

| | |
|---|---|
| ✅ | Name settled — `Bulk Chat Delete for ChatGPT` (safe under OpenAI's brand rules) |
| ✅ | Upload package built and verified — `bulk-chat-delete-v2.0.0.zip` |
| ✅ | Unit tests 9/9 passing; pacing simulation passing on all 18 scenarios |
| ✅ | Five 1280×800 screenshots, generated from sample data |
| ✅ | Listing copy, permission justifications, privacy policy — written |
| ✅ | Code committed and pushed to the private `Extensions` repo |

**The setup — two repositories, on purpose:**

- `vimalkhorajiya/Extensions` — **private**. Your source code. Stays private.
- `vimalkhorajiya/store` — **public**. Only this listing material, because Google must be able to
  read the privacy policy without logging in.

---

## Step 1 — Push this `store` repo (3 min)

The files are committed locally but not on GitHub yet. Pushing needs your login.

**Do:**
1. Open **GitHub Desktop**.
2. If `store` is not in the repository list: **File → Add local repository →**
   `D:\Vimal\Development\store` → Add.
3. Select it, then click **Push origin** in the top bar.

**Done when:** <https://github.com/vimalkhorajiya/store> shows `PRIVACY.md`, `README.md` and the
`screenshots` folder.

---

## Step 2 — Make this repo public (1 min)

**Do:** GitHub → the `store` repo → **Settings** → scroll to the bottom (**Danger Zone**) →
**Change visibility** → **Make public** → confirm by typing the repo name.

**Done when:** this link opens in a **private / incognito window** and shows the policy, with no
sign-in prompt:

```
https://github.com/vimalkhorajiya/store/blob/main/PRIVACY.md
```

**Copy that link — Step 4 needs it.**

> Your `Extensions` repo stays private. Only this one becomes public, and it holds no source code.

---

## Step 3 — Open the developer dashboard (3 min)

**Do:**
1. Go to <https://chrome.google.com/webstore/devconsole>
2. Click **Account** in the left sidebar. Check your contact email shows **Verified** — publishing
   is blocked without it.
3. Click **Add new item**.
4. Upload the zip:

```
D:\Vimal\Development\Extensions\chat-bulk-delete-extension\build\bulk-chat-delete-v2.0.0.zip
```

**Done when:** the upload is accepted and the listing form opens. Nothing is public yet — it stays a
draft until Step 6.

*If it says "Manifest file is missing or unreadable", the zip was rebuilt the wrong way. Rebuild
with* `powershell -ExecutionPolicy Bypass -File tools\package.ps1` *and upload again.*

---

## Step 4 — Store listing tab (10 min)

Open **[LISTING.md](LISTING.md)** section 1 beside the dashboard and copy each field across.

| Field | Value |
|---|---|
| Name | `Bulk Chat Delete for ChatGPT` |
| Short description | the one-line block in LISTING.md |
| Detailed description | the long block in LISTING.md |
| Category | **Productivity** |
| Language | English |
| Screenshots | all five PNGs from `screenshots/`, in numbered order |
| Privacy policy URL | the link from Step 2 |

**Done when:** no red warnings on the tab. Click **Save draft**.

---

## Step 5 — Privacy tab (10 min)

This is the tab that causes most rejections. Do not leave anything blank.

Copy from **[LISTING.md](LISTING.md)** section 2:

1. **Single purpose** — the one-paragraph statement.
2. **Permission justifications** — three separate boxes:
   - `storage`
   - `notifications`
   - host access to `chatgpt.com`

   **All three must be filled in.** An empty justification is an automatic rejection.
3. **Remote code** — select **"No, I am not using remote code."**
4. **Data usage** — leave every "collected data" checkbox **unchecked** (the extension transmits
   nothing off the device), then tick the **three certification boxes** at the bottom.

**Done when:** all three justifications have text and the three certifications are ticked.
Click **Save draft**.

---

## Step 6 — Submit (2 min)

**Do:**
1. **Distribution** tab → Visibility **Public** → Regions: all.
2. Click **Submit for review**.

**Done when:** the item shows **Pending review**. Google emails you in a few days.

That is the whole process.

---

## If Google rejects it

The rejection email names the exact policy clause. Fix it, then — **before re-uploading**:

1. In `manifest.json`, change `"version": "2.0.0"` to `"2.0.1"`.
2. Rebuild:

```bash
powershell -ExecutionPolicy Bypass -File tools\package.ps1
```

3. Upload the new zip to the **same** listing and submit again.

**Bump the version every single time.** The store permanently refuses a version number it has
already seen, even from a rejected submission. This is what people most often get stuck on.

## Releasing an update later

Change the code → bump `version` → rebuild → dashboard → your item → **Package** → upload →
**Submit for review**. Existing users update automatically within a few hours of approval.

---

## Two things worth knowing

**Your extension's code is readable by anyone, whatever you do with GitHub.** Chrome extensions ship
as plain JavaScript; Chrome unpacks them into the user's profile folder, and free "CRX viewer" sites
let anyone browse any published extension's source straight from its store URL. The Web Store also
*forbids* obfuscated code. Keeping `Extensions` private still hides your commit history, tests and
tooling — but not the shipped extension itself.

**`vimalkhorajiya@gmail.com` is in the privacy policy** and becomes public at Step 2. The store
requires a contact address, so one has to be public. If you would rather not use your personal
Gmail, change it in `PRIVACY.md` before you push.
