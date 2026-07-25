# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for Esporte Clube Itapetininga (EC Itapetininga), a sports club founded in 1950 in Itapetininga, São Paulo, Brazil. The site showcases the club's history, youth football academy categories, sponsorship opportunities, and contact information.

## Tech Stack

- **Frontend**: Vanilla HTML5, CSS3, and JavaScript (no frameworks)
- **Fonts**: Google Fonts (Inter, Bebas Neue, Barlow Condensed, Material Symbols)
- **Third-party**: VLibras (Brazilian Sign Language widget)
- **Development**: Live Server (VS Code extension, port 5501)

## Development Commands

### Running the Site Locally

```bash
# Using VS Code Live Server extension (configured on port 5501)
# Right-click index.html and select "Open with Live Server"
# OR install a simple HTTP server:

# Using Python 3
python -m http.server 5501

# Using Node.js http-server
npx http-server -p 5501
```

No build process, bundler, or compilation required - this is a static site that can be opened directly in a browser.

## Code Architecture

### File Structure

```
arquivo/
├── index.html          # Single-page application with all content
├── styles.css          # All styles in one file
├── img/               # Images and logos
│   ├── eci.png        # Club logo
│   ├── adfmi.png      # Partner logo
│   └── [others]       # Historical photos, jerseys, etc.
└── .vscode/
    └── settings.json  # Live Server configuration
```

### HTML Structure (index.html)

The site is organized as a single-page application with anchor-linked sections:

1. **Header** (`<header class="site-header">`)
   - Top navigation bar with logo and links
   - Mobile hamburger menu
   - Desktop support CTA button

2. **Main Sections** (in order):
   - `#hero` - Hero section with main tagline
   - `#history` - Club history timeline and milestones
   - Legends section - Notable players/coaches (Vadão, Carlinhos Itaberá, etc.)
   - Archive section - Historical photos carousel
   - `#categories` - Youth academy categories (Sub-11, Sub-13, Sub-15, Sub-17)
   - `#support` - Sponsorship information
   - `#contact` - Contact form and location map

3. **Modal** (`#support-modal`)
   - Support/donation modal with PIX payment info
   - Triggered by multiple CTAs throughout the page

4. **Footer**
   - Partnership logos (ECI + ADFMI)
   - Navigation links
   - Legal information

5. **Accessibility Panel**
   - Floating accessibility widget with contrast, font size, cursor controls
   - Text-to-speech functionality
   - VLibras integration for Brazilian Sign Language

### CSS Architecture (styles.css)

- **CSS Custom Properties**: All colors and spacing use CSS variables defined in `:root`
- **Utility-first approach**: Uses Tailwind-like utility classes (`flex`, `grid`, `text-*`, etc.)
- **Component-specific styles**: Scoped to specific sections (`.hero-section`, `.academy-card`, etc.)
- **Responsive Design**: Mobile-first with `@media` queries for tablet/desktop
- **High Contrast Mode**: `.ativo` class toggles high-contrast theme for accessibility

Key CSS variables:
- Primary colors: `--primary`, `--primary-container`, `--primary-fixed-dim`
- Secondary (yellow/gold): `--secondary-container`, `--secondary-fixed`
- Surface colors: `--surface-container-*` hierarchy
- Semantic colors: `--on-surface`, `--on-secondary-container`

### JavaScript Functionality

All JavaScript is inline in `index.html` (lines 929-1324):

1. **Modal Management** (lines 930-1067)
   - Opens/closes support modal
   - Manages focus trap and keyboard navigation
   - Hash-based deep linking (`#support-modal`)

2. **Mobile Menu** (lines 996-1018)
   - Toggle hamburger menu
   - Auto-close on link click or window resize

3. **Navigation** (lines 954-994)
   - Active link highlighting based on scroll position
   - Sticky header with scroll-based styling
   - Smooth scrolling to sections

4. **Contact Form** (lines 1161-1165)
   - Prevents default submission
   - Shows success message
   - Resets form fields

5. **Accessibility Features** (lines 1169-1324)
   - High contrast toggle (`alternarCores()`)
   - Font size controls (`aumentarFonte()`, `diminuirFonte()`)
   - Large cursor mode (`cursorGrande()`)
   - Text-to-speech (`lerPagina()`, `lerSelecao()`, `pararLeitura()`)
   - Accessibility menu open/close with keyboard support

## WCAG Compliance

This site has been extensively audited for WCAG (Web Content Accessibility Guidelines) compliance. Throughout the code you'll find comments like `<!-- WCAG fix: X.X.X -->` referencing specific success criteria:

- **1.1.1** - Text alternatives for images
- **1.3.1** - Info and relationships (semantic HTML)
- **1.4.3** - Contrast ratios
- **2.1.1** - Keyboard accessibility
- **2.4.3** - Focus order and management
- **3.3.2** - Labels and instructions for forms
- **4.1.2** - Name, role, value for UI components

**Important**: When modifying the site, maintain these accessibility standards. Always:
- Include proper `aria-label`, `aria-labelledby`, `aria-expanded`, `aria-pressed` attributes
- Ensure focus management in modals and menus
- Maintain keyboard navigation support
- Use semantic HTML elements
- Keep color contrast ratios compliant

## Content and Localization

- **Language**: Brazilian Portuguese (`lang="pt-BR"`)
- **Club Information**:
  - Founded: December 26, 1950 (originally as DERAC)
  - Renamed: 1994 to Esporte Clube Itapetininga
  - Current focus: Youth academy (Sub-11, Sub-13, Sub-15, Sub-17)
  - Partner: ADFMI (Associação Desportiva dos Funcionários Municipais de Itapetininga)

## Design System

The site uses a Material Design-inspired color system with club colors:

- **Primary (Blue)**: `#001241`, `#082567` - Club's traditional navy blue
- **Secondary (Yellow/Gold)**: `#fccc00`, `#ffe085` - Club's accent color
- **Typography**:
  - Body: Inter (weights: 400, 500, 600, 700)
  - Headlines: Bebas Neue, Barlow Condensed (weights: 500, 600, 700)
  - Icons: Material Symbols Outlined

## Common Modifications

### Adding a New Section

1. Add section markup in `index.html` between `<main>` tags
2. Add corresponding nav link in both desktop (`<nav class="site-nav">`) and mobile menu
3. Update `topNavLinks` and `sections` in JavaScript for scroll-based active state
4. Add section-specific styles in `styles.css`

### Updating Club Information

- Contact info: Lines 571-596 in `index.html`
- PIX/CNPJ: Lines 757-761 in `index.html`
- Footer info: Lines 809-811 in `index.html`

### Modifying Accessibility Features

All accessibility JavaScript is at the bottom of `index.html` (lines 1237-1324). The accessibility panel is defined in lines 889-928.

### Images

Images are stored in `/img/` and include:
- Club logos (eci.png, jersey.png)
- Partner logos (adfmi.png, adfmi-footer.png)
- Historical photos (1950.jpg, 1994.jpg, hoje.jpg)
- Player/coach photos (Vadao_2015.jpg, itabera.jpg, marquinho.jpg, etc.)
