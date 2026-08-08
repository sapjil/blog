---
name: dev
description: Start, build, preview, and verify the Sapjil Astro blog locally — dev server commands, default port, and how to confirm a change actually works in the browser.
---

# Dev

Use this whenever you need to run the site to see a change working, not just to read the code.

## Commands

- `npm run dev` (or `npm start`) — starts the Astro dev server, default port `4321` (`http://localhost:4321`). If 4321 is taken, Astro auto-picks the next free port — check the terminal output for the actual URL.
- `npm run build` — production build to `dist/`. This is exactly what CI runs on merge to `main`, so a failing build here means a failing deploy.
- `npm run preview` — serves the built `dist/` output, closer to production than `dev` (no HMR, real static output). Use this to sanity-check a build before pushing.

## Verifying a change

There is no test suite in this repo, so verification means:
1. Run `npm run dev` and open the relevant page:
   - Homepage list: `/`
   - A single post: `/<slug>/` (slug = the Markdown filename without `.md`, e.g. `/git-reflog/`)
   - RSS: `/rss.xml`
2. For content changes, confirm the frontmatter matches the schema in `src/content/config.ts` — a mismatch fails the build with a schema validation error, not a silent skip.
3. Run `npm run lint:astro` for `.astro` markup changes. For anything affecting rendered HTML output, run `npm run build && npm run lint:html`.
4. If a component change touches `Base.astro`, check both the homepage and a post page — it's the layout shared by both `src/pages/index.astro` and `src/pages/[...slug].astro`.
