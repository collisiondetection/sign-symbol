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
| 1f | Natural signs as the source of meaning in conventional signs: thought as the medium through which words signify things | yes |
| 2a | The first and second imposition of words: names signifying things and names signifying names | yes |
| 2b | The first and second intention of names: words signifying things and words signifying idea | yes |
| 2c | Intrinsic and extrinsic denominations: the naming of things according to their natures or by reference to their relations | yes |
| 2d | Proper and common names | yes |
| 2e | Abstract and concrete names | yes |
| 3a | Verbal ambiguity: indefiniteness or multiplicity of meaning | yes |
| 3b | The distinction between univocal and equivocal speech | yes |
| 3c(1) | The same word used literally and figuratively: metaphors derived from analogies or proportions and from other kinds of similitude | yes |
| 3c(2) | The same word used with varying degrees of generality and specificity: the broad and narrow meaning of a word | yes |
| 3c(3) | The same word used to signify an attribute and its cause of effect | yes |
| 3d | The significance of names predicated of heterogeneous things: the analogical as intermediate between the univocal and the equivocal | yes |
| 4a | The relation between univocal meaning and definition | yes |
| 4b | The dependence of demonstration on univocal terms: formal fallacies due to equivocation | yes |
| 4c | The nature and utility of semantic analysis: the rectification of ambiguity; the clarification and precision of meanings | citations only, no excerpt text |
| 4d | The use of metaphors and myths in science and philosophy | yes |
| 4e | The use of signs in reasoning: necessary and probable signs; the interpretation of symptoms in medicine | yes on `plain-text` only — compiled, not scanned, see below |
| 5a | Natural things as signs of divinity | yes |
| 5b | Supernatural signs: omens, portents, visitations, dreams, miracles | yes |
| 5c | The symbolism of the sacraments and of sacramental or ritualistic acts | yes (title supplied — see gotcha below) |
| 5d | The symbolism of numbers in theology | yes |
| 5e | The interpretation of the word of God | yes |
| 5f | The names of God: the use of words to signify the divine nature | yes |
| 6 | Symbolism in psychological analysis | yes |
| 6a | The symbolism of dreams: their latent and manifest content | yes |
| 6b | The symbolism of apparently normal acts: forgetting, verbal slips, errors | yes |
| 6c | The symbolism of anxieties, obsessions, and other neurotic manifestations | yes |

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
  `plain-text`, `4e The use of signs in reasoning/4e The use of signs in
  reasoning.md` here); treat its GBWW page locators as unverified
  (content/structure identity is solid, the literal page-letter codes are
  not).
- **`4c` is citations-only** (`references_4c-1`) — no excerpted body text,
  unlike every other section.
- **`5c`'s source docx has no title paragraph at all** (unlike `5a`/`5b`,
  which do) — the original conversion silently used the first citation
  group ("OLD TESTAMENT: Genesis, 17:9-14 / Exodus...") as the document H1
  instead, which also meant that whole citation group was missing its own
  `##` sub-header and its entry in the Citations index. Fixed on `markdown`
  by inserting the outline title as H1 (with an inline note, since nothing
  in the source itself says "5c") and restoring the orphaned group to its
  proper place. Confirmed via `git show plain-text:"5c/....txt" | head`
  that the gap is genuine in the source, not a conversion bug — same
  treatment as `4e`'s compiler's note. Not yet checked on `plain-text`
  (its `.txt` has the same missing title line, just no markdown structure
  to be wrong about) or `main` (original docx, unchanged).
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

**Title text used outside the file itself must match the file's own `#`
heading verbatim** (code→title table above, README's TOC, nav footers).
Found by direct visual reading on GitHub, not by any script: several
titles in this table and in README.md had been hand-shortened when first
written, silently drifting from the real heading — e.g. `3d` was missing
its whole second clause ("...the analogical as intermediate between the
univocal and the equivocal"). A link-resolves check doesn't catch this at
all, since the href is still correct — only the display text is wrong.
Regenerate the title lookup from each file's actual `# ` line (`grep -n
'^# '`), not from memory or a prior table, and diff any hand-written
title text against it before trusting it. The two deliberate exceptions
are `1d` and `5c`, which use the outline's title because their own
heading is wrong/absent (see gotchas above).

**Long citations that wrap across physical lines in the source PDF get
mis-detected as multiple separate headers, not one.** Found by reading the
rendered page directly — a citation like `8 ARISTOTLE: Categories, ... /
Topics, ... / Metaphysics, ...` that's long enough to wrap across several
lines in the original PDF sometimes had EACH wrapped line promoted to its
own `##` header, with the superscript Bekker/page-locator letters (`a`/`b`,
e.g. the "b" in `16b19-26`) that happened to fall at the wrap point dropped
entirely or scattered onto isolated stray lines in between (a bare `a`,
`b a`, etc. with no attached number). Confirmed across 12 files in this
pass (1b, 1d, 1e, 1f, 2d, 3c(1), 3c(2), 3c(3), 3d, 4a, 4b, 4c) — the worst
case (`4c`) had a single citation fragmented into 5 pieces across 3 stray
lines. The fix pattern: the file's own Citations index is untouched by
this bug (it's built differently) and holds the complete, correct text —
use it as ground truth to merge the fragments back into one header, and to
restore any bracket that's missing its letter even where no stray line
gives it away (check every `###` subheader's bracket against the index's
bracket set, not just presence-anywhere-in-body, since a *different*,
correctly-formed bracket elsewhere in the file can mask a broken one).
**GitHub's heading-anchor slug algorithm does NOT collapse whitespace —
ever.** Lowercase, strip to Unicode-aware `[\w \-]` (accented letters and
things like Aristotle's superscript Bekker `ᵃ`/`ᵇ` survive), replace each
space with a hyphen individually. A heading with `" / "` (space-slash-space)
loses the `/` but keeps both spaces, so the real anchor has a **double**
hyphen (`passim--objections`, not `passim-objections`). This was gotten
backwards mid-session — a "fix" was added to collapse consecutive spaces
into one, on the strength of a reference anchor that was never actually
checked against a live page, and it silently broke 6 already-committed
fixes before the mistake was caught. Do not trust a slug implementation
against another slug it also generated — that just checks the algorithm
against itself. Verify against GitHub's own output instead: open the file
on github.com, find the heading's `<a class="anchor" href="#...">` self-link
(rendered next to the heading, inside `<div class="markdown-heading">`),
and compare its `href` directly. Note separately that the real anchor
**id** on that same element is prefixed `user-content-` (e.g.
`id="user-content-citations"` for `href="#citations"`) — GitHub translates
between the two via its own JS, not native browser fragment matching, so
don't be alarmed that `document.getElementById('<slug>')` returns nothing;
that's expected and not a sign anything is broken.

**`5b`'s citation index was only 8 of 38 groups long** — someone had
linked the first 8 entries when the file was built, then a running
page-header (the printed edition's own "5. Symbolism in theology... 5b.
Supernatural signs..." breadcrumb) leaked into the list and silently
ended it; the remaining 30 stayed as bare unlinked text forever after.
The same page-header pattern (promoted to a fake `##` heading, splitting
one real citation group into two) recurs standalone in `5f`, not caught by
the citation-fragmentation check since it isn't a wrapped citation, just
page furniture. If a `##`/`###` heading's text looks like `(N. Group
title. Xy. Topic title.)` — parenthesized, restating the file's own outline
position — it's this artifact, not content; delete it and its index entry.
`5b` separately had 73 of its 74 `###` headers be false positives (bare
verse-line starts, stanza numbers, and section markers wrongly promoted —
the same false-positive class documented above, just far more of it in one
file) and a broken 2-row cipher table (a letter and its matching number had
both been orphaned onto stray lines by the same bug). See the commit
history on this branch for the exact fix if this recurs elsewhere.
