# sign-symbol — AI working notes

Reading notes and source citations for Chapter 85 ("Sign and Symbol") of the
*Great Books of the Western World Syntopicon* (Adler, 1952). See
[README.md](README.md) for the human-facing table of contents; this file is
for an agent that needs to work with the repo's structure or content directly.

## Branches — pick the right one

| Branch | Format | Use for |
|---|---|---|
| `main` | PDF (most sections) + `.docx` (4d, 5a–6c) | Preserving original formatting/layout |
| `plain-text` | Everything as `.txt`, PDF/docx removed | Grepping, diffing, quoting, any text-processing task |
| `markdown` | Everything as `.md`, real `#`/`##`/`###` headers, linked citation index | Reading on GitHub, human navigation |

Default to `plain-text` for anything that involves reading or searching
content — it's the same text, already extracted, no PDF/docx parsing needed.

## Structure

One folder per outline sub-topic, named `<code> <title>` (title sometimes
omitted or truncated — folder names are **not** reliable topic labels, see
gotchas below). Full code → title mapping:

| Code | Title | Present? |
|---|---|---|
| 1a | The distinction between natural and conventional signs | yes |
| 1b | The intentions of the mind: ideas and images as natural signs | yes |
| 1c | The things of nature functioning symbolically: the book of nature | yes |
| 1d | The conventional notations of human language: man's need for words | yes (folder misnamed, see below) |
| 1e | The invention of non-verbal symbols: money, titles, seals, ceremonies, courtesies | yes |
| 1f | Natural signs as the source of meaning in conventional signs | yes |
| 2a | The first and second imposition of words | yes |
| 2b | The first and second intention of names | yes |
| 2c | Intrinsic and extrinsic denominations | yes |
| 2d | Proper and common names | yes |
| 2e | Abstract and concrete names | yes |
| 3a | Verbal ambiguity: indefiniteness or multiplicity of meaning | yes |
| 3b | The distinction between univocal and equivocal speech | yes |
| 3c(1) | Literal and figurative use: metaphors | yes |
| 3c(2) | Varying degrees of generality and specificity | yes |
| 3c(3) | Used to signify an attribute and its cause or effect | yes |
| 3d | The significance of names predicated of heterogeneous things | yes |
| 4a | The relation between univocal meaning and definition | yes |
| 4b | The dependence of demonstration on univocal terms | yes |
| 4c | The nature and utility of semantic analysis | citations only, no excerpt text |
| 4d | The use of metaphors and myths in science and philosophy | yes |
| 4e | The use of signs in reasoning | yes on `plain-text` only — compiled, not scanned, see below |
| 5a | Natural things as signs of divinity | yes |
| 5b | Supernatural signs: omens, portents, visitations, dreams, miracles | yes |
| 5c | The symbolism of the sacraments | yes |
| 5d | The symbolism of numbers in theology | yes |
| 5e | The interpretation of the word of God | yes |
| 5f | The names of God | yes |
| 6 | Symbolism in psychological analysis (overview) | yes |
| 6a | The symbolism of dreams | yes |
| 6b | The symbolism of apparently normal acts (forgetting, slips) | yes |
| 6c | The symbolism of anxieties, obsessions, neurotic manifestations | yes |

## Gotchas

- **`1d` folder is misnamed.** Its folder name is a verbatim duplicate of
  `1a`'s ("The distinction between natural and conventional signs"), but per
  Adler's outline 1d actually covers "the conventional notations of human
  language." Don't trust the folder name for this one — the content inside
  is correct for topic 1d, only the label is wrong. Left as-is rather than
  renamed, to avoid breaking links/history.
- **`4e` is not a scan like every other section — it's a compilation.** It
  was missing from the repo entirely (no folder, either branch) until it was
  built from independent public-domain sources, because the original source
  material for this repo never had it split out into its own file. It exists
  **only on `plain-text`/`markdown`**, not `main` — there's no original
  PDF/docx to put there, since nothing was ever extracted from an original
  for this topic. Confidence notes are inline per-passage (`4e/4e.txt` on
  `plain-text`, `4e The use of signs in reasoning/4e.md` here); treat its
  GBWW page locators as unverified (content/structure identity is solid,
  the literal page-letter codes are not).
- **`4c` is citations-only** (`references_4c-1`) — no excerpted body text,
  unlike every other section.
- **Folder naming is inconsistent** — some have a trailing period after the
  code (`3b.`, `4a.`), some don't; `2e` has a double space after the code;
  only `3c` and `4c` use a parenthesized sub-index (`3c (1)`, `4c (1)`).
  Don't pattern-match on naming convention — enumerate folders directly.
  On **this branch only**, the 18 folders that used to be bare codes with
  no title at all (`1f`, `2c`, `3c (1)`–`(3)`, `4c (1)`, `4d`–`6c`) were
  renamed to include their title, matching the rest — `main` and
  `plain-text` still have the bare versions, unchanged.
- **Filenames contain spaces, commas, and parentheses.** Always quote paths
  in shell commands; parentheses in a folder name (`3c (1)`) will break an
  unescaped markdown link — wrap the destination in `<...>` or percent-encode
  it.
- **`5b`'s file is literally named "fixed"** (`5b fixed.docx` on `main`) —
  implies an earlier version was corrupted/wrong and this replaced it. There
  is no other copy; this is the canonical one.

## Regenerating `plain-text`

If `main` gains new or updated source files, the `plain-text` branch needs
re-conversion. Commands used originally:

```bash
# PDFs (real embedded text, no OCR needed — verified against every file in this repo)
pdftotext -layout "input.pdf" "input.txt"

# docx (no pandoc available when this was built; used LibreOffice headless)
soffice --headless --convert-to txt:Text --outdir "$(dirname "input.docx")" "input.docx"
```

Both tools preserve the citation-list layout reasonably well. `pdftotext`
without `-layout` reflows text and loses column alignment in the citation
lists — always use `-layout`.

**Line-wrapping gotcha:** LibreOffice's docx conversion does not wrap
paragraphs at all — it dumps each paragraph as one unbroken line, which for
a multi-page excerpt produced single lines up to ~9,800 characters (found
and fixed across all 9 docx-derived files: 4d, 5a–6c). `pdftotext -layout`
doesn't have this problem, since it preserves the PDF's real line breaks.
After any docx conversion, always reflow:

```bash
fold -s -w 90 "input.txt" > tmp && mv tmp "input.txt"
```

`fold -s` only splits lines *longer* than the width, breaking at the last
space — it never merges already-short lines together. That distinction
matters here: some sections (e.g. scripture quotes, one verse per line)
are already correctly formatted line-by-line, and a paragraph-reflow tool
like `fmt` would wreck that by merging consecutive short lines into one
justified block. `fold -s` leaves those alone and only touches the
pathological giant-line paragraphs.

## Regenerating `markdown`

Headers are derived from the *original* PDF/docx formatting (font weight,
Word paragraph styles), not guessed from the flattened text — this
preserves the human curator's actual section boundaries rather than
re-inventing them. Conversion scripts pull straight from `main` via
`git show main:<path>`, so this branch never needs `plain-text`'s `.txt`
files as an input (only as a verification reference, see below).

**Font/style conventions are not uniform across source files** — confirmed
by direct inspection, not assumed:
- Most PDFs: `WorkSans` family, `Medium`=header, `Italic`=subheader,
  `Regular`=body, sizes ~14/13/12pt
- `6b`/`6c`: plain `Calibri`, `Bold`=header, no italic tier at all (2-level,
  not 3-level)
- Some docx (4d, 5d, 5e, 5f, 6, 6a): real Word `toc 1`/`Heading 1` styles
- Other docx (5a, 5b, 5c): flat `Normal` style throughout, no heading
  styles — headers detected by whole-paragraph bold instead

Because of this, classification works relative to *each document's own*
body-text baseline (most common non-bold/non-italic size) rather than
hardcoded absolute sizes — a fixed threshold calibrated on one file's
font silently misclassifies another file using a different font at
different sizes.

**Known false-positive source (not yet fully solved):** a short line that
is *stylistically* a sub-reference (fully italic/bold, roughly body-sized)
isn't always *structurally* one — dialogue speaker labels
("*HERMOGENES:* Suppose...") and scholastic disputation markers ("*Obj.
2.*") are only styled for a short prefix, not the whole line, which is
now checked for (style must cover >70% of the line's characters, not just
be present). Block-quoted verse is often italicized line-by-line, which
matches a genuine sub-reference's font shape even though it isn't one —
a text-shape check (does it look like "Title, page-ref" or "Chap. N.
...", not prose) filters most of this out, but a verse line shaped like
"ProperName, rest of clause" (e.g. dialogue addressing someone by name)
is structurally identical to a real citation sub-reference and can still
slip through. This is cosmetic (the text is intact, just occasionally
over-promoted to a `###`), not data loss — confirmed via a repo-wide
word-diff against `plain-text`'s `.txt` files (see below), which would
catch actual content loss but can't catch a heading-level judgment call.

**Verifying a regeneration** — the scripts fix real extraction bugs found
by testing, not just add headers, so re-verify after any change:
- Missing inter-word spaces: some PDFs realize justified-text spacing as
  pure character positioning with no actual space glyph in the stream.
  Detected via character x-position gaps (~0 within a word, several points
  at a real word boundary).
- A font-encoding gap where certain ligature glyphs (`ff`/`ffi`) extract
  as a literal NUL byte instead of letters, and which ligature it was is
  ambiguous from the glyph alone — disambiguated by trying each candidate
  and checking which produces a real word, using `plain-text`'s `.txt`
  files as a reference vocabulary (present at conversion time via
  `git show plain-text:<path>`, not needed after — nothing here is a
  runtime dependency on that branch).
- Ligature characters (`ﬁ`, `ﬀ`, etc.) normalized to plain letters.

After any regeneration, check: every `.md` word either appears in the
`.txt` reference vocabulary or is a genuine new word (proper noun, Latin
term) — a word that *doesn't* match either and *does* split cleanly into
two real words is very likely a missing-space bug, not new content.
