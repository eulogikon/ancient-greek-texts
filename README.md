---
language:
  - grc
license: other
license_name: public-domain-mark-1.0
license_link: https://creativecommons.org/publicdomain/mark/1.0/
pretty_name: Ancient Greek Texts
tags:
  - ancient-greek
  - digital-humanities
  - corpus
  - classical-studies
  - public-domain
---

# Ancient Greek Texts

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20335421.svg)](https://doi.org/10.5281/zenodo.20335421)
[![License: Public Domain Mark 1.0](https://img.shields.io/badge/License-Public%20Domain%20Mark%201.0-brightgreen.svg)](https://creativecommons.org/publicdomain/mark/1.0/)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-dataset-yellow)](https://huggingface.co/datasets/eulogikon/ancient-greek-texts)
[![Website](https://img.shields.io/badge/read-eulogikon.org-1f6feb)](https://eulogikon.org)
[![Catalog](https://img.shields.io/badge/browse-catalog-8250df)](https://eulogikon.github.io/ancient-greek-texts/)

The surviving literary works of ancient Greece — 1,353 authors and 4,055 works, spanning Homer through late antiquity. Philosophy, history, drama, lyric, medicine, mathematics, rhetoric, and the fragmentary traditions, all in clean Unicode Greek.

This is the data store for [Eulogikon](https://eulogikon.org): the reading site, search, and browse experience live there. This repository holds the corpus as downloadable files.

No logins. No fees. No paywalls. Public Domain Mark 1.0.

---

## What's here

**1,353 authors · 4,055 works · PDF, Markdown, and plain text**

A complete index of every author and work lives in [`llms.txt`](llms.txt) (start here for AI assistants), [`manifest.authors.json`](manifest.authors.json) and [`manifest.works.min.csv`](manifest.works.min.csv) (compact lookup), [`MANIFEST.md`](MANIFEST.md) (human-readable, grouped by domain and affiliation), [`manifest.json`](manifest.json) (full machine-readable index), and [`manifest.csv`](manifest.csv) (one row per work).

The corpus spans the full arc of ancient Greek writing: pre-Socratic fragments, the Attic historians, Platonic dialogues, Aristotelian treatises, Hellenistic poetry, Stoic and Epicurean texts, medical writers, mathematicians, geographers, orators, dramatists, and late antique philosophers. Where only fragments survive, those fragments are included.

Files are produced from the same source as the Eulogikon website and updated alongside it.

---

## Layout

```
ancient-greek-texts/
├── grc/{work_display_string}-{eul_wid}.grc.pdf    # Greek text as PDF
├── grc/{work_display_string}-{eul_wid}.grc.md     # Greek text as Markdown
├── grc/{work_display_string}-{eul_wid}.grc.txt    # Greek text as plain text
├── en/{author_display_string}-{eul_aid}.en.pdf    # English author page
├── en/{author_display_string}-{eul_aid}.en.md     # English author page as Markdown
├── en/{author_display_string}-{eul_aid}.en.txt    # English author page as plain text
├── affiliations/{school}.pdf                       # Texts grouped by philosophical school
├── domains/{domain}.pdf                            # Texts grouped by domain (philosophy, drama, …)
├── llms.txt                                        # LLM entry point and lookup guide
├── manifest.authors.json                           # Compact author index
├── manifest.works.min.csv                          # Compact work index
├── MANIFEST.md                                     # Human-readable index of every author and work
├── manifest.json                                   # Machine-readable manifest
└── manifest.csv                                    # Manifest as one row per work
```

Files are flat — every Greek work and every English author page lives directly inside `grc/` or `en/`, with no per-author subdirectory.

**Display strings** use lowercase kebab-case: an author's is e.g. `plato`, `aristotle`, `thucydides-of-athens`, `sextus-empiricus`; a work's prefixes a short author form, e.g. `plato-republic`. They are the human-readable URL and filename piece — attributes, not identifiers.

**Identifiers** are the trailing tokens. `eul_aid` is the opaque three-letter author ID (`ffk`, `hgw`, …), not derived from the name. `eul_wid` is the full work ID, `{eul_aid}-{suffix}` (e.g. `ffk-ag`) — the suffix alone (`ag`) is not the ID. So the work filename `plato-republic-ffk-ag` is `{work_display_string}-{eul_wid}`, and the author filename `plato-ffk` is `{author_display_string}-{eul_aid}`.

**Domains covered:** biography, comedy, drama, epic, fiction, geography, grammar, history, law, mathematics, medicine, oratory, philosophy, poetry, rhetoric, science, theology.

**Philosophical schools:** Academic Sceptic, Aristotelian, Atomist, Cynic, Cyrenaic, Eleatic, Epicurean, Megarian, Neo-Platonist, Neo-Pythagorean, Platonist, Pre-Socratic, Pythagorean, Sophist, Stoic, and more.

---

## Formats

| Format | Greek texts | English author pages |
|--------|------------|---------------------|
| PDF | ✓ | ✓ |
| Markdown | ✓ | ✓ |
| Plain text | ✓ | ✓ |

The Markdown files carry the richest reading form — the full Greek text (or English author metadata: period, dialect, domain, affiliation, biography) with headings and structure preserved. Plain text and PDF carry the same content in their respective forms.

---

## A few highlights

| Author | Works |
|--------|-------|
| Plato | ~41 dialogues including the Republic, Phaedo, Symposium, and Apology |
| Aristotle | Complete surviving corpus |
| Homer | Iliad and Odyssey |
| Thucydides | History of the Peloponnesian War |
| Herodotus | Histories |
| Sophocles, Euripides, Aeschylus | Extant tragedies |
| Diogenes Laertius | Lives of the Eminent Philosophers |
| Pre-Socratics (Heraclitus, Parmenides, Democritus, …) | Fragments |
| Stoics (Chrysippus, Zeno, Epictetus, Marcus Aurelius) | Surviving texts and fragments |
| Epicurus | Surviving works and fragments |

---

## Using these files

**For reading:** go to [eulogikon.org](https://eulogikon.org) — it offers full search, browse by author, period, domain, and philosophical school.

**For downloading:** clone or use the GitHub UI. All files are named predictably; no build step is needed.

**For research / NLP / DH:** the Markdown files are the richest format — clean Unicode Greek with headings and structure preserved, one file per work. Plain text gives the same content without markup. Author-level metadata (period, dialect, domain, affiliation, biography) is in each author's Markdown page under `en/`. Each work and author has a stable Eulogikon identifier (`eul_wid` / `eul_aid`) for citing the text as a whole; resolve it via the manifests.

**For AI assistants / API callers:** read [`llms.txt`](llms.txt) first. It follows the [llms.txt](https://llmstxt.org/) convention — a short curated entry point that points to compact lookup files rather than the full manifest (~13,000-line `MANIFEST.md` or ~80,000-line `manifest.json`). Resolve an author or work there, then fetch individual files from `en/` or `grc/`.

```bash
# Clone the full corpus
git clone https://github.com/eulogikon/ancient-greek-texts.git

# Grab a single work (Plato's Republic, Greek text as Markdown)
curl -O https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/grc/plato-republic-ffk-ag.grc.md

# Get Plato's author page (biography, works list, period, dialect, …)
curl -O https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/en/plato-ffk.en.md
```

(File names follow the patterns in [Layout](#layout) above. Resolve the exact display string and identifier for any author or work via [`manifest.authors.json`](manifest.authors.json) or [`manifest.works.min.csv`](manifest.works.min.csv).)

---

## For AI training and inference

The ancient Greek texts are **Public Domain Mark 1.0** — public domain, no restrictions. Eulogikon's scaffolding (README, metadata shape, manifests) is CC0 1.0. AI training, fine-tuning, evaluation, retrieval-augmented generation, and any other use are explicitly permitted, with no opt-out, no attribution requirement, and no royalty.

If you are an AI assistant fetching this repository at inference time, start at [`llms.txt`](llms.txt). It is a short curated entry point listing the compact lookup indexes ([`manifest.authors.json`](manifest.authors.json), [`manifest.works.min.csv`](manifest.works.min.csv)) and the pre-built domain and affiliation PDF compilations. Do not crawl `grc/` or `en/` directly — together they hold 16,000+ files and the directory listings are essentially noise without the manifest.

Machine-readable dataset metadata is provided in three forms: [schema.org JSON-LD](dataset.jsonld), the embedded block below (parsed by Google Dataset Search), and [CITATION.cff](CITATION.cff).

```json
{
  "@context": "https://schema.org/",
  "@type": "Dataset",
  "name": "Ancient Greek Texts",
  "description": "The surviving literary works of ancient Greece: 1,353 authors and 4,055 works spanning Homer through late antiquity. Philosophy, history, drama, lyric, medicine, mathematics, rhetoric, and the fragmentary traditions, all in clean Unicode Greek. Public Domain Mark 1.0.",
  "url": "https://github.com/eulogikon/ancient-greek-texts",
  "sameAs": [
    "https://eulogikon.org",
    "https://github.com/eulogikon/ancient-greek-texts",
    "https://doi.org/10.5281/zenodo.20335421",
    "https://zenodo.org/records/20335421",
    "https://huggingface.co/datasets/eulogikon/ancient-greek-texts"
  ],
  "identifier": [
    "https://github.com/eulogikon/ancient-greek-texts",
    "https://doi.org/10.5281/zenodo.20335421"
  ],
  "version": "v2026.06.08",
  "license": "https://creativecommons.org/publicdomain/mark/1.0/",
  "isAccessibleForFree": true,
  "inLanguage": ["grc"],
  "temporalCoverage": "-0800/0600",
  "keywords": [
    "ancient Greek", "classics", "classical philology", "digital humanities",
    "text corpus", "Homer", "Plato", "Aristotle", "Stoicism", "Pre-Socratics",
    "Hellenistic literature", "late antiquity", "NLP dataset"
  ],
  "creator": {
    "@type": "Organization",
    "name": "Eulogikon",
    "url": "https://eulogikon.org"
  },
  "distribution": [
    {
      "@type": "DataDownload",
      "name": "Machine-readable manifest (JSON)",
      "encodingFormat": "application/json",
      "contentUrl": "https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/manifest.json"
    },
    {
      "@type": "DataDownload",
      "name": "Manifest (CSV)",
      "encodingFormat": "text/csv",
      "contentUrl": "https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/manifest.csv"
    },
    {
      "@type": "DataDownload",
      "name": "LLM entry point (llms.txt)",
      "encodingFormat": "text/plain",
      "contentUrl": "https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/llms.txt"
    },
    {
      "@type": "DataDownload",
      "name": "Zenodo archival snapshot",
      "encodingFormat": "application/zip",
      "contentUrl": "https://zenodo.org/records/20335421"
    },
    {
      "@type": "DataDownload",
      "name": "Hugging Face dataset",
      "encodingFormat": "application/x-parquet",
      "contentUrl": "https://huggingface.co/datasets/eulogikon/ancient-greek-texts"
    }
  ]
}
```

---

## Licence

The ancient Greek texts are **[Public Domain Mark 1.0](https://creativecommons.org/publicdomain/mark/1.0/)** — public domain, no restrictions. Eulogikon's own scaffolding and metadata (README, manifests, metadata shape) is dedicated to the public domain under [CC0 1.0 Universal](LICENSE). The full rights statement — including the public-domain notice for the texts — is in [NOTICE](NOTICE). The embedded Gentium Plus font (in PDFs) is under the [SIL Open Font License](https://openfontlicense.org/).

---

## Contributing

This is a generated data store. Files are produced upstream and written here automatically; pull requests against corpus files are not accepted. For text corrections, visit the [Eulogikon project](https://eulogikon.org).

Corrections and issues with scaffolding, metadata structure, or file naming can be raised as GitHub Issues.

---

## Links

| | |
|---|---|
| Reading site | [eulogikon.org](https://eulogikon.org) |
| Browse catalog | [eulogikon.github.io/ancient-greek-texts](https://eulogikon.github.io/ancient-greek-texts/) |
| Organisation | [github.com/eulogikon](https://github.com/eulogikon) |
| GitHub data store | [github.com/eulogikon/ancient-greek-texts](https://github.com/eulogikon/ancient-greek-texts) |
| Zenodo archive | [zenodo.org/records/20335421](https://zenodo.org/records/20335421) |
| Zenodo DOI | [doi.org/10.5281/zenodo.20335421](https://doi.org/10.5281/zenodo.20335421) |
| Hugging Face dataset | [huggingface.co/datasets/eulogikon/ancient-greek-texts](https://huggingface.co/datasets/eulogikon/ancient-greek-texts) |
| Licence | [Public Domain Mark 1.0](https://creativecommons.org/publicdomain/mark/1.0/) |
