---
id: doc-1
title: 'Gemtext conversion research: spec, prior art, test corpora'
type: specification
created_date: '2026-09-13 16:08'
updated_date: '2026-09-13 16:09'
---
Research gathered 2026-09-13 before planning the markdown-it-gemtext plugin. Nothing here is implemented yet.

## Gemtext spec essentials

Sources: https://geminiprotocol.net/docs/gemtext-specification.gmi (v0.24.1) and https://geminiprotocol.net/docs/gemtext.gmi

- Line-oriented. Each line has exactly one type, decided by its first three characters. Documents parse in one pass with one bit of state (normal vs preformatted).
- Line types: text (default, blank lines included), link `=>[ws]URL[ws label]`, preformat toggle ```` ``` ```` (no leading whitespace; text after the opening toggle is alt text, text after the closing toggle is ignored), heading `#`/`##`/`###` (three levels only), list item `* ` (space mandatory, `-` does nothing), quote `>`.
- Clients MUST handle text, link, and preformat lines. Heading, list, and quote lines are optional and fall back to text lines.
- Canonical line ending is CRLF, but LF is tolerated by the protocol. Plan: LF by default, CRLF as an option.
- Clients wrap each text line independently and MUST NOT join consecutive short lines. Consequence: a Markdown paragraph must be emitted as one line, with soft breaks joined by a space.
- Blank lines render verbatim and consecutive blank lines are not collapsed. Consequence: the renderer controls blank lines deliberately (one between blocks).
- URLs in link lines MUST be percent-encoded per RFC 3986.
- No inline formatting, inline links, nested lists, ordered lists, tables, images, footnotes, or horizontal rules exist in gemtext. A leading space defeats every prefix, which is how some converters fake nested lists.
- MIME type `text/gemini` with optional `charset` and `lang` parameters. File extension `.gmi`.

## Prior art

No markdown-it gemtext plugin exists on npm (checked 2026-09). JS converters found: gemdown 0.8.0, markdown-to-gemtext 1.0.2, md2gmi 1.0.3. All sit on marked. dioscuri 2.0.0 (wooorm) is a gemtext parser that can validate our output.

### md2gemini (Python, mistune, archived 2023)

https://github.com/makew0rld/md2gemini. Its option vocabulary is the de-facto standard.

- Link modes: `newline` (default, link line interrupts the paragraph), `paragraph` (inline `[n]` markers, `=> url n: url` lines after each paragraph), `at-end` (markers, all links at document end), `copy` (no markers, `=> url linktext` after the paragraph), `off` (drop links, keep text). Link-only paragraphs become bare link lines.
- `plain` strips emphasis markers and inline HTML. Default keeps markers, normalised to `**` and `*`.
- `strip_html` removes inline and block HTML. Default converts HTML blocks to a ```` ```html ```` fence.
- `base_url` prefixes root-relative links. `md_links` rewrites `foo.md#bar` to `foo.gmi`. `link_func` is an arbitrary URL rewriter.
- `img_tag` (default `[IMG]`) suffixes image link labels. `code_tag` is the alt text for unlabeled fences. `table_tag` (default `table`) is the alt text for table fences.
- Tables become Unicode or ASCII box-drawing tables inside a fence.
- Nested and ordered lists are emitted as indented lines, ordered items keep `1.` text.
- Front matter (Jekyll `---`, Zola `+++`) can be stripped. Checklists `[ ]`/`[x]` are rendered.
- Tests live in https://github.com/makew0rld/md2gemini/tree/master/tests (11 files, about 50 cases). A local clone was reviewed; notable cases: links in lists and quotes, multi-line list items joined with a space, nested fences inside list items preserving line count, hard line breaks inside quotes, indented code with trailing blank lines, empty input.

### gemgen and goldmark-gemtext (Go, ~kota)

https://github.com/kotajacob/gemgen and https://git.sr.ht/~kota/goldmark-gemtext. Closest architectural analogue: a renderer plugged into the parser. Links go below the paragraph as `=> url label`, link-only paragraphs and lists become pure link blocks, hard breaks produce real newlines, emphasis modes `none|markdown|unicode`, heading links `off|auto|below`, horizontal rule string configurable (default `~~~`), nested lists indented two spaces, ordered lists become `*`. Test data: `test.md` and `convert_test.go` in the gemgen repo root.

### gmnhg (Go, Hugo)

https://github.com/tdemin/gmnhg. `testdata/` holds 8 `.md` to `.gmi` golden pairs (general_text, links, lists, tables, front_matter yaml/toml/json/org). Links are grouped after the containing block, footnotes first, then images, then links. Markdown footnotes render as `[^n]:` paragraphs. Ordered lists keep `1.` as text lines. Nested lists indent with tabs. URLs are percent-encoded.

### md2gemtext (Python, markdown-it-py)

https://github.com/davep/md2gemtext. Walks the same token stream we will. Letter footnote markers `{a}`, options for retaining inline markup, spacing after blocks, front matter hiding, table preformatting, HTML handling `convert|preformat|striptags`.

### Community note

Existing converters ignore the link title attribute (https://lieba.ch/markdown-to-gemtext-converter.html). Using the title as an optional label is a cheap differentiator.

## markdown-it facts that shape the design

- Current version 15.0.2. Ships its own TypeScript declarations, so no `@types/markdown-it`. Dual ESM/CJS. Parser internals are static properties: `markdownit.Renderer`, `markdownit.Token`, and so on. Subpath imports like `markdown-it/lib/*` were removed.
- A plugin is `(md, options?) => void`. `md.render()` returns `md.renderer.render(tokens, options, env)`. `md.renderer` is a public mutable field.
- Renderer rules receive `(tokens, idx, options, env, renderer)`. `Renderer.render` walks top-level tokens, sends `inline` tokens to `renderInline`, and falls back to `renderToken` (HTML tag emitter) when no rule matches. Hidden tokens (tight-list paragraphs) still reach custom rules, so a gemtext paragraph rule must check `token.hidden` itself.
- Three plugin shapes seen in the wild: overwrite every entry in `md.renderer.rules`, replace `md.renderer` with a custom Renderer, or run a core rule that stores output on a side channel (markdown-it-plain-text). The whole-document link modes (`at-end`) favour a custom Renderer with its own walk.
- Token facts: `fence.info` holds the language, `code_block` has none, `link_open` carries `href` and `title` attrs, `image` is one token with alt text in `children`, `softbreak`/`hardbreak` are inline tokens, `list_item_open.markup` distinguishes bullet from ordered, `heading_open.tag` is h1..h6, tables come from the built-in GFM rule, `reference_definition` tokens exist in v15.
- Upstream tests use `node --test` with fixture files in `test/fixtures` using a `.`-delimited format (title, `.`, markdown, `.`, expected, `.`).

## Test corpora

| Corpus | Use | URL |
|---|---|---|
| md2gemini tests | Port as golden fixtures per option | https://github.com/makew0rld/md2gemini/tree/master/tests |
| gmnhg testdata | 8 golden `.md`/`.gmi` pairs | https://github.com/tdemin/gmnhg/tree/master/testdata |
| gemgen test.md | Golden input with expectations in convert_test.go | https://github.com/kotajacob/gemgen |
| md2gemtext tests | markdown-it-py token semantics match ours | https://github.com/davep/md2gemtext/tree/main/tests |
| CommonMark spec 0.31.2 | 652 examples as JSON, invariant and snapshot sweep | https://spec.commonmark.org/0.31.2/spec.json |
| GFM spec 0.29 | Tables, task lists, strikethrough, autolinks | https://raw.githubusercontent.com/github/cmark-gfm/master/test/spec.txt |
| markdown-it fixtures | tables.txt, strikethrough.txt, linkify.txt, commonmark_extras.txt | https://github.com/markdown-it/markdown-it/tree/master/test/fixtures |
| tree-sitter-gemtext test.gmi | Gemtext parsing edge cases for validating output | https://github.com/pebbe/tree-sitter-gemtext/blob/master/test.gmi |
| dioscuri | Gemtext parser for round-trip validation | https://github.com/wooorm/dioscuri |

Gap: no capsule publishes paired Markdown sources and `.gmi` output at scale, so real-world coverage will come from the spec sweeps plus hand-written fixtures.

## Unverified

- goldmark-gemtext testdata contents.
- gmnhg rendering of horizontal rules and HTML.
- Name of the reference-label field on v15 link and image tokens.
