# dmf95.github.io

Personal portfolio & blog of **Domenic Fayad** - a data scientist building decision-intelligence
products. Built with [Jekyll](https://jekyllrb.com/) and served by GitHub Pages at
**[www.domenicfayad.com](https://www.domenicfayad.com/)** (see [`CNAME`](CNAME)).

## Local development

Requires **Ruby 3.3** (with DevKit on Windows) and Bundler.

```bash
bundle install
bundle exec jekyll serve   # → http://localhost:4000 (auto-rebuilds on save)
```

> **Windows:** install Ruby with `winget install RubyInstallerTeam.RubyWithDevKit.3.3`, then open a
> **new** terminal so `ruby` is on `PATH`.

## Project structure

| Path | What it holds |
|---|---|
| `_works/` | Portfolio project posts - the `works` collection (`/work/:slug`) |
| `_posts/` | Blog posts (`/blog/:slug`) |
| `_pages/` | Standalone pages (About, Contact, …) |
| `_data/settings.yml` | Site-wide config: nav, hero, social links, section toggles |
| `_layouts/`, `_includes/` | Page templates and reusable partials |
| `_sass/` | Styles (Akio theme) |
| `images/` | Image assets |
| `archive/` | Retired content kept for reference (not linked from nav) |
| `_config.yml` | Jekyll configuration |
| `CNAME` | Custom domain for GitHub Pages |

## Adding a project or post

Create `_works/YYYY-MM-DD-slug.md` (or `_posts/…` for the blog). The **date prefix sets ordering**
(newest first) but is **stripped from the URL** - the file `2026-06-11-datarena.md` is served at
`/work/datarena`. Front matter:

```yaml
---
category: Machine Learning          # shown as the card/section label
title: My project
description: One-line summary shown on project cards.
date: 2026-06-11
image: /images/.../cover.jpg
image_caption: 'Optional caption for the header image.'
role: Data Scientist                # optional
tags: [all-projects, python]        # include `all-projects` to appear in the main list
---
```

## Deployment

Push to `main` - **GitHub Pages builds the site from source** and publishes it. The generated
`_site/` directory is git-ignored and must **not** be committed; editing it has no effect on the
live site.

## Changelog

Notable changes are tracked in [`CHANGELOG.md`](CHANGELOG.md).
