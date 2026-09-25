---
title: Settings
nav_order: 6
---

# Settings

**Easy Quotes → Settings.**

## Who can request a quote

| Mode | Who sees the quote button and link |
| --- | --- |
| Everyone | Any shopper |
| Logged-in customers | Guests see your store as normal, with no quote UI at all |
| Customers with a tag | Trade or wholesale accounts you approve yourself |
| B2B customers | Shoppers buying on behalf of a company |

Shoppers the rule excludes see your store exactly as it was, with prices and
Add to cart intact — they're never left with no way to buy.

## Prices and Add to cart

**Hide the theme's price on** — no product pages, tagged products only, or every
product page. If your theme puts the price somewhere unusual, add an extra CSS
selector and the app will hide that too.

**Quote-only tag** — products with this tag lose Add to cart entirely, so the
only route is a quote. Kept separate from the price setting, so hiding a price
and making something unbuyable stay independent decisions.

Prices stay visible for shoppers the visibility rule above excludes, since they
still need to be able to buy.

## Product tag

Set a tag and optionally limit the Add to quote button to products carrying it.
Useful when only part of your catalogue is quotable.

## Convert cart to quote (Pro)

Lets a shopper who has already filled their cart turn it into a quote request
instead. The cart's items move into their quote and they finish on your quote
page. Add the **Convert cart to quote** block to your cart page, or paste the
snippet.

## Quotes and draft orders

- **Draft order tag** — how Easy Quotes marks its draft orders in Shopify, so
  you can filter for them.
- **Quote validity** — how many days a quote is good for.
- **Default country** — pre-selects the country field for shoppers.
- **Notification email** — where new quote requests are announced.

## Marketing opt-ins (Pro)

Add email and SMS opt-in checkboxes to your quote form. Anyone who ticks one is
subscribed in Shopify, with their consent recorded properly.

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
