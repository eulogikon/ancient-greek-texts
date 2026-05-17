# Ancient Greek Texts

Archive and library of ancient Greek texts as **PDF**, published by
[Eulogikon](https://eulogikon.org). This repository is the English-scaffolded
PDF surface; HTML reading lives on the main site.

## Relationship to Eulogikon

| Surface | Location |
|---|---|
| HTML (reading, search, apparatus) | [eulogikon.org](https://eulogikon.org) |
| PDF (download, offline reading) | this repository |

Each work is a PDF under `{author-slug}/{work-slug}.pdf`. Author indexes,
affiliation indexes, and corpus navigation PDFs live at the repo root and under
`affiliations/`.

## Repository layout

```
ancient-greek-texts/
├── README.md
├── LINKING.md          # URL rules for HTML ↔ PDF (read before generating PDFs)
├── CONTRIBUTING.md     # branch invariant and contribution notes
├── LICENSE             # CC0 1.0
├── index.pdf
├── index_alphabetic.pdf
├── affiliations/
│   ├── schools.pdf
│   └── domains.pdf
└── {author-slug}/
    ├── README.md
    ├── index.pdf
    └── {work-slug}.pdf
```

## Licence

All Eulogikon scaffolding in this repository is [CC0 1.0](LICENSE). Ancient
texts are public domain where applicable.
