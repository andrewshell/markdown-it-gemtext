---
id: TASK-21
title: Port the md2gemini test suite as fixtures
status: To Do
assignee: []
created_date: '2026-09-13 16:14'
updated_date: '2026-09-13 16:34'
labels: []
milestone: m-3
dependencies:
  - TASK-12
  - TASK-13
  - TASK-15
  - TASK-16
  - TASK-17
  - TASK-18
  - TASK-20
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini/tree/master/tests'
priority: high
type: feature
ordinal: 21000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
md2gemini was the most used Markdown to gemtext converter and its tests encode years of user bug reports (issues 30, 31, 32, 40, 44 are cited inline). Port every case from its eleven test files into our fixture format, mapping each md2gemini option to our equivalent (links=paragraph to linkMode paragraph, plain=True to inline plain, strip_html to htmlInline/htmlBlock strip, img_tag to imageTag, table_tag to tableAlt, base_url to baseUrl, md_links to mdLinks, link_func to rewriteUrl, frontmatter to the front matter plugin). Where our defaults intentionally differ (for example we default to copy links and plain inline), set the option explicitly in the fixture rather than changing the expectation, and record each deliberate divergence in a DIVERGENCES section of the fixture README. Note that md2gemini normalises expected output by stripping trailing whitespace, so expectations should be compared after the same normalisation.

A local clone of the tests was reviewed during planning: test_base_url, test_codeblock, test_frontmatter, test_link_func, test_links, test_list, test_markdown_link, test_plain, test_quote, test_strip_html, test_tags.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Every test function and every parametrised variant in the eleven md2gemini test files has a corresponding fixture case that passes
- [ ] #2 Each fixture cites the md2gemini test name and any linked GitHub issue number
- [ ] #3 The nested-fence line-count tests (test_nested_fences, test_nested_fences_in_lists, and the ~~~ and long-fence variants) are expressed as line-count assertions
- [ ] #4 Every deliberate divergence from md2gemini output is listed with a reason in test/fixtures/README under a DIVERGENCES heading
- [ ] #5 The whole ported suite runs in the normal npm test invocation
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 New or updated npm packages and GitHub Actions use the latest released version; any older pin is justified in the task notes (for example a peer compatibility constraint)
<!-- DOD:END -->
