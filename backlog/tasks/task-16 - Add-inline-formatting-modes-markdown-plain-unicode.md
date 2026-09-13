---
id: TASK-16
title: 'Add inline formatting modes: markdown, plain, unicode'
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
labels: []
milestone: m-2
dependencies:
  - TASK-4
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_plain.py'
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_strip_html.py'
  - 'https://git.sr.ht/~kota/goldmark-gemtext'
priority: high
type: feature
ordinal: 16000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext has no emphasis, strong, code span, or strikethrough. Users split three ways: keep the Markdown markers as readable plain text (md2gemini default, gmnhg), strip them (md2gemini plain, gemgen default), or substitute Unicode mathematical bold and italic letters (gemgen unicode). Implement all three as one option that applies to emphasis, strong, code spans, and strikethrough (when the strikethrough rule is enabled, which it is by default in markdown-it), with per-construct overrides. The markdown mode normalises markers: __bold__ becomes **bold** and _italic_ becomes *italic* (md2gemini test_strip_html cases). Unicode substitution must leave characters with no bold or italic codepoint untouched and must not apply inside code spans.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Option inline accepts "markdown", "plain" (default), and "unicode", and applies to emphasis, strong, code spans, and strikethrough
- [ ] #2 In markdown mode, **bold**, __bold__, *italic*, _italic_ render as **bold** and *italic* (normalised markers), code spans keep backticks, and ~~strike~~ keeps tildes
- [ ] #3 In plain mode all markers are removed and the text is otherwise unchanged (md2gemini test_plain cases)
- [ ] #4 In unicode mode ASCII letters and digits in strong and emphasis map to mathematical bold and italic codepoints, other characters pass through, and code spans are rendered as plain text
- [ ] #5 Per-construct overrides (inlineEmphasis, inlineStrong, inlineCode, inlineStrikethrough) take precedence over inline
- [ ] #6 Nested emphasis (***both***) renders sensibly in every mode and never leaves unbalanced markers
- [ ] #7 A code span containing backticks or gemtext prefixes renders without breaking the line type
<!-- AC:END -->
