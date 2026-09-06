---
layout: ../../layouts/PostLayout.astro
title: "Hello, chivlog"
description: "Why this blog is intentionally small, plain, and text-first."
date: 2026-09-06
categories:
  - meta
  - building
---

This is the first post on **chivlog**.

I wanted a blog that feels closer to a document than an app: a narrow column, normal links, readable typography, and almost nothing competing with the words.

## Principles

- content before components
- Markdown before CMS
- static pages before runtime complexity
- links should look like links
- fast enough that performance is boring

## Writing a new post

Create another Markdown file under `src/pages/posts/` and add frontmatter like this:

```yaml
---
layout: ../../layouts/PostLayout.astro
title: "My new post"
description: "One sentence about the post."
date: 2026-09-07
categories:
  - ai
  - notes
---
```

The home page, posts page, and categories page discover Markdown posts automatically at build time.
