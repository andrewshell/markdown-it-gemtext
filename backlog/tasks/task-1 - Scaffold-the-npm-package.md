---
id: TASK-1
title: Scaffold the npm package
status: To Do
assignee: []
created_date: '2026-09-13 16:09'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-0
dependencies: []
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/markdown-it/markdown-it/blob/master/package.json'
  - 'https://www.conventionalcommits.org/en/v1.0.0/'
  - 'https://github.com/conventional-changelog/commitlint'
  - 'https://github.com/amannn/action-semantic-pull-request'
priority: high
type: chore
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Set up the markdown-it-gemtext repository as a publishable TypeScript library so every later task has a build, test, and lint loop to work in, and so the commit history can drive automated releases.

Context: markdown-it 15 ships its own type declarations (no @types/markdown-it), is dual ESM/CJS, and removed its lib/* subpath exports. The plugin should be ESM-first with a CJS fallback and treat markdown-it as a peer dependency. Upstream markdown-it tests with node --test and fixture files; either node:test or vitest is acceptable, pick one and note why in the implementation notes.

Commit hygiene: the project uses Conventional Commits so that release-please (see the publish task) can compute versions and the changelog. Enforce the format locally with a commit-msg hook (commitlint with the conventional config via husky or lefthook) and in CI with a pull request title check, since squash merges take the PR title as the commit subject.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 package.json declares markdown-it as a peerDependency covering ^14 || ^15 and exposes "exports" with import, require, and types conditions
- [ ] #2 npm run build emits ESM and CJS bundles plus .d.ts files into dist/
- [ ] #3 npm test runs the chosen test runner with a placeholder test that imports the built plugin from both ESM and CJS entry points, and npm run test:coverage reports coverage
- [ ] #4 npm run lint runs eslint with typescript-eslint and a formatter check (prettier or biome) with no errors on the scaffold, and npm run typecheck runs tsc --noEmit
- [ ] #5 A commit-msg hook rejects commit messages that do not follow Conventional Commits, verified by attempting a commit with the subject "bad message" and one with "feat: add thing"
- [ ] #6 A GitHub Actions workflow runs build, typecheck, lint, and test on push and pull request against Node 20, 22, and 24, and a separate job validates the pull request title against Conventional Commits
- [ ] #7 CONTRIBUTING.md documents the commit format with examples of feat, fix, docs, chore, and breaking-change footers, and explains that release-please derives versions from them
- [ ] #8 LICENSE (MIT), .gitignore, .editorconfig, and a minimal README stub exist
- [ ] #9 Every devDependency and every GitHub Action in the workflows is at its latest released version at the time of the task (check with npm outdated and the Actions marketplace), and the implementation notes list any deliberate exception with the compatibility reason
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
