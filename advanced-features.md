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
  `{{customer_name}}`, `{{customer_email}}`, `{{order_name}}`, `{{quote_id}}`,
  `{{item_count}}`, `{{total}}`, `{{shop}}`. Leave it empty for the default.
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

## Analytics

Quote events fire on **every** plan as DOM events on `window`, so your theme or
tag manager can listen for them:

`easyquotes:add_to_quote`, `remove_from_quote`, `view_quote`, `quote_submitted`,
`cart_converted_to_quote`.

Each carries GA4-shaped `items`, `value` and `currency`. On Pro the same events
are also pushed to `dataLayer` and `gtag()`.
