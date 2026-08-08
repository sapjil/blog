---
name: a11y
description: Accessibility checklist for Sapjil's Astro components and blog Markdown — alt text, heading structure, lang attribute, and this repo's markuplint rules.
---

# Accessibility (a11y)

Apply this when writing or reviewing `.astro` components, layouts, or blog post Markdown/frontmatter in this repo.

## Known project-specific issues to watch for

- **`lang` attribute mismatch**: `src/pages/index.astro` and the layouts in `src/layouts/` set `<html lang='en'>`, but blog content is almost entirely Korean. Flag this when touching these files — screen readers will mispronounce Korean text under an `en` lang tag. The correct fix (if asked to make it) is `lang='ko'`, or a per-page value if the site ever mixes languages.
- **Empty `alt` on hero images**: hero images in `BlogPost.astro`/`Base2.astro` render `alt=''`. Decorative-only images are fine with empty alt, but if a hero image conveys content (diagrams, screenshots referenced in the post), it needs real alt text — check the post content before assuming decorative.
- **Category/tag text as the only signal**: categories and tags are rendered as small colored `<span>`/text labels (see `BlogPost.astro`). Don't let color alone carry meaning — text content should already be present (it is), just don't remove it in favor of color-coded UI.

## Checklist

- Every `<img>` has `src` and a meaningful `alt` — enforced by `.markuplintrc` (`required-attr: ["src", "alt"]` on `img`), but markuplint doesn't judge alt *quality*, so review it manually.
- Heading order stays sequential: post pages should have exactly one `<h1>` (the post title in the layout's `.title` block) — don't introduce a second `<h1>` inside post body content.
- Interactive elements (`HeaderLink.astro`, nav links) remain real `<a>`/keyboard-focusable elements — don't replace with non-focusable `<div>`/`<span>` click handlers.
- `iframe` embeds (allowed without `required-attr`/`deprecated-attr` per `.markuplintrc`) should still get a `title` attribute when practical, even though the linter won't enforce it.
- Tables (used in some posts) should use proper `<th>`/`<td>` structure — markuplint's `require-accessible-name` is relaxed for tables in this repo, so this is on you to check manually.

## Verifying

- `npm run lint:astro` — lints `.astro` source against `.markuplintrc`.
- `npm run build && npm run lint:html` — lints the actual rendered output, which catches markuplint issues coming from Markdown content that `lint:astro` can't see (since post bodies aren't `.astro` files).
