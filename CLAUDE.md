# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A single-page personal portfolio served by GitHub Pages at https://ikpvk.github.io/ straight from the `main` branch. It is plain HTML, CSS and vanilla JS with no build step, package manager, linter or tests. Everything (styles, scripts, inline SVG icons) lives in `index.html`. The only other assets are `favicon.svg`, a self-hosted JetBrains Mono font (`fonts/`, SIL OFL), the music track in `audio/`, a copy of the Flappy Bird easter egg game in `flappy/`, and `Krishna_Prasad_V_K_resume.pdf`, which the "Download CV" buttons link to. The page content (experience, projects, skills, education) is taken from that résumé, so keep the two consistent.

## Running locally

Serve the folder over HTTP rather than opening the file directly, so the font preload and `localStorage` behave as they do in production:

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

Deploying means merging to `main`. Changes have so far gone in through PRs from feature branches. Testing is manual: `AGENTS.md` holds the style conventions, the manual test checklist (320/360px widths, both sides of 640px, with and without JS, both themes, reduced motion, player controls) and the commit/PR conventions. Keep it in step with this file when either changes.

## Architecture of `index.html`

**Theming.** All colours are CSS custom properties. Dark is the default. The palette is defined in three places that must stay in sync: `:root, :root[data-theme="dark"]`, the `@media (prefers-color-scheme: light)` block guarded by `:root:not([data-theme="dark"])`, and `:root[data-theme="light"]`. An inline script in `<head>` sets `data-theme` before first paint, using the saved `localStorage` "theme" or else the system preference, so the page never flashes the wrong theme. The same script adds the `js` class to `<html>`.

**Progressive enhancement.** The theme toggle and mobile menu button are hidden by default and only shown under `.js`. On mobile without JS there is no menu button, so the nav links wrap below the logo and the header becomes `position: static` (a taller sticky header would cover the 56px scroll-margin targets).

**Theme sweep transition.** The toggle (bottom `<script>`) uses `document.startViewTransition` to reveal the new theme with a diagonal mask sweep. The mask is an inlined SVG data URI, used twice (`-webkit-mask` and `mask`). While a sweep runs, the `theme-switching` class turns off the `body` colour transition. Overlapping toggles skip the earlier transition, so only the latest transition (tracked in `themeTransition`) may remove that class. Browsers without the API, and users who prefer reduced motion, get an instant switch.

**Music player.** A small card at the top of the footer, above the © line, plays `audio/rose-water.mp3` (a 128 kbps copy). Like the theme toggle, it's shown only under `.js`. Its license requires crediting both the artist and the song title ("massobeats - rose water", see `audio/CREDITS.md`), and the card always shows both. The `<audio>` element uses `preload="none"`, so nothing downloads until the first play. Below 640px, the progress bar wraps onto its own row. The volume slider is hidden on phones and on devices without hover, because iOS ignores volume set from scripts. The slider fill comes from a `--p` custom property set in the script. The Media Session API exposes the track to lock screens and media keys, so it can be paused after the card has scrolled out of view. The seek slider's `max` and the duration label are hard-coded to the track length (139 s, "2:19") because nothing loads until play; `loadedmetadata` then overwrites them. Swapping the track means updating those, the `MediaMetadata` title/artist, the visible credit and `audio/CREDITS.md` together. Seeking needs a server that supports HTTP byte ranges: GitHub Pages does, but `python3 -m http.server` does not, so seeking won't work in local preview.

**Flappy Bird easter egg.** Every 5th click of the theme toggle (counted since page load, no time limit) opens a full-screen modal `<dialog>` with the game in an `<iframe>`. The game is a copy of `flappy/` from the user's fork of nebez/floppybird (Apache-2.0, keep `flappy/LICENSE` and the game's credit footer). It needs an iframe: it looks up `#player`, which clashes with the music player, it calls `preventDefault()` on Space for the whole document, and its `reset.css` restyles `html`, `body` and `nav`. The iframe's `src` is set only on open, so normal visits download nothing, and it is reset to `about:blank` on close, which stops the game loop and sounds. Opening pauses the music. Keys pressed inside the iframe don't reach the page, so on load the script focuses the iframe (so Space works) and adds an Escape listener inside it. This relies on the game being same-origin. The copy differs from the fork in three places: `flappy/index.html` adds a `noindex` meta and `target="_blank"` on the credit links, and `flappy/css/main.css` and `flappy/js/main.js` honour `prefers-reduced-motion`. The parent page's motion rules don't reach into the iframe, so with reduced motion the game itself stops the background scrolling and wing flap and makes its fades and slides instant. Gameplay movement is unchanged.

**Accessibility conventions to keep.** Skip link, `:focus-visible` outlines, `aria-expanded`/`aria-controls` on the menu button (Escape and link clicks close it), `aria-hidden` on decorative SVGs, and a `prefers-reduced-motion` block that disables the cursor blink, smooth scrolling and colour fades.

**Layout.** Content is in `.wrap` (max width `--max`, 16px gutters). The only breakpoint is 640px. The sticky header is 56px tall, and sections use `scroll-margin-top: 56px` to match; the mobile dropdown menu is also positioned at `top: 56px`. Change all of them together.
