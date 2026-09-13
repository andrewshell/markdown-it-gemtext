---
id: TASK-13
title: 'Add URL rewriting: baseUrl, .md to .gmi, custom rewrite hook, percent-encoding'
status: To Do
assignee: []
created_date: '2026-09-13 16:13'
labels: []
milestone: m-1
dependencies:
  - TASK-11
references:
  - >-
    backlog/docs/doc-1 -
    Gemtext-conversion-research-spec-prior-art-test-corpora.md
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_base_url.py'
  - >-
    https://github.com/makew0rld/md2gemini/blob/master/tests/test_markdown_link.py
  - 'https://github.com/tdemin/gmnhg/tree/master/testdata'
priority: high
type: feature
ordinal: 13000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext link lines must carry URLs that are percent-encoded per RFC 3986, and capsule authors converting a Markdown site need to rewrite local links. Provide the three rewriting knobs md2gemini users rely on and a single hook that subsumes them: baseUrl prefixes root-relative links, mdLinks turns local .md targets into .gmi (dropping fragments, since gemtext has no anchors), and rewriteUrl(url, context) is an escape hatch that runs last and receives the link kind (link, image, autolink) and the original text. Apply the same pipeline to image sources.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Option baseUrl "https://example.com/" turns "/url" into "https://example.com/url" and leaves absolute URLs untouched (md2gemini test_base_url)
- [ ] #2 Option mdLinks true turns "foo.md" into "foo.gmi" and "foo.md#bar" into "foo.gmi", and leaves "https://x/foo.md" untouched unless option mdLinksRemote is true
- [ ] #3 Option rewriteUrl receives (url, {kind, text, title}) and its return value is used verbatim; returning null drops the link and keeps the text (md2gemini test_link_func)
- [ ] #4 A URL containing spaces or unencoded non-ASCII characters is percent-encoded in the link line, and an already-encoded URL is not double-encoded
- [ ] #5 The rewrite order is fixed and documented: mdLinks, then baseUrl, then rewriteUrl, then percent-encoding
- [ ] #6 The pipeline applies identically to image sources
<!-- AC:END -->
