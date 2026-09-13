---
id: TASK-8
title: 'Render blockquotes, including nested quotes and quoted blocks'
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
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_quote.py'
priority: high
type: feature
ordinal: 8000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Render Markdown blockquotes as gemtext quote lines. Every line produced by the content of the quote, whatever block type it is, gets a "> " prefix, so quoted lists, code, headings, and nested quotes need a rule for what they become.

Nested quotes render as "> > text" (the inner prefix becomes part of the text, which is how gmnhg behaves). Quoted code blocks are a hard case: prefixing the toggle line turns it into text, so render the code lines as quote lines without the toggles, or as a preformatted block after the quote, chosen by option. Quoted headings become "> # text" as plain text. Links inside quotes are handled in the links milestone; this task must leave the link placement hook in a spot where link lines can be emitted after the quote rather than inside it.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A single-line quote renders as "> text" and a multi-line quote where each source line has a > prefix renders as one quote line per paragraph (soft breaks joined)
- [ ] #2 Hard breaks inside a quote render as separate "> " lines (md2gemini test_quote_with_hard_linebreaks)
- [ ] #3 Two paragraphs inside one quote render as two quote lines separated by a ">" line with no trailing space
- [ ] #4 A nested quote renders with the inner prefix as text: "> > inner"
- [ ] #5 A list inside a quote renders as "> * item" lines
- [ ] #6 A code block inside a quote renders as quote lines by default and as a separate preformatted block after the quote when option quotedCode is "preformat"
- [ ] #7 Text after a quote is separated by exactly one blank line (md2gemini test_quote_with_text_after)
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
