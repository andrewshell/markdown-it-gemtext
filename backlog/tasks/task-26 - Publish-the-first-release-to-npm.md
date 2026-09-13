---
id: TASK-26
title: Automate versioning with release-please and document manual npm publishing
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
updated_date: '2026-09-13 16:32'
labels: []
milestone: m-4
dependencies:
  - TASK-25
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/googleapis/release-please-action'
priority: medium
type: chore
ordinal: 26000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Make every release version and changelog entry come from the Conventional Commits history, while the actual npm publish stays a manual step run locally by the maintainer. release-please (googleapis/release-please-action) watches main, opens and maintains a release pull request that bumps package.json and writes CHANGELOG.md from feat, fix, and breaking-change commits, and when that PR is merged it creates the git tag and GitHub release. No GitHub workflow publishes to npm; instead a documented local sequence (checkout the tag, clean install, build, test, npm publish) is run by hand.

Confirm the package name is free on npm before the first release (the research found gemdown, markdown-to-gemtext, and md2gmi but no markdown-it-gemtext). Decide the starting version in the release-please manifest (0.1.0 keeps the option of breaking changes before 1.0; 1.0.0 signals stability). Keep the published tarball to dist, README, LICENSE, CHANGELOG, and package.json. A prepublishOnly script should run build and test so a manual publish from a dirty or untested tree fails fast.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The package name markdown-it-gemtext is confirmed available and package.json name, repository, keywords (markdown-it, markdown-it-plugin, gemini, gemtext), and files fields are set
- [ ] #2 A release-please workflow runs on push to main with release-type node, a .release-please-manifest.json and release-please-config.json exist, and the starting version is recorded in the manifest
- [ ] #3 A feat commit merged to main results in release-please opening or updating a release PR whose CHANGELOG.md diff lists that commit under Features
- [ ] #4 Merging the release PR creates a vX.Y.Z tag and a GitHub release with the changelog section as its body
- [ ] #5 No GitHub Actions workflow runs npm publish and no npm token is stored as a repository secret
- [ ] #6 A RELEASING.md (or a README maintainer section) documents the manual publish sequence: check out the release tag, npm ci, npm publish, and verify the version on npm
- [ ] #7 package.json has a prepublishOnly script that runs build and test, so npm publish aborts when either fails
- [ ] #8 npm pack --dry-run lists only dist, README.md, LICENSE, CHANGELOG.md, and package.json
- [ ] #9 Installing the published package in a fresh project and rendering a sample file works from both ESM and CJS
<!-- AC:END -->
