# Copilot Instructions for uswds-site

This file provides guidance for AI coding agents working on the **U.S. Web Design System (USWDS) documentation website** repository.

## Key Documentation

- **[README.md](../README.md)** – Primary reference for setup, local development, available commands, deployment, and contributing. Start here.
- **[CONTRIBUTING.md](../CONTRIBUTING.md)** – Coding guidelines, pull request process, issue labels, and code standards.
- **[SECURITY.md](../SECURITY.md)** – Security policy and vulnerability disclosure information.

> **Note:** This repository does not currently have an `AGENTS.md`, `ACCESSIBILITY.md`, or `SUSTAINABILITY.md` file. If any of these are added to the root of the repository, update this file to reference them.

## Repository Overview

This is a [Jekyll](https://jekyllrb.com/) static site that documents the U.S. Web Design System (USWDS). It uses:

- **Jekyll** – Static site generator (Ruby-based)
- **Gulp.js** – Task automation (Node.js-based)
- **USWDS npm package** – Design system components (`@uswds/uswds`)
- **cloud.gov Pages** – Deployment platform

## Tech Stack Versions

Check these files for exact versions:

- `.ruby-version` or `.tool-versions` – Ruby version
- `.nvmrc` or `.tool-versions` – Node.js version
- `.bundler-version` – Bundler version

## Setup

```sh
npm install
bundle install
```

## Common Commands

| Command | Description |
|---|---|
| `npm start` | Build assets and start the local dev server at http://127.0.0.1:4000 |
| `npm run serve` | Incremental build + serve (faster rebuilds) |
| `npm run build` | Full production build (Gulp + Jekyll) |
| `npm run lint` | Run ESLint and Sass linter |
| `npm run clean` | Remove copied dependency assets |
| `npm test` | Run all tests and linters (requires a running Jekyll server) |
| `npm run watch` | Watch for changes and rebuild |

## Directory Structure

- `_components/` – USWDS component documentation pages
- `_layouts/` – Jekyll layout templates
- `_includes/` – Jekyll include partials
- `_patterns/` – Pattern documentation pages
- `_posts/` – "What's New" update posts
- `_templates/` – Form and page template documentation
- `css/` – Sass/SCSS source files
- `js/` – JavaScript source files
- `pages/` – General site pages
- `spec/` – RSpec tests

## Testing

The test suite requires a running Jekyll server. The full test suite (`npm test`) runs:
- RSpec (Ruby tests in `spec/`)
- ESLint and Sass linting
- HTML Proofer
- Pa11y accessibility checks against the running site

For faster iteration, run individual checks:
- `npm run lint` – JavaScript and Sass linting only
- `bundle exec rspec` – Ruby unit tests only

## Linting and Code Style

- **JavaScript**: Follow the [18F Front End Guide - JavaScript](https://pages.18f.gov/frontend/#javascript); use `npm run lint`
- **CSS/Sass**: Follow the [18F Front End Guide - CSS](https://pages.18f.gov/frontend/#css); use `npm run lint`
- **Prettier**: `npm run prettier:scss` formats SCSS files

## Content Conventions

- Component documentation lives in `_components/` as Markdown/HTML files
- Updates/blog posts go in `_posts/`
- Some content is dynamically fetched from the GitHub API at build time (releases, contributing guide, security policy)

## Deployment

- Merges to `main` automatically deploy to the live site via cloud.gov Pages
- Each branch gets a public preview deployment
- If a build fails on Pages, try `bundle update` to clear the cache

## Known Issues / Workarounds

- **Ubuntu 20.04**: If you see `bundler: failed to load command: jekyll`, run `gem install ffi -- --disable-system-libffi`
- **API rate limits**: Set `GITHUB_ACCESS_TOKEN` environment variable to avoid GitHub API rate limiting during local development; clear stale cache with `rm -rf .jekyll_get_cache`
- **Development USWDS version**: Use `npm link uswds` to test against a local USWDS build; see README.md for full instructions
