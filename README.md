# Red Bird Mobile Auto and Fleet

Marketing site for **Red Bird Mobile Auto and Fleet LLC**, a veteran owned mobile auto
service in the Globe-Miami area of Arizona.

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

**Change a price or service** — search `index.html` for the price (e.g. `$100.00`).
Each service is one `<article class="item">` block: a name, a price, and `<span class="chip">`
tags for the details. **Two places must change together** — the visible row *and* the matching
entry in the `application/ld+json` block near the top of the file, which is what Google reads.
Keep the Square booking catalog in sync too; this page does not read prices from Square.

**Change the booking link** — search for `book.squareup.com` and replace every link.

**Change the phone number** — search for `9288127575` (the `tel:` links) and `928-812-7575`
(the visible text). It appears in the header, the fleet section, the closing call to action,
the footer, the `/schedule` page and the structured data.

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

- [ ] **Service area detail.** The page says "Globe-Miami area". Naming the actual towns you
      cover is the biggest local-search win still on the table.
- [ ] **Photos.** A few real shots of the truck and a service in progress would carry more
      trust than any copy on the page.
- [ ] **Square service descriptions.** Several still mention a "free Red Bird Vehicle Health
      Check", which has been removed from this site. Those live in Square Dashboard →
      Items & Services, not in this repo, and they show inside the widget on `/schedule`.

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
