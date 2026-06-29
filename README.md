# Irvin Cossio — Portfolio

Personal portfolio site for Irvin Cossio, Senior Mobile & Frontend Engineer. Built with Astro v4, deployed to GitHub Pages.

**Live:** https://irvin373.github.io

## Stack

- [Astro v4](https://astro.build) — static site generator
- Tailwind CSS via CDN (not Astro integration)
- Lucide icons via CDN
- Inter + JetBrains Mono from Google Fonts

## Dev

```bash
npm install
npm run dev      # localhost:4321
npm run build    # output → dist/
npm run preview  # serve dist/ locally
```

## Structure

```
src/
  layouts/Layout.astro      # shell: fonts, Tailwind CDN, global CSS tokens, Lucide init
  pages/index.astro         # single route — composes all sections
  components/
    Nav.astro
    Hero.astro              # fixed-position behind scroll; floating SVG icons
    About.astro
    Experience.astro
    Projects.astro
    Contact.astro
assets/                     # static files (public/assets symlinks here)
  svg/                      # floating hero icons
  xp/                       # company logos
  skills/                   # skill icons
  countries/                # flag SVGs
```

## Design Notes

- Always dark mode — no light variant.
- Design tokens defined as CSS custom properties in `Layout.astro :root`. Use `var(--token)` everywhere, not hardcoded hex values.
- Accent colors: `--accent` `#e804af`, `--accent-green` `#00ff88`, `--accent-cyan` `#00d4ff`.
- All styles use `<style is:global>` — no scoped CSS.
- Tailwind config block in `Layout.astro` **must appear before** the Tailwind CDN `<script>` tag.

## Deployment

Push to `main` → build and deploy to GitHub Pages manually or via CI:

```bash
npm run build
# deploy dist/ to gh-pages branch
```
