# The Sword and the Trowel — Spurgeon-era annual volumes, 1865–1892 (JSON)

One JSON file per annual volume of C. H. Spurgeon's monthly magazine
*The Sword and the Trowel*, for the whole of Spurgeon's editorship:
`sword-and-the-trowel-1865.json` … `sword-and-the-trowel-1892.json`
(28 files, Vols. 1–28). Each volume is split into article records with
metadata, and also carries the cleaned full text of the year's issues
in order. This set parallels the Spurgeon Pulpit JSON set and reuses its
methods and tagging (see `TAGGING_NOTES.md`).

**Totals: 6,479 article records; 10,824,332 words of article text.**

## Contents of each file

```json
{
  "series": "The Sword and the Trowel",
  "year": 1865,
  "volume_label": "Vol. 1",
  "editor": "C. H. Spurgeon",
  "source": { "provider": "Theology on the Web (BiblicalStudies.org.uk)",
              "pdf_file": "...", "text_file": "...", "item_url": "...",
              "public_domain": true },
  "tagging": { ... schema 1.1 block, identical to the Pulpit set ... },
  "article_count": 189,
  "articles": [
    { "article_number": 1, "title": ..., "author": ...,
      "author_attribution": "signed|initials|pseudonym|unsigned|editorial",
      "month": "January", "department": null, "start_page": 1,
      "cross_references": [...], "proper_nouns": [...],
      "notes": ..., "text": "..." }
  ],
  "full_text": "..."
}
```

- `volume_label` follows the publisher's sequence (1865 = Vol. 1 …
  1892 = Vol. 28; the 1892 front matter itself refers to "Vols.
  I.–XXVIII"). The volume number is not printed on every year's title
  page, so treat the label as the publisher sequence, not a per-year
  transcription.
- `editor` is as printed. 1892's title page reads "Established and for
  27 years Edited by C. H. Spurgeon"; Spurgeon died on 31 January 1892
  and the rest of that volume was seen through the press by his circle;
  the 1892 file's `editor` field records exactly that.
- `start_page` is the magazine's own printed page, fitted from the
  running page numbers — never the PDF page.

## Source

Primary source for every year: the searchable PDF and extracted text
supplied by **Theology on the Web (BiblicalStudies.org.uk)**
(`biblicalstudies.gospelstudies.org.uk/pdf/sword-and-the-trowel/`),
public domain. The one notice sheet the site prepends to each PDF was
stripped before processing. Internet Archive copies were used as
cross-checks for four years during sourcing (identifiers in the table
below and in each file's `source.ia_cross_check`); the IA 1867 copy is
about 25% short and was never used as a text base.

## How the volumes were split

Article splits rest, in order of authority, on: (1) the volume's own
printed annual index (titles with printed start pages), anchored to
headings in the text; (2) the magazine's department headings (Reviews,
Notices, General Intelligence, Pastor's College, orphanage and fund
reports, etc.); (3) other printed headings not reached by the index.
Issue (month) boundaries rest on the printed mastheads. Where short
department material could not be split into items reliably, it is
grouped as one record per department section per month, and the record's
`notes` say so and list the indexed items the section contains.

Cleaning mirrors the Pulpit set: running headers and page-number lines
stripped, hyphenation rejoined, paragraphs rejoined, conservative OCR
fixes only where unambiguous, no modernization, no guessing. Titles,
authors and notes flag their own provenance wherever the printed
heading does not survive in the extracted text (title then comes from
the volume index, and `notes` say so).

## What is excluded from the article records

Front and back matter is not article content and is excluded from
`articles` (it is also absent from `full_text`, which covers the twelve
issues only): the title page, the publisher's page, the Preface, the
annual alphabetical index, the cumulative Index of Texts, advertisement
sheets, and the source site's prepended notice sheet. The volumes'
donation lists and £sd fund tables sit inside department sections
(orphanage/college reports) and are retained there as printed; their
OCR is the roughest in the set (see Defects).

## Per-year summary

"Index anchored" = printed-index entries matched to a heading in the
text, out of the index entries parsed for that year. It is a quality
signal, not a coverage figure: unanchored items are still present in
the text, inside neighbouring records or department groupings.

| Year | Volume | Articles | Words | Index anchored | IA cross-check |
|---|---|---|---|---|---|
| 1865 | Vol. 1 | 189 | 344,650 | 67/271 | — |
| 1866 | Vol. 2 | 149 | 352,751 | 55/219 | swordandtrowel00spurgoog |
| 1867 | Vol. 3 | 190 | 365,424 | 74/307 | swordandtrowele00tabegoog |
| 1868 | Vol. 4 | 247 | 363,305 | 56/348 | — |
| 1869 | Vol. 5 | 191 | 358,877 | 32/241 | — |
| 1870 | Vol. 6 | 209 | 366,851 | 17/246 | — |
| 1871 | Vol. 7 | 267 | 353,841 | 73/354 | — |
| 1872 | Vol. 8 | 253 | 360,059 | 59/404 | — |
| 1873 | Vol. 9 | 208 | 349,502 | 59/302 | — |
| 1874 | Vol. 10 | 216 | 366,299 | 62/403 | — |
| 1875 | Vol. 11 | 222 | 360,127 | 57/358 | — |
| 1876 | Vol. 12 | 237 | 352,151 | 61/393 | — |
| 1877 | Vol. 13 | 218 | 364,916 | 67/388 | — |
| 1878 | Vol. 14 | 283 | 375,657 | 62/377 | — |
| 1879 | Vol. 15 | 209 | 378,101 | 56/115 | — |
| 1880 | Vol. 16 | 260 | 408,722 | 76/113 | — |
| 1881 | Vol. 17 | 218 | 402,733 | 55/126 | — |
| 1882 | Vol. 18 | 200 | 404,777 | 46/96 | swordandtrowela00spurgoog |
| 1883 | Vol. 19 | 216 | 416,054 | 34/69 | — |
| 1884 | Vol. 20 | 244 | 413,389 | 60/135 | — |
| 1885 | Vol. 21 | 189 | 415,654 | 20/55 | — |
| 1886 | Vol. 22 | 287 | 414,803 | 17/65 | — |
| 1887 | Vol. 23 | 218 | 416,197 | 35/83 | — |
| 1888 | Vol. 24 | 279 | 414,813 | 23/93 | — |
| 1889 | Vol. 25 | 250 | 422,334 | 25/63 | swordtrowel25spur |
| 1890 | Vol. 26 | 222 | 423,468 | 11/31 | — |
| 1891 | Vol. 27 | 275 | 420,771 | 24/57 | — |
| 1892 | Vol. 28 | 333 | 438,106 | 3/17 | — |

## Verification

All 28 files were machine-verified after the build: valid JSON; exact
schema fields on every record; sequential article numbering;
`article_count` consistent; every cross-reference parses against the
canonical 66-book table (3,906 reference entries in total); every
proper noun carries one of the five controlled types (34,013 entries).
Article splits were spot-checked against the printed month-by-month
contents for five years spread across the run (1865, 1872, 1880, 1882,
1892). For 1865 the per-month record counts track the contents counts
(164 items) closely, with extra records where the magazine prints
sub-headed sections the contents list treats as one item. For 1892 see
the defects below.

## Defects and gaps — read before citing

- **OCR quality varies and declines in the later volumes.** Prose is
  generally clean; headings, display type and tables garble. Titles
  taken from a volume's index inherit that index's OCR noise.
- **The annual index parses well in early volumes and poorly in late
  ones.** From about 1885 the printed indexes are denser and their OCR
  worse, so fewer entries could be anchored (see the table) and more
  splits rest on headings alone. In **1892** the index yielded only 17
  usable entries; that volume's splits rest almost entirely on printed
  headings and are finer than the contents-list item count (333 records
  against roughly 250 contents items), because centred sub-headings
  inside long pieces (notably the Pastors' College conference
  proceedings and the annual reports in the June issue) become records
  of their own. Treat 1892's article boundaries as approximate.
- **Month attribution is reliable but not perfect.** All twelve issue
  starts were located in every year (worst-case spacing checked). A few
  mastheads survive only as illustration pages or garbled display type;
  those boundaries were fixed from the printed pagination and page
  character and can be a few pages out. Months so fixed: 1873 March;
  1874 May; 1876 September; 1879 June; 1880 June and December; 1881 May,
  November and December; 1883 May and June; 1884 June and July; 1885
  June and July; 1886 June and July; 1887 November; 1888 March and
  September; 1890 July; 1892 February and June. 1873's masthead years
  OCR as "1878"/"1872" — a print-reading artefact of that volume.
- **Nine volumes' page chains start at printed page 3** (1866, 1867,
  1874, 1875, 1880, 1883, 1887, 1888, 1889): in those scans the first
  leaf of the January issue (printed pp. 1–2) is either absent or
  counted in the chain before the first surviving folio, so `start_page`
  values are internally consistent but begin at 3. Nothing else is
  missing: the January text is present from the first scanned page.
- **`start_page` is least reliable in 1887 and 1889**, where the fitted
  pagination chain breaks most often; a minority of records there carry
  a start page a leaf or two off, and in a few stretches the sequence
  of start pages is not monotonic (101 and 111 records affected,
  respectively, out of 218 and 250).
- **The two one-page tracts printed in each early issue** (from 1865)
  have no headings of their own in the text; where the index anchors
  fail they are absorbed into the preceding article's record.
- **Donation lists and £sd tables** (Stockwell Orphanage, Pastor's
  College, funds) are the worst OCR in the set: names and figures there
  should not be quoted without checking the PDF.
- Post-1892 volumes (1893–1904) exist at the same source but are
  outside the Spurgeon era and outside this set.

## Files

- `sword-and-the-trowel-YYYY.json` — the 28 annual volumes.
- `TAGGING_NOTES.md` — how the tagging relates to the Spurgeon Pulpit
  set (identical) and the periodical-specific fields.
- Build and verification scripts, the source inventory, and the full
  build report are kept with the working files in
  `~/workspace/research_notes/sword-and-trowel-build/`
  (`build_sword_trowel.py`, `verify_sword_trowel.py`, `INVENTORY.md`,
  `build_report.json`).
