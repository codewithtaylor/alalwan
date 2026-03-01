# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm start          # Dev server with live reload (npx eleventy --serve)
npm run build      # Build to _site/ (npx eleventy)
```

There are no tests. The build output goes to `_site/` (gitignored).

## Architecture

This is an [Eleventy](https://www.11ty.dev/) static site for an Islamic Knowledge Library. It serves as a curated archive of scholarly works, fatawa (legal rulings), and translations.

### Configuration

`.eleventy.js` is the central config. It defines all collections and sets `_includes` as the template directory and `_site` as output. The `static/` directory is passed through directly (CSS lives there).

### Collections

Collections are defined in `.eleventy.js` and used in templates via `collections.*`:

| Collection | Source |
|---|---|
| `scholars` | Files tagged `scholars` |
| `works` | `content/works/**/*.md` (excluding index.md) |
| `fatawa` | `content/works/fatawa/*.md` |
| `books` | `content/works/books/*.md` |
| `lectures` | `content/works/lectures/*.md` |
| `poetry` | `content/works/poetry/*.md` |
| `sciences` | `content/sciences/*.{md,njk}` |

### Content Organization

**Scholars** (`content/scholars/profiles/`): Each scholar is a Markdown file. `profiles.json` sets layout, tag (`scholars`), and permalink pattern for the whole directory. Scholar files use a `scholar_id` frontmatter key (e.g., `al-barrak`) that works reference.

**Works** (`content/works/`): Subdirectories by type (`books/`, `fatawa/`, `lectures/`, `poetry/`). Each work uses this frontmatter schema:
```yaml
type: fatwa          # fatwa | poem | book | lecture
scholars: [al-barrak]  # array of scholar_id values
sciences: [aqeedah]    # array matching science page keys
language: ar-en        # ar | en | ar-en
permalink: /works/fatawa/slug/
source: "https://..."
```

**Sciences** (`content/sciences/`): Each `.njk` file is a category page (aqeedah, fiqh, poetry, etc.). They filter `collections.works` by matching `w.data.sciences` against their own `science` frontmatter key. Adding a new science means creating a `.njk` file here and using the matching key in work frontmatter.

**Fatawa index** (`content/fatawa/index.md`): A standalone listing page at `/fatawa/` that renders `collections.fatawa`.

### Templates

One shared layout: `_includes/layouts/base.njk`. It includes Google Fonts (EB Garamond for Latin, Amiri for Arabic), a site header with nav, and `{{ content | safe }}` for the page body.

### Arabic Content

Use the `.arabic` CSS class for RTL Arabic text blocks. The Amiri font is loaded for Arabic. Arabic text uses `direction: rtl` and `unicode-bidi: isolate`.
