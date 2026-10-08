# Repository Guidelines

## Project Structure & Module Organization

This repository contains a single-page personal portfolio hosted on GitHub Pages. `index.html` holds the page markup, inline CSS, vanilla JavaScript, and SVG icons. `favicon.svg` supplies the browser icon; `fonts/` contains the self-hosted JetBrains Mono font and its SIL OFL license. `README.md` describes the repository, and `CLAUDE.md` documents implementation details. There are no separate source modules, test directories, or package dependencies.

## Build, Test, and Development Commands

- `python3 -m http.server 8000`: serve the repository locally; visit `http://localhost:8000` to check changes with normal HTTP asset loading.
- `git diff --check`: check changes for whitespace errors before committing.
- `git diff -- index.html`: review page changes before opening a pull request.

There is no build step, automated test command, formatter, or linter. GitHub Pages serves the files directly from `main`; merging changes there deploys the site.

## Coding Style & Naming Conventions

Match the surrounding formatting: two-space indentation in CSS and JavaScript, double-quoted HTML attributes and JavaScript strings, and semicolons in JavaScript. Use descriptive kebab-case CSS classes such as `theme-toggle` and camelCase JavaScript names such as `setMenu`. Keep related styles in the existing commented sections.

Use CSS custom properties for colors, and keep the dark, system-light, and explicit-light palettes synchronized. Preserve the early theme initialization, JavaScript-disabled navigation, reduced-motion behavior, and accessible labels and focus styles. Keep sticky-header height and section scroll offsets aligned.

## Testing Guidelines

Validation is manual; no test framework or coverage threshold is configured. Check desktop and mobile layouts around the 640px breakpoint, both themes, saved theme persistence after reload, and rapid theme toggles. Verify keyboard navigation, the skip link, menu closing via Escape and link clicks, reduced-motion settings, and navigation with JavaScript disabled. Confirm assets load and inspect the browser console for errors.

## Commit & Pull Request Guidelines

Recent commits use short, imperative descriptions, such as “Animate the theme toggle with a diagonal sweep”; no mandatory prefix convention is established. Use descriptive feature branches such as `theme-sweep-transition` and open PRs targeting `main`. Include the change's purpose, manual checks performed, linked issues when applicable, and desktop/mobile screenshots for visual changes.
