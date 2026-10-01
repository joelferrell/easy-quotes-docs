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

### Writing the quote link yourself

The `easy_quotes_quote_link` placeholder is replaced by Easy Quotes' own link.
If you'd rather keep your theme's icon and classes, write the anchor yourself
and add **`data-easy-quotes-link`** to it:

```liquid
<a href="/pages/quote" data-easy-quotes-open data-easy-quotes-link class="header__icon">
  …your theme's icon…
  <span data-easy-quotes="quote_count"></span>
</a>
```

That attribute is what tells Easy Quotes a quote link is already on the page, so
the **Quote link block** and the app embed's automatic placement stand aside
instead of adding a second one. Without it, your link is just a link as far as
the app can tell, and you end up with two quote links in the header.

`data-easy-quotes-open` on its own does **not** suppress them — it only makes
something open the quote drawer, which you may well want on a footer link while
the header block stays.

## Product grids

**Theme blocks (Horizon and later).** Their product cards accept app blocks and
pass the card's product down, so adding the **Add to quote** block inside the
product card gives you a button on every card — collection pages, search
results and recommendations — with no code.

**Older themes (Dawn).** Their cards don't accept app blocks, so use the grid
snippet instead. Paste it into your product card snippet (Dawn:
`snippets/card-product.liquid`):

{% raw %}
```liquid
<div
  data-easy-quotes="add_to_quote"
  data-product-handle="{{ card_product.handle }}"
  data-product-tags="{{ card_product.tags | join: ',' | escape }}"
  data-button-text="Add to quote"
></div>
```
{% endraw %}

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
