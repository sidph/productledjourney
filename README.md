# Product Led Journey

Personal website and blog built with Astro.

## Running Locally

```bash
cd ~/productledjourney
npm install
npm run dev
```

Site runs at:

```text
http://localhost:4321
```

---

# Content Structure

## Blog Posts

Location:

```text
src/content/blog/
```

Each blog post should have frontmatter:

```yaml
---
title: "Post Title"
description: "Short description"
date: 2025-08-21
heroImage: "./images/cover.png"
---
```

Important:

* Use `date`, not `pubDate`
* Images referenced in markdown should exist locally
* Blog listing page reads from `date`

---

## Static Pages

Location:

```text
src/content/pages/
```

Current pages:

```text
about.md
launches.md
reading.md
```

Routes:

```text
/about
/launches
/reading
```

---

# Navigation Menu

File:

```text
src/components/Header.astro
```

Example:

```astro
<nav>
  <a href="/">Home</a>
  <a href="/blog">Blog</a>
  <a href="/about">About</a>
  <a href="/reading">Reading</a>
  <a href="/launches">Highlight Reel</a>
</nav>
```

Modify links here.

---

# Social Icons

File:

```text
src/components/Header.astro
```

SVG icons live inline in this file.

Example:

```astro
<a
  href="https://linkedin.com/in/yourprofile"
  target="_blank"
  rel="noopener noreferrer"
>
  <svg>...</svg>
</a>
```

---

# About Page

File:

```text
src/pages/about.astro
```

Main content:

```astro
<AboutPage />
```

Container width:

```astro
<main style="max-width:1200px; margin:0 auto; padding:2rem;">
```

Increase or decrease width here.

---

# Highlight Reel Page

Files:

```text
src/pages/launches.astro
src/content/pages/launches.md
```

The layout is controlled primarily inside:

```text
launches.md
```

This allows custom image/text layouts without touching Astro components.

---

# Image + Text Layouts

## 50 / 50 Split

```html
<div style="display:flex; gap:2rem; align-items:center;">
  <img
    src="/pages/images/example.png"
    style="width:50%;"
  />
  <div style="width:50%;">
    Text here...
  </div>
</div>
```

---

## Larger Image

```html
<div style="display:flex; gap:2rem;">
  <img
    src="/pages/images/example.png"
    style="width:65%;"
  />
  <div style="width:35%;">
    Text here...
  </div>
</div>
```

---

## Smaller Image

```html
<div style="display:flex; gap:2rem;">
  <img
    src="/pages/images/example.png"
    style="width:35%;"
  />
  <div style="width:65%;">
    Text here...
  </div>
</div>
```

---

## Image Width Only

```html
<img
  src="/pages/images/example.png"
  style="width:600px;"
/>
```

---

## Image Height Only

```html
<img
  src="/pages/images/example.png"
  style="height:400px;"
/>
```

---

## Stretch Image

```html
<img
  src="/pages/images/example.png"
  style="width:800px; height:300px;"
/>
```

Note: This may distort the image.

---

# Common Astro Commands

Find text:

```bash
grep -R "searchText" src
```

Find all references to pubDate:

```bash
grep -R "pubDate" src
```

---

# Nano Shortcuts

Find:

```text
Ctrl + W
```

Find next:

```text
Option + W
```

Replace:

```text
Ctrl + \
```

Save:

```text
Ctrl + O
```

Exit:

```text
Ctrl + X
```

Undo:

```text
Alt + U
```

Redo:

```text
Alt + E
```

On Mac Terminal:

```text
Alt = Option
```

---

# Common Migration Gotchas

## Blog page loads but individual posts fail

Usually caused by:

```text
pubDate
```

still being referenced somewhere.

Search:

```bash
grep -R "pubDate" src
```

Replace with:

```text
date
```

---

## Images not showing

Verify image exists:

```bash
ls public/pages/images
```

Images referenced like:

```html
<img src="/pages/images/example.png" />
```

must physically exist in:

```text
public/pages/images/
```

---

## Markdown shows raw HTML

Wrap image/text sections inside:

```html
<div>
  ...
</div>
```

instead of leaving HTML and markdown mixed together.

---

# Deployment

Local build:

```bash
npm run build
```

Preview production build:

```bash
npm run preview
```

Future deployment target:

```text
Cloudflare Pages
```

