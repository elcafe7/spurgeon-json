# Metadata protocol — Spurgeon Pulpit JSON (schema 1.1)

The contract every file in `volumes/` follows. One methodology produced all 63
volumes; this document defines the objects, fields, controlled vocabularies,
sorting rules and null rules that consumers can rely on. The *method* behind
the values is in [TAGGING.md](../TAGGING.md); provenance and defects are in
[BUILD_NOTES.md](../BUILD_NOTES.md).

## 1. Volume object (root of each file)

| Field | Type | Rule |
|---|---|---|
| `series` | string | Exactly `"New Park Street Pulpit"` (Vols. 1–6) or `"Metropolitan Tabernacle Pulpit"` (Vols. 7–63). |
| `volume` | int | Overall volume number, 1–63, continuous across both series. Always equals the number in the file name. |
| `volume_label` | string | As printed, e.g. `"Vol. VII"`. |
| `preaching_year` | int or string | Year (or range) the sermons in the volume were preached, from the title page. |
| `publication_year` | int \| null | `null` throughout schema 1.1: the re-typeset text base does not reproduce title pages, so no year is guessed. |
| `title` | string | Full title as printed for the series/volume. |
| `source` | object | See §2. |
| `tagging` | object | See §3. |
| `sermon_count` | int | Number of sermon records in `sermons`. Always `len(sermons)`. |
| `sermons` | array | Sermon objects (§4), ordered by published sermon number. |
| `full_text` | string | The whole volume's cleaned text, sermons in number order. |

## 2. `source` object

| Field | Type | Rule |
|---|---|---|
| `archive_identifier` / distributor id | string \| null | Identifier of the copy used, where the distributor provides one. |
| `item_url`, `text_url`, `pdf_url` | string \| null | Where the copy lives; the per-volume Spurgeon Gems PDF URL is always present. |
| `edition` | string | Edition note (AGES Collection re-typeset of Passmore & Alabaster). |
| `public_domain` | bool | `true` for every volume. |

## 3. `tagging` object (identical in every volume)

```json
{"schema_version": "1.1",
 "book_id_system": "Project canonical 66-book table (TAGGING.md): 3-letter codes, numeric prefix for numbered books",
 "cross_ref_sort": "canonical Bible order",
 "proper_noun_types": ["biblical_person", "historical_person", "place", "people_or_group", "other_name"]}
```

Any change to a field definition, vocabulary, or sort rule bumps
`schema_version` and is recorded here and in TAGGING.md — never silently.

## 4. Sermon object

| Field | Type | Rule |
|---|---|---|
| `sermon_number` | int | The published sermon number (1–3,563). Combined entries cover several numbers in one record (see `notes`); lettered sub-numbers share a number across two records (see `notes`). |
| `number_in_volume` | int | 1-based position of the record within its volume, in published order. |
| `title` | string | Sermon title as printed. |
| `scripture` | string \| null | The printed scripture reference line, or `null` when none is printed/parsed. |
| `delivered` | object | See §5. |
| `texts_taken` | array | The text(s) the sermon is preached from (§6). Empty only when no text could be identified from the heading or the volume's contents (1.2% of sermons). |
| `cross_references` | array | Explicit scripture citations in the sermon body (§7). May be empty — most quotations in Spurgeon are woven in without a formal citation. |
| `proper_nouns` | array | Extracted proper nouns (§8). May be empty. |
| `start_scan_page` | int \| null | Page within the sermon's own source PDF where the sermon starts (each sermon is paginated separately in the source PDFs). |
| `notes` | string \| null | Build and publication notes: combined/lettered numbers, supplied or reassembled text, source defects affecting this sermon. `null` when nothing needs flagging. |
| `text` | string | Cleaned full sermon text. Cleaning rules: BUILD_NOTES.md. |
| `_index_title` | string \| null | Title as given in the cross-check index, present on some records where it differs from the printed title. |

## 5. `delivered` object

| Field | Type | Rule |
|---|---|---|
| `date_as_printed` | string \| null | The delivery line's date exactly as printed, e.g. `"JUNE 2, 1889"`. |
| `date_iso` | string \| null | `YYYY-MM-DD` when a full date was printed and parsed; otherwise `null`. Never partially invented. |
| `year`, `month`, `day` | int \| null | Parsed components of `date_iso`. Filled only as far as the printed line supports; if only a year is known, `year` alone is set. |
| `occasion` | string \| null | Controlled forms as printed, e.g. `"Lord's-Day morning"`, `"Lord's-Day evening"`, `"Thursday evening"`. |
| `venue` | string \| null | As printed: `"New Park Street Chapel"`, `"Metropolitan Tabernacle"`, `"Exeter Hall"`, etc. |

## 6. `texts_taken` entries

One entry per text taken (normally exactly one).

| Field | Type | Rule |
|---|---|---|
| `reference_display` | string | Canonical form: full book name, arabic numerals — `"2 Timothy 3:5"`. |
| `reference_as_printed` | string | Exactly as printed in the heading — `"II Tim. 3:5"`, `"Psalm ciii. 1"`. When the heading could not be parsed, the volume contents/index form is recorded here instead (see TAGGING.md §1). |
| `book` | string | Canonical book name from the 66-book table. |
| `book_id` | string | 3-letter code from the same table, numeric prefix for numbered books (`2TI`, `1SA`). |
| `testament` | string | `"OT"` or `"NT"`. |
| `chapter` | int | Validated against the book's chapter count. |
| `verse_start`, `verse_end` | int \| null | `null` for whole-chapter texts. |
| `quote_as_printed` | string \| null | The verse wording printed under the heading; `null` when none is printed. |

## 7. `cross_references` entries

Explicit citations only — references actually printed in the body, extracted
against the canonical book table (abbreviations and roman-numeral chapters
included). Allusions are **not** references and are never entered.

Fields are the same as §6 minus `quote_as_printed`, plus:

| Field | Type | Rule |
|---|---|---|
| `occurrences` | int | How many times this normalized reference is cited in this sermon. |

**Deduplication & order:** one entry per normalized reference per sermon,
sorted in canonical Bible order (book order in the 66-book table, then
chapter, then verse) — identically in every volume.

## 8. `proper_nouns` entries

| Field | Type | Rule |
|---|---|---|
| `name` | string | Normalized citation form. Spelling variants of one name merge into a single entry only where identity is unambiguous. |
| `name_as_printed` | string | Most common printed form in this sermon. |
| `type` | string | One of the controlled set only: `biblical_person`, `historical_person`, `place`, `people_or_group`, `other_name`. Biblical figures are `biblical_person` even when also historical. |
| `occurrences` | int | Count within this sermon. |

**Order:** alphabetical by `name` within each sermon, in every volume.

## 9. Validation rules (checked across all 63 files)

- Every file parses as JSON; `sermon_count == len(sermons)`.
- Sermon numbers 1–3,563 are all covered after expanding combined entries;
  no unintended duplicates.
- Every `reference_display` parses back against the 66-book table; every
  `book_id` and `testament` comes from that table.
- `proper_nouns[].type` uses only the controlled set; cross-references are in
  canonical order; proper nouns are in alphabetical order.
- `null` means "not printed / not reliably extractable" — it never means zero,
  and no field is ever filled by guessing.
