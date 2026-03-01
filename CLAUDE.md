# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm start        # Dev server with live reload (http://localhost:8080)
npm run build    # Build static site to _site/
```

No test suite. No linter configured.

## Architecture

This is a personal blog built with [Eleventy](https://www.11ty.dev/) (v3, ESM). Source in `src/`, output in `_site/`.

**Key files:**
- `eleventy.config.js` — plugin setup (syntax highlighting, RSS), passthrough copies, custom filters (`readableDate`, `isoDate`, `readingTime`), and the `posts` collection
- `src/_data/site.json` — global site metadata (title, URL, author) available as `site.*` in all templates
- `src/_includes/layouts/base.njk` — root layout; all pages extend this
- `src/_includes/layouts/post.njk` — post layout; extends `base.njk`

**Content flow:**
- Blog posts live in `src/posts/*.md` with frontmatter: `title`, `date`, `excerpt`, optional `subtitle` and `tags`
- `src/posts/posts.json` applies `layout: layouts/post.njk` and `tags: posts` to all posts automatically
- Posts are collected and sorted by date (newest first) via the `posts` collection in `eleventy.config.js`

**Template engine:** Nunjucks (`.njk`) for HTML templates; Markdown files also processed through Nunjucks (`markdownTemplateEngine: "njk"`).

**Static assets:** `src/css/` and `src/public/` are copied as-is to `_site/`.

**RSS feed:** Generated at `/feed.xml` via `src/feed.njk` using the `@11ty/eleventy-plugin-rss` plugin.
