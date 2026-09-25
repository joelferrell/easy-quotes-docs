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
