---
id: TASK-2
title: 'Spike: choose the plugin architecture and record a decision'
status: To Do
assignee: []
created_date: '2026-09-13 16:11'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-0
dependencies:
  - TASK-1
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/markdown-it/markdown-it/blob/master/docs/architecture.md'
  - 'https://git.sr.ht/~kota/goldmark-gemtext'
  - 'https://github.com/wavesheep/markdown-it-plain-text'
priority: high
type: spike
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Decide how the plugin takes over markdown-it output so that md.render() returns gemtext, and record the choice as a Backlog decision before any renderer code is written.

Three shapes exist in the wild: overwrite every entry in md.renderer.rules (simple, but stateful whole-document features like at-end links are awkward and it clobbers HTML output for that instance); replace md.renderer with a custom Renderer subclass that does its own token walk (the goldmark-gemtext pattern, cleanest for document-level passes); or a core rule that stores output on a side channel while md.render() still returns HTML (the markdown-it-plain-text pattern, weak typing). Also decide the public API shape: options object, whether a typed helper like renderGemtext(md, src) is exported, and how TypeScript users get types without casting.

Prototype only headings and paragraphs, enough to feel the ergonomics. Throw the prototype away or keep it only if it is the chosen shape.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A Backlog decision records the chosen shape, the rejected alternatives, and the reasons, with status accepted
- [ ] #2 The decision states how document-level state (pending link lines, footnote counters) is carried without leaking between md.render() calls
- [ ] #3 The decision states the public API: plugin signature, options type name, and whether md.render() itself returns gemtext
- [ ] #4 The decision states how the plugin coexists with other markdown-it plugins that add token types (unknown tokens must degrade to text, not throw)
- [ ] #5 A minimal prototype proves md.use(gemtext) then md.render("# Hi\\n\\nText") yields "# Hi\\n\\nText\\n" under the chosen shape
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
