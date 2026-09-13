---
id: TASK-14
title: 'Handle autolinks, linkify URLs, reference links, and link titles'
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
labels: []
milestone: m-1
dependencies:
  - TASK-11
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://lieba.ch/markdown-to-gemtext-converter.html'
  - >-
    https://github.com/markdown-it/markdown-it/blob/master/test/fixtures/markdown-it/linkify.txt
priority: medium
type: feature
ordinal: 14000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Markdown produces links through more than the [text](url) syntax. Angle-bracket autolinks, bare URLs when markdown-it linkify is enabled, reference-style links with definitions, and mailto autolinks all arrive as link_open tokens with slightly different properties, and reference_definition tokens appear in markdown-it 15 streams. Each must go through the same link mode pipeline. A bare URL whose text equals its href should not produce a redundant "=> url url" plus inline copy in copy mode; treat it as a link-only fragment where sensible. Link titles are ignored by every existing converter; offer them as an optional label source.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 An autolink <https://example.com> and a linkified bare URL render as link lines under the active link mode with the URL as label, and the inline text is the URL
- [ ] #2 Reference-style links [text][ref] with a definition render identically to inline links, and unused reference definitions produce no output
- [ ] #3 reference_definition tokens (markdown-it 15) never leak into the output as text
- [ ] #4 mailto autolinks <a@b.c> render as "=> mailto:a@b.c a@b.c"
- [ ] #5 Option linkLabel "text" (default) or "title" uses the link title as the link line label when present, falling back to text
- [ ] #6 A paragraph that is only a bare linkified URL renders as a single link line, not a text line plus a link line
<!-- AC:END -->
