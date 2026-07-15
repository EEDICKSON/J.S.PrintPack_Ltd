# PROJECT BIBLE — J.S. PrintPack Ltd Website

The single source of truth for this project: what it is, how it works, how to run it, deploy it, edit it, and grow it.

---

## 1. Overview

**What:** A 7-page marketing website for J.S. PrintPack Ltd, a flexographic printing and flexible packaging manufacturer in Liberia serving Liberia and West Africa.

**Who it's for:** B2B customers — water producers, food/beverage manufacturers, distributors, detergent/cosmetics/pharma brands, retailers, and startups needing branded packaging.

**Goals:** Generate leads and showcase services. Primary visitor actions: call, WhatsApp, or send a message/quote request.

**Constraints:** Pro bono project — every service used is genuinely free-tier with no billing risk at low traffic. Optimized for slow connections and mobile-first usage common in the target market.

## 2. Tech Stack Summary

| Layer | Tool | Cost | Why |
|---|---|---|---|
| Site | Plain HTML/CSS/JS (no framework, no build step) | Free | Fastest possible load, zero dependencies, anyone can edit |
| Fonts | Google Fonts (Archivo, Public Sans, IBM Plex Mono) | Free | Loaded with `preconnect` + `display=swap` for speed |
| Hosting | Netlify free tier (recommended) or Vercel | Free | Auto-deploy from GitHub, free HTTPS, free subdomain |
| Forms | Netlify Forms (built into hosting) | Free (100 submissions/mo) | No backend needed; submissions arrive by email |
| Domain | Free `*.netlify.app` subdomain for now | Free | Custom domain (~$10–15/yr) is the client's only future cost |
| Analytics | None in v1 | — | Deliberately skipped; can add later |

## 3. File / Folder Structure

```
printpack-site/
├── index.html          # Home — hero, services preview, why-us, CTA band
├── about.html          # About — story, mission, who we serve
├── services.html       # Services — 6 service cards + 4-step process
├── portfolio.html      # Portfolio — 6 placeholder tiles for project photos
├── news.html           # News & Updates — placeholder posts, copy-paste pattern
├── faq.html            # FAQ — accordion (native <details>, no JS needed)
├── contact.html        # Contact — info panel + Netlify contact form
├── thanks.html         # Form success page (form redirects here)
├── css/
│   └── styles.css      # The entire design system — all styling lives here
├── js/
│   └── main.js         # Only JS on the site: mobile menu toggle
├── images/
│   └── logo-mark.svg   # PLACEHOLDER logo — replace with real logo, same filename
└── PROJECT_BIBLE.md    # This file
```

## 4. Setup — Run Locally

No build step, no installs. From a fresh clone:

```bash
cd printpack-site
python3 -m http.server 8000
# open http://localhost:8000
```

Or simply double-click `index.html` (everything works from the filesystem except form submission, which only works once deployed to Netlify).

## 5. Deployment (Netlify — recommended)

1. Push this folder to a GitHub repository.
2. Log in at netlify.com → **Add new site → Import an existing project** → pick the repo.
3. Build settings: leave **Build command** empty, set **Publish directory** to the repo root (or the `printpack-site` folder if nested). Deploy.
4. The site is live at `https://<something>.netlify.app`. Rename it: **Site settings → Change site name** → e.g. `jsprintpack` → `https://jsprintpack.netlify.app`.
5. **Enable form notifications:** Site settings → Forms → Form notifications → add the client's email so submissions land in their inbox.

**Connecting a custom domain later:** Buy a domain (e.g. `jsprintpack.com`, ~$10–15/yr from Namecheap/Porkbun). In Netlify: **Domain settings → Add custom domain** → follow the DNS instructions (point the domain's nameservers or add the CNAME/A records shown). HTTPS is issued automatically. Nothing in the code needs to change.

## 6. Content Editing Guide (for non-technical editors)

Everything that needs client content is marked `[PLACEHOLDER: ...]` — search the files for `PLACEHOLDER` to find every spot.

**Change text:** Open the `.html` file in any text editor, find the text, replace it. Save, commit, push — Netlify redeploys automatically.

**Replace the logo:** Overwrite `images/logo-mark.svg` with the real logo **using the same filename** (SVG or PNG both fine; if PNG, rename references in the HTML from `.svg` to `.png` — they appear in the header, footer and favicon `<link>` of every page).

**Add a portfolio item:** In `portfolio.html`, copy one whole `<figure class="portfolio-item">...</figure>` block, paste it below the others, and edit. To use a real photo, put the image in `images/` and replace the `<div class="thumb">...</div>` with `<img src="images/yourphoto.jpg" alt="describe the photo">`. **Compress photos first** (tinypng.com or squoosh.app) — target under 200 KB each.

**Add a news post:** In `news.html`, copy one `<article class="news-item">...</article>` block, paste it at the **top** of the list, edit the date, title, and text.

**Add an FAQ:** In `faq.html`, copy one `<details>...</details>` block and edit.

**Change the WhatsApp number:** Search all files for `231775056099` and replace with the new number (digits only, country code included, no `+`).

**Change phone numbers / email:** Search for `+231775056099`, `+231888574745`, and `georgejflomo9@gmail.com` and replace.

## 7. Design System

| Token | Value | Use |
|---|---|---|
| `--ink` | `#131210` | Near-black: header, footer, dark sections (printing-ink black) |
| `--gold` | `#C9A227` | Brand gold: accents, buttons, borders (from the logo) |
| `--gold-deep` | `#9A7A1B` | Darker gold: text-sized accents, links |
| `--gold-pale` | `#F3EAD0` | Pale gold tint: highlight sections, portfolio thumbs |
| `--paper` | `#FBFAF7` | Page background (press-sheet white) |
| `--text` / `--muted` | `#33312C` / `#6B675E` | Body text / secondary text |

**Type:** Archivo (bold display headings), Public Sans (body), IBM Plex Mono (eyebrow labels, specs, dates).

**Signature element:** section eyebrows flanked by print **registration marks** (the small crosshairs), echoing the crop marks on a press sheet. Keep this on any new section you add: use `<p class="eyebrow">Label</p>`.

**Layout rules:** content max-width 1120px; sections alternate paper → dark → tint; every dark section uses gold accents; all cards get a gold top border.

## 8. Form & WhatsApp Setup

**Contact form** (`contact.html`) uses Netlify Forms: the `data-netlify="true"` attribute on the `<form>` is what activates it — do not remove it. Includes a honeypot field for spam. On success, users are redirected to `thanks.html`. Submissions appear in the Netlify dashboard under **Forms**, and email notifications can be configured (see §5 step 5). Free tier: 100 submissions/month — far more than a site like this will see initially.

**If hosting on Vercel instead:** Vercel has no built-in forms. Create a free Formspree account, and change the form tag to `<form action="https://formspree.io/f/YOUR_ID" method="POST">`, removing the `data-netlify` and hidden `form-name` attributes.

**WhatsApp:** every WhatsApp button/link uses `https://wa.me/231775056099` — a free deep link that opens WhatsApp with a chat to that number. The floating green button (bottom-right of every page) is the `.wa-float` element before `</body>`.

## 9. Roadmap / Future Expansion

The site is deliberately simple so it can grow without a rebuild:

- **Online ordering / e-commerce:** Add Snipcart (usage-based) or migrate the Services page items into a lightweight store. Because the site is static, an e-commerce layer can be bolted on page-by-page. Alternatively, rebuild on Astro reusing all the current CSS unchanged.
- **Customer accounts:** Requires a backend — the natural path is Supabase (free tier) + a small amount of JS. Nothing in the current structure blocks this.
- **New pages:** Copy any existing page, edit the `<main>` content, add a nav link to the `<nav>` list in every page's header and footer.
- **Analytics:** Add Netlify Analytics (paid) or a free privacy-friendly option like GoatCounter — one `<script>` tag before `</body>` on each page.
- **Blog at scale:** If News grows beyond ~10 posts, consider moving to Astro with markdown posts; the design system CSS carries over as-is.

## 10. Known Limitations (intentional, not oversights)

| Left out | Why |
|---|---|
| Live chat widget | Needs constant staffing or looks abandoned; WhatsApp covers the need |
| Site search | Pointless on a 7-page site |
| Custom domain | Client's decision + only unavoidable cost (~$10–15/yr); free subdomain until then |
| Analytics | Not needed for v1; easy one-line add later |
| CMS | Direct HTML editing keeps everything free and dependency-free; revisit if a non-technical person must edit frequently |
| Real content | Client is supplying text/photos; every gap is marked `[PLACEHOLDER: ...]` |
| Real logo | Placeholder gold/black mark at `images/logo-mark.svg` until the real file is provided |
