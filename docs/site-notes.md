# Site Notes

## Project Structure

### Main Pages

| File                         | Purpose                              |
| ---------------------------- | ------------------------------------ |
| `src/pages/blog/index.astro` | Blog landing page                    |
| `src/layouts/BlogPost.astro` | Individual blog post layout          |
| `src/pages/about.astro`      | About page wrapper                   |
| `src/pages/launches.astro`   | Highlight Reel page wrapper          |
| `src/pages/reading.astro`    | Reading Recommendations page wrapper |

### Content Files

| File                            | Purpose                         |
| ------------------------------- | ------------------------------- |
| `src/content/blog/`             | Individual blog posts           |
| `src/content/pages/about.md`    | About Me content                |
| `src/content/pages/launches.md` | Highlight Reel content          |
| `src/content/pages/reading.md`  | Reading Recommendations content |

### Navigation

Navigation links and social icons live in:

`src/components/Header.astro`

Use this file to:

* Add/remove navigation items
* Change page order
* Update LinkedIn/Twitter/GitHub URLs
* Replace social icons

---

# Local Development

Run locally:

```bash
npm run dev
```

Build locally:

```bash
npm run build
```

Preview build:

```bash
npm run preview
```

---

# Deployment

Site deploys automatically from GitHub via Cloudflare.

Push changes:

```bash
git add .
git commit -m "Describe changes"
git push
```

Cloudflare automatically rebuilds.

If deployment behaves strangely:

```text
Cloudflare Pages
→ Deployments
→ Retry deployment
→ Clear build cache and retry
```

---

# Image Strategy

## Use public/pages/images

Most site images should live here:

```text
public/pages/images/
```

Reference them with:

```html
<img src="/pages/images/example.jpg" />
```

Advantages:

* Simpler
* Cloudflare-friendly
* No Astro image processing issues
* Easy to control sizing

---

## Use Astro Images For Blog Hero Images

Blog post hero images can remain in:

```text
src/content/images/
```

and be referenced through frontmatter.

Example:

```yaml
heroImage: ../../content/images/example.jpg
```

---

# About Page

Content:

```text
src/content/pages/about.md
```

Layout:

```text
src/pages/about.astro
```

Current layout uses a two-column design:

```html
<div class="intro-grid">
  <img />
  <div>
    text
  </div>
</div>
```

Adjust image width:

```html
style="width:350px;"
```

or

```css
.intro-grid img {
  width: 350px;
}
```

---

# Highlight Reel Page

Content:

```text
src/content/pages/launches.md
```

Layout Wrapper:

```text
src/pages/launches.astro
```

Most layout control happens directly inside:

```text
launches.md
```

---

# Image + Text Layouts

Most launch sections use:

```html
<div
  style="
    display:grid;
    grid-template-columns:52% auto;
    gap:3rem;
    align-items:center;
  "
>
  <img src="/pages/images/example.png" />

  <div>
    Text
  </div>
</div>
```

---

## Control Image/Text Ratio

Examples:

### Large image

```css
grid-template-columns:60% auto;
```

### Balanced

```css
grid-template-columns:50% auto;
```

### Smaller image

```css
grid-template-columns:35% auto;
```

---

## Control Individual Image Width

Example:

```html
<img
  src="/pages/images/example.png"
  style="width:700px;"
/>
```

Increase:

```html
width:900px;
```

Decrease:

```html
width:500px;
```

---

## Stretch Image Horizontally

```html
<img
  src="/pages/images/example.png"
  style="width:900px; height:auto;"
/>
```

Never set both width and height unless intentionally distorting.

---

# Blog Landing Page

File:

```text
src/pages/blog/index.astro
```

Current design:

* Card-based layout
* 3-column grid
* Featured image
* Title
* Date
* Excerpt

---

## Blog Width

Adjust:

```css
main {
  max-width: 1400px;
}
```

Wider:

```css
max-width: 1600px;
```

Full width:

```css
max-width: none;
```

---

# Individual Blog Posts

Layout file:

```text
src/layouts/BlogPost.astro
```

---

## Content Width

Current:

```css
.prose {
  width: 1000px;
}
```

Typical options:

```css
800px
1000px
1200px
```

---

## Hero Image Size

Current:

```css
.hero-image img {
  width: 800px;
}
```

Smaller:

```css
width: 600px;
```

Larger:

```css
width: 1000px;
```

---

## Center Hero Images

```css
.hero-image img {
  display: block;
  margin: 0 auto;
}
```

---

# Reading Recommendations Page

Content:

```text
src/content/pages/reading.md
```

Layout:

```text
src/pages/reading.astro
```

---

## Quotes

Use blockquotes:

```md
> Happiness and the theory of relativity...
```

Styling lives in:

```text
reading.astro
```

Example:

```css
blockquote {
  border-left: 4px solid #3b5cff;
  padding-left: 2rem;
  font-style: italic;
}
```

---

## Quote Width

Adjust:

```css
blockquote {
  max-width: 900px;
}
```

Narrower:

```css
max-width: 700px;
```

Wider:

```css
max-width: 1200px;
```

---

# Social Icons

File:

```text
src/components/Header.astro
```

Replace SVG:

```html
<a href="https://linkedin.com/in/your-profile">
  <img src="/pages/images/linkedin.svg" />
</a>
```

Icons generally live in:

```text
public/pages/images/
```

---

# Useful Search Commands

Find image references:

```bash
grep -R "img" src
```

Find image paths:

```bash
grep -R "images/" src
```

Find hero images:

```bash
grep -R "heroImage" src
```

Find old Astro starter fields:

```bash
grep -R "pubDate" src
```

Find page width settings:

```bash
grep -R "max-width" src
```

---

# Nano Shortcuts

Search:

```text
Ctrl + W
```

Search next:

```text
Alt + W
```

Save:

```text
Ctrl + O
```

Exit:

```text
Ctrl + X
```

Cut line:

```text
Ctrl + K
```

Paste:

```text
Ctrl + U
```

Undo:

```text
Alt + U
```

Redo:

```text
Alt + E
```

---

# Common Issues

## Broken Blog Pages

Usually caused by:

```text
pubDate vs date
```

Search:

```bash
grep -R "pubDate" src
```

---

## Missing Images On Cloudflare

Use:

```html
<img src="/pages/images/example.jpg" />
```

instead of relative paths.

Cloudflare is case-sensitive.

---

## Hero Images Not Showing

Check:

```yaml
heroImage:
```

exists in blog frontmatter and points to a valid file.

---

## Weird Cloudflare Behavior

Try:

```text
Clear build cache and retry deployment
```

before spending time debugging.

---

OLD

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
