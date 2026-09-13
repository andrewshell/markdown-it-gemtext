---
id: TASK-7
title: 'Render bullet, ordered, nested, and task lists'
status: To Do
assignee: []
created_date: '2026-09-13 16:11'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-0
dependencies:
  - TASK-4
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://geminiprotocol.net/docs/gemtext-specification.gmi'
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_list.py'
priority: high
type: feature
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext has one list construct: single-level unordered items starting with "* ". Markdown has bullet, ordered, nested, loose, and task lists, plus items spanning multiple lines and containing other blocks. Render all of them without producing invalid or surprising gemtext, with options for the lossy cases.

Ordered lists: default renders "* " items with the number kept as text ("* 1. First"), option to drop the numbers, matching the choice between gmnhg and gemgen. Nested lists: default flattens to a single level (only flat lists are real gemtext), option to indent with a configurable string (spaces or tab), which turns nested items into text lines but reads well in most clients. Loose lists (blank lines between items) must not emit blank lines between "* " lines. Multi-line items join on a space. Items containing a paragraph plus a code block or blockquote render the extra block after the item line. GFM task list checkboxes render as "[ ]" and "[x]" text unless disabled.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Bullet lists using -, +, or * render as "* item" lines with no blank lines between items, whether the source list is tight or loose
- [ ] #2 Two adjacent lists separated by a blank line and using different markers render as two lists separated by one blank line
- [ ] #3 An item whose text spans several source lines with 2 to 6 spaces of continuation indentation renders as one line joined by single spaces (md2gemini test_list cases)
- [ ] #4 Ordered lists render as "* 1. text" by default honoring the start number, and option orderedList "bullet" drops the numbers
- [ ] #5 Nested lists flatten to one level by default; option nestedList set to an indent string (for example "  " or "\\t") indents each sub-level by that string times the depth
- [ ] #6 A list item containing a code block or blockquote renders the item line, then the nested block on following lines, and the validator reports no violations
- [ ] #7 Task list items render as "* [ ] text" and "* [x] text" when the markdown-it-task-lists plugin or equivalent is present, and option taskList false renders them without the box
- [ ] #8 An empty list item renders as "*" followed by nothing, and the validator accepts the output
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
