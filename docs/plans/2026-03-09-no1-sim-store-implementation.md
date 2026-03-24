# No. 1 Sim Store — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a realistic-looking mock sim racing retailer website for SRCP demo video recording.

**Architecture:** 4 static HTML pages sharing one CSS file and one JS file. No build tools, no frameworks. Working navigation between pages, hover dropdowns, stock photos. Open `index.html` in a browser to view.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox), vanilla JS, Google Fonts (Inter), Unsplash stock photos via URL.

**Design doc:** `docs/plans/2026-03-09-no1-sim-store-design.md`

---

## Task 1: Project Scaffolding

**Files:**
- Create: `css/styles.css` (empty)
- Create: `js/main.js` (empty)
- Create: `images/` (directory)

**Step 1: Create directory structure**

```bash
cd "/Users/istrommen/Desktop/Fake Sim Store"
mkdir -p css js images
touch css/styles.css js/main.js
```

**Step 2: Verify**

```bash
ls -R
```

Expected: `css/styles.css`, `js/main.js`, `images/`, `docs/plans/`

---

## Task 2: SVG Logo

**Files:**
- Create: `images/logo.svg`

**Step 1: Create the SVG logo**

Create an SVG logo with "NO.1" in bold with a checkered flag motif, "SIM STORE" below. Orange accent (`#ff6b2b`) for the "1" and flag elements. White text for the rest. Design should work at both nav size (~40px height) and be crisp at any scale.

The logo should incorporate:
- A racing checkered flag pattern as a small accent element (top-right corner or integrated into the "1")
- "NO.1" as the dominant text element with the "1" in orange
- "SIM STORE" as smaller text below
- Clean, modern sans-serif letterforms (manually drawn paths, not font-dependent)

**Step 2: Verify**

Open `images/logo.svg` in browser. Should display cleanly at various sizes.

---

## Task 3: Global Stylesheet

**Files:**
- Create: `css/styles.css`

**Step 1: Write the complete stylesheet**

This is the single largest file. It must include ALL styles for ALL pages. Organize into these sections with comment headers:

```
/* ===== RESET & BASE ===== */
/* ===== CSS CUSTOM PROPERTIES ===== */
/* ===== TYPOGRAPHY ===== */
/* ===== UTILITY TOP BAR ===== */
/* ===== NAVIGATION ===== */
/* ===== DROPDOWN MENUS ===== */
/* ===== FOOTER ===== */
/* ===== HERO SECTION (Homepage) ===== */
/* ===== BRAND BAR (Homepage) ===== */
/* ===== FEATURED CATEGORIES (Homepage) ===== */
/* ===== PROMO BANNER (Homepage) ===== */
/* ===== BUILDER PAGE ===== */
/* ===== WHEELBASES PAGE ===== */
/* ===== PRODUCT CARDS ===== */
/* ===== FILTER SIDEBAR ===== */
/* ===== CHECKOUT PAGE ===== */
/* ===== BUTTONS ===== */
/* ===== RESPONSIVE ===== */
```

**CSS Custom Properties (root):**

```css
:root {
  --bg: #2a2a2a;
  --surface: #333333;
  --border: #444444;
  --nav-bg: #1e1e1e;
  --text-primary: #f5f5f5;
  --text-secondary: #999999;
  --accent: #ff6b2b;
  --accent-hover: #ff8c42;
  --max-width: 1280px;
  --nav-height: 60px;
  --topbar-height: 36px;
}
```

**Key design specifications:**

- Body: `background: var(--bg); color: var(--text-primary); font-family: 'Inter', sans-serif;`
- Nav: sticky, `background: var(--nav-bg)`, logo left, links center-right, max-width container inside
- Dropdowns: `position: absolute`, `background: var(--nav-bg)`, appear on hover via CSS (`.nav-item:hover .dropdown`), smooth `opacity` transition. Shop dropdown as a single column list. Brands dropdown as a 3-column grid layout to fit 15 brands.
- Cards: `background: var(--surface)`, `border: 1px solid var(--border)`, `border-radius: 8px`, hover lift effect (`transform: translateY(-4px)`, `box-shadow`)
- Buttons: `.btn-primary` with `background: var(--accent)`, `color: white`, `border-radius: 6px`, hover to `var(--accent-hover)`
- Product grid: `display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px;`
- Footer: 3-column grid, `background: var(--nav-bg)`
- All images in cards: `width: 100%; aspect-ratio: 4/3; object-fit: cover;`
- Hero: `min-height: 500px`, background-image with gradient overlay
- Checkout: two-column grid (7fr / 5fr), form inputs styled to match dark theme

**Step 2: Verify**

Create a minimal test HTML file, open in browser, confirm colors/fonts render correctly. Delete test file after.

---

## Task 4: JavaScript

**Files:**
- Create: `js/main.js`

**Step 1: Write main.js**

Minimal JS for:

1. **Mobile menu toggle** — hamburger button toggles `.nav-menu.active` class
2. **Dropdown click-away** — close dropdowns when clicking outside (mobile fallback)
3. **Cart badge** — static, no JS needed (pure HTML/CSS)

```javascript
// Mobile menu toggle
document.addEventListener('DOMContentLoaded', () => {
  const hamburger = document.querySelector('.hamburger');
  const navMenu = document.querySelector('.nav-menu');

  if (hamburger) {
    hamburger.addEventListener('click', () => {
      navMenu.classList.toggle('active');
      hamburger.classList.toggle('active');
    });
  }

  // Close mobile menu when clicking a link
  document.querySelectorAll('.nav-link').forEach(link => {
    link.addEventListener('click', () => {
      navMenu.classList.remove('active');
      hamburger.classList.remove('active');
    });
  });
});
```

**Step 2: Verify**

Will be tested when HTML pages are built.

---

## Task 5: Homepage (`index.html`)

**Files:**
- Create: `index.html`

**Step 1: Write the complete homepage HTML**

Structure:

```
<!DOCTYPE html>
<html lang="en">
<head>
  - meta charset, viewport
  - title: "No. 1 Sim Store — Premium Sim Racing Equipment"
  - Google Fonts link (Inter: 400, 500, 600, 700)
  - link to css/styles.css
</head>
<body>
  <!-- UTILITY TOP BAR -->
  div.topbar > div.container
    - "Free Shipping on Orders Over $500"
    - account icon (SVG inline) + cart icon with badge "3"

  <!-- NAVIGATION -->
  nav.navbar > div.container
    - a.logo > img(src="images/logo.svg")
    - button.hamburger (3 spans for lines)
    - ul.nav-menu
      - li.nav-item > a "Shop" + div.dropdown.dropdown-shop
        - ul with 8 category links (only Wheelbases → wheelbases.html)
      - li.nav-item > a "Brands" + div.dropdown.dropdown-brands
        - div.brands-grid with 15 brand links (all href="#")
      - li.nav-item.nav-cta > a "Build Your Rig" → builder.html
      - li.nav-item > a "Turnkeys" (href="#")
      - li.nav-item > a "Support" (href="#")

  <!-- HERO SECTION -->
  section.hero
    - background: Unsplash sim racing image URL
    - div.hero-content
      - h1 "Your Setup. Your Way."
      - p "Premium sim racing gear from the brands you trust."
      - a.btn-primary "Build Your Rig" → builder.html

  <!-- BRAND BAR -->
  section.brand-bar > div.container
    - 6 brand name spans: Fanatec, Simucube, Moza, Heusinkveld, Trak Racer, Next Level Racing

  <!-- FEATURED CATEGORIES -->
  section.featured > div.container
    - h2 "Shop by Category"
    - div.category-grid (3 columns)
      - div.category-card × 3 (Wheelbases, Cockpits, Pedals)
        - img (Unsplash URLs)
        - h3 category name
        - a "Shop Now" (only Wheelbases links)

  <!-- PROMO BANNER -->
  section.promo-banner
    - "Free Expert Rig Consultation — Let us help you build the perfect setup"
    - a.btn-primary "Get Started"

  <!-- FOOTER -->
  footer > div.container
    - div.footer-grid (3 columns)
      - col 1: logo, address, phone, email
      - col 2: quick links list
      - col 3: newsletter input + button
    - div.footer-bottom: "© 2026 No. 1 Sim Store. All rights reserved."

  - script src="js/main.js"
</body>
</html>
```

**Unsplash image URLs to use:**

- Hero: Use a high-quality sim racing / racing cockpit image from Unsplash (search: sim racing, racing cockpit, racing simulator). Use the `?w=1920&q=80` params for optimal size.
- Category cards: Use relevant hardware/gaming/tech images.

**Step 2: Open in browser and verify**

Open `index.html` in browser. Check:
- Logo renders in nav
- Hover over "Shop" → dropdown with 8 categories appears
- Hover over "Brands" → dropdown with 15 brands in grid appears
- "Build Your Rig" is orange, links to builder.html
- Hero banner displays with gradient overlay and text
- Brand bar shows 6 brand names
- 3 category cards display
- Promo banner shows
- Footer renders 3 columns
- Cart badge shows "3"

---

## Task 6: Builder Page (`builder.html`)

**Files:**
- Create: `builder.html`

**Step 1: Write the complete builder page HTML**

Same `<head>`, nav, and footer as `index.html`. Body content:

```
<!-- BUILDER HERO -->
section.builder-header
  - div.container (centered, max-width: 900px)
    - h1 "Sim Rig Builder"
    - p "Build your perfect sim racing setup — we'll make sure everything works together."

<!-- SRCP EMBED AREA -->
section.builder-embed
  - div.embed-container (full-width, 800px min-height)
    - <!-- PASTE YOUR SRCP EMBED CODE HERE -->
    - div.embed-placeholder (dashed border, centered text: "Configurator Widget Loads Here")

<!-- TRUST BADGES -->
section.trust-badges > div.container
  - div.badges-grid (3 columns)
    - div.badge: checkmark icon + "Compatibility Guaranteed"
    - div.badge: headset icon + "Expert Support"
    - div.badge: truck icon + "Free Shipping"
```

The embed placeholder should be styled with:
- `border: 2px dashed var(--border)`
- `min-height: 800px`
- `display: flex; align-items: center; justify-content: center;`
- Muted text "Configurator Widget Loads Here"

When the user pastes their SRCP embed code (an iframe or script tag), they delete the placeholder div and the widget fills the container.

**Step 2: Open in browser and verify**

- Nav works, links back to index.html
- Heading and intro text display centered
- Placeholder box visible with dashed border
- Trust badges show below
- Footer renders

---

## Task 7: Wheelbases Page (`wheelbases.html`)

**Files:**
- Create: `wheelbases.html`

**Step 1: Write the complete wheelbases page HTML**

Same `<head>`, nav, and footer. Body content:

```
<!-- BREADCRUMB -->
div.breadcrumb > div.container
  - a "Home" → index.html > span "/" > a "Shop" (href="#") > span "/" > span "Wheelbases"

<!-- PAGE HEADER -->
section.page-header > div.container
  - h1 "Wheelbases"
  - p "Direct drive and belt-driven bases from top brands"

<!-- PRODUCT LAYOUT -->
section.products > div.container > div.products-layout
  - aside.filter-sidebar
    - h3 "Filters"
    - div.filter-group "Brand"
      - label > input[checkbox] + "Fanatec" (×3 brands)
    - div.filter-group "Price Range"
      - label > input[checkbox] + "$200 - $500", "$500 - $1,000", "$1,000+"
    - div.filter-group "Drive Type"
      - label > input[checkbox] + "Direct Drive", "Belt Drive"

  - div.product-grid (3 columns, 8 cards)
    - div.product-card × 8
      - div.product-image > img (Unsplash hardware/tech images)
      - span.brand-tag "Fanatec" (etc.)
      - h3.product-name
      - div.product-rating (★★★★★ or ★★★★☆)
      - p.product-price "$349.95" (etc.)
      - button.btn-primary "Add to Cart"
```

**Product data (hardcoded):**

| Product | Brand | Price | Stars |
|---------|-------|-------|-------|
| CSL DD (8Nm) | Fanatec | $349.95 | 5 |
| Gran Turismo DD Pro | Fanatec | $699.95 | 4.5 |
| R5 Bundle | Moza | $299.99 | 4 |
| R12 | Moza | $569.99 | 4.5 |
| Simucube 2 Sport | Simucube | $1,299.00 | 5 |
| Simucube 2 Pro | Simucube | $1,495.00 | 5 |
| ClubSport DD+ | Fanatec | $699.95 | 4.5 |
| R16 | Moza | $849.99 | 4.5 |

Use filled star character (★) and empty star (☆) for ratings. Half-stars can use a ★ with reduced opacity or just round to full stars for simplicity.

**Step 2: Open in browser and verify**

- Breadcrumb links work (Home → index.html)
- Filter sidebar displays on left
- 8 product cards in 3-column grid
- Cards have hover lift effect
- Brand tags colored
- Prices display correctly
- "Add to Cart" buttons are orange

---

## Task 8: Checkout Page (`checkout.html`)

**Files:**
- Create: `checkout.html`

**Step 1: Write the complete checkout page HTML**

Same `<head>`, nav, and footer. Body content:

```
<!-- CHECKOUT HEADER -->
section.checkout-header > div.container
  - h1 "Checkout"

<!-- CHECKOUT LAYOUT -->
section.checkout > div.container > div.checkout-grid
  - div.checkout-form
    - h2 "Shipping Information"
    - form (no action, no submit)
      - div.form-row: label "Email" + input (pre-filled: "alex.thompson@email.com")
      - div.form-row: label "First Name" + input ("Alex")
      - div.form-row: label "Last Name" + input ("Thompson")
      - div.form-row: label "Address" + input ("1247 Racing Line Drive")
      - div.form-row.form-row-half:
        - label "City" + input ("Austin")
        - label "State" + select ("TX")
      - div.form-row: label "ZIP Code" + input ("78701")
    - h2 "Payment Method"
    - div.payment-placeholder
      - text: "Credit card form would appear here"
      - (subtle dashed box, similar style to builder embed placeholder)

  - div.order-summary
    - h2 "Order Summary"
    - div.order-items
      - div.order-item × 3:
        1. img + "Fanatec CSL DD (8Nm)" + "Qty: 1" + "$349.95"
        2. img + "Trak Racer TR80 Cockpit" + "Qty: 1" + "$599.99"
        3. img + "Heusinkveld Sprint Pedals" + "Qty: 1" + "$749.00"
    - div.order-totals
      - Subtotal: $1,698.94
      - Shipping: FREE
      - Tax: $140.16
      - Total: $1,839.10
    - button.btn-primary.btn-full "Place Order"
```

All form inputs pre-filled with fake data so it looks like a checkout in progress.

**Step 2: Open in browser and verify**

- Two-column layout displays
- Form fields are pre-filled
- Order summary shows 3 items with thumbnails
- Totals calculate correctly (visually)
- "Place Order" button is orange, full-width within summary

---

## Task 9: Visual Polish & Cross-Page Verification

**Step 1: Navigate all pages in sequence**

Open `index.html` in browser and navigate:
1. Homepage → click "Build Your Rig" → Builder page
2. Builder → click "Shop" dropdown → "Wheelbases" → Wheelbases page
3. Wheelbases → click cart icon or navigate to checkout.html
4. Verify footer links work back to homepage

**Step 2: Check hover states**

- Shop dropdown appears/disappears smoothly
- Brands dropdown shows 15 brands in grid
- Product cards lift on hover
- Buttons change to hover color
- "Build Your Rig" nav item is visually distinct (orange)

**Step 3: Verify desktop optimization**

- At 1280px+ width, all layouts look polished
- No horizontal scroll
- Images load from Unsplash URLs
- Text is readable against dark gray backgrounds

**Step 4: Final tweaks**

Fix any spacing, alignment, or color issues spotted during review.

---

## Parallelization Notes

- **Tasks 1-4** are sequential (scaffolding → logo → CSS → JS)
- **Tasks 5-8** (the 4 HTML pages) can be built in parallel once Tasks 1-4 are complete, as they all share the same CSS/JS/logo
- **Task 9** must run last (cross-page verification)

## Image Strategy

Use Unsplash source URLs with size parameters for reliable, high-quality images. Example pattern:
- `https://images.unsplash.com/photo-XXXXX?w=800&q=80`

Search for: sim racing, racing simulator, gaming setup, racing cockpit, racing wheel, computer hardware for relevant imagery. Download key images to `images/` directory for reliability rather than hotlinking.
