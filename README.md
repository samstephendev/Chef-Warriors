# The Chef Warriors — Website

A responsive, single-page marketing site for **The Chef Warriors** fast-food chain in Madurai.  
Built with plain HTML5 and CSS3 — no frameworks, no build tools, no JavaScript.

---

## File structure

```
/
├── index.html        — Main page (all sections)
├── styles.css        — All styles (mobile-first, three breakpoints)
├── README.md         — This file
└── assets/
    ├── logo.svg      — Brand logo (round, 44 × 44 px in nav; 48 × 48 px in visit tile)
    ├── bucket.svg    — Chicken bucket illustration (hero + menu tiles)
    ├── burger.svg    — Burger illustration (menu tile)
    └── shawarma.svg  — Shawarma wrap illustration (menu tile)
```

---

## How to view

Open `index.html` directly in any modern browser — no server required.  
For live reload during editing, run any static server, e.g.:

```bash
# Python 3
python -m http.server 8080

# Node (npx)
npx serve .
```

Then open `http://localhost:8080`.

---

## How to swap in real food photos

### 1. Replace SVG illustrations with photos

Each illustration in `assets/` (`bucket.svg`, `burger.svg`, `shawarma.svg`) is referenced with a plain `<img>` tag.  
To swap:

1. Drop your photo files into `assets/` (JPEG or WebP recommended for photos).
2. Update the `src` attribute on the relevant `<img>` element in `index.html`.
3. Update the `width` / `height` attributes to match your photo's natural dimensions (helps the browser reserve space).

Example — replacing the hero bucket:
```html
<!-- Before -->
<img src="assets/bucket.svg" … class="hero__bucket" width="470" height="588" …>

<!-- After -->
<img src="assets/bucket-photo.webp" … class="hero__bucket" width="470" height="600" …>
```

### 2. Add food photos to menu tiles

Each `.tile` card is currently colour-gradient only.  
To add a background food photo:

1. Add a class like `tile--photo` to the tile in `index.html`.
2. In `styles.css`, add:

```css
.tile--photo {
  background-image: url('assets/wings-bucket-photo.webp');
  background-size: cover;
  background-position: center;
}
```

3. Optionally add a dark overlay so the text remains legible:

```css
.tile--photo::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to top,
    rgba(13, 11, 10, 0.85) 40%,
    rgba(13, 11, 10, 0.30) 100%
  );
  border-radius: inherit;
}
```

### 3. Replace the logo

Drop your `logo.png` (preferably a square PNG with a transparent background, 200 × 200 px or larger) into `assets/`.  
The `onerror` fallback on the `<img>` will hide the broken image and show the "CW" text badge instead if the file is missing.

### 4. Optimise images for the web

For best performance:

- Use **WebP** format (better compression than JPEG/PNG).
- Target: hero bucket ≤ 120 KB, tile backgrounds ≤ 60 KB each.
- Add `loading="lazy"` to images below the fold (tiles, visit logo).
- Consider adding `srcset` for retina displays.

Example:
```html
<img
  src="assets/bucket-photo.webp"
  alt="A large red fried chicken bucket overflowing with crispy chicken"
  class="hero__bucket"
  width="470" height="600"
  loading="eager"
/>
```

---

## Breakpoints

| Breakpoint  | Width      | Notes                                              |
|-------------|------------|----------------------------------------------------|
| Mobile      | `< 768px`  | 1 column nav, stacked hero, 2-col bento, sticky bar |
| Tablet      | `≥ 768px`  | Side-by-side hero, 4-col menu, row footer          |
| Desktop     | `≥ 1100px` | Full nav links, floating chips, max-size headlines  |

---

## Contacts & links used in the site

| Purpose          | Value                                                        |
|------------------|--------------------------------------------------------------|
| Phone            | +91 97311 89551                                             |
| KK Nagar map     | https://www.google.com/maps/search/?api=1&query=Chef+Warriors+Shop+313+KK+Nagar+Madurai |
| Instagram        | https://www.instagram.com/the_chef_warriors_                |
| Facebook         | https://www.facebook.com/profile.php?id=61562975605877      |
