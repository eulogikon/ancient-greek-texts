# Ancient Greek Texts

The **published PDF archive** of [Eulogikon](https://eulogikon.org) — the
ancient Greek corpus as a parallel, independently indexable, forkable set of
PDFs, one per mirrored page, interlinked as a graph.

**Mission:** [docs/MISSION.md](docs/MISSION.md).

## What this repository is

This repository is the *artifact archive*: the PDFs and the contract they
satisfy. It has no pipeline of its own. The PDFs are produced upstream by the
Eulogikon project from the same single-source data as the HTML site, and
written here at the mirrored path.

| Surface | Where | Role |
|---|---|---|
| HTML | [eulogikon.org](https://eulogikon.org) | reading, search |
| PDF | this repository | download, offline reading, archival, indexing |

## Layout

```
ancient-greek-texts/
├── README.md
├── LINKING.md          # the link/path contract these PDFs satisfy
├── CONTRIBUTING.md      # corrections go upstream; the branch invariant
├── LICENSE              # CC0 1.0
├── docs/MISSION.md
├── grc/{author}/{work}.pdf
├── en/{author}.pdf
├── affiliations/{school}.pdf
└── domains/{domain}.pdf
```

Each mirrored page keeps the same path as `eulogikon.org`, with `.pdf`
appended (`/grc/aegimius/text` → `grc/aegimius/text.pdf`). Links between PDFs
follow [LINKING.md](LINKING.md): a link to another mirrored page points at its
PDF twin (a GitHub blob URL on `main`); a link to a non-mirrored page stays an
absolute `eulogikon.org` URL; every PDF links back to its HTML twin.

## Regenerating

The corpus is regenerated upstream from the Eulogikon source and written into
this repository; this repository is not built or run directly. Contributions
and corrections go to the upstream Eulogikon project (see
[CONTRIBUTING.md](CONTRIBUTING.md)).

## Licence

All Eulogikon scaffolding is [CC0 1.0](LICENSE). The ancient texts are public
domain where applicable; the corpus is attributed to no one. The embedded
Gentium Plus font is under the SIL Open Font License.
