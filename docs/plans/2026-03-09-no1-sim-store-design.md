# No. 1 Sim Store — Design Document

## Purpose

Mock sim racing retailer website used as a backdrop for an SRCP (Sim Rig Configurator Product) demo video. Not a real store — needs to look realistic on camera during screen recording.

## Technical Approach

**Option chosen:** Multi-page static HTML (Option A)

4 separate HTML files sharing a common CSS file. Working navigation between all pages. No build tooling — open `index.html` in a browser.

### File Structure

```
Fake Sim Store/
├── index.html          # Homepage
├── builder.html        # Sim Rig Builder (SRCP embed)
├── wheelbases.html     # Product category page
├── checkout.html       # Fake checkout
├── css/
│   └── styles.css      # All styles
├── js/
│   └── main.js         # Cart badge, mobile menu, dropdown hovers
└── images/             # Stock photos for hero and products
```

## Design Specifications

### Color Palette

| Token | Value | Usage |
|-------|-------|-------|
| Background | `#2a2a2a` | Page body |
| Surface | `#333333` | Cards, inputs |
| Border | `#444444` | Subtle dividers |
| Nav/Footer | `#1e1e1e` | Header, footer bg |
| Text Primary | `#f5f5f5` | Headings, body |
| Text Secondary | `#999999` | Captions, muted |
| Accent | `#ff6b2b` | CTAs, highlights |
| Accent Hover | `#ff8c42` | Button hovers |

### Typography

Inter (Google Fonts) or system sans-serif fallback. Clean weight hierarchy.

### Logo

Custom SVG logo — "NO.1 SIM STORE" with a stylized racing flag or steering wheel motif, using the orange accent color.

## Shared Layout (All Pages)

### Utility Top Bar
- Small dark bar (`#1e1e1e`)
- "Free shipping on orders over $500" centered
- Account icon + Cart icon (with "3" badge) on the right

### Navigation
- Logo "NO. 1 SIM STORE" on the left (SVG)
- Menu items center-right:
  - **Shop** — hover dropdown with categories:
    - Wheelbases (links to `wheelbases.html`)
    - Cockpits & Rigs (dead link)
    - Pedals (dead link)
    - Steering Wheels (dead link)
    - Seats (dead link)
    - Shifters & Handbrakes (dead link)
    - Accessories (dead link)
    - Monitors & Mounts (dead link)
  - **Brands** — hover dropdown with 15 brands (all dead links):
    - Fanatec, Simucube, Moza, Heusinkveld, Trak Racer, Next Level Racing, Ascher Racing, Cube Controls, Simagic, Thrustmaster, Logitech, Sparco, OMP, Precision Sim Engineering, Ricmotech
  - **Build Your Rig** — orange highlighted CTA, links to `builder.html`
  - **Turnkeys** — dead link
  - **Support** — dead link
- Cart icon with "3" badge

### Footer
- 3-column layout:
  - Column 1: Store info — "No. 1 Sim Store" + fake address, phone, email
  - Column 2: Quick links — Shop, Brands, Builder, Support, Returns, FAQ
  - Column 3: Newsletter signup (fake input + button)
- Copyright bar at bottom

## Page Designs

### 1. Homepage (`index.html`)

**Hero Banner:**
- Full-width, ~500px tall
- Sim racing lifestyle stock photo (cockpit/rig setup)
- Dark gradient overlay on left side for text readability
- Heading: "Your Setup. Your Way."
- Subtitle: "Premium sim racing gear from the brands you trust."
- Orange CTA button: "Build Your Rig" → `builder.html`

**Brand Logo Bar:**
- Horizontal strip below hero
- Slightly darker background
- Brand names displayed: Fanatec, Simucube, Moza, Heusinkveld, Trak Racer, Next Level Racing

**Featured Categories:**
- 3-column grid of category cards:
  - Wheelbases (links to `wheelbases.html`)
  - Cockpits (dead link)
  - Pedals (dead link)
- Each card: stock photo, category name, "Shop Now" link

**Promo Banner:**
- Full-width orange-accent strip
- "Free Expert Rig Consultation — Let us help you build the perfect setup"
- CTA button

### 2. Sim Rig Builder (`builder.html`)

**Heading Section:**
- Centered layout
- H1: "Sim Rig Builder"
- Intro text: "Build your perfect sim racing setup — we'll make sure everything works together."

**Embed Area:**
- Full-width container, 800px height
- HTML comment: `<!-- PASTE YOUR SRCP EMBED CODE HERE -->`
- Default state: subtle dashed-border box with "Widget loads here" text

**Trust Section (below embed):**
- Three icon-text badges in a row:
  - Compatibility Guaranteed
  - Expert Support
  - Free Shipping

### 3. Wheelbases (`wheelbases.html`)

**Breadcrumb:** Home > Shop > Wheelbases

**Page Title:**
- "Wheelbases"
- Subtitle: "Direct drive and belt-driven bases from top brands"

**Filter Sidebar (visual only, left column):**
- Fake checkboxes for Brand, Price Range, Drive Type
- Non-functional

**Product Grid (3 columns, 8 cards):**

| # | Product | Price |
|---|---------|-------|
| 1 | Fanatec CSL DD (8Nm) | $349.95 |
| 2 | Fanatec Gran Turismo DD Pro | $699.95 |
| 3 | Moza R5 Bundle | $299.99 |
| 4 | Moza R12 | $569.99 |
| 5 | Simucube 2 Sport | $1,299.00 |
| 6 | Simucube 2 Pro | $1,495.00 |
| 7 | Fanatec ClubSport DD+ | $699.95 |
| 8 | Moza R16 | $849.99 |

Each card:
- Product stock photo
- Brand tag
- Product name
- Price
- Star rating (4-5 stars)
- "Add to Cart" button (orange)

### 4. Checkout (`checkout.html`)

**Two-column layout:**

**Left — Shipping Form (pre-filled with fake data):**
- Name, email, address, city, state, zip
- All fields pre-populated so it looks like a real checkout in progress

**Right — Order Summary:**
- 2-3 items showing a configurator-style bundle:
  - Wheelbase (e.g., Fanatec CSL DD)
  - Cockpit (e.g., Trak Racer TR80)
  - Pedals (e.g., Heusinkveld Sprint)
- Each item: small thumbnail, name, quantity, price
- Subtotal, shipping, tax, total
- Orange "Place Order" button

## Images

Real stock photos from Unsplash for maximum realism:
- Hero: sim racing cockpit/lifestyle shot
- Product cards: wheelbase hardware photos
- Category cards: relevant component imagery

## Interactivity

- Nav links work between all 4 pages
- Shop and Brands dropdowns appear on hover
- Cart badge shows static "3" count
- Mobile menu toggle (hamburger)
- All other buttons/links are visual-only (dead links)
