# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A single-file Turkish-language landing page for "Nova.ai", a fictional AI-solutions consultancy. Everything lives in `public/index.html`: inline CSS in `<style>`, markup, and one inline `<script>` at the bottom. There is no build step, tests, linter, or git repo; `package.json` exists only for wrangler.

**Run/preview:** open `public/index.html` in a browser, or run `npm run dev` (wrangler). Deploy with `npm run deploy` (Cloudflare Workers static assets, config in `wrangler.jsonc`).

## Structure of public/index.html

- **Page sections** are anchored by id and linked from the nav: `#cozumler`, `#surec`, `#yorumlar`, `#paketler`, `#sss`, `#iletisim`. Adding or renaming a section means updating the nav `<ul>` as well.
- **Styling** is driven by CSS variables in `:root` (`--bg`, `--card`, `--line`, `--text`, `--muted`, `--accent`, `--accent2`). Change the theme there, not per-rule. The layout is built from shared classes (`.wrap`, `.grid`, `.card`, `.btn`) rather than per-section styles. Cards variants: `.quote`, `.price` (`.hot` highlights a plan), and `.steps` (numbered with a CSS counter, so step numbers are automatic).
- **Responsive/mobile nav:** below 720px the nav `<ul>` is hidden and shown via an `.open` class toggled by the `.menu-btn` inline `onclick`; a script line closes it when a link is clicked.
- **Scroll-reveal:** the script adds `.reveal` to `.card, .stat, section h2, .sub` at load and an `IntersectionObserver` adds `.in`. New elements of those types get the animation automatically. `prefers-reduced-motion` disables it.
- **Contact form (`#lead`)** has no backend. The submit handler builds a `mailto:` URL from the form fields using the `MAIL` constant in the script, then replaces the form with a thank-you message. The footer also hardcodes the same address, so change both places.

## Content conventions

- All copy is Turkish (`lang="tr"`); keep new text in Turkish.
- Placeholders are intentionally marked as sample content: testimonials ("örnek metindir"), prices (`₺—`), the `hello@nova.ai` address, and stats like "40+ proje". Replace them with real data rather than treating them as final.
