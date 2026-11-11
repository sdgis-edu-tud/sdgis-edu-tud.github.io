# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A [Quarto](https://quarto.org) static website (`project: type: website`) publishing GIS/spatial-analysis educational content for TU Delft's Department of Urbanism. There is no application code, build tooling, or test suite — the repo is almost entirely `.qmd` (Quarto Markdown) content plus a small set of R scripts used for content maintenance.

## Commands

``` bash
quarto preview          # live-reload local preview, http://localhost:4200
quarto render           # full site build, writes to docs/ (configured output-dir; local only, gitignored)
quarto render pages/learn-qgis/introduction.qmd   # render a single page
quarto publish gh-pages # render + push the built site to the gh-pages branch (this is how the live site updates)
```

### Publishing

The live site (https://sdgis-edu-tud.github.io/) is served by GitHub Pages from the **`gh-pages` branch, root `/`** — not from `main`. Pushing to `main` does **not** update the site; run `quarto publish gh-pages` (or RStudio's Publish button) after changes are merged. `docs/` is in `.gitignore` and must not be committed (switched over on 2026-11-11; before that, rendered output was committed to `main:/docs`, which caused constant merge conflicts).

- `quarto publish` renders whatever is on disk, including uncommitted edits — publish from a clean, up-to-date `main` (stash local WIP first) so drafts don't go live.
- If publish fails with `'gh-pages' is already used by worktree ...` (stale worktree left by a publish on another machine; `.git` syncs via OneDrive), run `git worktree prune` and retry.

There is no linter, formatter, or test runner configured. R scripts under `management/scripts/` are run manually/interactively (`Rscript management/scripts/<name>.R`), not as part of the Quarto build.

## Site architecture

Configuration lives entirely in **`_quarto.yml`**: navbar, sidebar (with nested `section:` groups per topic), theme (cosmo/cyborg), and global HTML output options. `output-dir: docs` — `docs/` is the local build output only (gitignored; see **Publishing** above). A stale, previously-committed `_site/` also still exists in the repo — ignore it.

**A page is only "live" if it's reachable from `_quarto.yml`'s `navbar`/`sidebar` entries.** Several older content trees exist under `pages/` (e.g. `pages/main/`, `pages/sources/`, `pages/getting_started/`, `pages/cartography_and_mapping/`, `pages/learn_gis.qmd`, snake_case naming) that predate a migration to the current `pages/learn-qgis/**` (kebab-case) structure and are **not** referenced anywhere in `_quarto.yml`. Don't assume a `.qmd` file is part of the site just because it exists in `pages/` — check whether its path appears in the sidebar `contents:` list first. Note also that many `pages/learn-qgis/**` paths are listed in `_quarto.yml` but commented out (`# - pages/...`) — these are planned/WIP pages not yet published.

### Two flavors of listing pages

- **Tutorial listings** (`pages/learn-qgis/index.qmd`, `pages/courses/index.qmd`): use Quarto's `listing:` directive pointed at a glob of `.qmd` files. Cards are auto-generated from each tutorial's YAML frontmatter (`title`, `description`, `categories`, `date`). Adding a new tutorial to a listing requires no code change — just correct frontmatter and getting the file added to the sidebar in `_quarto.yml`.
- **Data source listing** (`pages/find-data/index.qmd`): `listing:` points at `pages/find-data/sources.yml`, a hand-maintained YAML array (`name`, `description`, `type`, `region`, `format`, `categories`) rather than a set of `.qmd` files — it's a flat catalog rendered as a filterable table.

### Content templates

`templates/tutorial-template.qmd`, `templates/course-template.qmd`, `templates/template.qmd` are starting points for new content — copy one rather than hand-rolling frontmatter/CSS. The tutorial template embeds a large custom CSS block (badges, callout styling, workflow diagrams) inline in the page; follow that pattern for consistency rather than adding new global CSS unless the styling is truly site-wide (site-wide CSS goes in `styles.css`, referenced via `format.html.css` in `_quarto.yml`).

### `management/` — content database tooling

R scripts (require `tidyverse`, `yaml`, `fs`, `readxl`/`writexl`) that keep a spreadsheet inventory of tutorials/sources in sync with the `.qmd`/`.yml` content:

- `build_tutorial_db.R` — scans `pages/learn-qgis/**/*.qmd`, extracts YAML frontmatter + word count/callout/image flags, writes a dated snapshot to `management/db/tutorial_db_<date>.{csv,xlsx}`.
- `build_sources_db.R` — converts `pages/find-data/sources.yml` to `management/db/sources.csv`/`.xlsx`.
- `update_qmd_yamls.R` — reverse direction: reads an edited `management/db/tutorial_db_template.xlsx` and rewrites each tutorial's YAML frontmatter in place (title/description/categories/level/date).
- `split_categories.R`, `rename_png.R` — one-off maintenance utilities for frontmatter category lists and sequential image renaming.

These form an edit-in-Excel workflow for non-technical content editors: export → edit spreadsheet → re-import to update frontmatter in bulk. When editing tutorial frontmatter by hand, keep the fields these scripts expect (`title`, `description`, `categories`, `level`, `date`) intact and in the shape they parse.

## Instruction for content

- use different callouts for tips, questions, solutions, extra info, etc, warnings, etc
- use *bold* for steps (e.g., Go to *Vector → Geoprocessing Tools → Dissolve*) — in practice this means **double-asterisk bold** (`**...**`), not single-asterisk italics; every published tutorial uses `**Vector → Geoprocessing Tools → Dissolve**`.
- use `single quotes` for files and fields (e.g., `OBJECTID`) — this means backtick code formatting (`` `OBJECTID` ``), not literal quote characters.
- suggest where to add screenshots in the text for clarification and create placeholders. Use the name of the .qmd for the folder where images will be stored, and a progressive naming for the figures (e.g., fig 1.png, fig 2.png, etc)

### Callout conventions (as used across published `pages/learn-qgis/**` tutorials)

- Tips → `::: {.callout-tip appearance="minimal" icon="true"}`
- Extra info / background → `::: {.callout-note appearance="minimal" icon="true"}`
- Must-read setup/prerequisite notes → `::: callout-important`
- Warnings → `::: {.callout-warning appearance="minimal" icon="true"}`
- Critical warnings (irreversible actions, data loss) → `::: {.callout-danger appearance="minimal" icon="true"}`
- Questions + solutions: state the question in plain text (`**❓ Question:** ...`), then reveal the answer in a *collapsed* callout so students aren't shown it immediately: `**Solution (click to reveal):**` followed by `::: {.callout-tip collapse="true"}`.
- TA-only notes: `::: {.callout-important title="Note for TA"}` — public-facing (students see the rendered page) but visually distinct. Use for grading hints, known gaps/placeholders to fill in before publishing, or things intentionally left for the TA to confirm.

### Tutorial structure (for longer, multi-step tutorials)

- Major phases: `## Step N: Title`, separated by a horizontal rule (`------------------------------------------------------------------------`) between each one.
- Sub-actions within a phase: `### N.1 Subtask Title`.
- Each action block ends with a short **Result:** (or **Verify:**) paragraph describing what the student should see, so they can self-check before moving on.
- Field-calculator/processing expressions go in fenced code blocks, followed by a plain-language explanation as one bullet per function/term used.
- Longer tutorials (multi-hour) may also include end sections seen in mature tutorials: a **Troubleshooting Guide** table (Problem/Cause/Solution), a **Quick Reference** table (Task/Tool Path/Purpose), **References & Resources**, and **Extensions/Advanced Topics** — add these for substantial tutorials, not short exercises.
- Match a tutorial's actual scope to its slot in the relevant course plan (see `pages/courses/*.qmd`) rather than the length of any template — a 30-minute exercise shouldn't be padded out to a multi-hour workflow just because a template has more sections.

### Frontmatter shape

Tutorial frontmatter is **flat** — `title`, `description`, `categories`, `level`, `level_code`, `level_color`, `date` at the top level — not nested under a `tutorial:` key as `templates/tutorial-template.qmd` suggests. This flat shape is what `management/scripts/build_tutorial_db.R` and `update_qmd_yamls.R` actually parse, so match existing tutorials, not the template. `level` values in use are `Beginner` (`level_code: 1.0`, `level_color: '#A6CEE3'`) and `Intermediate` (`level_code: 2.0`, `level_color: '#1F78B4'`) — stick to this vocabulary/color pairing rather than inventing new level names.

Known quirk: several published tutorials carry `date: .na.character` in frontmatter — an artifact of the R metadata pipeline serializing a missing date (see `update_qmd_yamls.R`), not a value to copy into new files. Always set a real date.
