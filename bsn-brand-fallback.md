# BSN Brand Fallback
## Used when bsn-tools:bsn-brand MCP fetch is unavailable

This file is the local fallback for BSN brand standards. It is intentionally lightweight — it contains only the minimum tokens needed to produce on-brand HTML output. It is not a substitute for the full brand specification. Always prefer the MCP fetch.

When this file is used, every generated HTML file must include this notice in its version header comment:
```html
<!-- NOTICE: Brand applied from local fallback (bsn-brand-fallback.md).
     MCP server was unavailable at generation time.
     Verify output against current brand standards before sharing. -->
```

---

## Colors

```css
:root {
  --bsn-navy:    #082f49;  /* Primary dark background — hero, header, footer */
  --bsn-teal:    #308c83;  /* Cards, borders, checkmarks, standard accents */
  --bsn-mint:    #01ffe1;  /* Accent ONLY — badge borders, CTA strips, accent lines */
  --bsn-purple:  #39426f;  /* Secondary card / pillar color */
  --bsn-seafoam: #c1ddd8;  /* Footer text on dark backgrounds */
  --bsn-charcoal:#4c5454;  /* Body copy on light backgrounds */
  --bsn-lgray:   #d8dbe2;  /* Muted labels, subtext */
  --bsn-lblue:   #d1faff;  /* Secondary light fills */
  --bsn-mist:    #dde1ea;  /* Borders, fine separators */
  --bsn-white:   #ffffff;
  --bsn-slide:   #f0f8fb;  /* Light presentations, text-dense layouts */
}
```

**Hard rules:**
- `#01ffe1` (Electric Mint) is an accent only — never a fill, background, or button background
- Cream / beige (e.g. `#F8F6F1`) is outdated — do not use
- Navy is the primary dark background; `#f0f8fb` is the primary light background

---

## Typography

| Role | Font | Fallback stack |
|---|---|---|
| Headings (H1, H2, hero) | Jubilat Bold | `'Georgia', 'Playfair Display', serif` |
| Subheads (H3, H4) | Halyard Display SemiBold | `'Montserrat', 'Nunito Sans', sans-serif` |
| Body copy | Halyard Display Regular | `'Montserrat', 'Nunito Sans', sans-serif` |
| Captions / footnotes | Halyard Display Light | `'Montserrat', 'Nunito Sans', sans-serif` |
| Pill / badge labels | Halyard Display SemiBold, uppercase, tracked | `'Montserrat', sans-serif` |

**Google Fonts import for fallback:**
```css
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700;800&display=swap');
```

**Key rule:** Jubilat (or Georgia fallback) for headings only. Montserrat for everything else. Never swap them.

---

## Required structural elements

Every HTML output must include all of these:

### 1. Electric accent lines
Thin `#01ffe1` horizontal line (2px) directly below the header and directly above the footer.

```css
header::after, footer::before {
  content: '';
  display: block;
  height: 2px;
  background: #01ffe1;
}
```

### 2. Header
Navy (`#082f49`) background. White heading text in Jubilat/Georgia. Hex dot texture at low opacity.

### 3. Footer
Navy (`#082f49`) background. Seafoam (`#c1ddd8`) text. Must include: `"Internal use only — confidential"`

### 4. Hex dot texture
Applied to hero/header backgrounds. CSS implementation:

```css
background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='28' height='32' viewBox='0 0 28 32'><polygon points='14,2 26,9 26,23 14,30 2,23 2,9' fill='none' stroke='%23308c83' stroke-opacity='0.08' stroke-width='1'/></svg>");
background-repeat: repeat;
```

### 5. Cards
White background, teal glowing border:
```css
box-shadow: 0 0 0 1px #308c83, 0 0 12px rgba(48,140,131,0.25);
border-radius: 8px;
```

Use electric mint glow (`#01ffe1`) for CTA or highlighted cards only.

### 6. Pill badges
```css
background: #082f49;
border: 1px solid #01ffe1;
color: #ffffff;
font-size: 10px;
font-weight: 700;
letter-spacing: 0.12em;
text-transform: uppercase;
padding: 4px 12px;
border-radius: 999px;
```

### 7. Teal checkmarks
Filled teal circle with white checkmark — use for feature lists and inclusion lists in place of standard bullets.

---

## Layout modes

**Dark mode** (hero, marketing, social): Navy background throughout.

**Light mode** (internal reports, multi-page documents): White or `#f0f8fb` background with charcoal body text.

**Dark/light sandwich** (presentations, decks): Navy header + navy footer, light body in between. Preferred for most skill outputs.

---

## HTML output pattern

Minimum structure for every generated HTML file:

```html
<!-- Version header comment here -->
<header style="background:#082f49; background-image:[hex dot texture]; padding:28px 40px 24px; position:relative;">
  <!-- header::after mint line applied via CSS -->
  <h1 style="font-family:Georgia,serif; font-weight:700; color:#ffffff;">Document title</h1>
  <p style="color:#c1ddd8; font-family:'Montserrat',sans-serif;">Subtitle or descriptor</p>
  <span class="pill-badge">Internal use only</span>
</header>

<main style="background:#f0f8fb; padding:36px 40px;">
  <!-- Content here — white or #f0f8fb background, charcoal body text -->
</main>

<footer style="background:#082f49; padding:16px 40px; position:relative;">
  <!-- footer::before mint line applied via CSS -->
  <p style="color:#c1ddd8; font-family:'Montserrat',sans-serif; font-size:11px;">
    Breach Secure Now — Internal use only — confidential
  </p>
</footer>
```

---

## Hard rules — always enforced

1. `#01ffe1` is an accent only — thin lines, badge borders, small moments. Never fills.
2. No underlines beneath titles — use whitespace to separate.
3. Left-align all body text. Center titles only.
4. Jubilat/Georgia for headings. Montserrat for everything else. Never swapped.
5. Every output includes the confidential footer: *"Internal use only — confidential"*
6. Electric accent lines under every header, above every footer — no exceptions.
7. Always use the ℠ mark after "AI Risk to Adoption Program" and "AI Adoption Suite" — every occurrence.

---

## What to do if this file is also missing

If both the MCP fetch and this fallback file are unavailable, apply these absolute minimums and flag the output:

- Navy `#082f49` header, white text, Georgia serif headings
- `#f0f8fb` body background, `#4c5454` body text, Montserrat
- Thin `#01ffe1` line under header and above footer
- Footer with "Internal use only — confidential" in `#c1ddd8` on navy
- Add to version header comment: `NOTICE: Brand fallback file missing. Minimum brand tokens applied. Full review required before sharing.`
