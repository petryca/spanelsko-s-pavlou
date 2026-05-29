# Španělsko s Pavlou Website — Project Instructions

## Project overview

Czech-language landing page for "Španělsko s Pavlou" — a personal brand selling a relocation e-book for Czechs moving to Spain. The page is a continuous scroll divided into clearly defined sections. The website contains a set of article sub pages located in blog and ebook directory.

All content is in **Czech**.

---

## Tech stack

- Pure HTML + CSS + minimal vanilla JS (no frameworks, no build tools)
- No npm, no bundlers — keep it static and deployable anywhere

---

## Design direction

### Typography
- Primary family: **DM Sans** (Google Fonts), weights 300–800 — used for headings, body, UI
- Display accent: **Caveat** (Google Fonts), weights 500–700 — used **only** for the script "s Pavlou" in the hero title (and any future on-brand handwritten flourishes)
- Headings: bold/extra-bold (700–800), generous size hierarchy
- Body: regular weight, comfortable line-height (~1.6)
- Hero title combines a heavy DM Sans "Španělsko" stacked above a Caveat script "Pavlou" in the accent colour, with an ochre wavy SVG underline beneath — mirrors the e-book cover (`style-reference/book.png`)

### Colour
- **White background** (`#FFFFFF`) as the dominant surface
- Single warm accent: terracotta `#C8553D` (hover `#B04530`) for CTAs, links, accents, the script title
- Secondary ochre `#D4A95C` used only for the hero wavy underline accent
- Dark text `#1A1A1A` for body / `#555555` for muted secondary text
- Light grey `#F5F5F5` for alternating section backgrounds (visual rhythm)
- All colours defined as CSS custom properties in `:root`

### Layout
- Max content width: ~1100px, centred
- Generous whitespace between sections (80–120px vertical padding)
- Card grids for icon+text items: responsive CSS Grid
  - `.card-grid` → 3 columns desktop, 2 columns tablet, 2 columns mobile (default)
  - `.card-grid--five` modifier → capped at **3 columns** desktop and tablet, 2 columns mobile (used by the Stěhování grid; the modifier name is historical — it no longer means 5 columns)
- Mobile-first responsive approach (breakpoint at 768px)

### Icons
- **Do NOT use emoji for icons**
- Use the **Lucide** icon library loaded via CDN (`https://unpkg.com/lucide@latest`)
- Render icons using `<i data-lucide="icon-name"></i>` and call `lucide.createIcons()` in JS
- Icon sizing: ~48px × 48px in card layouts, styled via CSS (`width`, `height`, `stroke-width: 1.5`)
- Style icons in the terracotta accent colour — consistent across all cards

### Images
- **Images on the site:**
  - Pavla's photo: `images/pavla.jpg`
  - E-book cover: `images/ebook.jpg`
  - Hero backdrop wide: `images/hero-wide.jpg` (≥769px)
  - Hero backdrop square: `images/hero-square.jpg` (≤768px, served via `<picture>` source)
  - Section decor circles: `images/spain-1.jpg` … `images/spain-5.jpg` — 1:1 photos rendered as centred circles (max 200px) above the `.section__title` of Stěhování, Konzultace, Recenze, Blog, and Kontakt (in that order). Styled via `.section__image`.
- No product covers beyond the e-book, no blog thumbnails
- All other visual interest comes from typography, colour, whitespace, and Lucide icons
- Blog preview cards use text only (no thumbnail images)
- Blog articles may contain inline content images. Each article keeps its images in a sibling `<article-slug>-media/` folder (e.g. `blog/bydleni/zivot-v-jeskyni-media/image1.jpeg`) and references them with a relative path. Images use `loading="lazy" decoding="async"` and are wrapped in `<figure>`.

### Interactions
- Smooth scroll for anchor navigation
- Subtle fade-in on scroll for sections (`IntersectionObserver`, kept lightweight)
- Hover states on buttons and cards
- Mobile nav toggle (hamburger)

---

## Page structure (section order)

### 1. Header / Navigation
- Brand name "Španělsko s Pavlou" (text logo, no image logo)
- Nav links: **O Pavle · Stěhování · Recenze · Články**
- One CTA button in nav: "Získej e-book" (anchors to `#stehovani`)
- Sticky on scroll with translucent white background + backdrop blur

### 2. Hero
- Full-bleed responsive image backdrop (`<picture>` with `hero-wide.jpg` / `hero-square.jpg`)
- Translucent white centred card holds the title
- Title typography (book-cover style):
  - "Španělsko" — DM Sans 800, near-black, large
  - "s Pavlou" — Caveat script, terracotta accent, slightly smaller
  - Ochre wavy SVG underline beneath the script line
- Two tagline lines below the title:
  - "Praktický průvodce pro Čechy, kteří se stěhují do Španělska."
  - "Od prvních úvah až po každodenní život."
- Primary CTA: "Chci se dozvědět víc" (anchors to `#stehovani`)

### 3. O Pavle (mini intro)
- Photo: `images/pavla.jpg`
- 2–3 sentence personal pitch
- Trust signals (35+ let ve Španělsku, 100+ klientů, e-booky a průvodce)

### 4. Stěhování do Španělska
- Section headline + short intro
- Grid of icon + text cards (`.card-grid--five`, max 3 columns — see Layout). **Each card is an `<a class="card">` wrapper linking to its article page in `ebook/`:**
  - Doklady (`file-text`) → `ebook/doklady.html`
  - Bydlení (`home`) → `ebook/bydleni.html`
  - Banky (`landmark`) → `ebook/banky.html`
  - Práce (`briefcase`) → `ebook/prace.html`
  - Podnikání (`store`) → `ebook/podnikani.html`
  - Vzdělání (`graduation-cap`) → `ebook/vzdelani.html`
  - Zdravotnictví (`heart-pulse`) → `ebook/zdravotnictvi.html`
  - Důchod (`piggy-bank`) → `ebook/duchod.html`
  - Auto (`car`) → `ebook/auto.html`
  - LGBT (`rainbow`) → `ebook/lgbt.html` — **currently commented out in `index.html`; the `ebook/lgbt.html` page does not exist yet.** Keep the comment wrapper intact and re-enable the card once the page is created.
- **Product block** — single product, split half/half (`.product-feature`):
  - Left half: full-bleed `images/ebook.jpg` (no padding, `object-fit: cover`)
  - Right half: title, description, bullet list of inclusions, price, primary "Koupit e-book" CTA
- The e-book is positioned as covering all the listed topics

### 5. Proč Pavla / Social proof (`#recenze`)
- Testimonial cards (3) with stars, quote, attribution
- Light-grey card backgrounds

### 6. Blog preview (`#blog`)
- Section headline ("Nejnovější články")
- 3 hand-picked article preview cards (`.blog-card`): category label (`.blog-card__cat`), title, excerpt — no thumbnail images. Links point into `blog/<category>/<slug>.html`.
- "Všechny články →" link (`.btn--outline`) → `blog/index.html`
- These three cards are curated manually — when you publish a notable new article, swap one of them here so the homepage stays fresh.

### 7. Kontakt / Footer CTA (`#kontakt`)
- Newsletter signup form (email input + submit button)
- "Napsat Pavle" mailto link
- Social media icon links

### 8. Footer
- Legal links (GDPR, Obchodní podmínky)
- Copyright
- Repeat social links

### Sections currently commented out (preserved in markup)
- **Život ve Španělsku** (`#zivot`) — wrapped in `<!-- ... -->` between the Stěhování and Recenze sections
- **Cestování po Španělsku** (`#cestovani`) — wrapped in `<!-- ... -->` between the Stěhování (after Život block) and Recenze sections
- Keep the markup intact so they can be re-enabled later by removing the comment wrappers

---

## Article pages (`ebook/*.html`)

Each Stěhování card on the home page links to a dedicated article page that doubles as a sales landing page for the e-book.

### Structure (shared by every article page)
1. **Same sticky header** as the home page (brand → `../index.html`, nav links use `../index.html#anchor`, CTA scrolls to `#ebook` on the article page itself).
2. **Article hero** (`.article-hero`) on a grey background:
   - `← Zpět na všechny kapitoly` back-link to `../index.html#stehovani`
   - Big article title (`.article-hero__title`, DM Sans 800)
3. **Article body** (`.article` → `.article__body`):
   - Max-width 720px, optimised reading typography (17px / line-height 1.75)
   - Prose styles for `h2`, `h3`, `p`, `ul`/`ol`, `strong`, `em`, `blockquote`
   - Bullet markers use accent colour; blockquotes have a left accent border + grey background
4. **Inline CTA card** (`.article__cta`) below the body — light accent panel with a "Podívat se na e-book" button anchored to `#ebook`.
5. **Sales section** (`#ebook`, `.section--grey`) — reuses the home page's `.product-feature` (image left, content right, single product).
6. **Same footer** as the home page (legal links resolve to `../index.html`).

### Markdown source
- `ebook-md/` holds the source brief for each chapter, one file per page named to match the HTML (`doklady.md`, `banky.md`, `duchod.md`, …). The HTML is hand-written from these briefs — do **not** add a build step (see "What NOT to do").

### Stub pages / unfinished chapters
- The **LGBT** chapter is not built yet: there is no `ebook/lgbt.html` and no `ebook-md/lgbt.md`, and the card is commented out in `index.html`. When ready, write `ebook-md/lgbt.md`, create `ebook/lgbt.html` from the shared article structure, and un-comment the card.

### Asset paths
- Stylesheet: `../style.css`
- Script: `../script.js`
- Ebook image: `../images/ebook.jpg`
- Back to home anchors: `../index.html#…`

---

## Blog management (frequent updates)

The blog is the most actively-updated part of the site, so treat it as a small, repeatable content system rather than ad-hoc pages. It is **category-based** and fully hand-written (no build step — same rule as the e-book).

### Layout
- `blog/index.html` — the main hub: a `.blog-cats` row of category chips at the top, followed by one `.blog-category` block per category. Each block has a heading + "Vše z kategorie →" link and a `.blog-grid` of `.blog-card`s.
- `blog/<category>/index.html` — a per-category listing. Same `.blog-cats` chip row (with the current category's chip carrying `.blog-cat-chip--active`), an `.article-hero` titled with the category name + a `Kategorie` eyebrow, then a `.blog-grid` of that category's articles.
- `blog/<category>/<slug>.html` — the article itself.
- `blog/<category>/<slug>-media/` — inline images for that article (create only when needed).
- `blog-md/` mirrors the whole tree (`blog-md/<category>/<slug>.md` + matching `-media/`) and holds the source brief for each article.

### Current categories (slug → display name)
- `barcelona` → Barcelona (`building-2`)
- `bydleni` → Bydlení (`home`)
- `dobroty-a-restaurace` → Dobroty a restaurace (`utensils`)
- `spanelstina` → Španělština (`languages`)
- `spolecnost` → Společnost (`users`)
- `svatky-a-slavnosti` → Svátky a slavnosti (`party-popper`)

### Article page structure
Same shell as the e-book article pages, but assets resolve **two levels up** (`../../style.css`, `../../script.js`, `../../index.html#…`) because articles live in `blog/<category>/`.
1. Shared sticky **header** (brand → `../../index.html`, "Články" link → `../../blog/index.html`).
2. **`.article-hero`** — back-link to the category index (`index.html`, label e.g. `← Zpět na Bydlení`) + `.article-hero__title`.
3. **`.article` → `.article__body`** — prose (max-width 720px, 17px/1.75). Inline images go in `<figure><img loading="lazy" decoding="async"></figure>` referencing `<slug>-media/imageN.ext`.
4. **`.article__cta`** — the e-book cross-sell aside ("Plánujete přesun do Španělska?" → `../../index.html#stehovani`). Keep this on every article.
5. Shared **footer**.
6. `<head>`: unique `<title>` (`Název článku — Španělsko s Pavlou`) and a Czech `<meta name="description">`; same Google Fonts + analytics tags as the rest of the site.

### Publishing a new article — checklist
1. Drop the source brief in `blog-md/<category>/<slug>.md` (+ a `-media/` folder if it has images).
2. Create `blog/<category>/<slug>.html` from the structure above (copy an existing article as the template, e.g. `blog/bydleni/zivot-v-jeskyni.html`). Add any images under `blog/<category>/<slug>-media/`.
3. Add a `.blog-card` for it to **two** listings: `blog/<category>/index.html` and the matching `.blog-category` block in `blog/index.html`.
4. If it's a notable piece, swap it into one of the **3 homepage preview cards** in `index.html` (`#blog` section) so the homepage stays current.
5. Use a kebab-case, diacritics-free slug; keep excerpts ~1–2 sentences in Czech with proper diacritics.

### Adding a new category
1. Create `blog/<new-category>/index.html` (copy an existing category index) and a matching `blog-md/<new-category>/` folder.
2. Add the category chip to the `.blog-cats` row in **every** blog page (main hub, every category index — they all render the full chip row) and add a new `.blog-category` block to `blog/index.html`. Pick a Lucide icon for the chip.

---

## File structure

```
/
├── index.html
├── faq.html                  # standalone FAQ page (reuses the shared header/footer)
├── style.css
├── script.js                 # minimal — mobile nav toggle, IntersectionObserver, lucide.createIcons()
├── CNAME                      # custom domain for GitHub Pages
├── images/
│   ├── pavla.jpg
│   ├── ebook.jpg
│   ├── hero-wide.jpg
│   ├── hero-square.jpg
│   └── spain-1.jpg … spain-5.jpg   # section decor circles on homepage
├── ebook/                 # one HTML page per topic in the Stěhování grid (lgbt not built yet)
│   ├── doklady.html
│   ├── bydleni.html
│   ├── banky.html
│   ├── prace.html
│   ├── podnikani.html
│   ├── vzdelani.html
│   ├── zdravotnictvi.html
│   ├── duchod.html
│   └── auto.html
├── ebook-md/              # markdown source/brief per chapter — filenames match the HTML (doklady.md, banky.md, …)
├── style-reference/
│   └── book.png              # e-book cover used as typographic reference for the hero
├── blog/                  # category-based blog — see "Blog management" below
│   ├── index.html            # main listing: category chips + every article grouped by category
│   ├── barcelona/            # one folder per category
│   │   ├── index.html        # category listing (chips with this one --active)
│   │   ├── <slug>.html       # article pages
│   │   └── <slug>-media/     # per-article inline images (only when an article has images)
│   ├── bydleni/
│   ├── dobroty-a-restaurace/
│   ├── spanelstina/
│   ├── spolecnost/
│   └── svatky-a-slavnosti/
├── blog-md/               # markdown source mirroring blog/ (same category/slug + -media folders)
└── CLAUDE.md
```

---

## Code conventions

- Semantic HTML5 elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`, `<picture>`)
- Each section gets an `id` for anchor navigation (e.g. `id="stehovani"`, `id="recenze"`, `id="blog"`)
- BEM-like class naming: `.section-stehovani`, `.card`, `.card__icon`, `.product-feature`, `.product-feature__image-wrap`
- CSS custom properties for all colours, font sizes, spacing
- Mobile-first media queries (breakpoint at ~768px; a secondary tablet range at 769–1024px)
- All text content in Czech — use proper diacritics (č, ř, š, ž, etc.)
- Alt text on all images (in Czech)

---

## What NOT to do

- No emoji as icons
- No frameworks (React, Vue, Tailwind, Bootstrap)
- No build tools or package managers
- No placeholder lorem ipsum — use realistic Czech placeholder copy
- No decorative imagery on the marketing pages beyond those in `images/` (Pavla, e-book, hero, `spain-*` decor circles) — visual interest there comes from typography, Lucide icons, colour, and layout. Blog articles are the exception: they may carry their own inline content images in per-article `-media/` folders.
- Do not implement payment/checkout — buy buttons are links (hrefs to be filled in later)
- Do not delete the commented-out Život / Cestování sections — they are intentionally preserved for future re-enablement
- Do not add a build step to compile `ebook-md/*.md` → `ebook/*.html`. The HTML is hand-written and copy-edited; treat the markdown as a source brief, not a build input.
