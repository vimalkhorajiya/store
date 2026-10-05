# Privacy Policy — Bulk Chat Delete for ChatGPT

**Last updated: 5 October 2026**

Bulk Chat Delete for ChatGPT is a browser extension that helps you delete, archive or unarchive your own
ChatGPT conversations in bulk.

## The short version

**The extension does not collect, transmit, sell or share any of your data.** It has no servers, no
analytics, no telemetry and no third-party services. Everything it does happens inside your own
browser, against chatgpt.com, using the session you are already signed in to.

## What the extension accesses, and why

| Data | Why | Where it goes |
|---|---|---|
| Your chat list (titles, dates, IDs, archived/pinned state, project names) | To show you the list so you can choose what to delete or archive | Held in your browser's memory while the panel is open. Never transmitted anywhere. |
| Your ChatGPT authentication headers (including the `Authorization` bearer token) | To make the same delete/archive requests to chatgpt.com that the ChatGPT web app itself makes, as you | Kept **in memory only**, for the lifetime of the page. Never written to disk, never transmitted to any destination other than chatgpt.com. |
| Your settings (pace profile, safety options, panel layout) | To remember your preferences | `chrome.storage.local`, on your device only. |
| An unfinished job's queue (chat IDs and titles) | So an interrupted job can resume after a reload or crash | `chrome.storage.local`, on your device only. Cleared when the job finishes. |

The extension never reads the **contents** of your conversations — only the metadata listed above.

## Files the extension creates

When you use Export, or when "Save a backup before deleting" is enabled, the extension generates a
JSON, CSV or Markdown file and hands it to your browser's normal download flow. These files contain
chat titles, links and dates — never message content. They are saved to your computer, and the
extension does not upload them or retain a copy.

## Network requests

The extension makes requests to `https://chatgpt.com` (and `https://chat.openai.com`) only. It makes
no requests to any other host. It loads no remote code: all of its JavaScript ships inside the
extension package and is reviewable in the source.

## Permissions

- **storage** — saves your settings and an unfinished job's queue on your device.
- **notifications** — shows a desktop notification when a long job finishes or needs your attention.
  Off by default; only used if you turn it on in Settings.
- **Access to chatgpt.com / chat.openai.com** — the extension's entire purpose. It reads your chat
  list and sends the delete/archive requests on those sites.

## Data retention and deletion

Everything the extension stores lives in `chrome.storage.local` on your device. Removing the
extension deletes all of it. You can also clear the learned pacing data from Settings at any time.

## Children

The extension is not directed at children and collects no data from anyone.

## Changes

If this policy ever changes, the updated version will be published at this URL and the date above
will be updated.

## Contact

Questions or concerns: **vimalkhorajiya@gmail.com**

---

*Bulk Chat Delete for ChatGPT is an independent project. It is not affiliated with, endorsed by, or sponsored
by OpenAI. "ChatGPT" and "OpenAI" are trademarks of OpenAI.*
