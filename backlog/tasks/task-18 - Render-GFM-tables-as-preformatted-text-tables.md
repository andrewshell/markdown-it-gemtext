---
id: TASK-18
title: Render GFM tables as preformatted text tables
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
labels: []
milestone: m-2
dependencies:
  - TASK-6
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_tags.py'
  - 'https://github.com/makew0rld/md2gemini/blob/master/md2gemini/unitable.py'
  - >-
    https://github.com/markdown-it/markdown-it/blob/master/test/fixtures/markdown-it/tables.txt
priority: medium
type: feature
ordinal: 18000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext has no tables. The converter convention is a preformatted block with alt text "table" containing a text table, so screen readers get the alt text and sighted readers get aligned columns. markdown-it enables GFM tables by default, so table tokens will appear in ordinary input. Provide Unicode box-drawing (md2gemini default) and ASCII styles, honour column alignment from the delimiter row, and offer a "skip" style that drops the table and a "plain" style that emits aligned columns without borders. Cell content is inline and must go through the inline formatting mode; links inside cells flush after the table via the link pipeline. Width calculation must count East Asian wide characters and combining marks correctly or the borders will not line up.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A 3x2 table renders inside a "```table" fence as a Unicode box table matching the md2gemini test_table_tag layout, and option tableAlt changes the alt text
- [ ] #2 Option tableStyle accepts "unicode" (default), "ascii", "plain", and "skip"
- [ ] #3 Left, right, and center column alignment from the delimiter row is applied to cell padding
- [ ] #4 Escaped pipes inside cells (\\|) and inline code containing pipes render correctly (markdown-it tables.txt fixture cases)
- [ ] #5 Column widths account for wide CJK characters and emoji so borders align when displayed in a monospace font
- [ ] #6 Links inside cells keep their text in the cell and emit link lines after the table
- [ ] #7 Every cell of a ragged table (rows with fewer cells than the header) is padded so the table is rectangular
<!-- AC:END -->
