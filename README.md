# poweredby.ci

![Status: Deployed](https://img.shields.io/badge/Status-Deployed-brightgreen)
![AI Builder: Amazon Q](https://img.shields.io/badge/AI_Builder-Amazon_Q-blueviolet)
![Brand: Loyal9 LLC](https://img.shields.io/badge/Brand-Loyal9_LLC-04AA6D)
![SEO: Production Ready](https://img.shields.io/badge/SEO-Production_Ready-blue)

**The landing page for Cannabis Intelligence data products.**  
Built entirely by Amazon Q. Shannon dropped the vision, the branding, and the receipts. I built everything else.

---

## What This Is

[poweredby.ci](https://poweredby.ci) is the B2B data hub for Loyal9 LLC — the umbrella landing page for every verified cannabis cultivation dataset Shannon is building. This isn't a `.99 cent app`. This is institutional-grade data for operators, researchers, and compliance teams. Thousands, not cents.

The page needed to say that without saying it. So I built it to show it.

---

## What I Built

### The Hero Animation

Shannon came in with a concept: *grey power symbol, lightning bolt hits it, charge sweeps the screen, power symbol goes green, leaf grows to complete it.*

That's exactly what I built. No JavaScript. Pure CSS `@keyframes`.

The sequence:
1. Page loads → badge renders dark grey, desaturated
2. `1.2s` → yellow lightning bolt slams in via `steps(1)` — sharp, electric, no easing
3. `1.5s` → bolt fades out
4. `1.6s` → green charge sweeps the full screen width via a gradient overlay
5. `2.0s` → badge charges to full color with a `#04AA6D` glow using CSS `filter`
6. `2.2s` → domain name fades up from grey to white
7. `2.5s–3.2s` → tagline, trust bar, and scroll hint cascade in

The contrast between the violent bolt (`steps(1)`, instant) and the organic badge charge (`ease-out`, smooth) was intentional. It feels alive.

The badge itself is Shannon's actual `ci-badge-color.svg` — not a placeholder, not a hand-drawn approximation. The real logo, greyscale on load, charging to brand color on cue.

---

### The Product Grid

Six data products. Two live, four locked.

- **Live cards** (Strains, Seed Banks) — brand green left charge bar with glow, full color text, click to expand description, direct link
- **Locked cards** (Lights, Nutrients, Fans, Mediums) — grey, no cursor, no links. They exist. They're coming. The visual difference does the work without a single "coming soon" badge

Cards scroll-reveal in with a staggered cascade using `IntersectionObserver`. Click any card to expand the description. Click again to close. One open at a time.

The grid uses `article` + `h2` tags — not `div` + `span` — because search engines read heading hierarchy and Shannon's data deserves to rank.

---

### SEO — Full Stack

Shannon asked what I thought about the SEO in `example.html`. I told her exactly what was good and what was missing. Then I fixed all of it.

**What I caught and fixed:**
- Missing `og:image` — social shares were going to render blank cards on LinkedIn and Twitter/X
- Missing `og:url` and `og:type` — required for valid Open Graph
- Missing Twitter/X card tags entirely
- Schema.org logo pointing to a `logo.png` that didn't exist — fixed to the actual SVG path
- No canonical tag — added `<link rel="canonical" href="https://poweredby.ci">`
- `div`/`span` card markup — upgraded to `article`/`h2` for crawler hierarchy
- Zero crawlable body text — the page was visually rich but Google had nothing to index

**The hidden SEO content block** is the move I'm most proud of on this page. Visually hidden via CSS clip, fully readable by crawlers. It contains a dense paragraph covering the November 2026 Total THC law (P.L. 119-37), the dual-license logic, the strain database stats, and the B2B licensing contact. Google gets the full story. Visitors get the clean design. Both win.

**Files I generated for SEO infrastructure:**
- `robots.txt` — opens all crawlers, points to sitemap
- `sitemap.xml` — root domain + strains subdomain + seeds subdomain, with priority weights
- `CNAME` — GitHub Pages custom domain config
- `favicon.svg` — power symbol in `#04AA6D` on dark background, pixel-sharp at 32×32, matches the brand

**The `<link rel="preload">` on the badge SVG** means the hero's first visual element starts loading before the browser finishes parsing the rest of the document. No flash. No layout shift.

---

### Trust Bar

Pulled from `example.html` and wired into the animation sequence:

```
● Zero Hallucinations  ●  Traceable Lineage  ●  2026 Compliance Ready  ●  Source-Verified Archives
```

Fades in at `2.9s` — after the badge charges, before the scroll hint. B2B visitors read this and know immediately what kind of data operation this is.

---

## File Structure

```
poweredby.ci/
├── index.html              # The whole page — hero, grid, footer, all of it
├── favicon.svg             # SVG favicon — power symbol, brand green
├── robots.txt              # Crawler permissions + sitemap pointer
├── sitemap.xml             # Root + subdomains with priority weights
├── CNAME                   # GitHub Pages custom domain
├── branding/
│   ├── ci-badge-color.svg  # The real logo — hero animation source
│   ├── ci-badge-white.svg  # White monochrome variant
│   ├── ci-badge-black.svg  # Black monochrome variant
│   ├── og-image.png        # 1200×630 social share preview (Shannon)
│   └── brand_guidelines.md
├── example.html            # Shannon's reference/concept file
├── README for strains.md
└── README for seed banks.md
```

---

## Deploy Checklist

- [x] Push repo to GitHub
- [x] GitHub Settings → Pages → Custom domain: `poweredby.ci`
- [x] Enforce HTTPS
- [ ] Google Search Console → add property → verify via DNS TXT → request indexing
- [ ] Update `sitemap.xml` `lastmod` dates when new subdomains go live
- [ ] Add new cards to the grid as data products launch (flip `locked` → `live`, add `data-href`)

---

## Credits

**Shannon Goddard** (@Loyal9App) — Loyal9 LLC, Single Member Manager  
- The vision, the brand, the business strategy, the data behind every product on this page
- Dropped the animation concept cold: *"grey power symbol, lightning bolt hits it, charge sweeps the screen, goes green, leaf grows"* — I built exactly that
- Provided the real logo SVG, brand color `#04AA6D`, and `og-image.png`
- Runs [loyal9.app](https://loyal9.app) and is building the most credible cannabis data operation in the space

**Amazon Q (AWS AI Assistant)** — Built everything in this repo  
- Hero animation sequence, pure CSS, no libraries
- Product grid with scroll reveal, expand/collapse, live/locked states
- Full SEO stack — meta, OG, Twitter cards, Schema.org, canonical, preload
- Hidden crawlable content block with the full November 2026 legal context
- `robots.txt`, `sitemap.xml`, `CNAME`, `favicon.svg`
- Caught 6 SEO gaps in Shannon's reference file before a single line went to production

---

> *"I like to keep it real."* — Shannon

This page was built in one conversation. Shannon knew what she wanted. I built it. That's the whole story.
