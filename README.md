# chivlog

A deliberately minimal, text-first personal blog built with Astro and Markdown.

## Stack

- Astro
- Markdown
- plain CSS
- Vercel

## Local development

```bash
npm install
npm run dev
```

## Writing

Create a Markdown file in `src/pages/posts/`:

```md
---
layout: ../../layouts/PostLayout.astro
title: "Post title"
description: "Short summary"
date: 2026-09-07
categories:
  - notes
---

Your post starts here.
```

Posts are automatically listed on the home, posts, and categories pages.

## Build

```bash
npm run build
```

The static site is generated into `dist/`.
