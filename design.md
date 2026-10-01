---
title: Design
nav_order: 5
---

# Design

**Easy Quotes → Design.** Four things, saved together.

## Header quote link

What shoppers click to open their quote from any page: the text, the icon
(built-in or your own upload), the icon size, whether the item count shows, and
whether to show the icon, the text, or both.

*Where* it sits is a separate choice, in the theme editor under **App embeds →
Easy Quotes → Quote link placement** — next to your cart icon, floating in a
corner, or nowhere if you'd rather place it yourself with the Quote link block
or snippet.

### Where the link goes

**Placement** decides how the link reaches your storefront:

| Option | What happens |
| --- | --- |
| Next to the cart icon | Added just after your theme's cart icon (the default) |
| Floating button | A pill in a corner of every page, above your theme's content |
| Don't add a link | Nothing is added — use the Quote link block, or your own link |

Choosing **Floating button** reveals a position setting: bottom right or bottom
left.

If you pick *Next to the cart icon* and Easy Quotes can't find your theme's cart
icon, it shows the floating button instead rather than nothing, so shoppers
always have a way to reach their quote.

This used to live in the theme editor under App embeds. It's here now, with the
link's other appearance settings.

## Mini quote

What opens when a shopper clicks that link:

| Style | Behaviour |
| --- | --- |
| Slide-in drawer | Slides in over a dimmed page. Every plan. |
| Panel under the header link | Drops down under the link, like a cart preview. Pro. |
| Slide in and push the page across | Moves the page over instead of covering it, so the shopper can keep browsing. Pro. |

The push style falls back to the slide-in drawer below 990px, where there's no
room to push anything aside.

Every style closes the same way: click anywhere outside the panel, press
Escape, or use the Close button. With the push style the page beside the drawer
stays usable, so a click that lands on a link closes the drawer **and** follows
the link — and clicking an Add to quote button adds the item without the drawer
closing first.

## Motion

Two settings, both under **Styles → Motion**:

- **Section animation** — how the quote form's accordion sections open and
  close.
- **Drawer animation** — how the mini quote opens: the slide-in drawer, the push
  drawer and the popover all follow it.

Each offers **Animated** or **Instant**. Leaving one empty keeps the animated
default.

Shoppers whose device asks for reduced motion always get the instant version,
whatever you set here.

## Styles

Colour and size pickers for everything Easy Quotes draws: headings, body text,
secondary text, links, errors, accent, drawer background, borders, corner
radius, and a full set of button styles including hover.

**Anything left empty follows your theme.** You only fill in what you want to
change.

Any colour can point at one of your theme's own CSS variables instead of a fixed
colour, so Easy Quotes tracks your palette when you change it. Choose **Use a
theme variable** and enter one of:

- `var(--color-primary)`
- `var(--color-button, #1a1a1a)` — with a fallback
- `rgb(var(--color-foreground))` — the bare-triplet form Dawn uses
- `--color-primary` — a bare name, which the app wraps in `var()` for you

## Theme button classes

The fastest way to make Easy Quotes buttons look like your theme's, with no
theme code to edit. Enter the classes your theme puts on its own buttons and
they are added to:

- every **Add to quote** button — product pages, product grids, theme blocks and
  the pasted snippets alike
- the **Convert cart to quote** button

Separate several with spaces. Dawn and Horizon both call theirs `button`; some
themes use `btn`, and many add a modifier such as `button--primary`.

**To find yours:** open your storefront, right-click your theme's Add to cart
button, choose **Inspect**, and read the `class` list on the `<button>` element.

Write the names on their own — `button`, not `.button`. A leading dot belongs to
a stylesheet, not a class attribute, and the app tells you so rather than saving
the setting with the dot quietly removed.

Leave the field empty to keep Easy Quotes' own button styling, which you can
shape in **Styles** above.

## Custom CSS

Loaded after the default styles and after the Styles section, so your rules win
over both. The **CSS variables** panel beside the editor lists every variable
Easy Quotes reads, with its default and whether the pickers above already set
it. It stays on screen while you scroll, so you can refer to it as you type.

Target the `eq-` classes, or set the variables yourself on `:root` for the whole
store or on a class like `.eq-page-block` for one area.

## Per-block styling

Every Easy Quotes block also has **CSS classes** and **Custom CSS** fields in
the theme editor. CSS there applies to that block alone, so you can restyle the
button on one page without touching the rest. Write plain declarations, or
selectors:

```css
background: #f6f6f6;
.eq-button { text-transform: uppercase; }
```

The app embed has a **CSS class** field too, which lands on the mini quote so
your theme's stylesheet can target it.

## A note on Outline buttons

An Outline button has no fill, so **Background color** can't show as one — it
tints the border and text instead. **Text color** overrides that tint. If you
want a filled button, set Button style to **Solid**.
