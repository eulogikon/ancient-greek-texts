# Ancient Greek Texts

The data store for [Eulogikon](https://eulogikon.org). The ancient Greek
corpus as downloadable files: PDF, with Markdown and plain text to follow.

## What this repository is

A store of the corpus as files. PDFs are here now; Markdown and text will be
added alongside them.

The files are produced upstream by the Eulogikon project and stored here as
repository artifacts.

## Layout

```
ancient-greek-texts/
├── README.md
├── LICENSE              # CC0 1.0
├── docs/MISSION.md
├── grc/{author}/{work}.pdf
├── en/{author}.pdf
├── affiliations/{school}.pdf
└── domains/{domain}.pdf
```

Markdown and text versions will sit alongside the PDFs under the same paths,
with the appropriate extension.

## Contributions

Corrections go to the upstream Eulogikon project. Files here are regenerated
from source; pull requests against them are not accepted.

## Licence

All Eulogikon scaffolding is [CC0 1.0](LICENSE). The ancient texts are public
domain where applicable. The embedded Gentium Plus font is under the SIL Open
Font License.
