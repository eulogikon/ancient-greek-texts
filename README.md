# Ancient Greek Texts

A free, open archive of ancient Greek literature — 1,341 authors, spanning Homer through late antiquity. Philosophy, history, drama, lyric, medicine, mathematics, rhetoric, and the fragmentary traditions, all in clean Unicode Greek.

This is the data store for [Eulogikon](https://eulogikon.org): the reading site, search, and browse experience live there. This repository holds the corpus as downloadable files.

No logins. No fees. No paywalls. CC0.

---

## What's here

**1,341 authors · 4,000+ works · PDF, Markdown, plain text, and JSON**

The corpus spans the full arc of ancient Greek writing: pre-Socratic fragments, the Attic historians, Platonic dialogues, Aristotelian treatises, Hellenistic poetry, Stoic and Epicurean texts, medical writers, mathematicians, geographers, orators, dramatists, and late antique philosophers. Where only fragments survive, those fragments are included.

Files are produced from the same source as the Eulogikon website and updated alongside it.

---

## Layout

```
ancient-greek-texts/
├── grc/{author-slug}/{work-slug}.pdf      # Greek text as PDF
├── grc/{author-slug}/{work-slug}.md       # Greek text as Markdown
├── grc/{author-slug}/{work-slug}.txt      # Greek text as plain text
├── grc/{author-slug}/{work-slug}.json     # Structured data (sentences, metadata)
├── en/{author-slug}.pdf                   # English author page
├── en/{author-slug}.md                    # English author page as Markdown
├── en/{author-slug}.txt                   # English author page as plain text
├── en/{author-slug}.json                  # Author metadata and biography
├── affiliations/{school}.pdf             # Texts grouped by philosophical school
└── domains/{domain}.pdf                  # Texts grouped by domain (philosophy, drama, etc.)
```

**Author slugs** use lowercase kebab-case: `plato`, `aristotle`, `thucydides-of-athens`, `sextus-empiricus`.

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

```bash
# Clone the full corpus
git clone https://github.com/eulogikon/ancient-greek-texts.git

# Grab a single author's Greek texts
curl -O https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/grc/plato/republic.md

# Get Plato's structured metadata
curl -O https://raw.githubusercontent.com/eulogikon/ancient-greek-texts/main/en/plato.json
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
| Licence | [CC0 1.0](LICENSE) |
