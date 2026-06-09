# Contributing to docs.isograd.com

This repo serves the public Isograd documentation at **https://docs.isograd.com**.
It's a Jekyll site built by GitHub Pages on every push to `main`. The
two manuals — the **Account administrator manual** and the **Questions
module manual** — are bilingual (FR + EN) and most chapters are
illustrated with screenshots generated automatically by a Playwright
test suite that lives in a sibling repo (`isograd_app`).

This README is the authoritative reference for **anyone editing the
manuals**, whether human or AI. The two roles are:

- **Reviewer** — reads the manual, edits prose in `.md` files, commits.
- **Screenshot regenerator** — runs the Playwright suite in
  `isograd_app/tests` to refresh PNGs when the platform UI changes.

A typical workflow looks like:

1. Reviewer edits `ai/fr/candidates/index.md` to clarify a paragraph.
2. Reviewer commits with a message like *"clarify import flow — please
   regenerate screenshots after merging since the modal changed"*.
3. The screenshot regenerator (often an AI agent invoked via Claude
   Code) reads the commit message, runs the matching Playwright spec,
   commits the new PNGs.

For that workflow to be robust, **the manual editing rules MUST be
explicit** — that's what this document is for.

---

## Repo layout

```
docs.github.io/
├── _config.yml                 ← Jekyll site config (plugins, SEO, etc.)
├── robots.txt                  ← AI crawler allowlist + sitemap pointer
├── _layouts/                   ← Jekyll layouts (admin-manual, question-manual)
├── _includes/header.html       ← Custom site header (cross-manual nav + FR↔EN switcher)
├── _data/
│   ├── fr/
│   │   ├── admin_manual.yml    ← FR sidebar TOC for /ai/fr/
│   │   └── question_manual.yml ← FR sidebar TOC for /ai/fr/question-module/
│   └── en/
│       ├── admin_manual.yml    ← EN sidebar TOC for /ai/en/
│       └── question_manual.yml ← EN sidebar TOC for /ai/en/question-module/
├── assets/main.scss            ← All site CSS (Minima base + custom)
├── ai/
│   ├── index.md                ← Language picker landing page (/ai/)
│   ├── fr/
│   │   ├── index.md            ← Admin manual landing (FR)
│   │   ├── <chapter>/
│   │   │   ├── index.md        ← Chapter content (FR Markdown)
│   │   │   └── img/*.png       ← Screenshots (FR UI)
│   │   └── question-module/
│   │       ├── index.md
│   │       └── <chapter>/
│   │           ├── index.md
│   │           └── img/*.png
│   └── en/                     ← Mirror of fr/ in English
└── (other legacy manuals: tosamanual/, manuelplateforme_Tosa/, ...)
```

The `ai/fr/` and `ai/en/` trees must stay **structurally identical** —
same chapter slugs, same image filenames. Only the Markdown text differs.

---

## Page anatomy

Every chapter file is a Markdown document with this exact shape:

```markdown
---
layout: admin-manual          # or "question-manual" for the question module
---

# Chapter title

Intro paragraph(s).

![alt text](img/01-first-capture.png)

More prose.

## First section heading {#first-section-anchor}

...

## Second section heading {#second-section-anchor}

...
```

Three things matter:

1. **`layout:`** must be `admin-manual` (for `/ai/<lang>/<not-question-module>/`)
   or `question-manual` (for `/ai/<lang>/question-module/<anything>/`). The
   layout picks the correct sidebar TOC data file based on the URL.

2. **`{#anchor}` on `##` headings** — these are the URL fragment IDs.
   The sidebar TOC references them via `_data/<lang>/<manual>.yml`. If
   an anchor in the data file doesn't match an anchor in the chapter,
   the sidebar link 404s the in-page jump.

3. **Image references** are **language-agnostic paths** (`img/01-foo.png`).
   The same filename exists in `ai/fr/<chapter>/img/` and
   `ai/en/<chapter>/img/`, but the PNGs themselves are different (one in
   French UI, one in English).

---

## Sidebar TOC data file

`_data/<lang>/<manual>.yml` is a list of chapters, each with sections:

```yaml
- title: Account management            # ← sidebar label
  url: /ai/en/account/                 # ← chapter URL (MUST match folder)
  sections:
    - title: Account details           # ← sidebar sub-item label
      anchor: account-details          # ← matches {#account-details} in the .md
    - title: Packs and credits
      anchor: packs-and-credits
```

The layout iterates this list to render the left sidebar. **All four
data files (FR×2 + EN×2) must list the same chapters in the same order**,
just with translated titles and language-specific anchors/URLs.

---

## Bilingual rules

### Translation parity

- Every `ai/fr/<chapter>/index.md` MUST have a counterpart at
  `ai/en/<chapter>/index.md` with identical Markdown structure (same
  headings hierarchy, same image references, same blockquote types).
- The English file uses **English anchor slugs** (`{#account-details}`),
  the French file uses **French anchor slugs** (`{#details-du-compte}`).
- The canonical anchor slugs are listed in the two `_data/<lang>/*.yml`
  files — if a chapter section uses an anchor not in the data file, the
  sidebar won't link to it.

### Internal links

A link from one chapter to another stays inside the same language:

- ✅ `[Candidate management](/ai/en/candidates/)` from inside an EN page
- ✅ `[Gestion des candidats](/ai/fr/candidates/)` from inside an FR page
- ❌ Don't link to `/ai/candidates/` (no language prefix) — that URL
  doesn't exist any more.

For section-level links (`/ai/en/candidates/#add-a-candidate`), use the
canonical English anchor slug from the EN data file.

### Adding a new chapter

1. **FR first**: create `ai/fr/<chapter>/index.md` with `layout: admin-manual`
   or `layout: question-manual`. Choose French anchor slugs.
2. Add an entry to `_data/fr/<manual>.yml` listing the chapter and its
   anchors.
3. **EN counterpart**: create `ai/en/<chapter>/index.md` mirroring the
   structure, English anchors.
4. Add to `_data/en/<manual>.yml`.
5. **Spec**: add a `<chapter>.manual.spec.mjs` in `isograd_app/tests/specs/ui/`
   that captures the chapter's screenshots. Follow the template in
   [`tests/scripts/MANUAL-SCREENSHOTS.md`](../isograd_app/tests/scripts/MANUAL-SCREENSHOTS.md).
6. **Generate**: run the spec for both languages (see next section).

---

## Refreshing screenshots

When the platform UI changes and screenshots need to be regenerated:

```bash
cd ../isograd_app/tests

# One chapter, French
MANUAL_LANG=fr npx playwright test --project=ui-manual-screenshots \
  -g 'Gestion des candidats'

# Same chapter, English
MANUAL_LANG=en npx playwright test --project=ui-manual-screenshots \
  -g 'Gestion des candidats'

# All chapters, both languages (~25 min total)
MANUAL_LANG=fr npx playwright test --project=ui-manual-screenshots
MANUAL_LANG=en npx playwright test --project=ui-manual-screenshots
```

The PNGs are written **directly into this repo** at
`ai/<lang>/<chapter>/img/*.png` — commit them as part of the screenshot
refresh.

See [`tests/scripts/MANUAL-SCREENSHOTS.md`](../isograd_app/tests/scripts/MANUAL-SCREENSHOTS.md)
in the `isograd_app` repo for the full spec-side runbook (env vars,
helpers, troubleshooting).

---

## Reviewer workflow — commit message conventions

When a reviewer edits the manual and wants screenshots regenerated, the
**commit message should be explicit** about what to regenerate. The AI
or human running the screenshot job will key off this.

### Examples

✅ **Good** — explicit chapter and language:

> Clarify import workflow in Candidates chapter.
> Please regenerate screenshots — only Candidates, both FR and EN.

✅ **Good** — explicit scope:

> Fix typo in Question editor / Sortable section.
> No screenshot regen needed (text-only change).

✅ **Good** — multi-chapter:

> Add Visa note to Sessions and Mail-templates intros.
> Regenerate screenshots: Sessions (FR+EN), Mail-templates (FR+EN).

❌ **Bad** — too vague:

> Update docs.

The AI will be reading these commits in the future. **Tell it exactly
what to run.**

### Cheatsheet for commit instructions

| Phrase | Means |
|---|---|
| "Regenerate screenshots for <chapter>" | Run `-g '<chapter>'` for both langs |
| "Regenerate all screenshots" | Run the full suite for both langs |
| "FR only" | Skip the `MANUAL_LANG=en` run |
| "No screenshot regen" | Text-only edit, no spec run |
| "Add chapter X" | Means: chapter doesn't exist yet, follow "Adding a new chapter" above |

---

## SEO and crawlers

The site is publicly indexable and explicitly allows AI crawlers (see
[`robots.txt`](./robots.txt)). The relevant plugins in `_config.yml`:

- `jekyll-sitemap` → auto-generates `/sitemap.xml` from all pages
- `jekyll-seo-tag` → injects `<title>`, `<meta description>`, Open Graph,
  canonical, Twitter cards into every page's `<head>`

The sitemap covers all 42 chapter URLs (21 × 2 languages). No action
needed when adding a chapter — the plugin picks it up automatically.

If you need to **block** indexing of a specific page (e.g. a draft),
add `noindex: true` to its YAML frontmatter — `jekyll-seo-tag` will
inject the appropriate meta tag.

---

## Local preview

```bash
bundle install      # only the first time
bundle exec jekyll serve
# → site at http://localhost:4000/
```

GitHub Pages uses an allowlist of Jekyll plugins. Both plugins in our
`_config.yml` are on that allowlist, so the production build works
without a custom GH Actions workflow.

---

## Common pitfalls

### Indented HTML inside Markdown becomes a code block

If you write raw HTML inside a `.md` file with indentation, Kramdown
sees the 4-space indent and turns it into a `<pre>` code block. Either:

- **Strip all indentation** from raw HTML inside Markdown, or
- Add `markdown="0"` to the outer HTML element to disable Markdown
  processing inside it.

The language picker at [`ai/index.md`](./ai/index.md) demonstrates the
fix.

### Sidebar TOC entries that don't match

If the sidebar shows a chapter but clicking the link 404s, check:

- The chapter folder exists at `ai/<lang>/<chapter>/`
- It contains an `index.md`
- The `url:` field in `_data/<lang>/<manual>.yml` matches the folder
  path (with leading and trailing slash)

If a section sub-link is dead, the chapter's `## Heading {#anchor}`
doesn't match the `anchor:` field in the data file. Fix one or the other.

### The language switcher in the header

`_includes/header.html` detects the current language from the URL
(`/ai/fr/` vs `/ai/en/`) and:

- Highlights the active language pill (FR or EN).
- The other pill links to the **same** URL with the language prefix
  swapped (e.g. `/ai/fr/candidates/` ↔ `/ai/en/candidates/`).

This works because the FR and EN trees have identical structure. If
you add a chapter in only one language, the cross-language link will
404 — keep parity.

### The legacy manuals

Folders like `manuelplateforme_Tosa/`, `tosamanual/`, `itsmanual/`,
`manueladmin_Tosa/`, `itsadmin/`, `tosaadmin/`, `manueladmin_ITS/`,
`manuelplateforme_ITS/`, `guideplateformehebergement_ITS/` are the
**legacy manuals** — the originals before the bilingual `/ai/`
rebuild. They use a different layout (`layout: home`) and aren't part
of the screenshot automation. Leave them alone unless explicitly asked.

---

## Files you should NOT edit casually

- `_layouts/*.html` — the layouts are wired into the data files and
  header includes. Changing them affects every page.
- `assets/main.scss` — site-wide CSS; rebuild the whole site to test.
- `_config.yml` plugin list — these need to stay on the GH Pages
  allowlist, otherwise the build breaks.
- `robots.txt` — only change to add/remove crawler agents, never to
  block search engines from the docs.

When in doubt, ask for a code review.
