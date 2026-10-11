# Repository Guidelines

## Project Structure & Module Organization

This GitHub Pages portfolio keeps markup, CSS, vanilla JavaScript, and inline SVGs in `index.html`. Sections run hero, About, Skills, Experience, Projects, Contact; navigation follows that order. Contact holds Email, GitHub, LinkedIn, and the sole Download CV button. Keep content consistent with `Krishna_Prasad_V_K_resume.pdf`.

Assets live in `fonts/`, `audio/`, and `favicon.svg`. `flappy/` contains the Apache-2.0 Flappy Bird game and its scripts/assets; preserve its license and credits. `CLAUDE.md` explains architecture; keep it synchronized with this guide. `audio/CREDITS.md` specifies music attribution. `README.md` is a placeholder.

## Build, Test, and Development Commands

- `python3 -m http.server 8000`: preview at `http://localhost:8000` with HTTP asset loading.
- `git diff --check`: check whitespace before committing.
- `git diff -- index.html AGENTS.md CLAUDE.md`: review page and documentation changes.

There is no build step, test framework, coverage threshold, formatter, or linter. Merging to `main` deploys. Python's basic server lacks byte-range support; verify audio seeking with a range-capable server.

## Coding Style & Naming Conventions

Match surrounding code: two-space CSS/JavaScript indentation in `index.html`, double-quoted HTML attributes and JavaScript strings, and JavaScript semicolons. Use kebab-case classes (`theme-toggle`) and camelCase names (`setMenu`). Preserve existing formatting in `flappy/`.

Keep all three theme palettes synchronized, early theme initialization, transition cancellation, reduced-motion fallbacks, accessible labels, and focus styles. Keep the 56px header, dropdown offset, and section scroll margins aligned. At 640px and below without JavaScript, navigation wraps and the header is non-sticky.

## Music & Game Conventions

The player is the footer's only content; the entire footer is hidden without `.js`. Preserve `preload="none"`, looping, and visible massobeats / rose water credits. Track changes require updating credits, Media Session metadata, and initial duration/seek values (139 seconds, `2:19`). Keep slider fills and playback labels synchronized. At ≤640px, progress wraps; volume is hidden there and on devices without hover.

Every fifth theme toggle opens the same-origin game iframe and pauses music. Load it only on opening; unload on closing. Preserve Space/tap input, Escape handling, focus return, reduced motion, and Web Audio gesture unlocking on press/release. Audio failures must not block gameplay.

## Testing Guidelines

Manually check 320/360px and both sides of 640px, with/without JavaScript; both themes, persistence, rapid toggles, keyboard navigation, menus, and reduced motion. Verify player controls, OS media controls, game opening/closing, touch input, CV/assets, and console errors.

## Commit & Pull Request Guidelines

Use short imperative commits and descriptive branches; no mandatory prefix exists. Target `main`. Include purpose, checks performed, relevant issues, screenshots for visual changes, and newly referenced assets.
