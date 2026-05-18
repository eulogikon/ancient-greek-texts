# Mission

**Repository:** `eulogikon/ancient-greek-texts`
**Status:** Authoritative.
**Version:** 1.0

---

Eulogikon makes ancient Greek texts freely and permanently readable.

The texts of ancient Greek literature are part of the common inheritance of
humanity. They do not belong to any institution, database, or compiler.
Eulogikon publishes them as such: clean Unicode Greek, no logins, no fees, no
attribution to anyone — because there is no one to attribute them to.

The deliverable is the readable text. Every decision about this corpus — what
to build, what to refuse to build, what to remove — is judged against whether
it makes the texts more readable, more available, and more durable.

**Readable** means the reader can read it: clean polytonic Greek on a page that
does not obstruct it, exactly as the website presents it. The PDF is a faithful
print of the page — it never silently substitutes or "repairs" a glyph, and it
never hides the text behind editorial scaffolding. Where the source itself has
a rare-glyph gap, the gap is closed upstream in the data, not papered over by
the mirror and not used to block the mirror. Producing the readable text is the
source's job; reproducing it faithfully is this repository's.

**Available** means anyone can get it. Freely, without an account, without a
subscription, without a gatekeeper, in any country. On the live website. On
GitHub. As a PDF that can be downloaded, mirrored, forked, redistributed.

**Durable** means the texts outlive any single platform. The HTML site is one
surface. This repository is another. Neither depends on the other to remain
useful. If either disappears, the corpus survives in the other.

That is the mission. This repository is the **durable** and **available**
surface: the published PDF archive.

---

## Where things live

This repository is the artifact archive only — the PDFs and their contract.
The pipeline that produces them lives upstream in the Eulogikon project. See
[`../README.md`](../README.md) and [`../LINKING.md`](../LINKING.md).

---

## Version history

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2026-05-17 | Initial mission statement |
| 1.1 | 2026-05-17 | Clarified "Readable": faithful reproduction; rare-glyph gaps are upstream-data aspirations, not build gates. |
| 2.0 | 2026-05-18 | Repository re-conceived as the published PDF archive; the generation pipeline moved upstream into the Eulogikon project. Removed the in-repo pipeline-design docs (their content now lives upstream with the generator code). |
