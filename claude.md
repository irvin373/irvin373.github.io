# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # dev server at localhost:4321
npm run build     # static build → dist/
npm run preview   # serve dist/ locally
```

No test runner, no linter configured.

## Architecture

Single-page Astro v4 portfolio for Irvin Cossio. One route: `src/pages/index.astro` composes six section components in order: `Nav → Hero → About → Experience → Projects → Contact`, all wrapped in `src/layouts/Layout.astro`.

**Styling approach — critical detail:**
- Tailwind is loaded via **CDN** (`<script is:inline src="https://cdn.tailwindcss.com">`), not as an Astro integration. Tailwind config (custom colors, fonts) lives in a `<script is:inline>` block in `Layout.astro` that must appear *before* the CDN script.
- All component styles use `<style is:global>` (not scoped). CSS custom properties defined in `Layout.astro` are the design tokens; use them everywhere.
- Lucide icons are loaded via CDN (`unpkg.com/lucide`). Icons render via `<i data-lucide="icon-name">` + a `lucide.createIcons()` call on `DOMContentLoaded` in Layout.

**Design tokens** (defined in `Layout.astro` `:root`):
- Accent: `#e804af` (hot pink) — also `--accent-green: #00ff88`, `--accent-cyan: #00d4ff`
- Background: `#080808`, cards: `#111111`
- Always dark mode — no light-mode variant exists.

**Hero component pattern:**
- Hero is `position: fixed; inset: 0` behind the page scroll. A `height: 100vh` spacer div in the flow pushes content below.
- Scroll listener adds `.blurry` / `.high-contrast` classes to fade hero elements as user scrolls past 30vh.
- Floating SVG icons (`assets/svg/*.svg`) animate via a single `bubble-float` keyframe; per-icon `--s`, `--dur`, `--dd` CSS vars control scale/speed/delay.

**Shared section pattern:**
- Every section uses `.section-wrapper` > `.section-inner` (max-width 1200px, 100px vertical padding).
- Section headers: `.section-label` (monospace, uppercase, accent color) + `.section-title` (with `<em>` for accent-colored words).

**Assets:**
- `assets/` at repo root is the canonical location. `public/assets` is a symlink pointing to it — this is how Astro serves them at `/assets/...` URLs.
- `assets/svg/` — floating hero icons; `assets/xp/` — company logos; `assets/skills/` — skill icons; `assets/countries/` — flag SVGs; `assets/favicon/` — favicon.

**Global CSS utilities** (defined in `Layout.astro`, available in all components via `<style is:global>`):
- `.glass-card` — dark card with hover border glow + lift
- `.gradient-text` — hot-pink → green gradient on text
- `.btn-primary` / `.btn-ghost` — filled accent and bordered ghost buttons

**Fonts:**
- `Inter` (body/UI) and `JetBrains Mono` (`.section-label`, monospace elements) — both loaded from Google Fonts in `Layout.astro`.

**Deployment:**
- GitHub Pages at `https://irvin373.github.io` via `npm run build` → `dist/`.

**Legacy code:** `home/` directory contains the original Angular source used as reference when building the Hero. It is not part of the Astro build.
