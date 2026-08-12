# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## Commands

**Run locally:**
```bash
bundle exec jekyll serve
```

**Build:**
```bash
bundle exec jekyll build
```

## Branch Workflow

- `blog` — source/working branch (make all changes here)
- `master` — production branch (deployed to GitHub Pages)

Push changes to the `blog` branch; GitHub Actions builds the site and deploys it to `master`.

## Architecture

This is a Jekyll site using the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme (v4.6.0, "dirt" skin). The site acts as a hub hosting multiple independent blogs.

### Adding a New Blog

Three files must be updated together:

1. **`_config.yml`** — register the collection under `collections:` and add a `defaults:` scope for it with a permalink pattern
2. **`_data/blogs.yml`** — add an entry under `internal_blogs` with `name` (lowercase), `description`, and optionally `background`
3. **Create `_<blog-name>/`** — directory to hold the blog's markdown post files

The `name` in `_data/blogs.yml` must be **lowercase** and match the collection name (with spaces instead of hyphens). The home page (`_layouts/home.html`) auto-generates blog cards from this data file, and the autopage layout (`_layouts/autopage_collection.html`) generates the collection index pages.

### Blog Header Styling

Blog collection headers pull their background color/image from `_data/blogs.yml`:
- `background: <css-color>` — uses a CSS color value (e.g., `darkgoldenrod`)
- `background: <scss-class-name>` — references a custom CSS class defined in `_sass/minimal-mistakes/_page.scss` (used for image headers like `apple2header`, `rankdynamicsheader`, `llmpersonalizationheader`)

The `page__hero.html` include reads `site.data.blogs.internal_blogs` to look up the blog's background via `signature: collection` set in `autopage_collection.html`.

### Special Characters in Titles

If a post title or filename contains non-ASCII characters (e.g., **ñ**), explicitly set the `permalink` in the post's front matter to avoid broken auto-generated URLs.

### Key Files

| File | Purpose |
|---|---|
| `_data/blogs.yml` | Blog registry (names, descriptions, header styles) |
| `_config.yml` | Jekyll config, collections, pagination, defaults |
| `_layouts/home.html` | Homepage — renders blog cards from `_data/blogs.yml` |
| `_layouts/autopage_collection.html` | Auto-generated index page for each collection |
| `_includes/page__hero.html` | Hero header — resolves blog background color/image |
| `_sass/minimal-mistakes/_components.scss` | Custom `.blog_card` / `.blog_header` styles |
| `_sass/minimal-mistakes/_page.scss` | Custom header image CSS classes |
