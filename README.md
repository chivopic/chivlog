# chivlog

> Deliberately minimal. Text-first. Markdown over machinery.

A personal blog for thoughts, notes, and writing by [Chiv](https://github.com/chivopic) — almost no UI chrome, no CMS, no unnecessary JavaScript.

**Live:** [https://chivlog.vercel.app](https://chivlog.vercel.app)

[![Astro](https://img.shields.io/badge/Astro-static-BC52EE)](https://astro.build)
[![Markdown](https://img.shields.io/badge/Markdown-first-000000)](https://www.markdownguide.org)
[![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000)](https://chivlog.vercel.app)

## What it is

chivlog is a writing home: posts about building with AI, developer tools, systems, security, and notes worth keeping. The site stays small on purpose so reading and publishing stay out of the way.

## Why / design principles

- **Text-first** — content over chrome; plain CSS, almost no client JavaScript
- **Markdown-first** — posts are files in the repo, not rows in a CMS
- **No bloat** — static Astro output; no database, no auth, no newsletter stack
- **Readable by default** — home, posts, categories, about — and a quiet inbox for small scraps

## What you get

| For visitors | What it means |
| --- | --- |
| Recent writing on home | Latest posts (inbox items excluded) with date, title, and summary |
| Full post archive | `/posts` lists everything publishable |
| Categories | `/categories` groups posts by frontmatter tags |
| About | Who Chiv is and what this site is for |
| Inbox | Footer link to short “things worth keeping” entries |
| Fast static site | Prebuilt HTML on Vercel |

## Stack

- **Astro** (`output: 'static'`) — pages and Markdown posts
- **Markdown** — frontmatter for title, description, date, categories
- **Plain CSS** — `src/styles/global.css`
- **Vercel** — production host; pushes to `main` deploy automatically

```text
Markdown posts (src/pages/posts/)
        │
        ▼
   Astro static build
        │
        ▼
     dist/  →  Vercel
```

## For contributors / writing

### Local development

```bash
npm install
npm run dev
```

### Writing a post

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

Posts show up on home, `/posts`, and `/categories`. Use the `inbox` category for short scraps listed on `/inbox` (hidden from the main post lists). Templates live in `templates/` (`daily-review.md`, `inbox-entry.md`).

### Build

```bash
npm run build
```

Static output lands in `dist/`. Preview with `npm run preview`.

### Deployment

Connected to Vercel. Pushes to `main` trigger production deployments automatically.

---

Built to stay small: easy to read, easy to write, hard to accidentally complicate.