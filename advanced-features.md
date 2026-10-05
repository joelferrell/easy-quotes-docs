---
title: Advanced features
nav_order: 7
---

# Advanced features

**Easy Quotes → Advanced.** The integrations you set up once and then leave
alone: email notifications, Klaviyo, an outgoing webhook and Google Analytics.
They sit apart from Settings because those are day-to-day storefront choices
and these are plumbing.

## Notifications

**Send new quote notifications to** — where each new request is emailed. Replies
go straight to the shopper who asked, so hitting reply in your mail client
starts the conversation.

On **Pro** you also get:

- **Also send to** — extra recipients, comma separated. Everyone named gets the
  one email, not one each.
- **Subject line** — your own, with tokens filled in per quote:
  {% raw %}`{{customer_name}}`, `{{customer_email}}`, `{{order_name}}`,
  `{{quote_id}}`, `{{item_count}}`, `{{total}}`, `{{shop}}`{% endraw %}. Leave
  it empty for the default. An unknown token is refused when you save, and the
  message names the ones that work.
- **Opening note** — a line for your team above the quote summary. The shopper
  never sees it.

## Klaviyo (Pro)

Paste a Klaviyo **private API key** (it starts with `pk_`, from Klaviyo →
Settings → API keys) and every submitted quote sends a **Quote Submitted** event
to your account, carrying the shopper, the items, the total and their answers.
Build follow-ups, reminders and segments on it in Klaviyo as you would any other
event.

## Webhooks (Pro)

Every submitted quote is POSTed as flat JSON to a URL you choose — a Zapier
catch hook, Make, or your own endpoint. It runs after the draft order exists, so
the payload has everything.

The URL must be `https`. **Send test** posts a real-shaped payload marked
`quote.test`, so the receiving app can learn your fields before a real quote
arrives. Failures are recorded and shown here, and can never affect a shopper.

## Google Analytics

Quote events fire on **every** plan as DOM events on `window`, so your theme or
tag manager can listen for them without the app knowing anything about your
setup:

`easyquotes:add_to_quote`, `remove_from_quote`, `view_quote`, `quote_submitted`,
`cart_converted_to_quote`.

Each carries GA4-shaped `items`, `value` and `currency`. On **Pro** the same
events are also pushed to `dataLayer` and `gtag()`.

### The measurement ID

Leave it blank if GA4 already loads on your storefront — through Google Tag
Manager, or Shopify's Google & YouTube channel. The events are sent either way,
and a second copy of GA4 would double-count them.

Fill it in and Easy Quotes loads GA4 for you, which is what you want if it isn't
on your storefront already.

### Consent

When Easy Quotes loads GA4 itself, it waits for the shopper's consent first,
using Shopify's own Customer Privacy API:

- Consent already given → GA4 loads immediately.
- Not yet answered → GA4 loads only if the shopper then accepts.
- **Your theme has no privacy API at all → GA4 is never loaded.**

That last one is deliberate rather than a limitation. A store with no consent
banner is usually a store that hasn't set one up, and loading a tracker for
every visitor there would be your legal exposure, not ours. If you need GA4 in
that situation, add a consent banner — Shopify's own privacy settings provide
one — or load GA4 through your theme and leave this field blank.

## Slack (Pro)

Get a message in a channel the moment a quote arrives — who asked, what for,
the total, and a button straight to the draft order.

### Create the webhook

1. Go to [api.slack.com/apps](https://api.slack.com/apps) and choose
   **Create New App → From scratch**. Name it anything — "Easy Quotes" is fine
   — and pick your workspace.
2. In the left sidebar, open **Incoming Webhooks** and switch **Activate
   Incoming Webhooks** on.
3. Scroll down and choose **Add New Webhook to Workspace**.
4. Pick the channel the quotes should land in, and **Allow**.
5. Copy the webhook URL Slack shows you.

### Connect it

Paste the URL into **Advanced features → Slack** and **Save**. Then use **Send
test** — it posts a sample quote to your channel straight away, so you can
confirm the channel and the formatting before a real one arrives.

The button stays disabled until you save, because it sends the saved URL rather
than what's currently typed.

> **Two Slack features look alike.** The URL must begin
> `https://hooks.slack.com/services/`. Slack's **Workflow Builder** hands out
> `/triggers/` and `/workflows/` URLs instead — a different API, which Easy
> Quotes will refuse. If your URL is rejected, this is almost always why.

### What the message contains

The shopper's name, the total, the first ten items, and a button to the draft
order. Longer quotes are truncated with "…and N more" rather than filling the
channel.

Form answers are deliberately left out — a channel isn't the place for a
customer's full submission, and the draft order has all of it.

### Changing the channel

Webhooks are tied to one channel. To move the notifications, create a second
webhook in Slack pointing at the new channel and paste that URL in instead.

## HubSpot (Pro)

Push each shopper into your CRM as a contact, with their quote attached to the
timeline — so quotes live where the rest of your pipeline does.

### Create the private app

1. In HubSpot, open **Settings → Integrations → Private Apps → Keys → Service Keys** and choose
   **Create service key**.
2. Name it (again, "Easy Quotes" is fine).
3. On the **Scopes** tab, tick `crm.objects.contacts.write`.

   That single scope is all you need. HubSpot's Notes API runs on the contacts
   scope, so there is no `crm.objects.notes.write` to look for — ticking write
   also enables read, which the contact upsert needs.
4. Create the app and copy its **access token**. It starts with `pat-`.

### Connect it

Paste the token into **Advanced features → HubSpot** and **Save**.

There's no *Send test* button here on purpose: a test would create a real
contact and a real note in your CRM. To check it, submit a quote on your own
storefront and look that email up in HubSpot.

### What happens on each quote

Two things, in order:

1. **The contact** is created or updated, matched on **email address** — so a
   returning customer updates their existing record instead of creating a
   duplicate. Name, phone and company are filled in when the shopper gave them.
2. **A note** is attached to that contact's timeline with the items, every form
   answer, and a link to the draft order in Shopify.

If the contact saves but the note doesn't, the contact is kept — you still get
the customer. The app records that as "contact only".

### Your keys are encrypted

Your Slack webhook URL, Klaviyo API key and HubSpot token are encrypted with
AES-256-GCM before they're written to our database, and only decrypted at the
moment a quote is sent to that service. Nobody — including us — can read them
out of a database backup.

One consequence worth knowing: because they're stored encrypted rather than
hashed, we can still show them back to you on the Advanced features page, but
if a key is ever reported as unreadable, paste it again rather than trying to
repair it.

### Neither can break a quote

Slack and HubSpot both run *after* the quote is saved and the draft order
created. If either is down, slow, or misconfigured, the quote still goes
through and the shopper sees nothing wrong. The failure is logged for you
instead.
