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

## Sold-out products

**Allow quotes for sold-out products** — on by default. A quote is often exactly
how a shopper asks about something that isn't in stock: a backorder, a lead
time, a made-to-order run.

Switch it off and the Add to quote button reads **Unavailable** and can't be
used, on product pages and in collection grids alike.

If you use the grid *snippet* rather than the block, add
{% raw %}`data-available="{{ card_product.available }}"`{% endraw %} to it so a
sold-out card says so immediately instead of only when someone clicks.

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

## Where the integrations went

Email notifications, Klaviyo, webhooks and Google Analytics live on their own
page now — **[Advanced features]({{ '/advanced-features/' | relative_url }})**. They
are wired up once and then left alone, so they were pushed below the settings
you change week to week.

## Shopify Markets

Easy Quotes follows the market a shopper is browsing in.

- Prices in the drawer and on the quote page are shown in that market's
  currency.
- A market with its own price list is quoted at **that** price, not your base
  price.
- The draft order is created in the shopper's currency, so the invoice you send
  matches the quote they saw.
- The country list on the quote form is built from your markets' countries
  rather than every country in the world.

**One thing to check:** the currency has to be enabled on your store. If a
shopper quotes in a currency you haven't enabled, Easy Quotes still creates the
quote — in your store's currency — and notes it on the quote so you know why.

On the dashboard, quote totals show the shopper's currency, with the estimate in
your own currency underneath when they differ. The summary figures at the top
are always in your store's currency, so they can be added up.

## Languages

Easy Quotes ships translated into **English, Spanish and French**. If your
storefront is in one of those languages, the quote drawer, form and buttons are
translated with nothing to set up.

Everything else — and any wording you'd rather change — is editable in
**Shopify admin → Settings → Languages → Easy Quotes**. Anything you leave
alone keeps the shipped wording, and any language not listed above falls back
to English until you translate it there.

Your own text (form labels, help text, button wording) is separate: translate
it per form under **Forms → Translations**.

## On the draft order

Every quote creates a draft order, and Easy Quotes adds a **Quote details**
card to it showing:

- when the quote was submitted, and when it expires
- the shopper's email, phone, linked customer and address
- the quoted total (in the shopper's currency, with your own alongside it on a
  Markets store)
- every answer from your form, under your own field labels

If you don't see the card, add it from **Add app block** on the draft order
page.

## Hide on product pages

One group controls what Easy Quotes takes off a product page, and on which
products.

**Apply to** is the scope:

| Option | Effect |
| --- | --- |
| Nothing | The theme is left exactly as it is (the default) |
| Products with a tag | Only products carrying the tag you name |
| Every product | All of them |

Then tick what to hide: **the price**, **the Add to cart button**, **the Buy it
now button** — any combination.

If something is still showing, your theme names it differently. Add its CSS
selector under **Extra CSS selectors**; find it with your browser's inspector.

**Nothing is hidden from shoppers who can't request a quote.** If you've
limited quoting to logged-in or tagged customers, everyone else keeps the price
and the buttons — otherwise they'd be left with no way to buy.

This replaces two older settings that each did half the job: a price-hiding
option keyed on the quotable-products tag, and a separate "quote-only product
tag" that hid Add to cart. Your existing choices were carried across.
