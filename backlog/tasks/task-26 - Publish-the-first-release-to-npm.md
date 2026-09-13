---
id: TASK-26
title: Automate releases with release-please and publish to npm
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
updated_date: '2026-09-13 16:29'
labels: []
milestone: m-4
dependencies:
  - TASK-25
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://docs.npmjs.com/generating-provenance-statements'
  - 'https://github.com/googleapis/release-please-action'
  - 'https://docs.npmjs.com/trusted-publishers'
priority: medium
type: chore
ordinal: 26000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Ship the first version of markdown-it-gemtext to npm and make every later release driven by the Conventional Commits history rather than by hand. release-please (googleapis/release-please-action) watches main, opens and maintains a release pull request that bumps package.json and writes CHANGELOG.md from feat, fix, and breaking-change commits, and when that PR is merged it creates the git tag and GitHub release. A publish job then runs on the created release and publishes to npm with provenance.

Confirm the package name is free on npm before the first release (the research found gemdown, markdown-to-gemtext, and md2gmi but no markdown-it-gemtext). Decide the starting version in the release-please manifest (0.1.0 keeps the option of breaking changes before 1.0; 1.0.0 signals stability). Use npm trusted publishing (OIDC) if available for the account, otherwise a granular automation token stored as a repository secret. Keep the published tarball to dist, README, LICENSE, CHANGELOG, and package.json.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The package name markdown-it-gemtext is confirmed available and package.json name, repository, keywords (markdown-it, markdown-it-plugin, gemini, gemtext), and files fields are set
- [ ] #2 A release-please workflow runs on push to main with release-type node, a .release-please-manifest.json and release-please-config.json exist, and the starting version is recorded in the manifest
- [ ] #3 A feat commit merged to main results in release-please opening or updating a release PR whose CHANGELOG.md diff lists that commit under Features
- [ ] #4 Merging the release PR creates a vX.Y.Z tag and a GitHub release with the changelog section as its body
- [ ] #5 A publish workflow triggered by the created release runs build, lint, and test, then npm publish with --provenance, and the npm package page shows the provenance badge
- [ ] #6 npm pack --dry-run lists only dist, README.md, LICENSE, CHANGELOG.md, and package.json
- [ ] #7 Installing the published package in a fresh project and rendering a sample file works from both ESM and CJS
<!-- AC:END -->
