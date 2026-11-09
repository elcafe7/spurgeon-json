# The Spurgeon Pulpit — complete set, one JSON per volume

Charles H. Spurgeon's published sermons: the **New Park Street Pulpit**
(Vols. 1–6, sermons preached 1855–1860) and the **Metropolitan Tabernacle
Pulpit** (Vols. 7–63, 1861–1917, the later volumes posthumous). All
volumes are public domain.

**Totals: 63 volumes · 3,561 sermon records covering every published
sermon number from No. 1 to No. 3,563 · 24,795,244 words.**

## Contents of each file

One JSON object per volume:

- `series`, `volume`, `volume_label`, `preaching_year`, `publication_year`
  (null — see TAGGING.md §5), `title`, `source` (identifier/URLs, edition
  note, `public_domain: true`), `tagging` (schema block, see TAGGING.md),
  `sermon_count`, `sermons`, `full_text` (the whole volume, sermons in
  number order).
- Each sermon: `sermon_number`, `number_in_volume`, `title`, `scripture`
  (printed reference line or null), `delivered` {date_as_printed,
  date_iso, year, month, day, occasion, venue}, `texts_taken` (the text
  preached from, parsed — TAGGING.md §1), `cross_references` (explicit
  citations in the body, canonical Bible order — §3), `proper_nouns`
  (controlled types — §4), `start_scan_page`, `notes`, `text` (cleaned
  full text).
- `start_scan_page`: for this text base, each sermon is paginated
  separately in its source PDF, so the value is the PDF page where the
  sermon starts within its source file; the sermon's own printed pages
  restart at 1. (The Internet Archive djvu texts consulted contain no
  form feeds, so scan-page marking was only possible for the PDF base.)

## Sources — read this before citing the texts

**Text base (all 63 volumes): the Spurgeon Gems per-volume PDFs**
(`http://www.spurgeongems.org/chsbm<N>.pdf`, unpadded N), a clean
re-typeset text of the Passmore & Alabaster volumes (the AGES Spurgeon
Collection lineage), extracted with `pdftotext -layout`. Per volume the
JSON `source` block gives that volume's URL.

Why this base, and what else was checked:

- Internet Archive was inventoried first. Open full texts exist for the
  Classic Christian Library re-typeset compilations (Vols. 1–15, 19, 28)
  and for printed-volume scans of Vols. 18, 21, 22, 30, 32, 34, 36; the
  `metropolitantabeNNNNchsp` items for most later volumes are
  lending-restricted (their djvu.txt returns HTTP 401). All of those
  texts were downloaded and are kept with the build files.
- The IA texts were **not** used as the base: heading OCR in the CCL
  files garbles sermon numbers (`611` read as `6n`), making reliable
  segmentation impossible for several volumes, and in the scans the
  title headings of 42 of 61 sermons in Vols. 21 and 36 could not be
  located at all, with most delivery lines unreadable. The Gems text was
  spot-verified against the scans (e.g. sermon No. 1800 in both the Vol.
  30 scan and the Gems text: same sermon, 72% shared 8-word sequences,
  the differences being scan OCR error).
- Three sermons are missing or garbled in their Gems volume PDFs and are
  supplied from the same AGES collection text via another distributor,
  flagged in each sermon's `notes`: No. 1331 (Vol. 23, via SermonIndex,
  heading restored as printed), No. 1218 (Vol. 21, Gems-format single
  sermon via ccbiblestudy.net), No. 1589 (Vol. 27, same route). No. 696
  (Vol. 12) is split around No. 697 inside its PDF; its own pages were
  reassembled in printed order (build script `make_supp_696.py`).

## Cleaning applied

- Running page headers/footers, standalone page numbers, and the
  per-sermon promotional tail of the source PDFs ("Adapted from The
  C. H. Spurgeon Collection… / PRAY THE HOLY SPIRIT WILL USE THIS
  SERMON…") are stripped; scan advertising is absent from this base.
- Words hyphenated across line breaks are rejoined; lines are rejoined
  into paragraphs; excess blank lines collapsed.
- Spelling, punctuation, capitalisation and Bible wording are **not**
  modernised by this build (the re-typeset base itself presents the
  sermons in lightly modernised English — that is a property of the
  source edition, stated here plainly). Doubtful readings are kept as
  they stand; nothing is silently rewritten.
- Sermon structure is preserved: title, number, delivery line, scripture
  quotation and reference, body, and the closing "Portion of Scripture
  Read Before Sermon" / hymn lines as printed.

## Numbering — the published quirks, documented not hidden

Verification (script kept with the build files) confirms: all 63 files
valid JSON; sermon numbers 1–3,563 all covered; no unintended
duplicates. The count of records (3,561) differs from the count of
numbers (3,563) because of the original publication's own habits:

- **Combined entries:** some weekly numbers were published as one sermon
  covering two or three numbers (e.g. Nos. 7–8, 61–62, 268–270). These
  are single records whose `notes` state the combination.
- **Lettered sub-numbers:** some numbers carry two pieces (e.g. 1451A/B,
  1634 + "Loved and Loving", 369 + the 369A opening address). These are
  separate records sharing `sermon_number`, flagged in `notes`.
- **Vol. 5, No. 268–270** is not a sermon but the printed report of the
  ceremony of laying the first stone of the new Tabernacle (16 Aug.
  1859), published in place of those numbers; it is included, flagged.
- **Index disagreements:** the archive.spurgeon.org index (used as a
  cross-check) skips Nos. 2709, 3028 and 3471 that are present in the
  volumes, splits No. 3237 into two phantom entries, and stops Vol. 63
  at No. 3561; the volumes themselves contain 3,562 and 3,563, and the
  set ends at No. 3,563 as published.

## Source-PDF defects found and handled (per volume)

Duplicate printings of the same sermon inside one PDF were dropped
(keeping the in-sequence, or if one copy is a one-page preview fragment,
the full printing); stray sermons from other volumes inserted into two
PDFs were dropped; sermons printed out of sequence were placed in number
order; two sermons' final pages stranded at the end of their PDFs were
reattached. Details per volume:

| Vol. | Sermons | Numbers | Words | Source-PDF handling |
|---|---|---|---|---|
| 1 | 50 | 1–53 | 337,511 |  |
| 2 | 50 | 54–106 | 327,410 |  |
| 3 | 56 | 107–164 | 355,405 |  |
| 4 | 60 | 165–224 | 392,337 |  |
| 5 | 59 | 225–285 | 400,599 |  |
| 6 | 60 | 286–347 | 432,883 |  |
| 7 | 79 | 348–426 | 526,910 |  |
| 8 | 60 | 427–486 | 431,356 |  |
| 9 | 60 | 487–546 | 424,001 |  |
| 10 | 60 | 547–606 | 429,974 |  |
| 11 | 61 | 607–667 | 436,435 |  |
| 12 | 60 | 668–727 | 429,592 | duplicate/fragment printing(s) dropped: [696, 696] |
| 13 | 60 | 728–787 | 428,634 |  |
| 14 | 60 | 788–847 | 417,055 |  |
| 15 | 60 | 848–907 | 408,664 |  |
| 16 | 60 | 908–967 | 424,856 |  |
| 17 | 60 | 968–1027 | 430,512 |  |
| 18 | 61 | 1028–1088 | 436,562 |  |
| 19 | 61 | 1089–1149 | 424,262 |  |
| 20 | 60 | 1150–1209 | 424,165 |  |
| 21 | 61 | 1210–1270 | 425,681 |  |
| 22 | 60 | 1271–1330 | 432,570 |  |
| 23 | 60 | 1331–1390 | 433,104 |  |
| 24 | 60 | 1391–1450 | 439,738 |  |
| 25 | 69 | 1451–1510 | 433,092 |  |
| 26 | 64 | 1511–1574 | 434,915 |  |
| 27 | 63 | 1575–1636 | 440,226 |  |
| 28 | 61 | 1637–1697 | 436,385 |  |
| 29 | 59 | 1698–1756 | 433,605 |  |
| 30 | 59 | 1757–1815 | 422,824 |  |
| 31 | 61 | 1816–1876 | 423,010 |  |
| 32 | 61 | 1877–1937 | 427,064 |  |
| 33 | 63 | 1938–2000 | 437,941 |  |
| 34 | 61 | 2001–2061 | 424,491 |  |
| 35 | 59 | 2062–2120 | 409,479 |  |
| 36 | 61 | 2121–2181 | 420,203 |  |
| 37 | 55 | 2182–2236 | 394,115 |  |
| 38 | 52 | 2237–2288 | 365,264 |  |
| 39 | 53 | 2289–2341 | 378,143 |  |
| 40 | 52 | 2342–2393 | 374,405 |  |
| 41 | 52 | 2394–2445 | 368,409 |  |
| 42 | 52 | 2446–2497 | 375,315 |  |
| 43 | 52 | 2498–2549 | 380,311 |  |
| 44 | 53 | 2550–2602 | 369,095 |  |
| 45 | 53 | 2603–2655 | 381,034 |  |
| 46 | 52 | 2656–2707 | 364,282 |  |
| 47 | 52 | 2708–2759 | 366,142 |  |
| 48 | 52 | 2760–2811 | 366,178 |  |
| 49 | 52 | 2812–2863 | 366,227 |  |
| 50 | 52 | 2864–2915 | 367,101 |  |
| 51 | 52 | 2916–2967 | 368,702 |  |
| 52 | 52 | 2968–3019 | 363,085 |  |
| 53 | 53 | 3020–3072 | 363,393 |  |
| 54 | 52 | 3073–3124 | 361,416 |  |
| 55 | 53 | 3125–3177 | 367,440 |  |
| 56 | 53 | 3178–3230 | 356,634 |  |
| 57 | 52 | 3231–3282 | 341,440 |  |
| 58 | 52 | 3283–3334 | 344,414 |  |
| 59 | 52 | 3335–3386 | 347,519 |  |
| 60 | 53 | 3387–3439 | 358,971 |  |
| 61 | 53 | 3440–3492 | 353,506 |  |
| 62 | 52 | 3493–3544 | 338,778 |  |
| 63 | 19 | 3545–3563 | 120,474 |  |

## Tagging coverage

- Texts taken identified: 3,520 / 3,561 sermons (98.8%).
- Delivered dates parsed to a full ISO date: 3,247 / 3,561 (91.2%).
- Distinct cross-references indexed: 1,715. Distinct proper nouns: 1,991.
- Method: see **TAGGING.md**. Every cross-reference `reference_display`
  in the set was machine-checked to parse back against the book table;
  every proper-noun entry uses only the five controlled types.

## Rebuilding

Working files (source PDFs/texts, scripts, reports) are in
`~/workspace/research_notes/spurgeon-pulpit-build/`:
`build_spurgeon.py` (build), `tagging.py` (shared tagging),
`verify_spurgeon.py` (verification), `make_supp_1331.py`,
`make_supp_696.py`, `download_all.sh`, `sources/` (incl. `sources/gems/`),
`build_report.json`, `verify_report.json`.
