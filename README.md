---
language:
  - el
  - en
license: cc0-1.0
pretty_name: Ancient Greek Texts
tags:
  - ancient-greek
  - digital-humanities
  - corpus
  - classical-studies
---

# Ancient Greek Texts

A free, open archive of ancient Greek literature — 1,342 authors and 4,005 works, spanning Homer through late antiquity. Philosophy, history, drama, lyric, medicine, mathematics, rhetoric, and the fragmentary traditions, all in clean Unicode Greek.

This is the data store for [Eulogikon](https://eulogikon.org): the reading site, search, and browse experience live there. This repository holds the corpus as downloadable files.

No logins. No fees. No paywalls. CC0.

---

## What's here

**1,342 authors · 4,005 works · PDF, Markdown, plain text, and JSON**

A complete index of every author and work lives in [`llms.txt`](llms.txt) (start here for AI assistants), [`manifest.authors.json`](manifest.authors.json) and [`manifest.works.min.csv`](manifest.works.min.csv) (compact lookup), [`MANIFEST.md`](MANIFEST.md) (human-readable, grouped by domain and affiliation), [`manifest.json`](manifest.json) (full machine-readable index), and [`manifest.csv`](manifest.csv) (one row per work).

The corpus spans the full arc of ancient Greek writing: pre-Socratic fragments, the Attic historians, Platonic dialogues, Aristotelian treatises, Hellenistic poetry, Stoic and Epicurean texts, medical writers, mathematicians, geographers, orators, dramatists, and late antique philosophers. Where only fragments survive, those fragments are included.

Files are produced from the same source as the Eulogikon website and updated alongside it.

---

## Layout

```
ancient-greek-texts/
├── grc/{author-slug}-{work-slug}-{eul_aid}-{wid}.grc.pdf    # Greek text as PDF
├── grc/{author-slug}-{work-slug}-{eul_aid}-{wid}.grc.md     # Greek text as Markdown
├── grc/{author-slug}-{work-slug}-{eul_aid}-{wid}.grc.txt    # Greek text as plain text
├── grc/{author-slug}-{work-slug}-{eul_aid}-{wid}.grc.json   # Structured sentences + metadata
├── en/{author-slug}-{eul_aid}.en.pdf                        # English author page
├── en/{author-slug}-{eul_aid}.en.md                         # English author page as Markdown
├── en/{author-slug}-{eul_aid}.en.txt                        # English author page as plain text
├── en/{author-slug}-{eul_aid}.en.json                       # Author metadata, biography, and work list
├── affiliations/{school}.pdf                                 # Texts grouped by philosophical school
├── domains/{domain}.pdf                                      # Texts grouped by domain (philosophy, drama, …)
├── llms.txt                                                    # LLM entry point and lookup guide
├── manifest.authors.json                                       # Compact author index
├── manifest.works.min.csv                                      # Compact work index
├── MANIFEST.md                                                 # Human-readable index of every author and work
├── manifest.json                                               # Machine-readable manifest
└── manifest.csv                                                # Manifest as one row per work
```

Files are flat — every Greek work and every English author page lives directly inside `grc/` or `en/`, with no per-author subdirectory.

**Author slugs** use lowercase kebab-case: `plato`, `aristotle`, `thucydides-of-athens`, `sextus-empiricus`. The trailing three-letter token (`-ffk`, `-hgw`, …) is the Eulogikon author ID (`eul_aid`); the work suffix (`-aa`, `-ae`, …) is the per-author work ID (`eul_wid`).

**Domains covered:** biography, comedy, drama, epic, fiction, geography, grammar, history, law, mathematics, medicine, oratory, philosophy, poetry, rhetoric, science, theology.

**Philosophical schools:** Academic Sceptic, Aristotelian, Atomist, Cynic, Cyrenaic, Eleatic, Epicurean, Megarian, Neo-Platonist, Neo-Pythagorean, Platonist, Pre-Socratic, Pythagorean, Sophist, Stoic, and more.

---

## Formats

| Format | Greek texts | English author pages |
|--------|------------|---------------------|
| PDF | ✓ | ✓ |
| Markdown | ✓ | ✓ |
| Plain text | ✓ | ✓ |
| JSON | ✓ | ✓ |

The JSON files contain structured sentence-level data with metadata (period, dialect, domain, affiliation, biography) suitable for NLP, corpus linguistics, and digital humanities research.

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

**For research / NLP / DH:** the JSON files are the richest format. Each author JSON includes biography, period, dialect, domain, and affiliation metadata. Work JSONs include the text segmented into addressable units, each carrying a Eulogikon segment ID (`sid`) of the form `{eul_aid}-{work-suffix}-{segment}` (e.g. `ffk-ag-aaa`). A segment is a semantic unit — a sentence, a phrase, a clause, or a list — the fine-grained coordinate for citing a place in the text.

**For AI assistants / API callers:** read [`llms.txt`](llms.txt) first. It follows the [llms.txt](https://llmstxt.org/) convention — a short curated entry point that points to compact lookup files rather than the full manifest (~13,000-line `MANIFEST.md` or ~80,000-line `manifest.json`). Resolve an author or work there, then fetch individual files from `en/` or `grc/`.

```bash
# Clone the full corpus
git clone https://github.com/eulogikon/ancient-greek-texts.git

# Grab a single work (Plato's Republic, Greek text as Markdown)
curl -O https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/grc/plato-republic-ffk-ag.grc.md

# Get Plato's author-level metadata (biography, works list, period, dialect, …)
curl -O https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/en/plato-ffk.en.json
```

(File names follow the patterns in [Layout](#layout) above. Resolve an exact slug for any author or work via [`manifest.authors.json`](manifest.authors.json) or [`manifest.works.min.csv`](manifest.works.min.csv).)

---

## For AI training and inference

This corpus is released under [CC0 1.0 Universal](LICENSE) — public domain. AI training, fine-tuning, evaluation, retrieval-augmented generation, and any other use are explicitly permitted, with no opt-out, no attribution requirement, and no royalty.

If you are an AI assistant fetching this repository at inference time, start at [`llms.txt`](llms.txt). It is a short curated entry point listing the compact lookup indexes ([`manifest.authors.json`](manifest.authors.json), [`manifest.works.min.csv`](manifest.works.min.csv)) and the pre-built domain and affiliation PDF compilations. Do not crawl `grc/` or `en/` directly — together they hold 21,000+ files and the directory listings are essentially noise without the manifest.

Machine-readable dataset metadata is provided in three forms: [schema.org JSON-LD](dataset.jsonld), the embedded block below (parsed by Google Dataset Search), and [CITATION.cff](CITATION.cff).

```json
{
  "@context": "https://schema.org/",
  "@type": "Dataset",
  "name": "Ancient Greek Texts",
  "description": "A public-domain corpus of ancient Greek literature: 1,342 authors and 4,005 works spanning Homer through late antiquity. Includes philosophy, history, drama, lyric, medicine, mathematics, rhetoric, and the fragmentary traditions. Published in clean Unicode Greek as PDF, Markdown, plain text, and structured JSON, with English author metadata and biographies.",
  "url": "https://github.com/eulogikon/ancient-greek-texts",
  "sameAs": [
    "https://eulogikon.org",
    "https://github.com/eulogikon/ancient-greek-texts",
    "https://doi.org/10.5281/zenodo.20335421",
    "https://zenodo.org/records/20335422",
    "https://huggingface.co/datasets/eulogikon/ancient-greek-texts"
  ],
  "identifier": [
    "https://github.com/eulogikon/ancient-greek-texts",
    "https://doi.org/10.5281/zenodo.20335421"
  ],
  "version": "v2026.05.28",
  "license": "https://creativecommons.org/publicdomain/zero/1.0/",
  "isAccessibleForFree": true,
  "inLanguage": ["grc", "en"],
  "temporalCoverage": "-0800/0600",
  "keywords": [
    "ancient Greek", "classics", "classical philology", "digital humanities",
    "text corpus", "Homer", "Plato", "Aristotle", "Stoicism", "Pre-Socratics",
    "Hellenistic literature", "late antiquity", "Koine Greek", "NLP dataset"
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
      "contentUrl": "https://zenodo.org/records/20335422"
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

All Eulogikon scaffolding and metadata is [CC0 1.0 Universal](LICENSE) — public domain, no restrictions. The ancient texts themselves are likewise public domain. The embedded Gentium Plus font (in PDFs) is under the [SIL Open Font License](https://openfontlicense.org/).

---

## Contributing

This is a generated data store. Files are produced upstream and written here automatically; pull requests against corpus files are not accepted. For text corrections, visit the [Eulogikon project](https://eulogikon.org).

Corrections and issues with scaffolding, metadata structure, or file naming can be raised as GitHub Issues.

---

## Links

| | |
|---|---|
| Reading site | [eulogikon.org](https://eulogikon.org) |
| Organisation | [github.com/eulogikon](https://github.com/eulogikon) |
| GitHub data store | [github.com/eulogikon/ancient-greek-texts](https://github.com/eulogikon/ancient-greek-texts) |
| Zenodo archive | [zenodo.org/records/20335422](https://zenodo.org/records/20335422) |
| Zenodo DOI | [doi.org/10.5281/zenodo.20335421](https://doi.org/10.5281/zenodo.20335421) |
| Hugging Face dataset | [huggingface.co/datasets/eulogikon/ancient-greek-texts](https://huggingface.co/datasets/eulogikon/ancient-greek-texts) |
| Licence | [CC0 1.0](LICENSE) |
