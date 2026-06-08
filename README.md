# GearVault Deals v2 — Setup Guide

A rebuilt, conversion-focused affiliate review site for Northeast bass anglers.
Built with Hugo + PaperMod.

---

## What's Included

```
gearvault-v2/
├── hugo.toml                          ← Site config
├── content/
│   ├── _index.md                      ← Homepage placeholder
│   ├── reviews/_index.md              ← Reviews section index
│   ├── best-budget-bass-combos-under-150.md
│   ├── best-ultralight-spinning-combos-under-150.md
│   ├── best-bass-fishing-rods-under-100.md
│   ├── best-spinning-reels-under-100-bass.md
│   ├── how-to-choose-ultralight-rod-for-bass.md
│   ├── best-chatterbaits-for-bass.md
│   ├── best-ned-rig-setups-smallmouth.md
│   ├── best-football-jigs-quabbin-reservoir.md
│   ├── best-budget-fish-finders-kayak-shore.md
│   └── how-to-choose-fishing-line-for-bass.md
├── layouts/
│   ├── index.html                     ← Custom homepage
│   ├── _default/single.html           ← Article layout (no title dupe)
│   ├── reviews/list.html              ← Reviews page layout
│   └── partials/extend_head.html      ← Injects custom CSS
├── static/
│   ├── css/gearvault.css              ← All custom styles
│   └── images/
│       ├── hero-fishing.jpg
│       ├── combo.jpg
│       └── ultralight.jpg
└── themes/
    └── PaperMod/                      ← Install separately (see Step 2)
```

---

## Quick Setup (5 minutes)

### Step 1 — Install Hugo

**Mac (Homebrew):**
```bash
brew install hugo
```

**Windows (Chocolatey):**
```bash
choco install hugo-extended
```

**Linux:**
Download the latest extended binary from https://github.com/gohugoio/hugo/releases
and place it in `/usr/local/bin/`.

Verify: `hugo version`

### Step 2 — Install PaperMod Theme

Inside the `gearvault-v2` folder:

```bash
cd gearvault-v2
git init
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

Or download and unzip PaperMod manually:
1. Go to https://github.com/adityatelange/hugo-PaperMod
2. Click Code → Download ZIP
3. Unzip and rename the folder to `PaperMod`
4. Place it at `themes/PaperMod/`

### Step 3 — Run the Dev Server

```bash
cd gearvault-v2
hugo server -D
```

Open http://localhost:1313 in your browser.

### Step 4 — Build for Production

```bash
hugo --minify
```

Output goes to the `public/` folder. Upload contents of `public/` to your hosting.

---

## URL Structure

All articles are at flat URLs for clean, SEO-friendly paths:

| Article | URL |
|---------|-----|
| Best Budget Bass Combos | `/best-budget-bass-combos-under-150/` |
| Best Ultralight Combos | `/best-ultralight-spinning-combos-under-150/` |
| Best Bass Rods Under $100 | `/best-bass-fishing-rods-under-100/` |
| Best Spinning Reels Under $100 | `/best-spinning-reels-under-100-bass/` |
| How to Choose an Ultralight Rod | `/how-to-choose-ultralight-rod-for-bass/` |
| Best Chatterbaits | `/best-chatterbaits-for-bass/` |
| Best Ned Rig Setups | `/best-ned-rig-setups-smallmouth/` |
| Best Football Jigs — Quabbin | `/best-football-jigs-quabbin-reservoir/` |
| Best Budget Fish Finders | `/best-budget-fish-finders-kayak-shore/` |
| How to Choose Fishing Line | `/how-to-choose-fishing-line-for-bass/` |
| Reviews Hub | `/reviews/` |

---

## The Editorial Redesign (v3)

The site now uses a distinctive **editorial-magazine** look rather than the default PaperMod blog layout:

- **Custom masthead** (`layouts/partials/header.html`) fully replaces PaperMod's centered nav — left-aligned logo + tagline, "GV" mark badge, right-side nav with a rust CTA button, and a forest-green top rule. PaperMod's default nav and footer are hidden via CSS.
- **Full-bleed hero** — the headline now sits *over* a full-width edge-to-edge photo with a dark gradient scrim (not a floating image box). Left-aligned, asymmetric, magazine-style.
- **Asymmetric homepage** — one large "lead guide" beside a stack of two smaller cards, instead of a symmetric row.
- **Editorial reviews index** — numbered categories (01–04) with large, clickable list rows and hairline rules, like a magazine contents page.
- **New type system** — `Fraunces` (a high-contrast display serif) for headlines + `Archivo` (a clean grotesk) for body and UI. Drop-cap on the first paragraph of each article.
- **New palette** — warm cream paper, deep forest green, and a rust-orange accent. Reads as a trusted field-guide, not a generic template.

### Swapping the hero image (recommended)

The hero currently uses your existing `static/images/hero-fishing.jpg` so the site works immediately. For a more eye-catching, relevant hero, replace that file with a bass-in-hand action shot:

1. Download a free-to-use photo — e.g. this smallmouth bass catch on Pexels (free for commercial use, no attribution required):
   `https://www.pexels.com/photo/a-caught-smallmouth-bass-13615156/`
   (click **Free download**, choose a large size)
2. Rename the downloaded file to **`hero-fishing.jpg`**
3. Drop it into `static/images/`, replacing the existing file
4. That's it — the hero updates automatically. No code changes needed.

If you want to point the hero at a *different* filename instead, edit one line in `static/css/gearvault.css`:
```css
.gv-hero { background-image: url('/images/YOUR-FILE.jpg'); }
```

### What was fixed earlier (vs. the original v1)

| Problem | Fix |
|---------|-----|
| Title duplication on article pages | Custom `single.html` renders the title once; PaperMod's default is bypassed |
| Escaped characters in frontmatter (`\---`, `\#`) | All articles rewritten with clean YAML frontmatter |
| Windows line endings (\r\n) breaking Hugo | All files saved with Unix line endings |
| Empty, unstructured article pages | Editorial `single.html` with standfirst, drop-cap, styled tables and headings |
| Reviews page was a plain list | Numbered editorial index with large clickable rows |
| Homepage felt basic and bloggy | Full-bleed hero + asymmetric featured layout + horizontal trust band |
| No professional affiliate disclosure | Auto-injected on every article via `single.html` |
| Weak header / stray theme toggle | Custom masthead; theme toggle disabled in `hugo.toml` |

---

## Adding New Articles

1. Create a new `.md` file in `content/`
2. Use this frontmatter template:

```yaml
---
title: "Your Article Title"
description: "Meta description for SEO (150–160 chars)"
date: 2026-06-04
draft: false
tags: ["tag one", "tag two"]
---
```

3. Write body content in standard Markdown (no `# Title` at the top — the layout handles that)
4. Add the article to `layouts/reviews/list.html` in the appropriate category section

---

## Deployment Options

**Netlify (Recommended — free):**
1. Push to GitHub
2. Connect repo to Netlify
3. Build command: `hugo --minify`
4. Publish directory: `public`

**GitHub Pages:**
Use the Hugo GitHub Actions workflow: https://gohugo.io/hosting-and-deployment/hosting-on-github/

**Shared Hosting (FTP):**
Run `hugo --minify` locally, then upload contents of `public/` via FTP.

---

## Adding Affiliate Links

Replace placeholder product mentions with real affiliate links using standard Markdown:

```markdown
The [Pflueger President XT](https://www.amazon.com/dp/YOUR-ASIN?tag=yourtag-20) 
is the reel I recommend to most people at this price.
```

For Amazon Associates, your tag goes in the URL: `?tag=yourassociatetag-20`

---

*GearVault Deals — Honest gear for Northeast bass anglers.*
