# Contributing

This repository is a **generated archive**. The PDFs here are build output;
they are not edited by hand and pull requests against them are not accepted.

## Where changes go

- **Text or content corrections** — fix the source upstream in the
  Eulogikon project. The PDF regenerates from it.
- **Rendering / layout / linking changes** — handled upstream in the
  Eulogikon project, then regenerated here.
- **This repo** only receives regenerated PDFs and updates to these
  contract/readme docs.

## Fixed invariants

These cannot change without breaking every published cross-link:

### Default branch is `main`, forever

Every PDF-graph link is a GitHub blob URL that hard-codes `main`. Do not
rename the default branch or retarget links to another branch.

### The path/link contract

[`LINKING.md`](LINKING.md) is authoritative for PDF paths and cross-links.
Any change to URL shape or repo layout must be reflected there, and upstream,
first.

## Repository guard

This repo must contain only PDFs and these archive docs. A guard enforces it;
enable it once after cloning:

```sh
git config core.hooksPath .githooks
```

It rejects any commit that adds non-PDF/non-doc files or internal references.

## Licence

Contributions to scaffolding and metadata are released under CC0 1.0,
consistent with [LICENSE](LICENSE).
