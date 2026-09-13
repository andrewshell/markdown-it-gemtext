---
id: TASK-12
title: Render images as link lines
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
  - 'https://github.com/makew0rld/md2gemini/blob/master/tests/test_tags.py'
priority: high
type: feature
ordinal: 12000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Gemtext has no images; the convention is a link line to the image URL with the alt text as the label, optionally tagged so readers know it is an image. Images inside a paragraph follow the active link mode like any other link (in paragraph mode md2gemini skips the marker and just emits the link; match that). An image that is itself wrapped in a link ([![alt](img)](href)) must produce both the image link and the target link. The image title attribute is available as an alternative label.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 A paragraph containing only an image renders as "=> src alt [IMG]" with option imageTag defaulting to "[IMG]"
- [ ] #2 Option imageTag set to empty string renders "=> src alt", and an image with empty alt renders "=> src [IMG]" or "=> src" respectively (md2gemini test_tags cases)
- [ ] #3 An image inside a text paragraph keeps its alt text inline and emits the image link line after the paragraph in copy mode, and the same without a numeric marker in paragraph mode
- [ ] #4 An image wrapped in a link produces two link lines: the target link and the image link, in that order
- [ ] #5 Option imageLabel "alt" (default) or "title" chooses the label source, falling back to alt when title is absent
- [ ] #6 linkMode "off" drops the image link line and keeps only the alt text inline
<!-- AC:END -->
