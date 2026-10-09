# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Not a code project — a data repository. `Piesne/` holds ~1320 Slovak church songs (hymnbook "JKS", related sets, and the ejks.sk import) exported from **OpenLP 3.1.7** as one XML file per song. There is no build, lint, or test tooling and no README. All content is Slovak with diacritics; filenames contain spaces, commas, parentheses and non-ASCII characters, so always quote paths (and use `./*.xml` or `--` in shell globs in case a name starts with `-`).

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

- **"Authors" double as tags/categories.** The `<author>` list mixes real attribution (`JKS`, `Anonymous`, `Author Unknown`) with liturgical-season/usage labels (`Advent`, `Vianočná`, `Veľkonočná`, `Pôstna`, `Adorácia`, `Prijímanie`, `Obetné dary`, `Taize`, `detsky zbor`, `akordy`, …). The filename's trailing `(…)` is that same author/tag list joined by `, `.
- **Filename = `<title>` + ` (<authors>)`.** Numbered songs carry the hymnbook number in the title itself (`001 Ó, prekrásna Hviezda ranná`); numbering is inconsistent (`002.` vs `001 ` vs `026 `). Some songs have two `<title>`s (number, then name), e.g. `365 (JKS).xml`. A few use `<songbooks>` (e.g. `Ž 1 (JKS).xml` → "Kurima Žalmy").
- **`JKS3` tag = imported from ejks.sk (formerly tagged `eJKS`).** 339 files named `NNN. Názov (JKS3).xml` (author `JKS3` only, no `JKS`) were generated from the sources of https://ejks.sk (GitHub `stanislavbebej/ejks`, `hugo/content/piesne/*.md`, GPL-3.0; numbers 1–526 with gaps). Each numbered verse became one `<verse name="vN">` with the number stripped and the site's ` - ` line separators turned into `<br/>`; no `verseOrder`, no chords. They are deliberately separate from the older `(JKS…)` songs with the same hymnbook number, whose text may differ, so these are *not* duplicates to remove. The local download of the ejks repo (`eJKS/`) is not part of the data and must not be committed.
- **`JKS1` / `JKS2` tags = further imports of the same hymnbook from other sources.** Files `NNN. Názov (JKS1).xml` (444 songs, from spevnik.github.io) and `NNN. Názov (JKS2).xml` (525 songs, from http://www.nws.sk/ssv/JKS/, a scan of the printed book) carry author `JKS1` / `JKS2` only. Both are OCR-derived, so they contain residual typos and keep the book's archaic spellings (`přesvatý`, `dietky`, `preslávny`…); like JKS3 they are deliberately separate from the `(JKS…)` songs with the same number and are *not* duplicates to remove. In JKS2, songs printed in several variants carry a letter suffix in the number (`223a`/`223b`, `302a`/`302b`, `408a`–`c`, `409a`–`c`, `436`/`436b`, `484a`/`484b`); verses have the printed number stripped and are named `v1…vN`, repeat marks are kept as `[:` … `:]`, and in-text section labels (`Glória:`, `Krédo:`, `Ofertórium:`…) are the first line of the verse they introduce. Stub entries without lyrics (304, 305, 307, 309, 310, 313, 315, 527+) were skipped.
- **Duplicates were cleaned up; keep it that way.** The repo was deduplicated in several passes (see git history): all `-1`/`-2` copies (OpenLP appends these when title+authors collide) are gone, as are `(Author Unknown)` copies of `(detsky zbor)` songs and a few same-lyrics pairs under different titles/tags. Where variants differed, the fuller / better-split version was kept (usually with verse headers stripped of the hymnbook number). A fresh OpenLP export will recreate `-N` files, so compare them against the existing file before adding. Known remaining near-duplicates, kept deliberately: 35 children's-choir songs that exist both as a chord version tagged `akordy` (e.g. `Davaj pozor (akordy).xml`, or `… (MlaKa, akordy).xml` when there is a real author) and as a plain `(detsky zbor)` copy without chords (the chord versions sometimes carry in-text performance notes like `medzihra` that would show on slides, or differ slightly in wording), and songs sharing a title but with different lyrics across tag sets (e.g. `040. Čas radosti, veselosti (JKS)` vs `(JKS, Vianočná)`). Before editing a song, check for sibling files with the same title and keep them in sync. `duplicity.csv` in the repo root is a snapshot taken before the cleanup and is now obsolete. `duplicity.md` is the current review (Slovak): a checklist of remaining same-lyrics groups found by normalized-text comparison (most involve a `detsky zbor` copy), with a suggested keeper per group and open decisions; tick items off there as they are resolved.
- **Verse names** follow OpenLyrics: `v1…` verse, `c`/`c1` chorus, `b` bridge, `o` other, `e` ending; variants like `va`/`vb`/`vc` and `cb` also occur (~60 files use `va`/`vb`). `verseOrder` is only present in ~200 files; without it, verses play in document order.
- **Lyrics are literal text inside `<lines>`.** Line breaks are `<br/>`; entities (`&gt;`, `&amp;`) are escaped. Hymnbook verses start with a number and a long run of spaces, then a trailing marker (`1.      …   1.<br/>`) used for layout on slides — leave that whitespace intact.
- **Chords** (~1400 occurrences, only in a handful of files, mostly Taizé/praise songs) are inline `<chord name="Cmaj7"/>` elements placed mid-word, directly before the syllable they sit on. Don't strip or reflow them when changing lyrics. Inline directives like `[=>E]` (transpose/ending markers) may appear in lyric text. The `akordy` author tag marks chord versions of songs that also have a plain copy; keep both in sync when changing lyrics.
- Rare elements: `<copyright>`, `<ccliNo>`.

## Working with the data

- Use Grep/Glob for bulk questions; the corpus is plain text. XML-aware processing (Python `xml.etree`/`lxml`) is fine for read-only analysis, but write changes back as targeted text edits.
- `.gitattributes` sets `* text=auto`, so on Windows checkouts line endings are normalized by git; files in the working tree currently have LF.
- Do not rename files casually: the filename is derived from title + authors by OpenLP on export, so keep the `<title>`/`<author>` content and the filename consistent when you change one.
