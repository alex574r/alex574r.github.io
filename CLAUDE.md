# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Alejandro Hernández Maya (Fullstack Developer). Static site hosted on GitHub Pages — no build tools, no bundler, no package manager. All HTML/CSS/JS is hand-written and served directly.

## Architecture

The site is a multi-page static portfolio in Spanish (`lang="es"`):

- **`index.html` + `index.css`** — Main landing page (hero, experience, education, projects, contact, footer). All JavaScript is inlined in a `<script>` block at the bottom of the HTML.
- **`pSoftware/Software.html` + `pSoftware/Style.css`** — Software projects gallery page.
- **`pArte/Arte.html` + `pArte/Estilo.css`** — Art/illustration gallery page.
- **`img/`** — Shared images organized by page (`img/index/`, `img/arte/`, `img/software/`).
- **`archivos/CV.pdf`** — Downloadable resume.

There are no external JS files — all scripts are inline `<script>` tags at the end of each HTML file.

## Key Dependencies (CDN only)

- **GSAP 3.12.5** — Animation engine (gsap, Flip, CustomEase on index; gsap, ScrollTrigger on Software page)
- **Lenis 1.0.42** — Smooth scroll (Software page only)
- **Google Fonts** — Inter, Playfair Display, Cormorant Garamond, IBM Plex Mono, Pixelify Sans

## Development

No build step. Open HTML files directly in a browser or use any static file server:

```
# Python
python -m http.server 8000

# Node (npx)
npx serve .
```

## Design System

CSS custom properties are defined in `:root` in `index.css`. Key tokens:
- Primary accent: `--c-primary: #e95e3f`
- Dark background: `--c-dark: #141414`
- Light text: `--c-light: #CFCFCF`
- Typography: Inter (body), Playfair Display (headings), IBM Plex Mono (monospace accents)

The navbar and project cards use a "liquid glass" effect via SVG `feDisplacementMap` filter with `backdrop-filter`. Each page embeds the same inline SVG filter (`#glass-liquid`). Fallbacks for Firefox/Safari are handled via `@supports not (backdrop-filter: url(#x))`.

## Animation Patterns

The index page has a multi-phase entry animation orchestrated with GSAP timelines:
1. Revealer panels (clip-path wipe)
2. Image sequence (scale/fade)
3. Flip transition to stacked layout
4. Hero text/nav reveal (clip-path + translateY)
5. Scroll-triggered `.reveal` class for below-fold sections

Scroll reveal uses an IntersectionObserver that adds the `.revealed` class.

## Conventions

- Content is in Spanish — keep all user-facing text in Spanish.
- CSS is organized by section with comment block separators (`/* === SECTION NAME === */`).
- Responsive breakpoints: 900px (tablet), 600px (mobile).
