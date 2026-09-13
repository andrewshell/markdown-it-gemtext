---
id: TASK-17
title: Handle inline and block HTML
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-2
dependencies:
  - TASK-4
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_strip_html.py'
  - 'https://github.com/davep/md2gemtext'
priority: medium
type: feature
ordinal: 17000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Markdown documents contain HTML when markdown-it is created with html: true, and even with html: false the raw text arrives as text tokens. Gemtext cannot display HTML. Offer the strategies seen across converters: strip tags but keep their text content (md2gemini strip_html, md2gemtext striptags), keep raw HTML as text (md2gemini default for inline), or wrap HTML blocks in a preformatted block with alt text "html" (md2gemini default for blocks). Stripping inline tags must keep the text between them ("<b>x</b>" becomes "x"). HTML comments should be dropped in every mode. Recognise a few tags with obvious gemtext meaning when stripping: <br> becomes a line break, <a href> becomes a link through the link pipeline, <img src alt> becomes an image link.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Option htmlInline accepts "strip" (default) and "keep"; strip renders "<i>a</i> <b>b</b> <made-up>c</made-up>" as "a b c" (md2gemini test_remove_inline_html)
- [ ] #2 Option htmlBlock accepts "strip" (default), "preformat", and "keep"; preformat wraps the block in a "```html" fence (md2gemini test_convert_html_block), strip drops it and its surrounding blank lines collapse to one
- [ ] #3 HTML comments <!-- --> inline and block are dropped in every mode
- [ ] #4 With htmlInline strip, <br> renders as a hard line break, <a href="u">t</a> goes through the link pipeline, and <img src alt> goes through the image pipeline
- [ ] #5 Behaviour is identical whether markdown-it was created with html true or false, except that html false shows raw tags only in keep mode
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
