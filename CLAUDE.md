# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A single-page personal portfolio served by GitHub Pages at https://ikpvk.github.io/ straight from the `main` branch. It is plain HTML, CSS and vanilla JS with no build step, package manager, linter or tests. Everything (styles, scripts, inline SVG icons) lives in `index.html`. The only other assets are `favicon.svg`, a self-hosted JetBrains Mono font (`fonts/`, SIL OFL), and `Krishna_Prasad_V_K_resume.pdf`, which the "Download CV" buttons link to. The page content (experience, projects, skills, education) is taken from that résumé, so keep the two consistent.

## Running locally

Serve the folder over HTTP rather than opening the file directly, so the font preload and `localStorage` behave as they do in production:

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

Deploying means merging to `main`. Changes have so far gone in through PRs from feature branches.

## Architecture of `index.html`

**Theming.** All colours are CSS custom properties. Dark is the default. The palette is defined in three places that must stay in sync: `:root, :root[data-theme="dark"]`, the `@media (prefers-color-scheme: light)` block guarded by `:root:not([data-theme="dark"])`, and `:root[data-theme="light"]`. An inline script in `<head>` sets `data-theme` before first paint, using the saved `localStorage` "theme" or else the system preference, so the page never flashes the wrong theme. The same script adds the `js` class to `<html>`.

**Progressive enhancement.** The theme toggle and mobile menu button are hidden by default and only shown under `.js`. On mobile without JS, the nav links stay visible inline.

**Theme sweep transition.** The toggle (bottom `<script>`) uses `document.startViewTransition` to reveal the new theme with a diagonal mask sweep. The mask is an inlined SVG data URI, used twice (`-webkit-mask` and `mask`). While a sweep runs, the `theme-switching` class turns off the `body` colour transition. Overlapping toggles skip the earlier transition, so only the latest transition (tracked in `themeTransition`) may remove that class. Browsers without the API, and users who prefer reduced motion, get an instant switch.

**Accessibility conventions to keep.** Skip link, `:focus-visible` outlines, `aria-expanded`/`aria-controls` on the menu button (Escape and link clicks close it), `aria-hidden` on decorative SVGs, and a `prefers-reduced-motion` block that disables the cursor blink, smooth scrolling and colour fades.

**Layout.** Content is in `.wrap` (max width `--max`, 16px gutters). The only breakpoint is 640px. The sticky header is 56px tall, and sections use `scroll-margin-top: 56px` to match, so change both together.
