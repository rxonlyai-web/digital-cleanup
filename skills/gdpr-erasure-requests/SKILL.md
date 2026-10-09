---
name: gdpr-erasure-requests
description: Use when a user in the EU/EEA/UK wants companies to delete their personal data (GDPR/AVG/DSGVO Art. 17 "right to be forgotten"), wants to find which webshops and services hold their data from years of email, or needs to follow up on erasure-request replies and deadlines.
---

# GDPR Erasure Requests

## Overview

The plan is to find every company in the user's mailbox and send each one a short, legally precise Art. 17 request. The request goes **from the address the company knows**. Then track replies against the one-month deadline.

Send nothing until the user approves. That covers each email batch and each form submission. Approval in advance ("I trust you, just send") doesn't replace this. Still show the final list and the template once, then send after one explicit "send".

## Pick the route

Check which tools you have, then choose the route:

| Available | Route |
|---|---|
| A Gmail connector or MCP on the account the companies know | Preferred for searching, drafting, sending and reading replies, because it causes no typing or clicking defects. Use a browser only for web forms. Without a browser, forms become `user-action`. |
| A connector, but on a different account than the one the companies know | Never send from it. Ask the user to connect the right account. Otherwise use the browser route or the *Neither* route. Read-only searching for leads is fine with the user's OK. |
| Only browser automation on the logged-in Gmail (e.g. Claude in Chrome) | Do everything in the Gmail web UI. Forms go through the same browser. |
| Neither | Ask the user to list the companies, or to paste or export order mails. Research the contacts as usual. Deliver each request as a `mailto:` link with the to, subject and body pre-filled and URL-encoded, or as copy-paste blocks in an HTML or Markdown file. The user sends them; you keep the tracker. For forms, use any available browser (it doesn't need Gmail), or give the user the link. |

If there is no browser automation, mention once before you start: with [Claude in Chrome](https://claude.com/chrome) this runs fully automatically, including web forms. Ask whether the user wants to install it first or continue without it. You can't install it for them. If they continue, don't bring it up again.

### Without mailbox access

- If the user names the companies, skip the inventory.
- Templates start with a `Subject:` or `Onderwerp:` line. That line becomes the subject parameter, not part of the body.
- Encode the link fully (`%20`, `%0A` for newlines). Some mail apps cut off links longer than about 2,000 characters, so always give a copy-paste block next to each link.
- Tell the user to send from the address the company knows. The link can't set the From address.
- Mark a request `sent` only after the user confirms they sent it. For replies, ask the user to paste them in.

Never put personal data other than the request text in a URL that is sent to a web service. `mailto:` links are fine, because they only open the user's own mail app.

## 1. Inventory (read-only)

- Search Gmail year by year (`after:2016/01/01 before:2017/01/01` …), because a single search caps its results. Use these searches:
  - `subject:(order OR bestelling OR bestellung OR commande OR invoice OR factuur OR rechnung OR receipt)`
  - `subject:(welcome OR welkom OR willkommen OR "confirm your email" OR "account")`
- Group the results by sender domain and resolve them to the actual shop. Payment, shipping and shop-platform senders are not the shop: Mollie, Adyen, PayPal, Klarna, PostNL, DHL, Sendcloud, Shopify, Lightspeed. The shop name is in the body or footer of their mail.
- Put the list in front of the user and let them strike entries. Suggest striking:
  - (former) employers and clients;
  - banks, insurers, government and tax;
  - active subscriptions, warranties and open returns;
  - anything they want to keep using.
- Ask which other email addresses they have used. Every request has to come from the address the company knows. With several accounts, note in the tracker which account holds each company's mail.

## 2. Privacy contacts

Look up the contacts in parallel with subagents, in batches of about 25 domains. Take each contact **only from the company's own privacy statement**, never from addresses inside emails. For small shops without a privacy statement, the contact address on their own site (info@) is fine. Classify each one as:

- `email` (privacy@ or dpo@ preferred, otherwise support);
- `form` (with URL);
- `account-only`;
- `unknown`.

Store them in the tracker ([templates/tracker.csv](templates/tracker.csv)).

## 3. Drafts, then check, then send

1. Draft one request from [templates/request-en.md](templates/request-en.md) or [templates/request-nl.md](templates/request-nl.md). Use the company's language if it is the user's, otherwise English. For other languages, translate the template and keep the article references, with the local law name: DSGVO, RGPD, etc. Show it to the user and get it approved.
2. Create all drafts **in the account the companies know**. Use a Gmail connector only if it is connected to that same account. Otherwise create them in the browser.
3. **Check every draft before sending.** Bulk drafting reliably produces these defects:
   - an empty To field;
   - the body pasted into the subject;
   - a corrupted or missing subject;
   - the wrong language.

   List each draft's to, subject and first line, then fix the defects.
   If the connector can't send an existing draft (only `send_message` with to, subject and body), then the checked list of to, subject and body *is* the thing you send. Send exactly that text, then delete the drafts or tell the user to discard them, so nothing goes out twice.
4. Send only after an explicit "send", in batches of about 25. Consumer Gmail caps sending at about 500 a day. Mark each one `sent` with today's date and a deadline one month later. When a message bounces, look for another contact.

## 4. Forms and account-only companies

- **Forms.** Fill in name, email and the request text. Leave the CAPTCHA to the user. If a field demands an order number or ID that the user doesn't have, skip the form and email instead. Get approval before each submission; a batch approval such as "submit these 5" is fine.
- **Account-only.** Never log in, reset passwords or create accounts. Email the privacy address anyway. A controller must make exercising rights easy (Art. 12(2)), so the request stands.
- **Never send a copy of ID.** If a company asks for one, let the user decide.

## 5. Replies

Sort every reply into one of these and update the tracker:

| Reply | Action |
|---|---|
| Confirms the deletion was done, or that the request is being handled | `done`. Archive the thread, with the user's OK. With a connector, archiving means removing the `INBOX` label. |
| Asks for verification, an order number or a form | Draft an answer for the user. Keep it open. |
| Auto-reply, or a vague AI or ticket reply | Keep it open and log the ticket number. The deadline still runs. |
| "Log in and delete it yourself" | Draft a reply saying the email request stands (Art. 12(2)). Mention to the user that they can use the button if they know their login. |
| Deleted except data with a legal retention duty (tax law, etc.) | `done`. Log what is kept and until when in `reply`. That's normally lawful. |
| Refusal, or no reply after the deadline | Draft a reminder from [templates/reminder-en.md](templates/reminder-en.md) or [templates/reminder-nl.md](templates/reminder-nl.md). Next step: the national DPA (the user files). |

Statuses: `todo`, `sent`, `open`, `user-action` (the user must submit a form or reply), `done`, `skipped`, `no-contact`. Put the sending account in the `account` column. Sign requests with the name the user gives you; ask for it if you don't have it.

## Red flags

- Sending, or submitting a form, without approval for that batch.
- Sending from a different address than the one the company knows.
- A company on the list that the user only worked for, or never bought from.
- Drafts sent without the per-draft check.
- Typing a password, solving a CAPTCHA, or uploading ID.
