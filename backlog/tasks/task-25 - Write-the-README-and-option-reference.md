---
id: TASK-25
title: Write the README and option reference
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
labels: []
milestone: m-4
dependencies:
  - TASK-21
  - TASK-22
  - TASK-23
  - TASK-24
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini#link-modes'
priority: high
type: docs
ordinal: 25000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The README is the product page for the plugin. It must let a markdown-it user go from install to a converted capsule page in two minutes and let a md2gemini refugee map every option they used. Follow the md2gemini README structure for link modes because it is the explanation people already know: one sample Markdown paragraph followed by the exact output under each mode. Every option gets a table row with name, type, default, and one sentence. Include a limitations section (no escaping of three backticks in code, nested lists are not real gemtext, h4 to h6 clamp, tables are preformatted text) and a comparison table against md2gemini, gemgen, gmnhg, gemdown, and markdown-to-gemtext so users can see what is different. Generate the option examples from real renderer output in a test so the README cannot drift.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 README has install, quick start (ESM and CJS), and a TypeScript example that compiles with no casts
- [ ] #2 README shows the two-paragraph link mode sample with exact output for all five modes, and a test asserts the README code blocks match live renderer output
- [ ] #3 Every plugin option appears in an options table with type, default, and description, and a test asserts the table lists every key of the options type
- [ ] #4 README has a Limitations section covering the known lossy conversions and the text guard trade-off
- [ ] #5 README has a comparison table against the five converters named in the research doc
- [ ] #6 README documents loading markdown-it-front-matter, markdown-it-footnote, and linkify for the corresponding features
<!-- AC:END -->
