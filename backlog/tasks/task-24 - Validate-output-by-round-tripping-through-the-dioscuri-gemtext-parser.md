---
id: TASK-24
title: Validate output by round-tripping through the dioscuri gemtext parser
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
labels: []
milestone: m-3
dependencies:
  - TASK-3
  - TASK-11
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/wooorm/dioscuri'
priority: medium
type: feature
ordinal: 24000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Our own validator checks the grammar, but an independent parser catches disagreements about what the grammar means. dioscuri (wooorm) is a maintained JavaScript gemtext parser producing an AST. Use it as a dev dependency to parse every fixture and spec output and assert structural facts: the number of heading, link, list, quote, and preformatted nodes matches what the Markdown token stream implies; link node URLs equal the hrefs we intended; preformatted node alt text equals the fence info; no text node begins with a gemtext prefix that was meant to be text. This also gives us a place to test the CRLF option, since dioscuri handles both endings.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 dioscuri is a devDependency only and never appears in the published package dependencies
- [ ] #2 A helper parses rendered output with dioscuri and returns counts by node type plus the list of link URLs and preformatted alt texts
- [ ] #3 For every fixture in the suite, dioscuri link URLs equal the set of link lines our renderer intended to emit
- [ ] #4 For every fixture, the number of heading nodes equals the number of headings rendered as gemtext headings (clamped or not), and the number of preformatted nodes equals the number of code blocks plus tables plus preformatted HTML blocks
- [ ] #5 The same assertions pass with lineEnding "crlf"
- [ ] #6 A failing assertion prints the Markdown input, our output, and the dioscuri node summary
<!-- AC:END -->
