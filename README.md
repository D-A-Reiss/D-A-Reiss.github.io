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

> Tip: `hugo server` writes rendered output into `public/` on disk. If a
> production-build check (`hugo build`) ever seems to show stale content
> (e.g. after previewing drafts), `rm -rf public` first — it is gitignored,
> and the CI workflow always builds `public/` fresh in its own workspace.

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

## Privacy / DSGVO posture

The site is deliberately built data-sparing so that it needs **no consent
banner** (per TDDDG § 25, consent is only required for technologies that store
or read information on end devices, or track users):

- No cookies, no analytics/tracking, no embedded third-party content, no
  external webfonts, no third-party CDNs — all CSS/JS/icons are self-hosted
  and the live page loads zero external *resources* (only outbound links).
- Social links (GitHub, LinkedIn, Google Scholar) are plain outbound
  hyperlinks with inline local SVG icons — nothing is transmitted to those
  services unless the visitor actively clicks a link.
- Site-level template overrides (`layouts/partials/header.html`,
  `layouts/partials/footer.html`) **remove all client-side storage**
  (localStorage) from the stock PaperMod theme: the dark/light preference and
  the menu scroll position are no longer persisted (they reset to the OS
  color scheme per visit — accepted trade-off).
- Legal pages: `/impressum/` (§ 5 DDG) and `/datenschutz/` (Art. 13 DSGVO),
  linked from every page's footer via `params.footer.text`.
- Hosting: GitHub Pages. GitHub processes access logs as a processor (GitHub
  Data Protection Addendum; EU-US Data Privacy Framework / SCCs) — disclosed
  in the Datenschutzerklärung.

**Rules to keep it that way (apply to any future change):**

- Analytics/tracking of any kind ⇒ requires a consent banner + policy update
  (TDDDG § 25, DSGVO).
- Embedding YouTube or any other third-party content ⇒ consent-gated 2-click
  solution, or don't embed (links only).
- Contact forms / comments / newsletter ⇒ update the Datenschutzerklärung.
- Fonts and images only from this domain — never fonts.googleapis.com or
  other CDNs.
- Do not re-introduce localStorage/cookies in theme updates; keep the two
  overrides (see *Updating the theme*).

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

> ⚠️ **DSGVO/TDDDG note:** the site carries two deliberate template overrides —
> `layouts/partials/header.html` and `layouts/partials/footer.html` — that strip
> all client-side storage (localStorage). After updating the theme, re-check
> both overrides against the new theme versions and re-apply the same removals
> if upstream reintroduces them (a `grep -r localStorage` over `public/` after
> a build must return zero matches; see the *Privacy / DSGVO posture* section).

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

## Open TODOs (placeholders to fill in)

- [ ] Real bio/tagline — `hugo.yaml` → `params.homeInfoParams.content`
- [ ] `static/cv.pdf` — linked from `/cv/`
- [ ] LinkedIn slug — `hugo.yaml` → `params.socialIcons`
- [ ] Favicon files — `static/` (avoids the theme's default 404s)
- [ ] Impressum — postal address + contact email (`content/impressum.md`)
- [ ] Datenschutzerklärung — address/email + supervisory authority to fill in
      (`content/datenschutz.md`); update the "Stand" date after editing
