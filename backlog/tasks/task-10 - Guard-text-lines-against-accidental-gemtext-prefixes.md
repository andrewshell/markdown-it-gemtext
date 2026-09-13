---
id: TASK-10
title: Guard text lines against accidental gemtext prefixes
status: To Do
assignee: []
created_date: '2026-09-13 16:11'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-0
dependencies:
  - TASK-5
  - TASK-6
  - TASK-7
  - TASK-8
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://geminiprotocol.net/docs/gemtext-specification.gmi'
priority: high
type: feature
ordinal: 10000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Any text line whose first characters happen to be "=>", "```", "#", "* ", or ">" will be parsed by gemtext clients as that line type. Markdown text can legitimately begin with those characters: an escaped "\# not a heading", a paragraph starting with "=> arrow", a line after a hard break beginning with "> ", or heading text under the clamp policy. Gemtext has no escape mechanism, so the renderer needs a documented, deliberate strategy applied at the single place where text lines are emitted.

Options worth evaluating: prefix a single space (a leading space defeats every prefix and most clients hide it), insert a zero-width space, or leave as-is with a warning. Pick one default and expose an option. The three backtick case is the most important because it flips preformat mode for the rest of the document.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A paragraph beginning with "=> " renders as a text line that validateGemtext classifies as text, not link
- [ ] #2 A paragraph beginning with three backticks renders without toggling preformat mode, and the rest of the document still validates
- [ ] #3 Escaped "\\# heading" and "\\* item" and "\\> quote" at line start render as text lines, not heading, list, or quote lines
- [ ] #4 A hard-break continuation line beginning with "> " inside a paragraph renders as a text line
- [ ] #5 Option textGuard selects the strategy ("space" default, "zwsp", "none") and the README limitation section explains the trade-off
- [ ] #6 The guard is not applied inside preformatted blocks, real quote lines, or real list items
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
