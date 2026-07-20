# The Abbey Group — Web Bundle

A static site bundle for **The Abbey Group** hospitality proposal by OneDesign.
Each page is a self-contained HTML file (inline CSS + JS) deployed on Vercel.

## Pages

| File | URL (clean) | Venue |
| --- | --- | --- |
| `index.html` | `/` | The Abbey Group — landing / digital proposal |
| `blackrabbit.html` | `/blackrabbit` | Black Rabbit — Chester-le-Street |
| `hibou.html` | `/hibou` | Hibou Blanc — Newcastle |
| `restaurant.html` | `/restaurant` | The Restaurant @ Hibou Blanc |
| `cocktailbar.html` | `/cocktailbar` | The Cocktail Bar @ Hibou Blanc |
| `court.html` | `/court` | The Court, Durham — coming soon |

## Deployment

Deploys as static files on **Vercel**. Configuration lives in `vercel.json`:

- **`cleanUrls`** — pages serve without the `.html` extension (`/blackrabbit`).
  Existing `*.html` links keep working (redirected automatically).
- **Security headers** — `X-Content-Type-Options`, `X-Frame-Options`, and a
  site-wide **`Referrer-Policy: no-referrer`** (see Images below).

## Images

Photography is **hotlinked** from the live venue websites
(`hiboublanc.co.uk`, `blackrabbitchesterlestreet.com`) and an AI-image CDN,
rather than being stored in this repo.

Many WordPress hosts use **hotlink protection**, which blocks image requests
that arrive with a foreign `Referer` header — this is the usual cause of
broken images once the site is live on a different domain. To fix it, every
page now sends **no referrer**:

- `<meta name="referrer" content="no-referrer">` on each page, and
- a site-wide `Referrer-Policy: no-referrer` header in `vercel.json`.

A small global handler also hides any image that still fails to load, so a
dead URL degrades gracefully instead of showing a broken-image icon.

> **Recommendation:** for long-term reliability, the referenced images should
> be downloaded and committed into the repo (e.g. an `/images` folder) so the
> site does not depend on third-party servers staying up or permitting
> hotlinks. That step needs the original image files and was left as a
> follow-up.

## Favicon

`favicon.svg` — an Abbey Group "A" monogram in the brand palette
(ink `#0b0a09`, gold `#c8a25c`), referenced by every page.
