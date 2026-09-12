# AquaPond Guide (811022.xyz)

Static English content site — koi pond & aquarium care. Built with plain HTML/CSS/JS (no build step), hosted on GitHub Pages, monetised with Google AdSense.

## Structure

```
├── index.html            # Homepage
├── about.html / contact.html / privacy.html / terms.html / 404.html
├── articles/             # 12 SEO articles (each with JSON-LD + canonical)
├── css/style.css         # Design system (responsive, no frameworks)
├── js/main.js            # Mobile nav + footer year
├── img/                  # Generated & compressed images (hero + 4 category)
├── favicon.svg
├── ads.txt               # ← replace pub-XXXXXXXXXXXXXXXX after AdSense approval
├── robots.txt
├── sitemap.xml
└── CNAME                 # custom domain: 811022.xyz
```

## Deploy to GitHub Pages

```bash
git init && git add -A && git commit -m "Initial site"
gh repo create aquapond-guide --public --source=. --push
gh api repos/<USERNAME>/aquapond-guide/pages \
  -X POST -f "source[branch]=main" -f "source[path]=/"
```

Then verify: `https://<USERNAME>.github.io/aquapond-guide/` works before pointing DNS.

## Cloudflare DNS (user action)

In Cloudflare → DNS → Records for `811022.xyz`:

| Type  | Name | Target                     | Proxy |
|-------|------|----------------------------|-------|
| CNAME | @    | `<USERNAME>.github.io`     | Proxied |
| CNAME | www  | `<USERNAME>.github.io`     | Proxied |

Then: SSL/TLS → mode **Full (strict)** (Flexible causes redirect loops with GitHub Pages).
Wait for DNS propagation, then visit https://811022.xyz — GitHub will issue a certificate automatically.

## Google AdSense checklist

1. Site live + indexed (submit to Search Console, request indexing for all URLs).
2. Replace `pub-XXXXXXXXXXXXXXXX` in `ads.txt` with your publisher ID.
3. Apply at adsense.google.com once the site has ~20 indexed pages.
4. After approval, paste the AdSense script into `<head>` of each page (search for `<!-- ADSENSE -->` placeholder) and add ad units in the marked spots.
5. Optional: add Google Analytics tag in `<head>`.

## Editing / adding articles

Copy an existing article, keep the same template (head meta, canonical, JSON-LD, breadcrumb, related-links box, disclaimer), add the new file to `sitemap.xml`, then commit and push — GitHub Pages updates automatically.

## Content notes

- All articles are evergreen, beginner-oriented, and include tables/callouts for readability.
- Fish-health pages carry a veterinary disclaimer (YMYL-safe).
- Contact email uses a placeholder (`hello@811022.xyz`) — change in `contact.html` once you have a mailbox.
