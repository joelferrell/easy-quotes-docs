---
title: Troubleshooting
nav_order: 8
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
  [Theme setup]({{ site.baseurl }}/theme-setup/).
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

## I changed a setting and the storefront hasn't caught up

Settings publish to your storefront when you save. Reload the storefront page
rather than trusting a cached view. If it still looks stale, save the settings
page once more.

## Still stuck

Have this ready and it'll go much faster:

- Your store's theme and whether the element is a block or a snippet
- The page URL it happens on
- Anything logged in your browser console on that page
