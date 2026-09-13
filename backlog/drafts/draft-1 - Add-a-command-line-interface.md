---
id: DRAFT-1
title: Add a command-line interface
status: Draft
assignee: []
created_date: '2026-09-13 16:14'
labels: []
milestone: m-4
dependencies:
  - TASK-25
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini#command-line'
priority: low
type: feature
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Optional follow-up, drafted because it is not required for the plugin itself. md2gemini users relied on its CLI (files or stdin to stdout, --write to emit .gmi files next to the source, --dir for an output directory, and a flag per option). A thin bin that wraps the plugin would make the package a drop-in md2gemini replacement for shell pipelines and static site build steps. Decide whether it belongs in this package or a separate markdown-it-gemtext-cli package before promoting this draft.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 bin markdown-it-gemtext reads Markdown from file arguments or stdin and writes gemtext to stdout
- [ ] #2 --write emits a .gmi file next to each input and --dir redirects those files
- [ ] #3 Every plugin option has a CLI flag with the same name in kebab-case, and --help lists them with defaults
- [ ] #4 A --front-matter flag loads markdown-it-front-matter and --footnotes loads markdown-it-footnote
- [ ] #5 Exit code is non-zero and an error names the file when input cannot be read or output cannot be written
<!-- AC:END -->
