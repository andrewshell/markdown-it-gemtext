---
id: TASK-23
title: Sweep the CommonMark and GFM spec examples for invariants and snapshots
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-3
dependencies:
  - TASK-10
  - TASK-14
  - TASK-16
  - TASK-17
  - TASK-18
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://spec.commonmark.org/0.31.2/spec.json'
  - 'https://raw.githubusercontent.com/github/cmark-gfm/master/test/spec.txt'
priority: high
type: feature
ordinal: 23000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The CommonMark spec ships 652 examples as JSON and the GFM spec adds tables, task lists, strikethrough, and autolink cases. There is no gemtext expectation for any of them, but they are the most thorough stress input that exists for the parser side, and every example must at minimum produce valid gemtext without throwing. Run all of them under the default options and under each link mode and inline mode, assert invariants, and store snapshots so that any rendering change to an edge case is reviewed rather than silent.

Invariants: the renderer does not throw; validateGemtext reports no violations; preformat toggles are balanced; every href in the input tokens appears in exactly one link line (except in off mode); no HTML tag from the expected html field appears in the output when the input contained no raw HTML; no line ends with trailing whitespace; the document ends with exactly one line ending. Snapshots are stored one file per section so reviews stay readable.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A script downloads and vendors spec.json (CommonMark 0.31.2) and the GFM spec.txt extension examples into test/fixtures/spec with the spec version recorded
- [ ] #2 All 652 CommonMark examples render without throwing under default options and under every combination of linkMode and inline mode
- [ ] #3 validateGemtext reports zero violations for every example under every option combination
- [ ] #4 For every example, each link href in the token stream appears in exactly one link line under copy, paragraph, at-end, and newline modes
- [ ] #5 Snapshot files per spec section are committed and a snapshot mismatch fails the test suite with a diff
- [ ] #6 GFM extension examples (Tables 4.10, Task list items 5.3, Strikethrough 6.5, Autolinks 6.9) run under the same invariants
- [ ] #7 The sweep completes in under ten seconds in CI
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
