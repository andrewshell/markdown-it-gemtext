---
id: TASK-9
title: Render thematic breaks
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
priority: medium
type: feature
ordinal: 9000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext has no horizontal rule. Render Markdown thematic breaks (---, ***, ___) as a configurable text line, defaulting to a visible separator, with the option to omit them entirely. gemgen defaults to "~~~"; some authors prefer a blank line or a row of dashes. The chosen string must not start with a gemtext prefix, and the renderer should reject or escape a configured value that would (for example "* * *" or "---" is fine, "# --" is not).
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A thematic break renders as the option hr string (default "~~~") on its own line, surrounded by one blank line on each side
- [ ] #2 Option hr set to empty string or false omits the break, leaving one blank line between the surrounding blocks
- [ ] #3 The plugin throws at configuration time if hr starts with =>, ```, #, "* ", or >, with a message naming the option
- [ ] #4 Three thematic breaks in a row render as three separator lines each separated by one blank line
<!-- AC:END -->
