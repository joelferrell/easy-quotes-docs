---
title: Troubleshooting
nav_order: 9
---

# Troubleshooting

In rough order of how often each one is the answer.

## Nothing from Easy Quotes appears at all

**Check the app embed is on.** Online Store → Customize → App embeds → Easy
Quotes. It loads the script and carries your settings; blocks and snippets both
depend on it.

If it's on and there's still nothing, check **Settings → who can request a
quote**. If it's set to logged-in or tagged customers, a guest sees your store
with no quote UI at all — that's working as intended.

## The button is there but clicking it does nothing

Open your browser console on that page. Easy Quotes logs a warning naming the
block and what it found. The usual cause is that the block can't tell which
product it's for.

- **On a product page** — make sure the block is inside your product section,
  not in a standalone section above or below it.
- **In a product grid** — on themes that don't accept app blocks in product
  cards, use the grid snippet instead. See
  [Theme setup]({{ '/theme-setup/' | relative_url }}).
- **Anywhere else** — pick a product in the block's own settings.

In the theme editor, a block that can't work out its product says so in place of
the button. Only you see that message.

## The quote link is floating when I asked for it beside the cart

Easy Quotes looks for your theme's cart link in the header. If it can't find
one — some themes build headers unusually — it falls back to a floating button
rather than showing nothing.

Fix it by placing the link yourself: add the **Quote link** block to your
header, or paste the `easy_quotes_quote_link` snippet where you want it, then
set **Quote link placement** to *Don't add a link*.

## A colour I set isn't applying

**On an Outline button, Background color can't show as a fill** — there isn't
one. It tints the border and text instead, and Text color overrides that tint.
Switch Button style to **Solid** if you want a filled button.

Otherwise, check what's setting the same value elsewhere. Easy Quotes applies
styles in this order, each winning over the one before:

1. The app's default stylesheet
2. **Design → Styles**
3. A block's own settings, for that one placement
4. **Design → Custom CSS**, and a block's own Custom CSS

## Submitting says it worked but no draft order appears

Check **Easy Quotes → Quotes** in the app. A failed quote is still recorded
there with the reason, which is usually a product or variant that's no longer
available.

If the quote isn't listed at all, the submission never reached the app —
re-check the app embed, and look for errors in your browser console.

## The same element shows twice

You have both a block and a snippet for it on the same page. The snippet wins
and the block is hidden automatically, so this shouldn't happen — but if it
does, remove one. The theme editor flags the hidden block with a note.

## A quote arrived but I wasn't emailed

Check the address under **Advanced features → Notifications** first. If it's
set and nothing arrived, the app's email provider isn't configured or its
sending domain isn't verified — that's on the app's side rather than yours, so
get in touch.

Quotes are never lost to this: the request is recorded in the app and the draft
order is created either way.

## GA4 isn't recording quote events

If you filled in a measurement ID, Easy Quotes only loads GA4 once the shopper
has consented, via Shopify's Customer Privacy API — and never at all on a theme
with no privacy API. See
[Advanced features]({{ '/advanced-features/' | relative_url }}).

If GA4 already loads through Google Tag Manager or the Google & YouTube channel,
leave the measurement ID blank; the events are sent regardless, and a second
copy would double-count them.

## The draft order total doesn't match what the shopper saw

Easy Quotes always prices a draft order from your **current** Shopify prices. The
line items it sends carry only the product and the quantity, so Shopify works out
the value itself at the moment the quote is submitted.

The shopper's quote is kept in their browser, and it can sit there for days. So
that the two don't drift apart, Easy Quotes re-checks every item against your
store when the quote page or the mini quote opens: prices are brought up to
date, and any line whose price has changed since it was added says so under the
product name. Items that are no longer for sale are flagged there too, so they
can be removed before the form is filled in.

Two things can still put a gap between the figures:

- **A price changed in the last few moments** — between the shopper opening the
  page and pressing submit. The draft order gets the new price, which is the
  safer way round: a shopper's browser can't set what a draft order is worth.
- **The check couldn't run.** If a product can't be read — a dropped connection,
  say — Easy Quotes deliberately leaves that line showing the price the shopper
  already saw rather than blanking it or blocking the quote.

Nothing is wrong when this happens, and you're setting the final price before you
send the invoice anyway. If it's still causing awkward conversations:

- Let quotes expire sooner (**Settings → Quote validity**), so fewer sit around
  across a price change.
- Say so on your quote page — that prices are confirmed when you reply.

## I changed a setting and the storefront hasn't caught up

Settings publish to your storefront when you save. Reload the storefront page
rather than trusting a cached view. If it still looks stale, save the settings
page once more.

## Still stuck

Open **Support** in the app — it has the same answers plus a few more, and the
links to jump straight to the page that fixes them. Or email
**[help@canonicalscale.com](mailto:help@canonicalscale.com)**.

Have this ready and it'll go much faster:

- Your store's theme and whether the element is a block or a snippet
- The page URL it happens on
- Anything logged in your browser console on that page

## A customer is missing their phone number, or SMS marketing is off

Shopify won't let two customers share a phone number. If a shopper requests a
quote using a number that already belongs to another customer, Easy Quotes
creates the customer **without** the phone — and because Shopify needs a phone
on the customer before it will accept SMS marketing consent, the SMS opt-in
can't be applied either, even if the shopper ticked it.

The number isn't lost: it's on the draft order, so you can still call them.

The **Quote details** card on the draft order tells you when this happened,
under "Some details couldn't be saved". To fix it, find the other customer with
that number and remove or correct it, then add the number to the right
customer.

This is most common while testing, when several test quotes reuse one phone
number.

## Easy Quotes won't accept my Slack webhook URL

It has to be an **incoming webhook**, which starts with
`https://hooks.slack.com/services/`.

Slack's **Workflow Builder** produces `/triggers/` and `/workflows/` URLs
instead. Those are a different API and won't work here. Create the webhook from
your Slack app under **Incoming Webhooks → Add New Webhook to Workspace**.

## A quote came in, but nothing reached Slack or HubSpot

Work through these in order:

1. **Check your plan.** Both are Pro features. Below Pro the section shows an
   upgrade notice instead of the field, and your saved credential is kept, not
   deleted — upgrading restores it.
2. **Check it's saved**, not just typed. Slack's *Send test* button is disabled
   until you save, because it sends the stored URL.
3. **Use *Send test*** for Slack. If the test lands but real quotes don't,
   the quote itself is failing — check **Quotes** in the app.
4. **For HubSpot**, look the shopper's email up in your CRM. If the contact is
   there but the quote isn't on its timeline, the note failed; the app records
   that as "contact only". That usually means the private app is missing the
   `crm.objects.notes.write` scope.

Neither integration can delay or fail a quote, so a shopper never sees an error
from them. That also means a silent failure is possible — which is why the test
button exists.
