# Red Bird Mobile Auto and Fleet

Marketing site for **Red Bird Mobile Auto and Fleet LLC** — veteran owned, firefighter
operated mobile auto service in Arizona.

Static site, no build step. Open `index.html` in a browser and it works.

**Live:** https://redbirdmobile.com  (also serves at https://calisirmori.github.io/redbird-mobile/)
**Booking:** handled by Square — every "Book" button links to the Square appointments page.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The entire site — markup, styles and the small scroll script, in one file |
| `404.html` | Branded not-found page |
| `assets/logo.webp` | Logo used on the page (transparent background) |
| `assets/logo.png` | Same logo, PNG, referenced by the structured data |
| `assets/og-image.jpg` | 1200×630 link-preview card for texts, Facebook, iMessage |
| `assets/favicon-32.png`, `assets/apple-touch-icon.png` | Browser tab and home-screen icons |
| `robots.txt`, `sitemap.xml` | Search engine basics |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |

## Common edits

**Change a price or service** — search `index.html` for the price (e.g. `$85.00`).
Each service is one `<article class="item">` block. Update the price in the
`<span class="price">` and the copy underneath. Keep the Square booking page in sync;
this page does not read prices from Square.

**Change the booking link** — search for `book.squareup.com` and replace all 6 links.

**Colors** — every color is a CSS variable at the top of the `<style>` block in
`index.html`, under `:root`. The brand values are sampled from the logo:

| Variable | Value | Where it came from |
| --- | --- | --- |
| `--cardinal` | `#C62C22` | the red in the RED BIRD wordmark |
| `--ember` | `#C56227` | the sun in the badge |
| `--sand` | `#F6E1C6` | the desert sky in the badge |
| `--ink` | `#14100E` | the black banner in the badge |

The site has a light and a dark version. Both are defined by re-declaring those
variables — the dark set lives in the `prefers-color-scheme: dark` block. Visitors get
whichever their phone or laptop is set to.

## Still to add

- [ ] **Phone number.** Deliberately left out — there is no placeholder number anywhere,
      so nothing fake is live. To add a text-us button, drop this next to any
      "Book an appointment" link:
      `<a class="btn btn-ghost-dk btn-lg" href="sms:+1XXXXXXXXXX">Text us</a>`
- [ ] **Address / service radius.** The page says "Arizona" and "across the valley".
      Naming the actual cities you serve is the single biggest local-search win available.
- [ ] **Business details in structured data.** `index.html` has a `TODO` comment on the
      `application/ld+json` block for `telephone` and `address`.
- [ ] **Photos.** A few real shots of the truck and a service in progress would carry
      more trust than any copy on the page.

## Deploying

Pushing to `main` publishes automatically — GitHub Pages serves the repo root.

```sh
git add -A
git commit -m "Update pricing"
git push
```

Give it a minute, then hard-refresh.

## Domain

`redbirdmobile.com` is the live address. Two pieces make that work:

- The `CNAME` file in this repo, which tells GitHub Pages to claim the domain. **Don't delete it** —
  removing it drops the site back to the `github.io` URL.
- DNS at the registrar: four `A` records on `@` pointing at GitHub's edge
  (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`), and a `CNAME` on `www`.

Email is handled separately by the `MX` and `TXT` (SPF / DKIM / DMARC) records and is not
affected by anything in this repo.

If you ever move the site off GitHub Pages, change the `A` records — leave the mail records alone.
