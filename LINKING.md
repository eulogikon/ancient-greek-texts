# Eulogikon Linking Strategy

The canonical reference for how every link is constructed across the Eulogikon corpus — in every HTML page on `eulogikon.org` and in every PDF in the per-language GitHub repositories.

This document lives in the root of every per-language PDF repo and is the
single source of truth for URL generation in both the HTML build pipeline and the
PDF build pipeline. **This repository** (`eulogikon/ancient-greek-texts`) is the
English (`en`) scaffold. Additional languages use `ancient-greek-texts-{lang}`
(e.g. `ancient-greek-texts-ru`).

---

## Purpose

Eulogikon publishes ancient Greek texts in two parallel access surfaces:

- **HTML** on `eulogikon.org`, served via Cloudflare Pages
- **PDF** on GitHub, in per-language repositories

The two surfaces cross-reference each other heavily. Each surface is independently usable, and together they form a redundant, distributed publication: if the HTML site fails the PDFs remain readable and navigable on their own; if GitHub fails the HTML site remains operational, and any pre-existing forks of the corpus remain.

The link strategy supports this redundancy. Every artifact carries the URLs needed to reach every other artifact on both surfaces. No link is left implicit.

---

## Invariants

Three things are fixed and cannot change without breaking every artifact ever published. Lock these in before generating anything.

### 1. Default branch is `main`, forever

Every PDF and every downloaded HTML file hard-codes `main` in raw `githubusercontent.com` URLs. Renaming the default branch would break every link in every artifact published to that point.

Documented as a project invariant in `CONTRIBUTING.md` at repo creation.

### 2. Absolute URLs in all HTML and PDF artifacts

Relative paths are used **only** inside in-repo Markdown files (`README.md` and similar) where they support repo browsing on github.com. Everywhere else — every HTML page, every PDF — URLs are fully qualified with scheme and domain.

### 3. Per-language repos with the suffix convention

Repository names follow the pattern `ancient-greek-texts-{lang}` where `{lang}`
is the ISO language code. The English-scaffolded corpus lives in
`ancient-greek-texts` (this repo). Russian will be `ancient-greek-texts-ru`.
Chinese will be `ancient-greek-texts-zh`.

The Greek text itself is identical across all repos. Only the scaffolding — apparatus, metadata, synopsis, bios, navigation labels — changes between languages.

---

## URL surfaces

There are exactly three host surfaces in this architecture, used in distinct roles:

| Host | Serves | Used for |
|---|---|---|
| `eulogikon.org` | HTML pages via Cloudflare Pages | All HTML reading and navigation |
| `raw.githubusercontent.com` | Binary file streams from the GitHub repos | All PDF downloads and PDF-internal links |
| `github.com/{owner}/{repo}/blob/...` | GitHub's repo wrapper pages | Optional "View on GitHub" affordance only |

The `github.com/blob/` form is **not** used inside PDFs, never used in nav strips, and never used as a primary link target. It exists for one purpose: a discreet affordance on the HTML site (and inside in-repo Markdown) for users who want to see the file in its GitHub context.

---

## Path conventions

### On the HTML site (`eulogikon.org`)

```
https://eulogikon.org/                                          home
https://eulogikon.org/index_alphabetic                          A-Z author index
https://eulogikon.org/affiliations                              schools
https://eulogikon.org/affiliations?tab=domains                  domains
https://eulogikon.org/{lang}/{author-slug}                      author page (scaffolded)
https://eulogikon.org/grc/{author-slug}/{work-slug}             work page (Greek view)
https://eulogikon.org/{lang}/{author-slug}/{work-slug}          work page (scaffolded, if present)
```

`{lang}` is the ISO code: `en`, `ru`, `zh`, etc. `grc` is the language-neutral Greek-only view.

### In the GitHub repo (`ancient-greek-texts-{lang}`)

```
ancient-greek-texts-{lang}/
├── README.md                                  repo homepage (GitHub-rendered)
├── LINKING.md                                 this document
├── CONTRIBUTING.md                            project conventions including branch invariant
├── LICENSE                                    CC0
├── index.pdf                                  PDF homepage
├── index_alphabetic.pdf                       A-Z author index PDF
├── affiliations/
│   ├── schools.pdf
│   └── domains.pdf
└── {author-slug}/
    ├── README.md                              author page (GitHub-rendered)
    ├── index.pdf                              author page PDF
    └── {work-slug}.pdf                        individual work PDFs
```

The repo path mirrors the site path with the language prefix stripped — the repo name itself carries the language, so `/en/` is not repeated inside `ancient-greek-texts`.

---

## The four link directions

### 1. HTML → HTML (within `eulogikon.org`)

**Rule.** Absolute URLs, always.

**Format.**
```
https://eulogikon.org/{path}
```

**Why absolute.** Downloaded HTML kept on a user's disk still navigates the live site. HTML files placed in the repo work identically whether viewed locally, on github.com, or via any future mirror. No URL rewriting is required at any consumption surface.

**Examples.**
```
https://eulogikon.org/en/menander-of-athens
https://eulogikon.org/grc/menander-of-athens/coneazomenae
https://eulogikon.org/affiliations
https://eulogikon.org/affiliations?tab=domains
https://eulogikon.org/index_alphabetic
```

---

### 2. HTML → PDF (`eulogikon.org` → GitHub)

**Rule.** Absolute raw URLs for downloads. Blob URLs only for the optional "View on GitHub" affordance.

**Format (download button).**
```
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts-{lang}/main/{path}
```

**Format (optional "View on GitHub" link).**
```
https://github.com/eulogikon/ancient-greek-texts-{lang}/blob/main/{path}
```

**Why raw for downloads.** Clicking "Download PDF" should produce a PDF — rendered in the browser's PDF viewer or saved to disk. Raw URLs serve the binary directly with `Content-Type: application/pdf`. Blob URLs route through a GitHub HTML wrapper page with an embedded viewer, which is friction for the download action.

**Why blob for "View on GitHub".** Users who deliberately want to see the file inside its repository context (to fork, to inspect, to open an issue) need the GitHub UI. Blob URLs deliver that.

**Examples.**

On `eulogikon.org/en/menander-of-athens/coneazomenae`, the download button targets:
```
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/coneazomenae.pdf
```

The optional "View on GitHub" link:
```
https://github.com/eulogikon/ancient-greek-texts/blob/main/menander-of-athens/coneazomenae.pdf
```

---

### 3. PDF → HTML (GitHub → `eulogikon.org`)

**Rule.** Absolute URLs to `eulogikon.org`. UTM-tag the bottom-of-PDF canonical link. Do **not** tag in-PDF navigation back to indexes.

**Format (canonical link, UTM-tagged).**
```
https://eulogikon.org/{lang}/{author-slug}/{work-slug}?utm_source=github&utm_medium=pdf&utm_campaign={lang}
```

If the site does not yet have language-scaffolded work pages and only `/grc/{author-slug}/{work-slug}` exists, fall back to:
```
https://eulogikon.org/grc/{author-slug}/{work-slug}?utm_source=github&utm_medium=pdf&utm_campaign={lang}
```

The `utm_campaign={lang}` parameter remains the language differentiator either way — analytics will still distinguish English-PDF traffic from Russian-PDF traffic even when both PDFs link to the same Greek-view page.

**Why UTM-tagged.** Lets analytics distinguish traffic from `ancient-greek-texts` vs `ancient-greek-texts-ru`, etc. Constants `utm_source=github` and `utm_medium=pdf` identify the surface; `utm_campaign={lang}` identifies the originating repo.

**Why not tag in-PDF nav.** Every tagged nav click would dilute the canonical-link signal and obscure which PDFs convert readers to the HTML site. Tag the canonical link only.

**Example.**

In `coneazomenae.pdf` (English scaffolding), the canonical link at the bottom of the document:
```
https://eulogikon.org/en/menander-of-athens/coneazomenae?utm_source=github&utm_medium=pdf&utm_campaign=en
```

---

### 4. PDF → PDF (within the GitHub repo)

**Rule.** Absolute raw URLs.

**Format.**
```
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts-{lang}/main/{path}
```

**Why raw.** Clicking a link inside a PDF should open the next PDF directly, preserving the reading flow. Blob URLs would route the user through a GitHub wrapper page and break the experience.

**Why absolute.** PDF readers do not have a reliable concept of "current location" the way browsers do. Relative URLs in PDFs behave inconsistently across viewers (Preview, Adobe Reader, browser-built-in viewers, mobile readers). Absolute URLs work everywhere.

**Examples.**

Top-of-PDF navigation strip in `coneazomenae.pdf`:

```
Previous work in Menander:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/{prev-work}.pdf

Menander author index:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/index.pdf

Next work in Menander:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/{next-work}.pdf
```

Global navigation strip (home, A-Z, schools, domains):
```
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/index.pdf
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/index_alphabetic.pdf
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/affiliations/schools.pdf
https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/affiliations/domains.pdf
```

---

### Fifth direction: in-repo Markdown navigation

`README.md` files inside the repo are consumed by GitHub's web UI when a user browses the repo. These use **relative paths**, not absolute URLs.

**Rule.** Relative paths only, inside Markdown files in the repo.

**Why relative.** Inside the GitHub UI, relative paths resolve correctly to the blob/wrapper page for files in the same repo. This is the right surface for repo browsing — the user is already in GitHub's interface and expects to navigate within it.

**Example.** In `menander-of-athens/README.md`:

```markdown
## Works

- [Coneazomenae](./coneazomenae.pdf)
- [Dyskolos](./dyskolos.pdf)

[← Back to author index](../index_alphabetic.pdf)
[← Back to home](../README.md)
```

When clicked on github.com, these resolve through GitHub's UI to the appropriate blob page. The user stays in the repo browsing context.

---

## Per-PDF link inventory

Every PDF in the corpus carries exactly the following links, no more and no less.

### Top of every PDF — navigation strip

| Link | URL form | Targets |
|---|---|---|
| ← Previous work | raw | Previous work in the same author's `{author-slug}/` directory |
| Author index | raw | `{author-slug}/index.pdf` |
| A-Z index | raw | `index_alphabetic.pdf` |
| Schools | raw | `affiliations/schools.pdf` |
| Domains | raw | `affiliations/domains.pdf` |
| Home | raw | `index.pdf` |
| Next work → | raw | Next work in the same author's `{author-slug}/` directory |

All raw, all absolute, all pointing within the same per-language repo.

### Bottom of every PDF — reference block

| Label | URL form | Purpose |
|---|---|---|
| Read online | UTM-tagged canonical to `eulogikon.org` | Drives HTML traffic, primary attribution, analytics |
| View source | blob URL on `github.com` | For users who want to see the file in its repo |
| Direct file | raw URL on `raw.githubusercontent.com` | For mirrors, programmatic ingestion, shareable file URL |

These three lines are present in identical form on every PDF, parameterised by `{lang}`, `{author-slug}`, `{work-slug}`.

---

## UTM tagging

Used **only** on the canonical link at the bottom of each PDF. Not used anywhere else.

```
?utm_source=github&utm_medium=pdf&utm_campaign={lang}
```

| Parameter | Value | Role |
|---|---|---|
| `utm_source` | `github` | Constant — identifies the upstream surface |
| `utm_medium` | `pdf` | Constant — identifies the artifact type |
| `utm_campaign` | `{lang}` | Language code of the originating repo (`en`, `ru`, `zh`, ...) |

Optional finer granularity for analytics, if useful:
```
&utm_content={author-slug}-{work-slug}
```

This is opt-in and not required by the spec.

---

## Worked example: Menander, *Coneazomenae* (English)

Complete link inventory for `coneazomenae.pdf` in `ancient-greek-texts`.

### Top navigation strip

```
← Previous: {prev-work}
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/{prev-work}.pdf

Menander author page:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/index.pdf

A-Z author index:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/index_alphabetic.pdf

Schools:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/affiliations/schools.pdf

Domains:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/affiliations/domains.pdf

Home:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/index.pdf

Next: {next-work} →
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/{next-work}.pdf
```

### Bottom reference block

```
Read online:
  https://eulogikon.org/en/menander-of-athens/coneazomenae?utm_source=github&utm_medium=pdf&utm_campaign=en

View source on GitHub:
  https://github.com/eulogikon/ancient-greek-texts/blob/main/menander-of-athens/coneazomenae.pdf

Direct file:
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/coneazomenae.pdf
```

### Inbound from the HTML site

On `eulogikon.org/en/menander-of-athens/coneazomenae` (or `/grc/menander-of-athens/coneazomenae`):

```
Download PDF →
  https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/menander-of-athens/coneazomenae.pdf

(Optional) View on GitHub →
  https://github.com/eulogikon/ancient-greek-texts/blob/main/menander-of-athens/coneazomenae.pdf
```

---

## Summary table

| From | To | URL form | Domain |
|---|---|---|---|
| HTML page | HTML page (within site) | absolute | `eulogikon.org` |
| HTML page | PDF (download) | absolute, raw | `raw.githubusercontent.com` |
| HTML page | PDF (view on GitHub, optional) | absolute, blob | `github.com/.../blob/main/...` |
| PDF | HTML canonical (bottom ref) | absolute, UTM-tagged | `eulogikon.org/...?utm_*` |
| PDF | PDF (in-PDF nav strip) | absolute, raw | `raw.githubusercontent.com` |
| Repo Markdown | PDF (same directory) | relative | `./{slug}.pdf` |
| Repo Markdown | PDF (different directory) | relative | `../{path}.pdf` |
| Repo Markdown | Another Markdown | relative | `./README.md`, `../README.md` |

---

## Implementation notes

### For the HTML site build pipeline

- Every internal link uses the absolute form `https://eulogikon.org/...`. No relative paths in rendered HTML.
- Download buttons target `https://raw.githubusercontent.com/eulogikon/ancient-greek-texts-{lang}/main/...` — URL is generated at build time, not at runtime.
- Optional "View on GitHub" links target `https://github.com/eulogikon/ancient-greek-texts-{lang}/blob/main/...`.
- The build pipeline must know which `{lang}` it is generating for, in order to point downloads at the correct repo.

### For the PDF generation pipeline

- The top-of-PDF navigation strip is populated from the repo's directory structure. Previous/next within an author come from the author's work ordering; A-Z, schools, domains, home are constants.
- The bottom-of-PDF reference block is identical in every PDF, parameterised by `{lang}`, `{author-slug}`, `{work-slug}`.
- All URLs are embedded as PDF link annotations (clickable in PDF viewers), not just as rendered text.
- All URLs are absolute. No relative URLs in PDF link annotations.

### For per-language expansion

When generating a new language repo (e.g., Russian):

- Repo: `ancient-greek-texts-ru`
- All raw URLs swap `ancient-greek-texts` → `ancient-greek-texts-ru`
- Canonical PDF → HTML links use `eulogikon.org/ru/{author-slug}/{work-slug}` (or `/grc/{author-slug}/{work-slug}` if no Russian-scaffolded work page exists) and `utm_campaign=ru`
- Repo internal structure is identical to the English repo
- The Greek text inside each PDF is unchanged across languages; only the scaffolding and navigation labels are translated

---

## Open question to confirm

This spec assumes work-level pages exist at `eulogikon.org/{lang}/{author-slug}/{work-slug}` as a per-language scaffolded view, parallel to `eulogikon.org/grc/{author-slug}/{work-slug}` which is the Greek-only view.

If the site only has work-level pages at `/grc/{author-slug}/{work-slug}` and per-language work pages do not exist, the canonical PDF → HTML link should target the `/grc/` URL for every language repo, with the language differentiation carried entirely by `utm_campaign={lang}`.

This needs to be confirmed against the actual site URL structure before the PDF build pipeline is implemented. Once confirmed, either delete this section or document the resolution here.

---

## Licence

This document, like the rest of Eulogikon's own contributions, is released under CC0 1.0. The texts are the texts. No conditions on reuse, no attribution required.
