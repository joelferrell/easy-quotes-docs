---
title: Notifications
nav_order: 7
---

# Notifications

Everything Easy Quotes sends — the email your team gets, the quote you send a
customer for approval, the design of both, and sending from your own domain.

## Customer notifications

The quote you send a customer so they can approve it. Nothing goes out
automatically: you send it by hand from a quote's own page, once you've priced
it, adjusted the lines and added shipping.

### Sending a quote

Open **Quotes**, click the quote, and use **Send to customer** in the right-hand
column. It's disabled until the draft order exists — the customer needs
something to approve — and until you've saved any changes you're part-way
through.

The email carries a **Review and approve** button. It takes the customer to a
page on your own storefront (`yourshop.com/apps/quote/approve`), not to an
Easy Quotes address, where they can:

- **Approve** — recorded against the quote, and they're offered a **Pay now**
  link to Shopify's invoice page.
- **Decline**, optionally with a reason, which you'll see on the quote.

### Knowing what's been sent

Every step tags the draft order in Shopify, so you can filter on them there
without opening this app:

| Tag | Means |
|:--|:--|
| `quote-sent` | The quote has been emailed to the customer |
| `quote-approved` | They approved it |
| `quote-declined` | They declined it |

Your own **Draft order tag** from Settings stays on the order alongside these.

The quote's page shows the same thing in words: *Not sent yet*, *Waiting on the
customer*, *Approved by the customer*, or *Declined by the customer*, with the
date it was sent and the reason if they gave one.

### Sending again

**Send again** re-sends the same quote. The approval link is deliberately the
same one, so a customer who kept the first email can still use it.

---

## Internal notifications

The email your team gets when a quote comes in.

- **Send new quote notifications to** — the main recipient. Replies go straight
  to the shopper who asked, so hitting reply starts the conversation.
- **Also send to** (Pro) — extra recipients, comma separated. Everyone named
  gets the one email, not one each.
- **Subject line** (Pro) — your own, with tokens. Leave it blank for the
  default.
- **Opening note** (Pro) — a line for your team above the summary. The shopper
  never sees it.

There's no preview for this one. Send yourself a test quote if you want to see
how it looks.

### Subject line tokens

Both the internal subject and the customer subject accept the same tokens:

{% raw %}
`{{shop}}` `{{quote_id}}` `{{order_name}}` `{{customer_name}}`
`{{customer_email}}` `{{item_count}}` `{{total}}`
{% endraw %}

An unrecognised token is left visible rather than blanked, so a typo shows up
as {% raw %}`{{custmer_name}}`{% endraw %} in the subject instead of vanishing
silently.

---

## Designing the emails with Liquid

Both emails are **Liquid** — the same templating language as your theme — so if
you've edited a Shopify theme you already know it.

Each starts from a standard invoice-style design. The editor is pre-loaded with
it, so you're editing working markup rather than starting from an empty box.
A badge above the editor says **Standard template** or **Customised**, and once
you've changed something a **Reset to the standard template** button appears.

**Saving an untouched copy of the standard template keeps you *on* the standard
template** rather than pinning you to today's version — so you keep getting
improvements to it. Only a real edit is stored as your own.

### Your branding

Four fields feed the standard design, so you can brand the email without
touching any Liquid:

- **Logo URL** — an `https://` link. Upload the image in Shopify under
  **Content → Files** and copy the link.
- **Company name** — the header and footer. Defaults to your shop domain.
- **Company address** — the footer.
- **Accent colour** — hex, like `#1f7a4d`. Used for the rule under the header,
  the total, and the buttons.

### What you can use in a template

{% raw %}

| Variable | What it is |
|:--|:--|
| `{{ shop.name }}` | Your company name |
| `{{ shop.logo_url }}` | Your logo |
| `{{ shop.address }}` | Your company address |
| `{{ shop.accent }}` | Your accent colour |
| `{{ quote.name }}` | The draft order name, e.g. `#D16` |
| `{{ quote.created_at }}` | When it was submitted |
| `{{ quote.expires_at }}` | When it expires |
| `{{ quote.total }}` | Formatted total |
| `{{ quote.item_count }}` | Number of lines |
| `{{ customer.name }}` | Full name, falling back to the email |
| `{{ customer.email }}` | Email address |
| `{{ customer.phone }}` | Phone, if your form collects one |
| `{{ customer.company }}` | Company, if your form collects one |
| `{{ customer.address }}` | Shipping address on one line |
| `{{ links.approve }}` | The approval page — **customer email only** |
| `{{ links.invoice }}` | Shopify's payment page — **customer email only** |
| `{{ links.draft_order }}` | The draft order in your admin — **internal only** |

Line items and answers are loops:

```liquid
{% for item in line_items %}
  {{ item.quantity }} × {{ item.title }}
  {% if item.variant_title %}({{ item.variant_title }}){% endif %}
  {{ item.sku }} — {{ item.price }} — {{ item.line_total }}
{% endfor %}

{% for answer in answers %}
  {{ answer.label }}: {{ answer.value }}
{% endfor %}
```

{% endraw %}

The editor suggests all of these as you type — start typing a variable name, or
type a dot after `customer` or `quote`, and it offers what's available.

### Things worth knowing

**An empty value is `nil`, not `""`.** That means
{% raw %}`{% if customer.phone %}`{% endraw %} behaves the way you'd expect and
doesn't render an empty line when the shopper left the field blank.

**Everything the shopper typed is escaped for you.** You write HTML on purpose;
their answers can't inject any. You never need `| escape`.

**Write for email, not the web.** Use tables and inline styles. Outlook ignores
most of a stylesheet and doesn't support flexbox or grid. The standard template
is deliberately old-fashioned for this reason — copy its structure.

**A template that doesn't render won't save.** You'll get the error with its
line number. If a saved template somehow fails at send time, the email still
goes out using the standard design rather than not arriving.

**Preview before you send.** The customer email has a live preview below the
editor, rendered with a sample quote. Press **Refresh preview** after an edit.

---

## Sending from your own domain

By default quotes send from an Easy Quotes address, with replies going to you.
That works with no setup. Verify your own domain and they'll come from you
instead — better for your branding, and your own sending reputation rather than
ours.

### Set it up

1. In **Notifications → Sending domain**, enter a subdomain you control, like
   `quotes.yourdomain.com`. A subdomain is recommended over your root domain:
   it keeps this separate from your normal mail.
2. Press **Add this domain**. A table of DNS records appears.
3. Add each record to your DNS (see below), then press **Check DNS now**.
4. Set the **From mailbox** and **From name** — the `quotes` and `Acme Co` in
   *Acme Co &lt;quotes@quotes.yourdomain.com&gt;*.

Until the domain is verified, mail keeps sending from the Easy Quotes address.
A half-finished setup never stops your email.

### Adding the DNS records

Sign in wherever your domain's DNS is managed — the registrar you bought it
from, or whoever hosts it (Cloudflare, Route 53). If your domain points at
Shopify, Shopify manages it: **Settings → Domains**, open the domain, then
**DNS settings**.

For each row in the table, add a record of exactly that type. A TXT record
added as CNAME will never verify.

**The name field is where almost everyone goes wrong.** Most DNS providers
append your domain automatically. If the table says
`resend._domainkey.quotes.yourdomain.com` and your provider already shows
`.yourdomain.com` beside the field, enter only `resend._domainkey.quotes`.
Getting this wrong puts the record on your root domain, where nothing looks for
it.

Use the **Copy** button rather than retyping — DKIM values are hundreds of
characters and a single wrong one fails silently.

**Add these as their own records. Don't merge them into an existing SPF.** The
"only one SPF record per domain" rule applies to a single *hostname*. The SPF
here goes on `send.quotes.yourdomain.com`, not your root domain, so it never
conflicts with the SPF you already have. Merging it into your root record
leaves the record we actually check missing, and authorises a sender you didn't
intend on your main domain.

### It says "not verified yet"

Work through these in order:

1. **Check the names are fully qualified correctly.** The most common fault.
   Look up the record yourself to be sure — on a Mac or Linux:

   ```bash
   dig +short resend._domainkey.quotes.yourdomain.com TXT
   ```

   Nothing back means the record isn't where you think it is.

2. **Check the type matches** — TXT, MX and CNAME are not interchangeable.

3. **Check the value is complete.** A DKIM key ends in `IDAQAB`. If yours
   doesn't, it was truncated on the way in.

4. **Wait.** This is usually the answer when the records are right but it still
   won't verify. If a record was missing or wrong when you first pressed
   **Check DNS now**, resolvers cache that "doesn't exist" answer — commonly
   for **30 minutes**, set by your domain's SOA minimum. Fixing the record
   doesn't clear that cache. Wait half an hour from when you fixed it and press
   **Check DNS now** once.

   A good sign you're in this situation: the records that were right from the
   start show as verified, while the ones you corrected are still pending.

5. **Pressing it repeatedly doesn't help** and can refresh the cached answer.
   Once, after waiting, is enough.

---

## Slack

Covered here because it's a notification: a message in a channel the moment a
quote arrives, with who asked, what for, the total and a button to the draft
order.

Set up the incoming webhook and the message wording under
**Notifications → Slack**. See
[Advanced features]({{ '/advanced-features/' | relative_url }}) for creating
the webhook in Slack itself.

**Message headline** (Pro) is the first line of the message, and takes the same
tokens as the subject lines. This is what lets you notify a channel:

{% raw %}
```
<!here> New quote from {{customer_name}} — {{total}}
```
{% endraw %}

Use `<!here>` to notify everyone currently online, or `<!channel>` for everyone
in the channel. The contact details, line items and the draft order button are
added underneath automatically.
