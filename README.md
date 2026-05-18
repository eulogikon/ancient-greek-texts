# Ancient Greek Texts

This is the data store for the [Eulogikon](https://eulogikon.org) project.

[Eulogikon](https://eulogikon.org) is a free, open library of ancient Greek
literature. The corpus spans Homer through late antiquity — philosophy,
history, medicine, drama, lyric, mathematics, and the fragmentary traditions
— published as clean Unicode Greek with no logins, no fees, and no
paywalls. The mission is to make these texts permanently readable and
freely available to anyone, anywhere.

The reading site lives at [eulogikon.org](https://eulogikon.org). This
repository holds the corpus as downloadable files.

## What this repository is

A store of the corpus as files. PDFs are here now; Markdown and plain text
will be added alongside them.

The files are produced upstream by the Eulogikon project from the same
source as the website. This repository is not built or run directly.

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

Markdown and text versions will sit alongside the PDFs under the same
paths, with the appropriate extension.

## Contributions

Corrections go to the upstream Eulogikon project. Files here are
regenerated from source; pull requests against them are not accepted.

## Links

- Reading site: [eulogikon.org](https://eulogikon.org)
- About the project: [eulogikon.org](https://eulogikon.org)

## Licence

All Eulogikon scaffolding is [CC0 1.0](LICENSE). The ancient texts are
public domain where applicable. The embedded Gentium Plus font is under
the SIL Open Font License.