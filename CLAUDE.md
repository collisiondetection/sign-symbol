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
  **only on `plain-text`**, not `main` — there's no original PDF/docx to put
  there, since nothing was ever extracted from an original for this topic.
  Confidence notes are inline per-passage in `4e/4e.txt`; treat its GBWW page
  locators as unverified (content/structure identity is solid, the literal
  page-letter codes are not).
- **`4c` is citations-only** (`references_4c-1`) — no excerpted body text,
  unlike every other section.
- **Folder naming is inconsistent** — some have a trailing period after the
  code (`3b.`, `4a.`), some don't; `2e` has a double space after the code;
  only `3c` and `4c` use a parenthesized sub-index (`3c (1)`, `4c (1)`).
  Don't pattern-match on naming convention — enumerate folders directly.
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
