# Publish Work & Presence for greytHR — step by step

You have done this once already for Bulk Chat Delete, so this is the short version. Everything
that does not need your accounts is ready.

**Already done:**

| | |
|---|---|
| ✅ | Name — `Work & Presence for greytHR` (trademark last, as reviewers expect) |
| ✅ | Original icon — the old purple "g" resembled greytHR's own and would read as impersonation |
| ✅ | Permissions trimmed to `storage`, `alarms`, `notifications` + `*.greythr.com` |
| ✅ | Package built — `build/greythr-work-presence-v2.0.0.zip` |
| ✅ | Tests — 49/49 passing |
| ✅ | Five 1280×800 screenshots and both promo tiles, 24-bit, sample data only |
| ✅ | Privacy policy, listing copy, and paste-ready Privacy-tab answers |

---

## Step 1 — Publish the privacy policy (3 min)

The policy is in the public `store` repo under `work-presence/`, next to the Bulk Chat Delete
one. Push it: **GitHub Desktop → `store` → Push origin.**

If you have not yet made `store` public (Settings → Danger Zone → Change visibility → Public),
do it now — it holds no source code.

**Done when** this opens in an incognito window without signing in:
```
https://github.com/vimalkhorajiya/store/blob/main/work-presence/PRIVACY.md
```

## Step 2 — Add the item (3 min)

<https://chrome.google.com/webstore/devconsole> → **Add new item** → upload:
```
D:\Vimal\Development\Extensions\work-time-extension\build\greythr-work-presence-v2.0.0.zip
```
Your publisher email is already verified from last time.

## Step 3 — Store listing tab (10 min)

From **[LISTING.md](LISTING.md)** §1: name, short description, detailed description, category
**Productivity**, language English. Upload the five screenshots in numbered order and both promo
tiles. Paste the privacy URL from Step 1. **Save draft.**

## Step 4 — Privacy tab (5 min)

Open **[PRIVACY-TAB.txt](PRIVACY-TAB.txt)** and paste block by block:
- Single purpose
- **Four** justifications: `storage`, `alarms`, `notifications`, host permission
- Remote code → **No**
- Data usage → all nine boxes **unchecked**, all three certifications **ticked**

**Save draft.**

## Step 5 — Submit

**Distribution** → Public → **Submit for review.**

---

## If it is rejected

Fix what the email names, then change `"version"` in `manifest.json` (e.g. `2.0.0` → `2.0.1`),
run `npm run package`, and upload the new zip. The store refuses any version number it has seen
before — including a rejected one.

## One thing worth knowing before you publish

The extension relies on greytHR's attendance page staying roughly as it is. The scraper tries
greytHR's current markup first and falls back to scanning table rows for IN/OUT and a time, so a
class rename will not break it — but a complete redesign of that page could. If figures ever stop
appearing after a greytHR update, that is the first place to look.
