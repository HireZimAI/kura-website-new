# Kura Growth Systems — website

Static site. No build step, no dependencies. Deploys to Cloudflare Pages as-is.

## Before you publish — three placeholders

The site will deploy with broken links until these are replaced.

| Placeholder | Occurrences | Replace with |
|---|---|---|
| ~~`REPLACE_WITH_YOUR_GHL_LANDING_PAGE`~~ | done | Currently a Google Calendar link. Swap for the GHL landing page once built |
| `263XXXXXXXXX` | 2 in `index.html` | Your WhatsApp business number, digits only, no `+` (e.g. `263771234567`) |
| `<!-- ANALYTICS ... -->` | 1 in `<head>` | Plausible, GA4, or Cloudflare Web Analytics snippet |

Find and replace across `index.html`, then commit.

## Deploying to Cloudflare Pages

1. Push this folder to a **new** GitHub repo — do not drop it into the existing Next.js `kura-website` repo, or Pages will try to run `next build`.
2. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
3. Select the repo. Then:
   - **Framework preset:** None
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
4. **Save and Deploy.**
5. **Custom domains** → add `www.kuragrowthsystems.com`, then add the apex `kuragrowthsystems.com`. Cloudflare creates the DNS records if the domain is on your account.

Every push to `main` redeploys automatically.

### If you must reuse the existing repo
Delete `app/`, `package.json`, `package-lock.json`, `next.config.*` and `tsconfig.json` first, then set the build command to empty as above.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole site — HTML, CSS and JS in one file |
| `sample-report.html` | Printable Monthly Recovery Report sample. `noindex`, not linked from the site. Send it directly to prospects |
| `404.html` | Not-found page. Cloudflare Pages picks this up automatically |
| `favicon.svg` | Gradient K mark |
| `robots.txt` | Allows the site, blocks the sample report |
| `sitemap.xml` | Single URL. Add entries if you add pages |
| `_headers` | Security headers, caching, `noindex` on the sample report |
| `_redirects` | Forces apex → `www` |

## Still to do

- **Social share image.** No `og:image` is set, so links shared on WhatsApp and Facebook will preview without a picture. Add a 1200×630 PNG as `/og.png` and uncomment the meta tag in `<head>`.
- **A real name and face** on the specialist section and the report signature. Both currently say "Your Kura specialist".
- **Response-time test offer** — the strongest urgency driver still missing from the page.

## Editing

Everything is in `index.html`. The design tokens live in the `:root` block at the top:

```
--navy-900  page background
--navy-800  section background
--cyan      accent
--red       CTAs
--wa        WhatsApp green
```

Three animated sections (`#race`, `#rec`, `#calc`) autoplay on scroll and respect `prefers-reduced-motion`.
