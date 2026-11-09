# Tagging notes — The Sword and the Trowel (1865–1892)

## Tagging is identical to the Spurgeon Pulpit set

The `cross_references` and `proper_nouns` tagging in these volumes uses
exactly the same methodology as the Spurgeon Pulpit JSON set
(`spurgeon-pulpit-json`, schema 1.1), implemented by the same code:

- **One canonical 66-book Bible table** with the same `book_id`s, in
  canonical Bible order. Every cross-reference entry has the same shape:
  `book_id`, `book`, `chapter`, `verse_start`, `verse_end`, optional
  `chapter_end`, `page_or_section`, and the `text` span as printed.
- **Same reference-parsing rules**: ranges, chapter-only references,
  multi-reference lists, "Psalm" numbering, roman-numeral chapters, and
  the same conservative treatment of ambiguous forms. A reference is only
  recorded when it can be resolved against the book table.
- **Proper nouns** use the same five controlled types and no others:
  `biblical_person`, `historical_person`, `place`, `people_or_group`,
  `other_name` — with the same entry shape (`name`, `type`,
  `occurrences`).
- The `tagging` block embedded in each volume file is the Pulpit set's
  schema-1.1 block, unchanged.

See `TAGGING.md` in the Spurgeon Pulpit set (or the copy of the tagging
documentation kept with that set) for the full methodology statement.

## Periodical-specific fields (not part of tagging)

A monthly magazine needs fields a sermon volume does not. These are
article metadata, not text tagging:

- `month` — the issue the article appeared in, from the issue masthead.
- `department` — the magazine's own section heading where one governs the
  item (Reviews, Notices, General Intelligence, Pastor's College, etc.);
  short department material is grouped one record per department section
  per month rather than split into fabricated items, and the record's
  `notes` say so.
- `author` / `author_attribution` — a periodical has many contributors.
  `author` is the name exactly as printed (byline or signature); it is
  never guessed. `author_attribution` classifies what is printed:
  `signed` (a name, including initials + surname), `initials` (initials
  only, no surname), `pseudonym`, `unsigned` (nothing printed), and
  `editorial` (unsigned opening/editorial matter). Where the byline is
  missing from the extracted text but the volume's own index author list
  names the author of an item on that page, the author is supplied from
  the index and the record's `notes` say so.
- `start_page` — the printed page (the magazine's own pagination, fitted
  from the running page numbers), not the PDF page.
- `title` — the printed heading where one survives in the text. Where a
  heading does not survive in the extracted text (a recurring OCR/layout
  artefact of this source), the title is taken from the volume's own
  printed index and `notes` say so; where neither exists, `title` is null.
