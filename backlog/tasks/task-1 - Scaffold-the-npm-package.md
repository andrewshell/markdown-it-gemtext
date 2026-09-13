---
id: TASK-1
title: Scaffold the npm package
status: To Do
assignee: []
created_date: '2026-09-13 16:09'
labels: []
milestone: m-0
dependencies: []
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/markdown-it/markdown-it/blob/master/package.json'
priority: high
type: chore
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Set up the markdown-it-gemtext repository as a publishable TypeScript library so every later task has a build, test, and lint loop to work in.

Context: markdown-it 15 ships its own type declarations (no @types/markdown-it), is dual ESM/CJS, and removed its lib/* subpath exports. The plugin should be ESM-first with a CJS fallback and treat markdown-it as a peer dependency. Upstream markdown-it tests with node --test and fixture files; either node:test or vitest is acceptable, pick one and note why in the implementation notes.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 package.json declares markdown-it as a peerDependency covering ^14 || ^15 and exposes "exports" with import, require, and types conditions
- [ ] #2 npm run build emits ESM and CJS bundles plus .d.ts files into dist/
- [ ] #3 npm test runs a placeholder test that imports the built plugin from both ESM and CJS entry points
- [ ] #4 A lint/format step (eslint + prettier or biome) runs in npm run lint with no errors on the scaffold
- [ ] #5 A GitHub Actions workflow runs build, lint, and test on push and pull request against Node 20, 22, and 24
- [ ] #6 LICENSE (MIT), .gitignore, .editorconfig, and a minimal README stub exist
<!-- AC:END -->
