---
id: TASK-22
title: Import gmnhg and gemgen golden corpora
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
labels: []
milestone: m-3
dependencies:
  - TASK-15
  - TASK-18
  - TASK-19
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/tdemin/gmnhg/tree/master/testdata'
  - 'https://github.com/kotajacob/gemgen'
priority: medium
type: feature
ordinal: 22000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
gmnhg ships eight .md/.gmi golden pairs (general_text, links, lists, tables, and four front matter formats) and gemgen ships a test.md with expectations in convert_test.go. These are the only real end-to-end Markdown to gemtext expectations written by other maintainers, and they cover long mixed documents rather than one construct at a time. Import them into the paired-file fixture directory under their original licenses with attribution, run them under the option set that best matches each tool (gmnhg keeps ordered numbers and indents nested lists with tabs; gemgen strips emphasis and uses ~~~ rules), and diff. Expect differences in blank-line placement and link grouping; resolve each by either adjusting our renderer when their behaviour is better, or editing the expected file with a comment explaining why ours differs.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 All eight gmnhg pairs and the gemgen test.md are present under test/fixtures/external with a LICENSE and ATTRIBUTION file
- [ ] #2 Each external corpus has a fixture options header that reproduces the originating tool defaults as closely as our options allow
- [ ] #3 Every line that differs between their expected output and ours is either fixed in the renderer or documented next to the fixture with a one-line reason
- [ ] #4 The gmnhg links.gmi grouping (footnotes, then images, then links after a block) is either matched or its divergence is recorded in the DIVERGENCES section
- [ ] #5 All imported cases pass in npm test
<!-- AC:END -->
