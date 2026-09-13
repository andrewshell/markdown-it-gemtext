---
id: TASK-6
title: Render fenced and indented code blocks as preformatted blocks
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
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_codeblock.py'
priority: high
type: feature
ordinal: 6000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Render every Markdown code block as a gemtext preformatted block, preserving content byte for byte, and carry the fence info string across as alt text.

Fenced blocks carry an info string (language) that maps naturally to the preformat alt text. Indented code blocks have no info string; md2gemini offers a codeTag option for the default alt text on unlabeled blocks. Content must keep internal blank lines, trailing blank lines inside the block, and leading whitespace exactly. Fences using ~~~ or more than three backticks, and nested fences inside list items, must still produce exactly three backticks in gemtext. A known limitation: gemtext cannot escape a line that begins with three backticks inside a preformatted block; document it and make the renderer emit the block anyway rather than mangling code.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A fenced block with info string "python" renders as a line "```python", the content verbatim, and a closing "```"
- [ ] #2 A fenced block with no info string uses option codeAlt (default empty) as alt text
- [ ] #3 Indented code blocks render as a preformatted block with codeAlt alt text and their four-space indentation removed
- [ ] #4 Fences using ~~~ or four or more backticks, including nested fences inside list items, render with exactly three backticks and the inner content unchanged (line counts match md2gemini test_nested_fences cases)
- [ ] #5 Content lines are never trimmed, joined, or re-wrapped, and blank lines inside the block are kept, including a trailing blank line inside the block
- [ ] #6 A code block is followed by exactly one blank line before the next block, even when the source has none or several
- [ ] #7 Only the first word of the info string is used as alt text when option codeAltFullInfo is false (default); the full info string is used when true
<!-- AC:END -->
