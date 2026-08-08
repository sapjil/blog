# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Sapjil is a personal tech blog (`sapjil.net`) by a Korean freelance markup engineer, built as a static Astro site. Content is almost entirely in Korean.

## Commands

- `npm run dev` / `npm start` — start the Astro dev server
- `npm run build` — production build to `dist/` (this is what CI runs)
- `npm run preview` — preview the built site locally
- `npm run lint:astro` — markuplint against `.astro` source files
- `npm run lint:html` — markuplint against built `dist/**/*.html` (run `build` first)

There is no test suite in this repo. Both `yarn.lock` and `package-lock.json` are present, but CI uses `npm ci`/`npm run build`, so npm is the canonical package manager. Node version is pinned via `.nvmrc` (18.18.2).

## Architecture

**Content collection**: Blog posts are Markdown files in `src/content/blog/*.md`. The schema is defined in `src/content/config.ts` (`title`, `description`, `pubDate`, `updatedDate?`, `heroImage?`, `categories?`, `tags[]`) — use an existing post like `src/content/blog/git-reflog.md` as a frontmatter reference. `src/content/temp/temp.md` is a blank frontmatter template, not a real/published post, and sits outside the defined `blog` collection.

**Routing**: `src/pages/index.astro` fetches all posts via `getCollection('blog')`, sorts by `pubDate` descending, and lists them. `src/pages/[...slug].astro` is the single dynamic route rendering every post — it generates paths with `getStaticPaths()` and wraps rendered content in the `Base` layout. `src/pages/rss.xml.js` generates the RSS feed via `@astrojs/rss`.

**Layouts**: `src/layouts/Base.astro` is the layout actually used by both pages above. `src/layouts/Base2.astro` and `src/layouts/BlogPost.astro` are near-duplicate variants (differing in whether they render `categories`/`tags` and the buymeacoffee banner) that aren't referenced by any current page — don't assume they're live without checking.

**Shared components** (`src/components/`): `Header`, `Footer`, `BaseHead` (meta/SEO tags), `Analytics`, `FormattedDate`. Site-wide constants (`SITE_TITLE`, `SITE_DESCRIPTION`) live in `src/consts.ts`.

**Styling**: global styles in `src/styles/global.css` and `src/styles/style.scss`, imported per-page as needed.

**Integrations** (`astro.config.mjs`): `@astrojs/mdx` and `@astrojs/sitemap` are active. `@astrojs/partytown` is a dependency but its integration is currently commented out.

## Deployment

Firebase Hosting (project `sapjilblog`), serving `dist/` per `firebase.json`. GitHub Actions deploys to production on push to `main` (`.github/workflows/firebase-hosting-merge.yml`) and creates preview channels for pull requests (`.github/workflows/firebase-hosting-pull-request.yml`).
