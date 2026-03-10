# AGENTS.md

Repository guidance for coding agents working on this Hugo blog.

## Project Overview

- **Site:** [blog.gerard.space](https://blog.gerard.space/) — Gerard's personal blog.
- **Stack:** Hugo static site generator. No npm, bundler, linter, test framework, or external dependencies.
- **Hugo version:** 0.152.2, pinned via [Hermit](https://cashapp.github.io/hermit/) in `bin/`.
- **Config:** single `hugo.yml` at repo root. Custom theme built in-repo (`layouts/` + `assets/`).
- **Languages:** English (default), Catalan (`ca`), Spanish (`es`).
- **Content:** `content/blog/` — Markdown posts only. No other content sections.

## Setup & Build

```bash
source ./bin/activate-hermit   # or let direnv handle it via .envrc
./bin/hugo server --buildDrafts # Dev server with drafts
./bin/hugo --gc --minify        # Production build (same as CI)
```

**No lint or test commands.** The production build is the only verification step. Always run it after changes.

## Content Conventions

- Filename pattern: `YYYY-MM-DD-slug-in-kebab-case.md`. Date extracted from filename — do NOT add `date` in frontmatter.
- Permalinks: `/:year/:month/:title/`.
- **Articles** (long-form): frontmatter has `title` (required) and `description` (optional excerpt).
- **Notes** (short-form): frontmatter has `title`, `style: note`, optional `link`. Omit `description`. Content is 1-3 lines.
- Translations use language suffixes: `slug.ca.md`, `slug.es.md`. Keep `i18n/*.yaml` keys in sync.

## Code Style

- **Templates:** Hugo idioms (`with`, `range`, `default`, `i18n`). `{{ define "main" }}` block system. Assets via Hugo Pipes (`resources.Get | toCSS | minify | fingerprint`). Tabs for HTML indentation. Preserve hook IDs: `#theme-toggle`, `#page-wrapper`.
- **SCSS:** Edit `assets/css/` only. Theming via `--blog-*` CSS custom properties. Dark mode uses **both** `prefers-color-scheme` AND `[data-theme="dark"]` — keep in sync. Accent: `#2B546B` light / `#5b9bb5` dark. `rem` units. Responsive at `max-width: 700px`. BEM-ish naming.
- **JS:** Plain browser JS in IIFEs, processed via Hugo Pipes. `const`/`let` only. Guard element access: `if (!el) return;`.
- **No new dependencies.** No npm, no CDN scripts. Use Hermit for binaries.

## General Guidelines

- Keep changes **minimal and behavior-preserving**. Match existing patterns; no broad reformatting.
- Use Hugo `default` function to prevent nil panics in templates.
- Always verify with `./bin/hugo --gc --minify` after changes.
- Commit messages: `scope: description` (e.g., `blog: add note "Title"`).

## CI/CD

- `hugo-pages.yml` — push to `main`/`master` builds and deploys to GitHub Pages.
- `opencode.yml` — AI agent responds to `/oc` or `/opencode` comments on issues/PRs.
- `publish-note.yml` — manual dispatch to create a note post, commit, and trigger deploy.

## Maintaining AGENTS.md

- Update this file when repository conventions change.
- Keep under 50 lines. Trim ruthlessly; prioritize actionable guidance over explanation.
