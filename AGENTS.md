# Repository Guidelines

## Project Structure & Module Organization

This is a single-page portfolio hosted on GitHub Pages. `index.html` contains markup, CSS, vanilla JavaScript, and inline SVG icons. Assets include `favicon.svg`, `fonts/` (JetBrains Mono and its SIL OFL license), `Krishna_Prasad_V_K_resume.pdf`, and `audio/` (the MP3 and `CREDITS.md`), and `flappy/` (a copied Flappy Bird game, Apache-2.0, opened by every 5th theme toggle). Keep portfolio content consistent with the résumé. `CLAUDE.md` documents implementation details. There are no separate source modules, tests, or package dependencies.

## Build, Test, and Development Commands

- `python3 -m http.server 8000`: serve the repository locally; visit `http://localhost:8000` to check changes with normal HTTP asset loading.
- `git diff --check`: check changes for whitespace errors before committing.
- `git diff -- index.html AGENTS.md CLAUDE.md`: review page and documentation changes.

There is no build step, automated test command, formatter, or linter. Merging to `main` deploys the site. Python's basic HTTP server lacks byte-range support; use a server supporting ranges to verify audio seeking.

## Coding Style & Naming Conventions

Match surrounding formatting: two-space CSS/JavaScript indentation, double-quoted HTML attributes and JavaScript strings, and JavaScript semicolons. Use kebab-case CSS classes (`theme-toggle`) and camelCase JavaScript names (`setMenu`). Keep related styles in existing commented sections.

Keep CSS color palettes synchronized and preserve early theme initialization, reduced-motion behavior, accessible labels, and focus styles. On mobile without JavaScript, navigation wraps and the header is non-sticky. Keep sticky-header height and section scroll offsets aligned.

## Music Player & Asset Conventions

The footer player uses `audio/rose-water.mp3`. Preserve visible artist and track credits per `audio/CREDITS.md`, `preload="none"`, and visibility only under `.js`. At 640px and below, progress moves to a separate row; volume controls are hidden there and on devices without hover. Keep slider fills (`--p`), play/pause labels, and Media Session handlers synchronized with playback.

## Testing Guidelines

Validation is manual, with no coverage threshold. Check 320px/360px layouts and both sides of 640px, with and without JavaScript. Verify both themes, persistence, rapid toggles, keyboard focus, skip link, menu closing, and reduced motion. Test playback, pause, seeking, volume, and supported OS media controls. For the easter egg, check that 5 toggles open the game, that Space and taps play it, and that Escape and the close button both close it and return focus to the toggle. Confirm CV/assets load and inspect console errors.

## Commit & Pull Request Guidelines

Use short, imperative commit messages and descriptive feature branches; no mandatory prefix convention exists. Target `main` in PRs. Include purpose, manual checks, relevant issues, and screenshots for visual changes. Include newly referenced assets in commits.
