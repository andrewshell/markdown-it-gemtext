---
id: TASK-26
title: Publish the first release to npm
status: To Do
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
  - 'https://docs.npmjs.com/generating-provenance-statements'
priority: medium
type: chore
ordinal: 26000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Ship version 1.0.0 of markdown-it-gemtext to npm with provenance and a changelog, and make future releases a one-command affair. Confirm the package name is free on npm before tagging (the research found gemdown, markdown-to-gemtext, and md2gmi but no markdown-it-gemtext). Use npm trusted publishing or a token-based GitHub Actions release workflow triggered by a version tag, generate provenance attestations, and keep the published tarball to dist, README, LICENSE, and CHANGELOG.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The package name markdown-it-gemtext is confirmed available and package.json name, repository, keywords (markdown-it, markdown-it-plugin, gemini, gemtext), and files fields are set
- [ ] #2 npm pack --dry-run lists only dist, README.md, LICENSE, CHANGELOG.md, and package.json
- [ ] #3 A GitHub Actions workflow publishes on a v* tag with npm provenance, after build, lint, and test pass
- [ ] #4 CHANGELOG.md follows Keep a Changelog and has a 1.0.0 entry
- [ ] #5 Installing the published package in a fresh project and rendering a sample file works from both ESM and CJS
<!-- AC:END -->
