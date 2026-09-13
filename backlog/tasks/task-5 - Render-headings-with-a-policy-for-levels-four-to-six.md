---
id: TASK-5
title: Render headings with a policy for levels four to six
status: To Do
assignee: []
created_date: '2026-09-13 16:11'
labels: []
milestone: m-0
dependencies:
  - TASK-4
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://geminiprotocol.net/docs/gemtext-specification.gmi'
priority: high
type: feature
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext has exactly three heading levels. Markdown has six plus setext underlines. Render ATX and setext headings as gemtext heading lines and give users a policy for h4 to h6.

Default policy: clamp to ### (what md2gmi does). Alternatives to offer as an option: render as a plain text line, or render as a text line with a prefix such as bold markers. Heading text is inline content and must be flattened to plain text before this task ends (inline formatting modes come later, but a heading containing a code span or emphasis must not throw). Headings that consist only of a link are handled in the links milestone; leave a note in the code where that hook belongs.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 ATX headings h1 to h3 render as "# ", "## ", "### " followed by the heading text on one line
- [ ] #2 Setext headings (=== and ---) render as level one and two gemtext headings
- [ ] #3 Option headingDepth ("clamp" default, "text") controls h4 to h6: clamp renders them as ###, text renders them as a plain text line
- [ ] #4 Closing ATX hashes (# Title #) are not present in the output
- [ ] #5 A heading is preceded and followed by exactly one blank line (except at document start), matching gemgen default spacing
- [ ] #6 An empty heading (#) renders as "#" with no trailing space
<!-- AC:END -->
