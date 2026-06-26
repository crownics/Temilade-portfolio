# Temilade Adekeye — Product Designer Portfolio

A single-page portfolio site built as static HTML/CSS/JS — no framework, no build step. Open `index.html` directly in a browser or deploy as-is to Vercel/Netlify.

## Structure

```
portfolio/
├── index.html        ← Entire site (markup, styles, and routing logic)
├── README.md          ← This file
└── assets/            ← All images (hero photo + case study screenshots)
```

## How it works

- **Single HTML file, multiple "pages."** Each project case study is a `<div class="page">` with a unique `id` (e.g. `#snappay`, `#vegaz`, `#zoldtyme`). Only one `.page` has the `active` class at a time — that's the one currently visible.
- **Navigation** is handled by a tiny vanilla JS function at the bottom of the file:
  ```js
  function showPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  }
  ```
  Every link/button that switches views calls `showPage('project-id')` via `onclick`.
- **No routing library, no React, no bundler.** Everything — including animations — is plain CSS (`@keyframes`, `transition`) and a few inline `style="animation-delay:..."` attributes for staggered entrance effects.
- **Images** are referenced with relative paths like `assets/Frame_30.png`. As long as the `assets/` folder stays next to `index.html`, nothing breaks when you move or rename the project folder.

## Pages / sections included

- `#home` — Hero (with photo), featured project, full project grid, About, Contact, footer
- `#snappay`, `#vegaz`, `#zoldtyme`, `#prism`, `#fintrack`, `#lwc`, `#genzaar`, `#linqit`, `#keepevery`, `#campushire` — full case studies, each with their own hero, meta bar, cover image, and detailed sections (personas, design systems, wireframes, final screens, etc.)

Each case study page has **Previous / Next** navigation at the bottom (`cs-footer-nav`) wired to the adjacent project in the sequence: Snappay → Vegaz → Zoldtyme → Prism → Fintrack → LWC → Genzaar → Linqit → Keepevery → CampusHire → back to home.

## Editing content

To change copy or swap an image:
1. Find the relevant `<div id="...">` block in `index.html` (search for the project name)
2. Edit text directly inside the `<p>`, `<h1>`, `<h2>` tags
3. To swap an image, replace the file in `assets/` (keep the same filename) or update the `src="assets/..."` path

To add a new project:
1. Duplicate an existing `<div id="..." class="page">...</div>` block
2. Give it a new unique `id`
3. Add a corresponding card in the `.work-grid` on the home page with `onclick="showPage('your-new-id')"`
4. Update the Previous/Next buttons on the adjacent pages to slot the new project into the sequence

## Theme

- **Colors:** White background (`#FFFFFF`), near-black text/accents (`#111111`), light grey card backgrounds (`#FAFAFA`)
- **Fonts:** [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) (serif, headings) + [Outfit](https://fonts.google.com/specimen/Outfit) (sans, body) — both loaded via Google Fonts `@import` at the top of the `<style>` block
- **Animations:** Fade-up entrances on hero text and project cards (staggered via `animation-delay`), hover lift/shadow on cards and buttons, a pulsing "available" status dot

## Deployment

This is a fully static site — no server, no build step required.

- **Vercel / Netlify:** drag the whole `portfolio` folder onto their dashboard, or run `vercel` / `netlify deploy` from inside this folder
- **GitHub Pages:** push this folder to a repo and enable Pages on the `main` branch root
- **Anywhere else:** any static file host works — just make sure `assets/` is uploaded alongside `index.html`

## Possible next steps in Claude Code

- Convert to a proper front-end framework (Vite + React, Astro, etc.) if you want component-based editing
- Add a contact form backend (e.g. Formspree, Resend) instead of the `mailto:` link
- Set up Git + CI/CD for automatic redeploys on push
- Add image optimization / lazy-loading for faster load times (some screenshots are large PNGs)
