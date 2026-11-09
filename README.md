# spurgeon-json

> JSON editions of Charles H. Spurgeon's published output, in three sections —
> the sermons from **New Park Street**, the sermons from the **Metropolitan Tabernacle**,
> and his monthly magazine, ***The Sword and the Trowel***.

| Section | Contents | Status |
|---|---|---|
| [New Park Street Pulpit](#new-park-street-pulpit--vols-16) | Vols. 1–6 · sermons preached 1855–1860 | ✅ Complete |
| [Metropolitan Tabernacle Pulpit](#metropolitan-tabernacle-pulpit--vols-763) | Vols. 7–63 · 1861–1917 | ✅ Complete |
| [The Sword and the Trowel](#the-sword-and-the-trowel--18651892) | Annual volumes 1865–1892 | 28 files · 6,479 articles |

**Pulpit totals: 63 volumes · 3,561 sermon records covering every published number,
No. 1 to No. 3,563 · 24,795,244 words.** All underlying works are public domain.

Every sermon carries, beside its cleaned full text: the **text taken** (the scripture
passage preached from, parsed and normalized — identified for 98.8% of sermons),
parsed **delivery date, occasion and venue** (full date for 91.2%), **cross-references**
in the body (1,715 distinct), and **proper nouns** (1,991 distinct) — one consistent
tagging protocol across the set: [TAGGING.md](TAGGING.md) ·
[docs/METADATA_PROTOCOL.md](docs/METADATA_PROTOCOL.md).

## Repository layout

```
.
├── README.md                       ← this landing page
├── LICENSE
├── TAGGING.md                      Tagging methodology (book table, cross-refs, proper nouns, dates)
├── BUILD_NOTES.md                  Pulpit set: sources, cleaning, defects and numbering quirks
├── docs/
│   ├── FOLDER_STRUCTURE.md         How this repository is organized
│   └── METADATA_PROTOCOL.md        Field-by-field schema/protocol (schema 1.1)
├── new-park-street-pulpit/         6 JSON files, one per volume (Vols. 1–6)
├── metropolitan-tabernacle-pulpit/ 57 JSON files, one per volume (Vols. 7–63)
└── sword-and-the-trowel/           The Sword and the Trowel, 1865–1892 (28 annual-volume JSONs)
```

## Quick start

```python
import json

vol = json.load(open("new-park-street-pulpit/new-park-street-pulpit-vol-01.json"))
first = vol["sermons"][0]
print(first["sermon_number"], first["title"])             # 1  The Immutability of God
print(first["texts_taken"][0]["reference_display"])        # Malachi 3:6
print(first["delivered"]["date_iso"], first["delivered"]["venue"])
```

Find every sermon preached from a given text, across both pulpit sections:

```python
import json, glob

def sermons_on(book_id, chapter):
    for path in glob.glob("new-park-street-pulpit/*.json") + glob.glob("metropolitan-tabernacle-pulpit/*.json"):
        for s in json.load(open(path))["sermons"]:
            for t in s["texts_taken"]:
                if t["book_id"] == book_id and t["chapter"] == chapter:
                    yield s["sermon_number"], s["title"]

list(sermons_on("2TI", 3))   # sermons on 2 Timothy 3, incl. No. 2088
```

## Sources & honesty notes

The pulpit text base is the Spurgeon Gems per-volume PDFs (AGES Collection re-typeset
of the Passmore & Alabaster volumes), spot-verified against Internet Archive scans.
IA OCR was inventoried but **not** used as the base — its heading OCR garbles sermon
numbers and many delivery lines are unreadable; the cleanest IA items are
lending-restricted. The re-typeset base presents the sermons in *lightly modernised
English* — a property of the source edition; this build modernised nothing further
and silently rewrote nothing. Supplied/reassembled sermons, duplicate printings and
all published numbering quirks (combined numbers, lettered sub-numbers) are itemised
in [BUILD_NOTES.md](BUILD_NOTES.md).

## New Park Street Pulpit — Vols. 1–6

| Vol. | Preached | Sermons | Nos. | Words | File |
|---|---|---|---|---|---|
| 1 | 1855 | 50 | 1–53 | 337,511 | [`new-park-street-pulpit-vol-01.json`](new-park-street-pulpit/new-park-street-pulpit-vol-01.json) |
| 2 | 1856 | 50 | 54–106 | 327,410 | [`new-park-street-pulpit-vol-02.json`](new-park-street-pulpit/new-park-street-pulpit-vol-02.json) |
| 3 | 1857 | 56 | 107–164 | 355,405 | [`new-park-street-pulpit-vol-03.json`](new-park-street-pulpit/new-park-street-pulpit-vol-03.json) |
| 4 | 1858 | 60 | 165–224 | 392,337 | [`new-park-street-pulpit-vol-04.json`](new-park-street-pulpit/new-park-street-pulpit-vol-04.json) |
| 5 | 1859 | 59 | 225–285 | 400,599 | [`new-park-street-pulpit-vol-05.json`](new-park-street-pulpit/new-park-street-pulpit-vol-05.json) |
| 6 | 1860 | 60 | 286–347 | 432,883 | [`new-park-street-pulpit-vol-06.json`](new-park-street-pulpit/new-park-street-pulpit-vol-06.json) |

## Metropolitan Tabernacle Pulpit — Vols. 7–63

| Vol. | Preached | Sermons | Nos. | Words | File |
|---|---|---|---|---|---|
| 7 | 1861 | 79 | 348–426 | 526,910 | [`metropolitan-tabernacle-pulpit-vol-07.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-07.json) |
| 8 | 1862 | 60 | 427–486 | 431,356 | [`metropolitan-tabernacle-pulpit-vol-08.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-08.json) |
| 9 | 1863 | 60 | 487–546 | 424,001 | [`metropolitan-tabernacle-pulpit-vol-09.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-09.json) |
| 10 | 1864 | 60 | 547–606 | 429,974 | [`metropolitan-tabernacle-pulpit-vol-10.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-10.json) |
| 11 | 1865 | 61 | 607–667 | 436,435 | [`metropolitan-tabernacle-pulpit-vol-11.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-11.json) |
| 12 | 1866 | 60 | 668–727 | 429,592 | [`metropolitan-tabernacle-pulpit-vol-12.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-12.json) |
| 13 | 1867 | 60 | 728–787 | 428,634 | [`metropolitan-tabernacle-pulpit-vol-13.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-13.json) |
| 14 | 1868 | 60 | 788–847 | 417,055 | [`metropolitan-tabernacle-pulpit-vol-14.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-14.json) |
| 15 | 1869 | 60 | 848–907 | 408,664 | [`metropolitan-tabernacle-pulpit-vol-15.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-15.json) |
| 16 | 1870 | 60 | 908–967 | 424,856 | [`metropolitan-tabernacle-pulpit-vol-16.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-16.json) |
| 17 | 1871 | 60 | 968–1027 | 430,512 | [`metropolitan-tabernacle-pulpit-vol-17.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-17.json) |
| 18 | 1872 | 61 | 1028–1088 | 436,562 | [`metropolitan-tabernacle-pulpit-vol-18.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-18.json) |
| 19 | 1873 | 61 | 1089–1149 | 424,262 | [`metropolitan-tabernacle-pulpit-vol-19.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-19.json) |
| 20 | 1874 | 60 | 1150–1209 | 424,165 | [`metropolitan-tabernacle-pulpit-vol-20.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-20.json) |
| 21 | 1875 | 61 | 1210–1270 | 425,681 | [`metropolitan-tabernacle-pulpit-vol-21.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-21.json) |
| 22 | 1876 | 60 | 1271–1330 | 432,570 | [`metropolitan-tabernacle-pulpit-vol-22.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-22.json) |
| 23 | 1877 | 60 | 1331–1390 | 433,104 | [`metropolitan-tabernacle-pulpit-vol-23.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-23.json) |
| 24 | 1878 | 60 | 1391–1450 | 439,738 | [`metropolitan-tabernacle-pulpit-vol-24.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-24.json) |
| 25 | 1879 | 69 | 1451–1510 | 433,092 | [`metropolitan-tabernacle-pulpit-vol-25.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-25.json) |
| 26 | 1880 | 64 | 1511–1574 | 434,915 | [`metropolitan-tabernacle-pulpit-vol-26.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-26.json) |
| 27 | 1881 | 63 | 1575–1636 | 440,226 | [`metropolitan-tabernacle-pulpit-vol-27.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-27.json) |
| 28 | 1882 | 61 | 1637–1697 | 436,385 | [`metropolitan-tabernacle-pulpit-vol-28.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-28.json) |
| 29 | 1883 | 59 | 1698–1756 | 433,605 | [`metropolitan-tabernacle-pulpit-vol-29.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-29.json) |
| 30 | 1884 | 59 | 1757–1815 | 422,824 | [`metropolitan-tabernacle-pulpit-vol-30.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-30.json) |
| 31 | 1885 | 61 | 1816–1876 | 423,010 | [`metropolitan-tabernacle-pulpit-vol-31.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-31.json) |
| 32 | 1886 | 61 | 1877–1937 | 427,064 | [`metropolitan-tabernacle-pulpit-vol-32.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-32.json) |
| 33 | 1887 | 63 | 1938–2000 | 437,941 | [`metropolitan-tabernacle-pulpit-vol-33.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-33.json) |
| 34 | 1888 | 61 | 2001–2061 | 424,491 | [`metropolitan-tabernacle-pulpit-vol-34.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-34.json) |
| 35 | 1889 | 59 | 2062–2120 | 409,479 | [`metropolitan-tabernacle-pulpit-vol-35.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-35.json) |
| 36 | 1890 | 61 | 2121–2181 | 420,203 | [`metropolitan-tabernacle-pulpit-vol-36.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-36.json) |
| 37 | 1891 | 55 | 2182–2236 | 394,115 | [`metropolitan-tabernacle-pulpit-vol-37.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-37.json) |
| 38 | 1892 | 52 | 2237–2288 | 365,264 | [`metropolitan-tabernacle-pulpit-vol-38.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-38.json) |
| 39 | 1893 | 53 | 2289–2341 | 378,143 | [`metropolitan-tabernacle-pulpit-vol-39.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-39.json) |
| 40 | 1894 | 52 | 2342–2393 | 374,405 | [`metropolitan-tabernacle-pulpit-vol-40.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-40.json) |
| 41 | 1895 | 52 | 2394–2445 | 368,409 | [`metropolitan-tabernacle-pulpit-vol-41.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-41.json) |
| 42 | 1896 | 52 | 2446–2497 | 375,315 | [`metropolitan-tabernacle-pulpit-vol-42.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-42.json) |
| 43 | 1897 | 52 | 2498–2549 | 380,311 | [`metropolitan-tabernacle-pulpit-vol-43.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-43.json) |
| 44 | 1898 | 53 | 2550–2602 | 369,095 | [`metropolitan-tabernacle-pulpit-vol-44.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-44.json) |
| 45 | 1899 | 53 | 2603–2655 | 381,034 | [`metropolitan-tabernacle-pulpit-vol-45.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-45.json) |
| 46 | 1900 | 52 | 2656–2707 | 364,282 | [`metropolitan-tabernacle-pulpit-vol-46.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-46.json) |
| 47 | 1901 | 52 | 2708–2759 | 366,142 | [`metropolitan-tabernacle-pulpit-vol-47.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-47.json) |
| 48 | 1902 | 52 | 2760–2811 | 366,178 | [`metropolitan-tabernacle-pulpit-vol-48.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-48.json) |
| 49 | 1903 | 52 | 2812–2863 | 366,227 | [`metropolitan-tabernacle-pulpit-vol-49.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-49.json) |
| 50 | 1904 | 52 | 2864–2915 | 367,101 | [`metropolitan-tabernacle-pulpit-vol-50.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-50.json) |
| 51 | 1905 | 52 | 2916–2967 | 368,702 | [`metropolitan-tabernacle-pulpit-vol-51.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-51.json) |
| 52 | 1906 | 52 | 2968–3019 | 363,085 | [`metropolitan-tabernacle-pulpit-vol-52.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-52.json) |
| 53 | 1907 | 53 | 3020–3072 | 363,393 | [`metropolitan-tabernacle-pulpit-vol-53.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-53.json) |
| 54 | 1908 | 52 | 3073–3124 | 361,416 | [`metropolitan-tabernacle-pulpit-vol-54.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-54.json) |
| 55 | 1909 | 53 | 3125–3177 | 367,440 | [`metropolitan-tabernacle-pulpit-vol-55.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-55.json) |
| 56 | 1910 | 53 | 3178–3230 | 356,634 | [`metropolitan-tabernacle-pulpit-vol-56.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-56.json) |
| 57 | 1911 | 52 | 3231–3282 | 341,440 | [`metropolitan-tabernacle-pulpit-vol-57.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-57.json) |
| 58 | 1912 | 52 | 3283–3334 | 344,414 | [`metropolitan-tabernacle-pulpit-vol-58.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-58.json) |
| 59 | 1913 | 52 | 3335–3386 | 347,519 | [`metropolitan-tabernacle-pulpit-vol-59.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-59.json) |
| 60 | 1914 | 53 | 3387–3439 | 358,971 | [`metropolitan-tabernacle-pulpit-vol-60.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-60.json) |
| 61 | 1915 | 53 | 3440–3492 | 353,506 | [`metropolitan-tabernacle-pulpit-vol-61.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-61.json) |
| 62 | 1916 | 52 | 3493–3544 | 338,778 | [`metropolitan-tabernacle-pulpit-vol-62.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-62.json) |
| 63 | 1917 | 19 | 3545–3563 | 120,474 | [`metropolitan-tabernacle-pulpit-vol-63.json`](metropolitan-tabernacle-pulpit/metropolitan-tabernacle-pulpit-vol-63.json) |

## The Sword and the Trowel — 1865–1892

Spurgeon's monthly magazine, edited by him from its founding in 1865 until his death
in January 1892. All 28 annual volumes of his era are here — one JSON file per
annual volume, split to individual articles with authors as printed: **6,479
article records, 10,824,332 words**, tagged with the same schema-1.1 methodology
as the Pulpit set. Sources: public-domain scans via Theology on the Web,
cross-checked against Internet Archive copies for 1866, 1867, 1882 and 1889.
The files live in [sword-and-the-trowel/](sword-and-the-trowel/); see that
folder's README for method, exclusions, per-year counts and the documented
defects (index anchoring thins toward 1892, its weakest volume).

## Citation

Spurgeon, C. H. *The New Park Street Pulpit* (Vols. 1–6), *The Metropolitan
Tabernacle Pulpit* (Vols. 7–63), Passmore & Alabaster, 1855–1917; *The Sword and
the Trowel*, 1865–1892. JSON edition: this repository, schema 1.1.
