---
id: TASK-20
title: Interoperate with front matter and unknown plugin tokens
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
  - 'https://github.com/ParkSB/markdown-it-front-matter'
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_frontmatter.py'
priority: medium
type: feature
ordinal: 20000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Two robustness concerns. First, static site sources begin with YAML (---) or TOML (+++) front matter. If the user loads markdown-it-front-matter the block arrives as a front_matter token that must render as nothing; without that plugin, a leading "---" block renders as a thematic break followed by text, which is surprising but correct Markdown, so document that users should load the front matter plugin. Second, any other plugin (containers, emoji, attrs, math, task lists, anchors) adds token types this renderer has never seen. The default for an unknown block token must be to render its children or content as text, never to throw or emit HTML tags, and a debug option should log unknown token types so users can report them.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 With markdown-it-front-matter loaded, YAML and TOML front matter produces no output and the following content starts at line one (md2gemini test_frontmatter cases)
- [ ] #2 Without the front matter plugin, a leading "---" block renders as a thematic break plus text lines, and the README documents loading markdown-it-front-matter
- [ ] #3 An unknown block token with content renders its content as text lines; an unknown inline token renders its content or children as text; neither throws
- [ ] #4 markdown-it-emoji, markdown-it-container, and markdown-it-attrs each render their example input without HTML tags in the output or validator violations
- [ ] #5 Option onUnknownToken receives the token type once per type per render for diagnostics
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
