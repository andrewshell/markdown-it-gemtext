---
id: TASK-19
title: Support markdown-it-footnote output
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-2
dependencies:
  - TASK-11
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/markdown-it/markdown-it-footnote'
  - 'https://github.com/tdemin/gmnhg/blob/master/testdata/links.gmi'
priority: low
type: feature
ordinal: 19000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
markdown-it-footnote is the standard way markdown-it users write [^1] footnotes, and it adds footnote_ref, footnote_block_open, footnote_open, and footnote_anchor tokens that a gemtext renderer would otherwise emit as HTML or drop. Only gmnhg among existing converters handles footnotes; it renders "[^n]: text" paragraphs at the end and renumbers labels sequentially. Match that: inline references render as "[^n]" markers, the footnote block renders as text lines at the end of the document, back-reference anchors are dropped, and links inside footnote text flush after the footnote block. The plugin must not depend on markdown-it-footnote; it only needs to recognise its token types when present.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 With markdown-it-footnote loaded, "text[^a]" renders as "text[^1]" and a "[^1]: footnote text" line appears at the end of the document after one blank line
- [ ] #2 Footnote labels are renumbered sequentially in order of first reference regardless of their source labels
- [ ] #3 Multi-paragraph footnotes render each paragraph as a text line under the "[^n]:" line
- [ ] #4 Links inside footnote text emit link lines after the footnote block under the active link mode
- [ ] #5 Footnote back-reference anchors produce no output
- [ ] #6 Without markdown-it-footnote loaded, the plugin has no dependency on it and [^1] renders as literal text
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
