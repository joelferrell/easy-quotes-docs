---
title: Theme setup
nav_order: 3
---

# Theme setup

There are two ways to put Easy Quotes elements on your storefront. Use blocks
where you can, snippets where you can't.

## App blocks (no code)

In **Online Store → Customize**, add these wherever your theme accepts app
blocks:

| Block | Where it goes |
| --- | --- |
| Add to quote button | A product section, or a product card on newer themes |
| Quote form | The page you use as your quote page |
| Quote link | A header that supports app blocks |
| Convert cart to quote | Your cart page (Pro) |

Each block has its own settings — button style, spacing, colours, and its own
CSS classes and Custom CSS for that one placement.

## Snippets (full control)

Some themes don't accept app blocks everywhere — headers and product cards are
the usual gaps. For those, paste a placeholder into your theme code and Easy
Quotes fills it in:

```liquid
<div id="easy_quotes_add_to_quote"></div>
```

**Easy Quotes → Integration** lists every snippet with its options and a copy
button. A snippet takes precedence over the matching block on the same page, so
nothing is ever shown twice — and if you add both, the theme editor shows a note
on the hidden block explaining why. Only you see that note.

## Product grids

**Theme blocks (Horizon and later).** Their product cards accept app blocks and
pass the card's product down, so adding the **Add to quote** block inside the
product card gives you a button on every card — collection pages, search
results and recommendations — with no code.

**Older themes (Dawn).** Their cards don't accept app blocks, so use the grid
snippet instead. Paste it into your product card snippet (Dawn:
`snippets/card-product.liquid`):

```liquid
<div
  data-easy-quotes="add_to_quote"
  data-product-handle="{{ card_product.handle }}"
  data-product-tags="{{ card_product.tags | join: ',' | escape }}"
  data-button-text="Add to quote"
></div>
```

Two notes on that one:

- Your theme may call the card's product something other than `card_product` —
  check what the surrounding code uses.
- `data-product-tags` only matters if you've limited the button to tagged
  products in Settings. Without it the product is looked up on page load to
  check the tag, which is one request per card.

A grid card adds the product's **first available variant**, the same as a
theme's quick-add button. Shoppers who need to choose options can still open the
product page.

## After changing anything

Theme changes take effect immediately. App changes need a moment — if you've
just updated the app, reload the storefront page rather than trusting a cached
view.
