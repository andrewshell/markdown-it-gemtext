---
id: TASK-11
title: 'Implement link modes: newline, paragraph, at-end, copy, off'
status: To Do
assignee: []
created_date: '2026-09-13 16:12'
labels: []
milestone: m-1
dependencies:
  - TASK-4
  - TASK-7
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini#link-modes'
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_links.py'
  - 'https://github.com/kotajacob/gemgen'
priority: high
type: feature
ordinal: 11000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext only allows links on their own line, so every inline Markdown link has to move. This is the core feature of the plugin and the one users compare converters on. Implement the five link modes that md2gemini established as the vocabulary, plus the special case every good converter has: a paragraph, list item, or heading whose entire content is one link becomes a bare link line with no footnote marker.

Modes: "newline" (the link line is emitted in the middle of the paragraph, splitting it), "paragraph" (inline marker [n], then "=> url n: url" lines after the paragraph, numbering continues through the document), "at-end" (same markers, all link lines at the end of the document), "copy" (no markers, "=> url link text" lines after the paragraph, default because it reads best in clients), "off" (link text kept, URL dropped). Footnote numbering must reset per md.render() call. The link label in paragraph and at-end modes uses "n: url" by default; an option should allow "n: link text" instead since bare URLs read poorly.

Inline link handling inside lists and quotes is a separate task, but the design here must put pending links in a per-block queue that those contexts can flush at the right point.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Option linkMode accepts "newline", "paragraph", "at-end", "copy" (default), and "off", and each mode reproduces the exact README example output from md2gemini for the two-paragraph sample
- [ ] #2 A paragraph consisting solely of one link renders as a single "=> url text" line with no marker and no duplicate, in every mode except off
- [ ] #3 A list item consisting solely of one link renders as a "=> url text" line in place of the "* " line (gemgen and gmnhg behaviour) unless option linkOnlyListItems is "bullet"
- [ ] #4 In paragraph and at-end modes, marker numbers continue across paragraphs and reset between separate md.render() calls
- [ ] #5 In paragraph and at-end modes, option footnoteLabel "url" (default) renders "=> url n: url" and "text" renders "=> url n: link text"
- [ ] #6 A link with empty text renders with the URL as the label
- [ ] #7 Two links to the same URL in one paragraph produce two link lines in copy mode and two markers in paragraph mode (no deduplication unless option dedupeLinks is true)
- [ ] #8 Link lines are separated from the preceding paragraph by one blank line in copy, paragraph, and at-end modes, and consecutive link lines have no blank lines between them
<!-- AC:END -->
