# Security notes

This is a static GitHub Pages site: no server, no database, no user
accounts, no payment processing, no credentials of any kind in the code.

## Why this site is one self-contained file
An earlier version of this site split the CSS and JavaScript into
separate `css/style.css` and `js/app.js` files to tighten the security
policy further. In practice this made the deployment fragile: if those
two folders were not uploaded to exactly the right place, the page loads
with no styling at all (which is what happened). Reliability matters
more than a marginal security gain here, so everything is back in a
single `index.html`, exactly like the version that worked. Upload that
one file (plus `legal.html`, `privacy.html`, `general.html`, `robots.txt`,
`sitemap.xml`, and the existing `assets/` folder) and there is nothing
left to place incorrectly.

## Hardening still in place
- **Content-Security-Policy** (via meta tag, since GitHub Pages does not
  allow custom HTTP response headers): `object-src 'none'`, `base-uri
  'self'`, `frame-src` limited to Google Maps only, `form-action` limited
  to Formspree only, and no script/style origins beyond this page and
  Google Fonts.
- The chat assistant no longer inserts the visitor's own message into the
  page as raw HTML — it is written as plain text, so typing HTML or a
  `<script>` tag into the chat box cannot execute anything.
- `robots.txt`, `sitemap.xml` and every canonical/Open Graph URL point at
  the site's real address, https://alexandarngoranov-lang.github.io/Bike-n-You/.
  **Please double-check this is genuinely the address you use** — if your
  GitHub Pages URL is different, tell me the exact address and I will
  correct every reference in one pass.

## What a static host cannot do
GitHub Pages does not let you set real HTTP response headers, so
`X-Content-Type-Options`, `X-Frame-Options` and `Strict-Transport-Security`
cannot be enforced from this repository alone. If you want those too, put
the site behind Cloudflare Pages, Netlify or Vercel instead of (or in
front of) GitHub Pages and set the headers there — the HTML itself does
not need to change.

## Reporting
Contact bikenyouatelier@gmail.com for anything security-related.
