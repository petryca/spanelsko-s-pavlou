# Španělsko s Pavlou — Project Instructions

## Project overview

Single-page Czech-language landing page for "Španělsko s Pavlou" — a personal brand selling relocation advice, e-books, and tour guide services for Czechs interested in Spain. The page is a continuous scroll divided into clearly defined sections. A separate blog section (listing + article template) will be added later.

All content is in **Czech**.

---

## Tech stack

- Pure HTML + CSS + minimal vanilla JS (no frameworks, no build tools)
- Single `index.html` file with linked `style.css`
- No npm, no bundlers — keep it static and deployable anywhere

---

## Design direction

### Typography
- Simple, modern, clean typographic system
- Use Google Fonts — pick **one sans-serif family** with multiple weights (e.g. DM Sans, Outfit, Satoshi, or similar — avoid Inter, Roboto, Arial)
- Headings: bold/semibold weight, generous size hierarchy
- Body: regular weight, comfortable line-height (~1.6)
- Keep font usage to a single family for cohesion

### Colour
- **White background** (`#FFFFFF`) as the dominant surface
- Use a single warm accent colour for CTAs and highlights (suggest Spanish-inspired — terracotta, warm ochre, or deep orange — confirm with client)
- Dark text (`#1A1A1A` or similar near-black) for readability
- Subtle light grey (`#F5F5F5` or similar) for alternating section backgrounds to create visual rhythm
- Define all colours as CSS custom properties in `:root`

### Layout
- Max content width: ~1100px, centred
- Generous whitespace between sections (80–120px vertical padding)
- Card grids for icon+text items: responsive CSS Grid, 2–3 columns on desktop, 1 column on mobile
- Mobile-first responsive approach

### Icons
- **Do NOT use emoji for icons**
- Use the **Lucide** icon library loaded via CDN (`https://unpkg.com/lucide@latest`)
- Render icons using `<i data-lucide="icon-name"></i>` and call `lucide.createIcons()` in JS
- Icon sizing: ~48px × 48px in the card layouts, styled via CSS (`width`, `height`, `stroke-width`)
- Choose semantically appropriate Lucide icon names for each card (e.g. `file-text` for Dokumenty, `home` for Bydlení, `landmark` for Banky, etc.)
- Style icons using the accent colour or a muted variant — keep consistent across all cards

### Images
- **Only two images on the entire site:**
  - Pavla's photo: `images/pavla.jpg`
  - E-book cover: `images/ebook.jpg`
- No hero background image, no additional product covers, no blog thumbnails
- Hero section and all other visual interest comes from typography, colour, whitespace, and Lucide icons only
- Blog preview cards use text only (no thumbnail images)

### Interactions
- Smooth scroll for anchor navigation
- Subtle fade-in on scroll for sections (CSS `animation` or `IntersectionObserver` — keep it lightweight)
- Hover states on buttons and cards

---

## Page structure (section order)

### 1. Header / Navigation
- Brand name "Španělsko s Pavlou" (text logo, no image logo)
- Navigation links anchoring to page sections
- One CTA button in nav (e.g. "Získej e-book")
- Sticky on scroll

### 2. Hero
- Main slogan: "Praktické rady pro cestování, život i stěhování do Španělska"
- Short subtitle explaining what Pavla offers
- Primary CTA button
- No background image — use typography, whitespace, and accent colour for visual impact

### 3. O Pavle (mini intro)
- Photo: `images/pavla.jpg`
- 2–3 sentence personal pitch
- Trust signals (years in Spain, number of people helped, etc.)

### 4. Stěhování do Španělska
- Section headline
- Short intro paragraph
- Grid of icon + text cards:
  - Dokumenty
  - Bydlení
  - Banky
  - Zdravotnictví
  - Školy
  - Práce
  - Podnikání
- **Product block** with two options side by side:
  - E-book — cover image (`images/ebook.jpg`), description, price placeholder, buy button
  - E-book + Zoom konzultace — description, what's included, price placeholder, buy button
- Make it clear the e-book covers all the listed topics

### 5. Život ve Španělsku
- Section headline
- Short intro paragraph
- Grid of icon + text cards:
  - Každodenní fungování
  - Kulturní rozdíly
  - Služby
  - Doprava
  - Rodinný život
- **Product block** — same two-option layout as section 4 (same products, reinforced from a different angle)

### 6. Cestování po Španělsku
- Section headline
- Short intro paragraph
- Two product cards only (larger format than the icon cards above):
  - **Barcelona s Pavlou** — e-book, short description, button linking to external URL (placeholder `href`)
  - **Osobní průvodce na míru** — description of Pavla as a personal tour guide, "Napsat Pavle" or booking CTA

### 7. Proč Pavla / Social proof
- Testimonials or client quotes (placeholder cards)
- Optional: Pavla's direct "proč já" pitch

### 8. Blog preview
- Section headline ("Nejnovější články")
- 3 article preview cards (title, excerpt, date — no thumbnail images)
- "Všechny články →" link (href placeholder)

### 9. Kontakt / Footer CTA
- Newsletter signup form (email input + submit button)
- Contact form or "Napsat Pavle" link
- Social media icon links

### 10. Footer
- Legal links (GDPR, Obchodní podmínky)
- Copyright
- Repeat social links

---

## File structure

```
/
├── index.html
├── style.css
├── script.js          # minimal — smooth scroll, intersection observer, lucide.createIcons()
├── images/
│   ├── pavla.jpg
│   └── ebook.jpg
├── blog/
│   ├── index.html            # blog listing (future)
│   └── post-template.html    # single article (future)
└── CLAUDE.md
```

---

## Code conventions

- Semantic HTML5 elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`)
- Each section gets an `id` for anchor navigation (e.g. `id="stehovani"`, `id="zivot"`, `id="cestovani"`)
- BEM-like class naming: `.section-stehovani`, `.card`, `.card__icon`, `.card__title`, `.card__text`
- CSS custom properties for all colours, font sizes, spacing
- Mobile-first media queries (breakpoint at ~768px)
- All text content in Czech — use proper diacritics (č, ř, š, ž, etc.)
- Alt text on all images (in Czech)

---

## What NOT to do

- No emoji as icons
- No frameworks (React, Vue, Tailwind, Bootstrap)
- No build tools or package managers
- No placeholder lorem ipsum — use realistic Czech placeholder copy that reflects the actual content intent
- No images beyond `images/pavla.jpg` and `images/ebook.jpg` — all visual interest comes from typography, Lucide icons, colour, and layout
- Do not implement payment/checkout — buy buttons are links (hrefs to be filled in later)
