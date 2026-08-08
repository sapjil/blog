---
name: code-review
description: Project-specific review checklist for Sapjil — content collection schema, layout duplication between Base/Base2/BlogPost, markuplint compliance, and Firebase deploy impact.
---

# Code Review (Sapjil-specific)

Use this alongside the general `/code-review` command for changes in this repo. This skill covers what's specific to this codebase; it doesn't replace looking for correctness bugs generally.

## What to check

- **Frontmatter matches schema**: any new/edited post in `src/content/blog/*.md` must satisfy the `blog` schema in `src/content/config.ts` (`title`, `description`, `pubDate`, `updatedDate?`, `heroImage?`, `categories?`, `tags: string[]`). A mismatch breaks the build entirely, not just that page — this is a hard blocker, not a style nit.
- **Layout duplication**: `src/layouts/Base.astro` is the only layout wired into live pages (`index.astro`, `[...slug].astro`). `Base2.astro` and `BlogPost.astro` are unused near-duplicates. If a change is being made to layout logic, make sure it's landing in `Base.astro` — don't add new features only to the unused variants, and don't assume changes to `Base2`/`BlogPost` have any live effect unless something now imports them.
- **Component reuse**: shared chrome (`Header`, `Footer`, `BaseHead`, `Analytics`, `FormattedDate`) lives in `src/components/`. New pages/layouts should reuse these rather than re-implementing meta tags or date formatting inline.
- **markuplint compliance**: run `npm run lint:astro` (and `npm run lint:html` after a build) on any markup change — see the `a11y` skill for the specific rules this repo relaxes/enforces via `.markuplintrc`.
- **Build-breaks-deploy risk**: there's no separate CI lint/test gate — `.github/workflows/firebase-hosting-merge.yml` runs `npm ci && npm run build` directly and deploys on success. Treat "does `npm run build` succeed" as the actual quality gate, not just a nice-to-have.
- **RSS/sitemap side effects**: `src/pages/rss.xml.js` and the `@astrojs/sitemap` integration both derive from the `blog` collection. Changes to post slugs, `pubDate` semantics, or the collection schema can silently affect the feed/sitemap output — check those if touching content collection logic.
- **Encoding/Korean text**: content is predominantly Korean; watch for mojibake or escaping issues in diffs touching Markdown content or string interpolation in `.astro` files.
