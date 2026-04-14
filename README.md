# CaneToadFL — Astro Site

South Florida cane toad removal lead generation site.

---

## Quick Start (First Time)

You need Node.js installed. Check with: `node --version`
If you don't have it: download from https://nodejs.org (LTS version)

### 1. Install dependencies
```bash
cd canetoadfl
npm install
```

### 2. Run locally
```bash
npm run dev
```
Open http://localhost:4321 in your browser. You'll see the live site.
Any file you save auto-refreshes the browser instantly.

### 3. Build for production
```bash
npm run build
```
This creates a `dist/` folder with the fully built site.

---

## How to Add / Edit Pages

### Edit an existing page
Open any file in `src/pages/` in VS Code and edit the content directly.
The layout (header, nav, footer, styles) lives in `src/layouts/BaseLayout.astro` — edit that once and it updates everywhere.

### Add a new page
1. Create a new folder in `src/pages/` — e.g. `src/pages/cane-toad-florida/`
2. Create `index.astro` inside it
3. Copy the structure from an existing page and replace the content
4. The URL will be `/cane-toad-florida/` automatically

### Reusable content components
- `src/components/ContentToc.astro` — standardized table of contents block

### Page structure (copy this template)
```astro
---
import BaseLayout from '../../layouts/BaseLayout.astro';
import ContentToc from '../../components/ContentToc.astro';
---

<BaseLayout
  title="Your SEO Title Here | CaneToadFL"
  description="Your meta description — 150-160 characters, include target keyword."
>

  <div class="hero">
    <h1>Your H1 Here</h1>
    <p>Intro paragraph.</p>
    <a href="#get-quote" class="btn btn-lg">Get a Free Quote →</a>
  </div>

  <!-- Paste your Tally form embed here -->

  <div class="content">
    <ContentToc
      title="Quick Links"
      items={[
        { href: '#section-1', label: 'Section 1' },
        { href: '#section-2', label: 'Section 2' },
      ]}
    />

    <h2>Section Heading</h2>
    <p>Content here...</p>
  </div>

</BaseLayout>
```

---

## Deploying to Cloudflare Pages (Free Hosting)

1. Push this folder to a GitHub repo (free at github.com)
2. Go to pages.cloudflare.com → Create a project → Connect GitHub repo
3. Build settings:
   - Build command: `npm run build`
   - Build output directory: `dist`
4. Click Deploy — your site is live in ~60 seconds
5. Every time you push to GitHub, Cloudflare auto-rebuilds and republishes

---

## Adding Your Tally Forms

1. Go to tally.so and create a free account
2. Create your lead capture form (Name, Phone, Address, "Describe what you're seeing")
3. Click Share → Embed → copy the iframe code
4. In each page file, find the `tally-placeholder` div and replace it with your iframe

---

## File Structure

```
canetoadfl/
├── astro.config.mjs          ← site URL config
├── package.json              ← dependencies
├── src/
│   ├── components/
│   │   └── ContentToc.astro      ← reusable TOC section
│   ├── layouts/
│   │   └── BaseLayout.astro  ← header, footer, styles (edit once, applies everywhere)
│   └── pages/
│       ├── index.astro                        ← Homepage (/)
│       ├── cane-toad-removal/index.astro      ← /cane-toad-removal/
│       └── providers/index.astro              ← /providers/
└── public/                   ← images, favicon (drop files here, reference as /filename.png)
```

---

## Content Calendar Status

All pages in the current PRD content calendar are now built.
Use `toad_PRD.md` as the source of truth for priority updates and future phase expansion.
