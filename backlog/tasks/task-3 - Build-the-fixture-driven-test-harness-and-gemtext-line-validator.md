---
id: TASK-3
title: Build the fixture-driven test harness and gemtext line validator
status: To Do
assignee: []
created_date: '2026-09-13 16:11'
labels: []
milestone: m-0
dependencies:
  - TASK-1
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://geminiprotocol.net/docs/gemtext-specification.gmi'
  - 'https://github.com/markdown-it/markdown-it/tree/master/test/fixtures'
  - 'https://github.com/pebbe/tree-sitter-gemtext/blob/master/test.gmi'
priority: high
type: feature
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Provide the testing infrastructure every rendering task will use: fixture files that pair Markdown input with expected gemtext, and a validator that checks any output string against the gemtext line grammar.

Two fixture formats are needed. The markdown-it upstream format (title line, ".", markdown, ".", expected output, ".") lets us copy upstream fixtures such as tables.txt directly. Paired files (foo.md next to foo.gmi in a directory) let us drop in gmnhg golden pairs unchanged. Each fixture may carry a header or sidecar specifying plugin options so the same runner covers every link mode and inline mode.

The validator classifies each output line per the spec ABNF (link, preformat toggle, heading, list item, quote, text), tracks preformat mode, and reports violations such as an unbalanced preformat toggle, a link line with an empty or unencoded URL, a list item without the mandatory space, a heading deeper than three levels, or CRLF/LF mixing.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A test helper loads upstream-format fixture files and runs each case as a named test with exact string comparison and a readable diff on failure
- [ ] #2 A test helper loads .md/.gmi paired directories and runs each pair as a named test
- [ ] #3 Fixtures can declare plugin options (for example linkMode or emphasis) that the runner passes to the plugin
- [ ] #4 validateGemtext(output) returns a list of violations with line numbers, and unit tests cover each violation type using cases from tree-sitter-gemtext test.gmi (for example "###I" is a heading, "####" is not, "*not an item" is text)
- [ ] #5 A test helper asserts validateGemtext returns no violations for a given rendered output, used by later tasks as a one-line invariant
- [ ] #6 Fixture files live under test/fixtures with a README explaining both formats and the options header
<!-- AC:END -->
