---
name: eulogikon-ancient-greek-texts
description: Access the Eulogikon ancient Greek text archive via the GitHub Pages catalog and the eulogikon/ancient-greek-texts data store — 1,353 authors and 4,055 works, Homer through late antiquity, all public domain (Public Domain Mark 1.0). Resolve works by stable eul_wid in manifest indexes, then fetch Greek text as Markdown or plain text from raw GitHub URLs.
---

# Eulogikon ancient Greek texts (catalog + data store)

This skill covers the **GitHub Pages catalog** at https://eulogikon.github.io/ancient-greek-texts and the
**downloadable data store** at https://github.com/eulogikon/ancient-greek-texts. Greek work files live in the
data store; the catalog orients agents and hosts discovery files on this origin.

Start at https://eulogikon.github.io/ancient-greek-texts/llms.txt on the catalog site, or install from this origin:

```bash
npx skills add https://eulogikon.github.io/ancient-greek-texts
```

## Identifiers

- `eul_aid` — opaque three-letter author code (Plato is `ffk`). Never guess from a name.
- `eul_wid` — work identifier beginning with its `eul_aid` (Apology is `ffk-aa`).
- Display strings (`author_display_string`, `work_display_string`) compose file
  names but are **not** identifiers. Resolve by `eul_aid` / `eul_wid` first.

## Lookup (same GitHub repo, raw URLs)

1. Read https://eulogikon.github.io/ancient-greek-texts/llms.txt on the catalog site for orientation.
2. Fetch https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/manifest.authors.json — compact author index keyed by `eul_aid`.
3. Fetch https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/manifest.works.min.csv — grep-friendly work index (one row per work).
4. For the full nested index, use https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/manifest.json (large; do not load whole).

Do not crawl `grc/` or `en/` directories by guesswork — use the manifests.

## Fetch a single work

1. Find the row for your `eul_wid` in `manifest.works.min.csv` or `manifest.json`.
2. Read the `md` or `grc_md` path from that row.
3. Fetch `https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/<path>` (Markdown is the richest text format).

Example (Plato, Apology):

```bash
curl -L "https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/grc/plato-apology-ffk-aa.grc.md"
```

## File naming

- Greek work: `grc/{work_display_string}-{eul_wid}.grc.{pdf|md|txt}`
- English author page: `en/{author_display_string}-{eul_aid}.en.{pdf|md|txt}`

## Licence

Ancient Greek texts: **Public Domain Mark 1.0** — no restrictions on use,
redistribution, or training. Eulogikon scaffolding (indexes, metadata) is
**CC0 1.0**.

## Optional human reading site

For browser reading with search and browse UI, humans may use
https://eulogikon.org. Agents completing lookup and fetch do not need it.

## Citation

Dataset DOI: https://doi.org/10.5281/zenodo.20335421
