---
id: TASK-4
title: 'Render paragraphs, line breaks, blank lines, and line endings'
status: To Do
assignee: []
created_date: '2026-09-13 16:11'
labels: []
milestone: m-0
dependencies:
  - TASK-2
  - TASK-3
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://geminiprotocol.net/docs/gemtext-specification.gmi'
priority: high
type: feature
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Render the most basic gemtext: paragraphs as single text lines, with deliberate blank-line and line-ending control. This is the foundation every other block builds on because gemtext clients wrap each line independently and never join lines, and never collapse blank lines.

Markdown soft breaks inside a paragraph become a single space. Hard breaks (trailing backslash or two spaces) become a real line break so poetry and addresses survive. Blocks are separated by exactly one blank line regardless of how many blank lines the source had. Output ends with exactly one newline. Line ending defaults to LF with a CRLF option because the spec canonical form is CRLF but LF is tolerated everywhere. Text tokens must be unescaped (backslash escapes and entities decoded) since gemtext has no escaping. Tight-list paragraph tokens are hidden and must not emit blank lines; that interaction is finished in the lists task but the paragraph rule must respect token.hidden from the start.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A paragraph with soft line breaks renders as one line with breaks replaced by single spaces, and runs of whitespace around the join are collapsed to one space
- [ ] #2 A hard break renders as a newline within the paragraph and the following text is not indented
- [ ] #3 Two paragraphs separated by one or five blank lines both render with exactly one blank line between them
- [ ] #4 Output always ends with exactly one line ending, and empty input renders as an empty string
- [ ] #5 Option lineEnding accepts "lf" (default) and "crlf" and every emitted line break uses it consistently, verified by the validator
- [ ] #6 Backslash escapes (\\*, \\_, \\#) and HTML entities (&amp;, &copy;, &#35;) render as the literal characters
- [ ] #7 Leading and trailing whitespace on a paragraph line is trimmed
<!-- AC:END -->
