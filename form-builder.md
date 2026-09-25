---
title: The form builder
nav_order: 4
---

# The form builder

**Easy Quotes → Forms.** A form is what a shopper fills in on your quote page.
Base includes one form; Pro allows up to 25, so you can run different forms for
trade and retail, per collection, or per market.

## Fields

Every form starts with the contact and address fields Shopify needs to build a
draft order: email, first and last name, phone, company, address, city,
state/province, ZIP, country. You can relabel, reorder, require, or switch off
any of them — except email, which every quote needs.

On top of those you can add:

| Type | Notes |
| --- | --- |
| Text | Single line |
| Paragraph text | Multi-line |
| Email | Validated |
| Phone | Validated |
| Number | Optional min and max |
| Dropdown | Your own options |
| Radio buttons | Pro |
| Checkbox | Single tick box — Pro |
| Checkboxes | Multi-select group — Pro |

Fields can be full width or half width, so two short answers sit side by side.

## Sections

Group related questions under a heading — "Delivery", "Site details", "About
your project". Sections can also be made collapsible, which keeps a long form
from looking daunting.

## Conditional fields (Pro)

Show a field or a whole section only when an earlier answer calls for it: ask
for a delivery date only when they've said they need delivery, or for a
loading-dock note only when the site is commercial.

The condition is read on the storefront as the shopper types, and checked again
on the server when they submit — so a hidden field is never required and never
saved with a stale answer.

## After submitting

Each form carries its own success and failure screens, edited under **After
submitting**:

- **Success** — heading, message and icon. Replaces the form.
- **Failure** — heading, message and icon. Shown above the submit button so the
  shopper keeps everything they typed.
- **Validation message** — shown when a required answer is missing.

If your store has a specific reason a quote failed — a product that sold out,
say — the shopper sees that reason instead of your generic message.

## How answers are saved

Answers are recorded against your **original field labels**, not the translated
ones. Rename a field later and old quotes keep the label they were submitted
under, so your history stays readable and comparable.

Each quote's answers are attached to its Shopify draft order, so everything you
need is in one place when you price the job.

## Translations (Pro)

Merchant-written text — field labels, help text, options, the after-submit
screens — can be translated per language under a form's **Translations**. The
app's own wording (buttons, errors, the drawer) ships translated already.

An option's stored value never changes when its label is translated, so a
shop's quotes stay comparable whatever language the shopper used.
