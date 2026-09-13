---
id: TASK-15
title: 'Place links correctly inside lists, quotes, headings, and nested blocks'
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
labels: []
milestone: m-1
dependencies:
  - TASK-11
  - TASK-7
  - TASK-8
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_links.py'
  - 'https://github.com/tdemin/gmnhg/blob/master/testdata/links.gmi'
priority: high
type: feature
ordinal: 15000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Links inside a list item, a blockquote, a heading, or a table cell cannot be emitted where the paragraph rule would put them, because a "=> " line inside a list breaks the list and a "=> " line inside a quote is not a quote. Define and implement where each context flushes its pending links. Established answers: a list flushes its links after the whole list (md2gemini copy mode), or per item in newline mode; a quote flushes its links after the quote, not as quote lines (md2gemini issue 44, gmnhg); a heading that is only a link becomes a link line (gemgen auto); a heading containing a link among other text flushes the link after the heading. Nested combinations (a link in a list inside a quote) flush at the outermost block.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A link inside a list item in copy mode keeps the text inline and emits the link line after the whole list, separated by one blank line (md2gemini test_links_in_lists copy case)
- [ ] #2 A link inside a list item in newline mode splits the item as md2gemini does (test_links_in_lists newline case), and the validator accepts the result
- [ ] #3 A link inside a quote emits its link line after the quote as a non-quote line in paragraph and copy modes (md2gemini test_link_in_quote and test_link_in_quote_newline)
- [ ] #4 A heading that is only a link renders as "=> url heading text" when option headingLinks is "auto" (default), and as a heading plus a link line below when "below"
- [ ] #5 A link inside a list inside a quote emits its link line after the quote
- [ ] #6 In at-end mode every link from every context appears once at the document end in source order
- [ ] #7 A footnote marker counter inside nested contexts continues the document sequence without gaps or duplicates
<!-- AC:END -->
