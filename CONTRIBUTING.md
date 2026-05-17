# Contributing

Thank you for helping improve the Eulogikon PDF archive.

## Project invariants

These rules are fixed. Breaking them breaks every link embedded in published
PDFs and HTML.

### Default branch is `main`, forever

Every PDF hard-codes `main` in `raw.githubusercontent.com` URLs. Do not rename
the default branch. Do not retarget links to another branch name.

### Absolute URLs in PDFs

PDF link annotations must use fully qualified URLs. Relative paths are allowed
only in in-repo Markdown (`README.md` files) for GitHub browsing.

### Read `LINKING.md` before changing URLs

`LINKING.md` is the canonical spec for HTML ↔ PDF linking. Any change to URL
shape or repo layout must be reflected there first.

## Pull requests

1. Fork or branch from `main`.
2. Keep commits focused (one author, one fix, or one structural change).
3. Open a PR against `main` with a short summary of what changed and why.

For text corrections, prefer opening an issue on
[eulogikon/eulogikon](https://github.com/eulogikon/eulogikon) if the HTML
canonical record also needs updating.

## Licence

Contributions to scaffolding and metadata are released under CC0 1.0, consistent
with [LICENSE](LICENSE).
