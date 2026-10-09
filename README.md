# digital-cleanup

Two Claude Code skills for a digital spring clean:

- **gmail-inbox-cleanup**: unsubscribes from newsletters via Gmail's *Manage subscriptions*, clears Promotions, Social, Updates, Forums and Purchases, and archives old mail until you reach inbox zero.
- **gdpr-erasure-requests**: finds every webshop and service in years of email, looks up their privacy contact, and drafts GDPR Art. 17 erasure requests (English and Dutch templates). It sends them only after you approve, then tracks the replies against the one-month deadline.

Nothing is sent, deleted or submitted without your explicit OK. The skills never type passwords, solve CAPTCHAs or upload ID.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [Claude in Chrome](https://claude.com/chrome), logged in to the Gmail account you want to clean up

## Install

```
/plugin marketplace add <github-user>/digital-cleanup
/plugin install digital-cleanup@digital-cleanup
```

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
