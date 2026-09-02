# David A. Reiss — Personal Pages

Personal website (about me, CV, work, writings, research, open-source contributions,
publications, talks …) built with [Hugo](https://gohugo.io), the
[PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme (pinned to release
`v8.0` as a git submodule), and the academic publications/projects layout overrides
adapted from [hugo-PaperMod-academics](https://github.com/shinying/hugo-PaperMod-academics).

Live site: https://d-a-reiss.github.io/

Content is classified in two ways:

- **Sections** (`writings/`, `research/`, `publications/`, `projects/`, `talks/`) —
  what kind of thing it is (its structure / URL).
- **Topics + tags** (taxonomies) — what it is about (cross-cutting, many-to-many).
  A post in `writings/`, a paper in `publications/`, and a research page can all
  share the topic `AI`; the page `/topics/ai/` aggregates all of them.
  - `topics` are a small **controlled vocabulary** of broad areas. Current vocabulary:
    **AI**, **Math**, **Physics**, **Open Source Software**, **Writing**
    (each has a description page under `content/topics/<slug>/_index.md` — extend it
    when adding a new topic).
  - `tags` are free-form, granular labels (e.g. `transformers`, `rust`, `vim`).

## Prerequisites

- **Hugo (extended)** ≥ 0.146 — `brew install hugo` (macOS), or see
  https://gohugo.io/installation/
- Basic tools: `git`

## Getting a local copy

The theme is a git submodule, so clone recursively (or init submodules afterwards):

```sh
git clone git@github.com:D-A-Reiss/D-A-Reiss.github.io.git
cd D-A-Reiss.github.io
git submodule update --init --recursive
```

## Local preview & drafts

- `hugo server` — live preview with rebuild-on-save at **http://localhost:1313/**;
  only published pages.
- `hugo server -D` (same as `--buildDrafts`) — live preview **including draft pages**.
  This is how you view pages whose front matter has `draft: true` before publishing them.

**How drafts work:** every new page created with `hugo new …` starts with
`draft: true` (the archetypes in `archetypes/` set this). While `draft: true`:

- it is visible locally via `hugo server -D` only,
- it is **excluded from the production build**, and the GitHub Actions workflow
  builds without drafts — so drafts never appear on the live site.

To publish a page, change `draft: true` to `draft: false` (or remove the line)
in its front matter.

> Future-dated pages use the same idea with `--buildFuture`/`-F` for local preview;
> they are also excluded from the default production build.

## Creating content

```sh
hugo new writings/my-new-post/index.md      # blog post (leaf bundle, so images can live next to it)
hugo new research/another-project/index.md  # research page
hugo new publications/paper-slug.md         # publication entry
hugo new projects/project-slug.md           # project entry
hugo new talks/talk-slug.md                 # talk entry
```

Each archetype pre-fills the relevant front matter (`title`, `date`, `draft: true`,
`topics: []`, `tags: []`; the publications archetype also pre-fills
`authors`, `venue`, `year`, `arxiv`, `code`, `selected`, `summary`).

Standalone pages live at the content root: `about.md`, `cv.md`, `archives.md`
(archive index), `search.md` (search UI). A `cv.pdf` is served from
`static/cv.pdf` — drop your file in `static/`  as `cv.pdf`.

## Front-matter conventions

```yaml
---
title: "…"
date: 2026-09-02
draft: true
description: "Short summary used in lists and meta tags."
topics: ["AI", "Writing"]     # broad areas — keep to the controlled vocabulary
tags: ["transformers", "gpt"] # granular, free-form
---
```

For `publications/` entries additionally:

```yaml
authors:
  - name: "David A. Reiss"
    home: "https://d-a-reiss.github.io/"
venue: "Conference/Journal name"
year: 2026
arxiv: "https://arxiv.org/abs/…"
code: "https://github.com/…"
video: "https://…"
selected: true   # only `selected: true` entries are shown on the homepage
                 # (site param: ShowOnlySelectedPubs)
summary: "One-paragraph abstract/summary."
---
```

## Deployment (GitHub Pages)

- Site is deployed by `.github/workflows/hugo.yaml` on every push to `main`
  (or manual `workflow_dispatch` run in the Actions tab).
- Requires the repo setting: **Settings → Pages → Build and deployment →
  Source = “GitHub Actions”**.
- Production builds never include drafts (`buildDrafts` is off and the workflow
  does not pass `-D`).

## Updating the theme

The submodule is pinned to the `v8.0` release tag. To update:

```sh
cd themes/PaperMod
git fetch --tags
git checkout vX.Y            # desired release tag
cd ../..
git add themes/PaperMod
git commit -m "Update PaperMod to vX.Y"
```

(Or track master by leaving the submodule on `master` — but the pinned release
keeps builds reproducible.)

## Structure

```
├── assets/            # site-level CSS/SVG additions (icons, pub styling)
├── content/           # all site content (sections + standalone pages + topics)
├── layouts/           # local template overrides (home, publications, projects, …)
├── archetypes/        # front-matter templates for `hugo new`
├── static/            # static files (cv.pdf, favicon, …)
├── themes/PaperMod/   # git submodule → PaperMod v8.0
└── .github/workflows/ # Pages deployment workflow
```
