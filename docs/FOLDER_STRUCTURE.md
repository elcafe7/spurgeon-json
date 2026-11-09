# Folder structure

How this repository is organized, and the rules that keep it that way.

```
spurgeon-json/
├── README.md                       Landing page: the three sections, quick start, full pulpit index
├── LICENSE
├── TAGGING.md                      Tagging methodology (schema 1.1)
├── BUILD_NOTES.md                  Pulpit set provenance: sources, cleaning, defects, numbering quirks
├── docs/
│   ├── FOLDER_STRUCTURE.md         This file
│   └── METADATA_PROTOCOL.md        Field-by-field metadata protocol
├── new-park-street-pulpit/         SECTION 1 — New Park Street Pulpit JSON (Vols. 1–6)
│   └── new-park-street-pulpit-vol-<NN>.json   one file per volume
├── metropolitan-tabernacle-pulpit/ SECTION 2 — Metropolitan Tabernacle Pulpit JSON (Vols. 7–63)
│   └── metropolitan-tabernacle-pulpit-vol-<NN>.json   one file per volume
└── sword-and-the-trowel/           SECTION 3 — The Sword and the Trowel (1865–1892)
    ├── README.md                   Section status and sourcing
    └── sword-and-the-trowel-<YYYY>.json   one file per annual volume (landing as built)
```

## Rules

1. **Each work gets its own section folder.** Nothing is mixed across sections;
   a file lives in exactly one section.
2. **One volume, one file.** Each published volume is exactly one JSON file in
   its section folder — never merged, split, or partially duplicated.
3. **File naming is fixed.** Pulpit: `<series-slug>-vol-<NN>.json` with `<NN>`
   the overall volume number zero-padded (01–63); the number in the file name
   always equals the `volume` field inside the file. Sword and the Trowel:
   `sword-and-the-trowel-<YYYY>.json` with `<YYYY>` the annual volume's year,
   equal to the `year` field inside.
4. **Documentation stays at the root and in `docs/`.** No notes, scripts, or
   working files inside the section folders; build scripts and raw sources
   are kept outside this repository.
5. **Root files have single jobs:** `README.md` introduces and indexes;
   `TAGGING.md` defines how metadata was produced; `BUILD_NOTES.md` records
   pulpit provenance and defects; `docs/` defines structure and protocol.
   Update the doc that owns the fact, not all of them.
