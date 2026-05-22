# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```sh
npm run dev       # dev server at localhost:4321
npm run build     # production build → ./dist/
npm run preview   # preview built site locally
npm run astro ... # Astro CLI (e.g. astro add, astro check)
```

Requires Node ≥ 22.12.0.

## Stack

- **Astro 6** — file-based routing, pages in `src/pages/`
- **Tailwind CSS v4** — loaded via `@tailwindcss/vite` Vite plugin (no `tailwind.config.*`)
- **GSAP 3** — available for animations (installed, not yet used)
- **TypeScript** — strict mode (`astro/tsconfigs/strict`)

## CSS Architecture

Three files compose the global stylesheet, imported in order inside `src/styles/global.css`:

1. `fonts.css` — Google Fonts import (Inter + Instrument Serif)
2. `tailwindcss` — Tailwind base
3. `theme.css` — `@theme` overrides (`--font-sans`, `--font-serif`) and custom `@utility` animation classes (`animate-fade-rise`, `animate-fade-rise-delay`, `animate-fade-rise-delay-2`)

Custom animation utilities live in `theme.css` using Tailwind v4 `@utility` syntax — not `tailwind.config.*` plugins.

## Page Structure

Single page (`src/pages/index.astro`). Layout pattern:

- Root container with `overflow-hidden` and `relative min-h-screen`
- Video background layer (`z-0`, absolute) with inline `requestAnimationFrame` loop for fade-in/fade-out at loop boundaries
- Nav and hero sections (`z-10`, relative) layered above video

Inline `<script>` at bottom of `index.astro` handles all video playback logic (no separate JS module).

## Design Tokens

Brand uses two colors: `black` (#000) and muted gray `#6F6F6F`. No Tailwind color aliases defined — use hex directly in classes or inline styles.
Fonts: `font-serif` = Instrument Serif, `font-sans` = Inter.
