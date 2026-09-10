# chivlog

**A deliberately minimal, text-first personal blog.**

Thoughts, notes, and writing by [Chiv](https://github.com/chivopic) — almost no UI chrome, no CMS, and no unnecessary JavaScript. Built to stay small so reading and publishing stay out of the way.

**[Read the live site →](https://chivlog.vercel.app)**

[![Astro](https://img.shields.io/badge/Astro-static-BC52EE)](https://astro.build)
[![Markdown](https://img.shields.io/badge/Markdown-first-000000)](https://www.markdownguide.org)
[![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000)](https://chivlog.vercel.app)

---

## What it is

chivlog is a quiet writing home on the web: posts about building with AI, developer tools, systems, security, and notes worth keeping. It is closer to a document than an app — a narrow column, normal links, readable typography, and almost nothing competing with the words.

## Who it’s for

- **Readers** who want clear writing without popups, feeds, or dashboard noise
- **Portfolio visitors** looking at how a small static site can feel finished
- **Writers** who prefer Markdown files in git over a CMS

## Design philosophy

| Principle | Practice |
| --- | --- |
| **Text-first** | Content over chrome; plain CSS; almost no client JavaScript |
| **Markdown-first** | Posts are files in the repo, not rows in a database |
| **No bloat** | Static Astro output — no database, auth, or newsletter stack |
| **Readable by default** | Home, posts, categories, about — plus a quiet inbox for scraps |

## Experience

| On the site | What you get |
| --- | --- |
| **Home** | Latest posts (inbox excluded) with date, title, and summary |
| **`/posts`** | Full archive of publishable writing |
| **`/categories`** | Posts grouped by frontmatter tags |
| **`/about`** | Who Chiv is and what this site is for |
| **`/inbox`** | Short “things worth keeping” entries (footer link) |
| **Static host** | Prebuilt HTML on Vercel — fast by construction |

## How posts work

Every post is a Markdown file under `src/pages/posts/`. Frontmatter carries the metadata Astro needs to render and list it:

- **`layout`** — shared post layout
- **`title`** / **`description`** — display title and short summary
- **`date`** — used for sorting and archive display
- **`categories`** — tags for `/categories`; the special `inbox` category keeps short scraps on `/inbox` and off the main lists

Starter shapes for daily reviews and inbox entries live in `templates/`. Push to `main` and Vercel deploys the static site automatically.

## Stack (light)

- **[Astro](https://astro.build)** — `output: 'static'`; pages and Markdown posts
- **Markdown** — content and frontmatter in the repo
- **Plain CSS** — `src/styles/global.css`
- **[Vercel](https://vercel.com)** — production host

```text
Markdown posts (src/pages/posts/)
        │
        ▼
   Astro static build
        │
        ▼
     dist/  →  Vercel
```

---

**[Visit chivlog.vercel.app](https://chivlog.vercel.app)** — built to stay small: easy to read, easy to write, hard to accidentally complicate.