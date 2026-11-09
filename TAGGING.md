# Tagging methodology — Spurgeon Pulpit JSON set (schema 1.1)

Every volume JSON carries a `tagging` object:

```json
"tagging": {"schema_version": "1.1",
            "book_id_system": "Project canonical 66-book table (TAGGING.md): 3-letter codes with numeric prefix for numbered books (e.g. 2TI)",
            "cross_ref_sort": "canonical Bible order",
            "proper_noun_types": ["biblical_person", "historical_person", "place", "people_or_group", "other_name"]}
```

The same two functions in `tagging.py` produced the metadata for all 63
volumes, so the methodology is identical across the set. The build and
verification scripts live in `~/workspace/research_notes/spurgeon-pulpit-build/`
(`build_spurgeon.py`, `tagging.py`, `verify_spurgeon.py`).

## 1. The text taken (`texts_taken`)

For each sermon, the scripture passage printed in the sermon heading is
parsed into one entry per text taken (most sermons have exactly one; a
sermon preached from two texts, or from a whole chapter, is represented
faithfully):

```json
{"reference_display": "2 Timothy 3:5", "reference_as_printed": "II Tim. 3:5",
 "book": "2 Timothy", "book_id": "2TI", "testament": "NT",
 "chapter": 3, "verse_start": 5, "verse_end": 5,
 "quote_as_printed": "Having a form of godliness, but denying the power thereof…"}
```

Rules:

- The reference is taken **only** from the printed heading (the quotation
  paragraph ending in the attribution, with or without an em-dash, or the
  heading reference line). A text is never guessed. If the heading could
  not be parsed, the volume's own contents/index reference (archive.spurgeon.org
  index, itself compiled from the printed volumes) is used and
  `reference_as_printed` records that form; if neither exists,
  `texts_taken` is empty and `scripture` is null.
- `reference_as_printed` preserves the printed form (e.g. `Psalm ciii. 1`,
  `Galatians iv. 3—6`); `reference_display` is the canonical form produced
  by the shared parser (full book name, arabic chapter and verses).
- `quote_as_printed` is the verse wording printed under the heading, or
  null when the heading prints no quotation.
- Coverage: 3,520 of 3,561 sermons (98.8%) have at least one text identified.

## 2. Canonical book table

One 66-book table is used for `texts_taken`, `cross_references`, sorting,
and validation. `book_id` is a 3-letter code, with a numeric prefix for
numbered books (1SA, 2TI, 1JN…). Chapters are validated against the
book's chapter count.

| book_id | book | testament | chapters |
|---|---|---|---|
| GEN | Genesis | OT | 50 |
| EXO | Exodus | OT | 40 |
| LEV | Leviticus | OT | 27 |
| NUM | Numbers | OT | 36 |
| DEU | Deuteronomy | OT | 34 |
| JOS | Joshua | OT | 24 |
| JDG | Judges | OT | 21 |
| RUT | Ruth | OT | 4 |
| 1SA | 1 Samuel | OT | 31 |
| 2SA | 2 Samuel | OT | 24 |
| 1KI | 1 Kings | OT | 22 |
| 2KI | 2 Kings | OT | 25 |
| 1CH | 1 Chronicles | OT | 29 |
| 2CH | 2 Chronicles | OT | 36 |
| EZR | Ezra | OT | 10 |
| NEH | Nehemiah | OT | 13 |
| EST | Esther | OT | 10 |
| JOB | Job | OT | 42 |
| PSA | Psalms | OT | 150 |
| PRO | Proverbs | OT | 31 |
| ECC | Ecclesiastes | OT | 12 |
| SNG | Song of Solomon | OT | 8 |
| ISA | Isaiah | OT | 66 |
| JER | Jeremiah | OT | 52 |
| LAM | Lamentations | OT | 5 |
| EZK | Ezekiel | OT | 48 |
| DAN | Daniel | OT | 12 |
| HOS | Hosea | OT | 14 |
| JOL | Joel | OT | 3 |
| AMO | Amos | OT | 9 |
| OBA | Obadiah | OT | 1 |
| JON | Jonah | OT | 4 |
| MIC | Micah | OT | 7 |
| NAM | Nahum | OT | 3 |
| HAB | Habakkuk | OT | 3 |
| ZEP | Zephaniah | OT | 3 |
| HAG | Haggai | OT | 2 |
| ZEC | Zechariah | OT | 14 |
| MAL | Malachi | OT | 4 |
| MAT | Matthew | NT | 28 |
| MRK | Mark | NT | 16 |
| LUK | Luke | NT | 24 |
| JHN | John | NT | 21 |
| ACT | Acts | NT | 28 |
| ROM | Romans | NT | 16 |
| 1CO | 1 Corinthians | NT | 16 |
| 2CO | 2 Corinthians | NT | 13 |
| GAL | Galatians | NT | 6 |
| EPH | Ephesians | NT | 6 |
| PHP | Philippians | NT | 4 |
| COL | Colossians | NT | 4 |
| 1TH | 1 Thessalonians | NT | 5 |
| 2TH | 2 Thessalonians | NT | 3 |
| 1TI | 1 Timothy | NT | 6 |
| 2TI | 2 Timothy | NT | 4 |
| TIT | Titus | NT | 3 |
| PHM | Philemon | NT | 1 |
| HEB | Hebrews | NT | 13 |
| JAS | James | NT | 5 |
| 1PE | 1 Peter | NT | 5 |
| 2PE | 2 Peter | NT | 3 |
| 1JN | 1 John | NT | 5 |
| 2JN | 2 John | NT | 1 |
| 3JN | 3 John | NT | 1 |
| JUD | Jude | NT | 1 |
| REV | Revelation | NT | 22 |

## 3. Cross-references (`cross_references`)

Explicit citations in the sermon **body** (the text after the heading
block, which ends at the scripture-attribution paragraph) are extracted
by a rule-based parser — never inferred from allusions or quotations
without a citation.

- **Forms recognised:** full names and the standard abbreviations of the
  period (`Ps.`, `Isa.`, `Rom.`, `II Tim.`, `1 Cor.`…), with arabic or
  roman-numeral chapters (`Psalm 23:1`, `Rom. viii. 28`, `Isa. liii.`),
  colon or period verse separators, verse ranges, comma-separated verse
  lists (split into separate entries), and chapter-only citations
  (`Isa. liii.` → chapter with null verses). Compact index forms
  (1Sa, Re, Ac) are recognised when parsing contents/index references.
- **Guards against false positives:** an uppercase roman-numeral chapter
  requires an abbreviation dot or a colon form (so "Am I" is not Amos 1);
  ambiguous one-word aliases that are also English words (Am, Is, So,
  Job, Mark…) require a dot or colon form unless the full book name is
  used; the chapter must exist in the book.
- **Entry shape:** `{"reference_display", "reference_as_printed", "book",
  "book_id", "testament", "chapter", "verse_start", "verse_end",
  "occurrences"}`. Entries are deduplicated within a sermon by
  normalised reference (occurrences counted) and **sorted in canonical
  Bible order** (book order above, then chapter, then verse) in every
  volume.
- The body text itself is **not** altered: references live in metadata only.
- Yield is honest but modest — Spurgeon's sermons weave most quotations
  into the prose without formal citations, so a typical sermon has 0–3
  explicit citations. 1,715 distinct references are indexed across the set.

## 4. Proper nouns (`proper_nouns`)

Extracted conservatively, per sermon, from capitalised-name evidence
plus curated gazetteers (biblical persons and places, peoples/groups,
and historical persons of the period):

- **Controlled types (only these five):** `biblical_person`,
  `historical_person`, `place`, `people_or_group`, `other_name`.
  Biblical figures are `biblical_person` even when also historical.
- **Entry shape:** `{"name", "name_as_printed", "type", "occurrences"}`,
  where `name` is the normalised citation form and `name_as_printed`
  the most common form in that sermon.
- **Normalisation:** spelling/OCR variants are merged only where the
  identity is unambiguous (e.g. Melchisedec → Melchizedek, Simon Peter →
  Peter, Saul of Tarsus → Paul, Pontius Pilate → Pilate, Judea → Judaea).
  Divine names and titles (God, Lord, Jehovah…) are excluded; venue
  names ("Metropolitan Tabernacle", "New Park Street Chapel"), month and
  weekday names are excluded. Single names that are also common verbs
  (e.g. Mark) require a mid-sentence occurrence. Unattested multi-word
  capitalised phrases become `other_name` only with at least 3
  occurrences, at least 2 of them mid-sentence.
- Entries are deduplicated and sorted alphabetically (case-insensitive)
  within each sermon. 1,991 distinct proper nouns are indexed across the set.

## 5. Dates and occasions (`delivered`, `preaching_year`, `publication_year`)

Per sermon:

```json
"delivered": {"date_as_printed": "DELIVERED ON LORD'S-DAY MORNING, JANUARY 2, 1870,",
              "date_iso": "1870-01-02", "year": 1870, "month": 1, "day": 2,
              "occasion": "Lord's-Day morning", "venue": "Metropolitan Tabernacle"}
```

- Parsed only from the printed delivery line. Month names are matched in
  full or abbreviated form, with ordinal day suffixes (1st, 2nd, 3rd,
  4th…) stripped. `date_as_printed` preserves the printed line (first
  120 characters); fields that cannot be read are null, never invented.
- `occasion` captures Lord's-Day/Sabbath morning or evening, Thursday
  evening, etc., as printed. `venue` is normalised to "New Park Street
  Chapel" or "Metropolitan Tabernacle" when the heading names one of
  them; otherwise the printed venue is kept, or null.
- Posthumous volumes (1893–1917) print both a publication line and the
  delivery line; the **delivered** date is the one recorded. Where a
  heading prints only an "intended for reading" date (common in the
  posthumous volumes), that printed date is what is parsed — it is the
  date of the printed sermon's issue, and no earlier delivery date is
  printed to record. Some headings carry no date at all; those sermons
  have null date fields (venue may still be present).
- Coverage: 3,247 of 3,561 sermons (91.2%) have a full `date_iso`.
- Volume level: `preaching_year` is the volume's year in the original
  publication sequence (NPSP vol. 1 = 1855 … MTP vol. 63 = 1917). The
  re-typeset text base does not reproduce the original title pages, so
  the year is not read off a title page in hand; it is corroborated by
  the delivery dates of the sermons each volume contains.
  `publication_year` is null throughout, for the same reason: no year is
  asserted that the source in hand does not print.
