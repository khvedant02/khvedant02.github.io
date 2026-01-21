# AGENT.md

This file provides guidance to AI agents (e.g., Claude Code, Codex, Gemini, or similar systems) when working with code in this repository.

## Commonly Used Commands

```bash
# Ruby dependencies
bundle install

# Optional local gem install path if permissions fail
bundle config set --local path 'vendor/bundle'

# Local dev server (Jekyll)
jekyll serve -l -H localhost
bundle exec jekyll serve -l -H localhost

# JavaScript deps + build
npm install
npm run build:js
npm run watch:js

# CV JSON generation
bash scripts/update_cv_json.sh

# Docker (containerized dev server)
chmod -R 777 .
docker compose up
```

Test commands: no automated test suite is defined in this repo, so there is no single-test runner.

## High-Level Architecture

- Jekyll renders content from collections (`_publications/`, `_talks/`, `_teaching/`, `_portfolio/`, `_posts/`) and static pages in `_pages/` into the site output.
- Layouts and reusable components live in `_layouts/` and `_includes/`, with styling in `_sass/` compiled into `assets/` during the build.
- Site-wide configuration and theme settings are in `_config.yml`, while structured data for navigation and CV live in `_data/navigation.yml` and `_data/cv.json`.
- The JS build pipeline concatenates vendor scripts and `assets/js/_main.js` into `assets/js/main.min.js` via `npm run build:js`.
- Bulk content generation uses `markdown_generator/` to convert TSV inputs into `_publications/` and `_talks/` markdown entries.

## Usage Notes and Constraints

- Do not edit `_site/` (generated output), `vendor/`, or `.bundle/` (local dependencies).
- GitHub Pages builds in safe mode; only allowlisted plugins in `_config.yml` will work.
- Changes to `_config.yml` require restarting the Jekyll server; Markdown/HTML changes auto-reload.
