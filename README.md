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

## Deploying to Cloudflare Pages (GitHub)

Repo: connect this GitHub repository in the Cloudflare dashboard. The first “connect Git” step may not show build fields; set them **after** the project is created.

1. [Cloudflare Dashboard](https://dash.cloudflare.com/) → **Workers & Pages** → your **Pages** project (not a generic Worker).
2. **Settings** → **Builds** (or **Build** / build configuration, depending on UI):
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
   - **Root directory:** leave empty (repo root).
3. **Settings** → **Variables and Secrets** (or **Environment variables**):
   - Set **`NODE_VERSION`** = **`22`** (or **`22.14.0`**) for Production and Preview. **Astro 6 requires Node `>=22.12.0`**; Node 20 will fail at `astro build`.
   - If you previously set `NODE_VERSION=20`, **change or remove** it so it does not override **`.node-version`** in the repo.
   - This repo includes **`.node-version`** (currently `22.14.0`) for local and CI consistency.
4. **Custom domains:** attach `canetoadfl.com` (and use **Rules → Redirect Rules** if you want `www.canetoadfl.com` → `https://canetoadfl.com`).
5. Every push to the connected production branch triggers a new build.

Official reference: [Cloudflare Pages — Build configuration](https://developers.cloudflare.com/pages/configuration/build-configuration/) (Astro preset uses `npm run build` and `dist`).

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
