# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Not a code project — a data repository. `Piesne/` holds ~1550 Slovak church songs (hymnbook "JKS" and related sets) exported from **OpenLP 3.1.7** as one XML file per song. There is no build, lint, or test tooling and no README. All content is Slovak with diacritics; filenames contain spaces, commas, parentheses and non-ASCII characters, so always quote paths (and use `./*.xml` or `--` in shell globs, since some names start with `-`, e.g. `-NIČ (...).xml`).

The files are re-exported wholesale from OpenLP (all `modifiedDate` values are the same export timestamp), so the XML is machine-generated. Preserve the exported format (UTF-8, LF, 2-space indent, single-quoted XML declaration) when editing by hand, and never "pretty print" or re-serialize files with tools that change this — it would produce huge noisy diffs.

## File format (OpenLyrics 0.8)

Namespace `http://openlyrics.info/namespace/2009/song`. Typical shape:

```xml
<song xmlns="…" version="0.8" createdIn="OpenLP 3.1.7" modifiedIn="OpenLP 3.1.7" modifiedDate="…">
  <properties>
    <titles><title>…</title></titles>        <!-- sometimes 2 titles: number + name -->
    <authors><author>JKS</author><author>Advent</author></authors>
    <songbooks><songbook name="…"/></songbooks>   <!-- optional -->
    <verseOrder>v1 c1 v2 c1</verseOrder>          <!-- optional -->
  </properties>
  <lyrics>
    <verse name="v1"><lines>line<br/>line<br/>line</lines></verse>
  </lyrics>
</song>
```

Things that aren't obvious from a single file:

- **"Authors" double as tags/categories.** The `<author>` list mixes real attribution (`JKS`, `Anonymous`, `Author Unknown`) with liturgical-season/usage labels (`Advent`, `Vianočná`, `Veľkonočná`, `Pôstna`, `Adorácia`, `Prijímanie`, `Obetné dary`, `Taize`, `detsky zbor`, …). The filename's trailing `(…)` is that same author/tag list joined by `, `.
- **Filename = `<title>` + ` (<authors>)`.** Numbered songs carry the hymnbook number in the title itself (`001 Ó, prekrásna Hviezda ranná`); numbering is inconsistent (`002.` vs `001 ` vs `026 `). Some songs have two `<title>`s (number, then name), e.g. `365 (JKS).xml`. A few use `<songbooks>` (e.g. `Ž 1 (JKS).xml` → "Kurima Žalmy").
- **Duplicates are expected.** OpenLP appends `-1`, `-2`, … when title+authors collide. The 474 byte-identical `-N` copies were deleted (still in git history, commit `99985cc`), but a fresh OpenLP export will recreate them. Remaining `-N` files are real variants: ~19 differ only in `<author>` order, a few split verses differently (e.g. `Agnus Dei (Baránok Boží)-1.xml`), ~10 have different text. Also ~80 songs exist under different tag sets with identical lyrics (e.g. `X (Author Unknown).xml` and `X (detsky zbor).xml`) and ~50 titles have different lyrics across files. Before editing a song, check for sibling files and keep them in sync (or ask whether to dedupe). `duplicity.csv` in the repo root is a pre-cleanup report; its group-A rows are now obsolete.
- **Verse names** follow OpenLyrics: `v1…` verse, `c`/`c1` chorus, `b` bridge, `o` other, `e` ending; variants like `va`/`vb`/`vc` and `cb` also occur (~60 files use `va`/`vb`). `verseOrder` is only present in ~200 files; without it, verses play in document order.
- **Lyrics are literal text inside `<lines>`.** Line breaks are `<br/>`; entities (`&gt;`, `&amp;`) are escaped. Hymnbook verses start with a number and a long run of spaces, then a trailing marker (`1.      …   1.<br/>`) used for layout on slides — leave that whitespace intact.
- **Chords** (~1400 occurrences, only in a handful of files, mostly Taizé/praise songs) are inline `<chord name="Cmaj7"/>` elements placed mid-word, directly before the syllable they sit on. Don't strip or reflow them when changing lyrics. Inline directives like `[=>E]` (transpose/ending markers) may appear in lyric text.
- Rare elements: `<copyright>`, `<ccliNo>`.

## Working with the data

- Use Grep/Glob for bulk questions; the corpus is plain text. XML-aware processing (Python `xml.etree`/`lxml`) is fine for read-only analysis, but write changes back as targeted text edits.
- `.gitattributes` sets `* text=auto`, so on Windows checkouts line endings are normalized by git; files in the working tree currently have LF.
- Do not rename files casually: the filename is derived from title + authors by OpenLP on export, so keep the `<title>`/`<author>` content and the filename consistent when you change one.
