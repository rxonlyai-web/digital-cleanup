# Mail Doctor

Two Claude Code skills that cure a sick mailbox:

- **gmail-inbox-cleanup**: unsubscribes from newsletters via Gmail's *Manage subscriptions*, clears Promotions, Social, Updates, Forums and Purchases, and archives old mail until you reach inbox zero.
- **gdpr-erasure-requests**: finds every webshop and service in years of email, looks up their privacy contact, and drafts GDPR Art. 17 erasure requests (English and Dutch templates). It sends them only after you approve, then tracks the replies against the one-month deadline.

Nothing is sent, deleted or submitted without your explicit OK. The skills never type passwords, solve CAPTCHAs or upload ID.

## Requirements

- [Claude Code](https://claude.com/claude-code) (or another client that supports skills)
- **Recommended:** [Claude in Chrome](https://claude.com/chrome), logged in to the Gmail account you want to clean up
- **Alternative:** a Gmail connector. GDPR requests work fully with it. Inbox cleanup works, but slower and without one-click unsubscribing.
- **Neither?** The skills still help. Claude finds the privacy contacts and prepares every request as a ready-to-send `mailto:` link, and for inbox cleanup it guides you step by step.

## Install

### Claude Code

```
/plugin marketplace add rxonlyai-web/mail-doctor
/plugin install mail-doctor@mail-doctor
```

### Cowork (Claude desktop app)

1. In the sidebar, open **Customize → Plugins**.
2. Click **Add marketplace** and enter `rxonlyai-web/mail-doctor`.
3. Find **mail-doctor** and click **Install**.

On Team or Enterprise plans, your admin may restrict which plugins you can install.

### claude.ai (browser)

claude.ai takes skills one at a time, as ZIP files. You need a Pro, Max, Team or Enterprise plan, with code execution turned on.

1. Download the skills you want:
   - [gmail-inbox-cleanup.zip](https://github.com/rxonlyai-web/mail-doctor/releases/latest/download/gmail-inbox-cleanup.zip)
   - [gdpr-erasure-requests.zip](https://github.com/rxonlyai-web/mail-doctor/releases/latest/download/gdpr-erasure-requests.zip)
2. Go to **Settings → Capabilities → Skills**, click **Upload skill**, and choose the ZIP file.
3. Make sure each skill is switched on.

## Use

Just ask, for example:

- "Unsubscribe me from all newsletters and get my Gmail to inbox zero"
- "Find every shop I ordered from and send them a GDPR deletion request"
- "Go through the replies to my GDPR requests"

## Real-world result

A first run, on a personal Gmail with ten years of history:

- 83 newsletters unsubscribed;
- inbox zero;
- about 110 erasure requests sent or submitted in one afternoon;
- 13 companies confirmed the deletion the same day.

## Disclaimer

This is not legal advice. Erasure requests may lose you warranties, loyalty points or access to digital purchases. Check the list before you send.
