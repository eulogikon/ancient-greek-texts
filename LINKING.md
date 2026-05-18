# Linking Contract

The contract every PDF in this archive satisfies. It is enforced upstream by
the Eulogikon project; this document is the spec the output satisfies.

## Path rule

A mirrored PDF's path is the site path with `.pdf` appended. No `pdf/`
wrapper, no reorganisation.

```text
/grc/aegimius/text     ->  grc/aegimius/text.pdf
/en/marcus-aurelius    ->  en/marcus-aurelius.pdf
/domains/epic          ->  domains/epic.pdf
/affiliations/stoic    ->  affiliations/stoic.pdf
```

Mirrored page classes: `/grc/<author>/<work>`, `/en/<author>`,
`/domains/<domain>`, `/affiliations/<school>`.

## The PDF graph

Every in-content link is resolved by one mechanical path rule:

- a link to a **mirrored** page → that page's PDF twin, an absolute GitHub
  blob URL:
  `https://github.com/eulogikon/ancient-greek-texts/blob/main/<site_path>.pdf`
- a link to a **non-mirrored** page → its absolute `eulogikon.org` HTML URL
- external links and `#fragments` → untouched

So the PDFs interconnect exactly as the pages do — a work links to its
author's and related works' PDFs, authors back to their works, works to their
domain/affiliation.

## Back-link

Every PDF carries a quiet footer linking to its own HTML twin
(`https://eulogikon.org/<site_path>`) — the PDF→HTML backlink.

## Branch invariant

Every PDF-graph URL hard-codes the `main` branch. The default branch is
`main`, forever (see [CONTRIBUTING.md](CONTRIBUTING.md)) — this is
load-bearing: every cross-link in every published PDF depends on it.
