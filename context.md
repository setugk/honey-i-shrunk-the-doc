# Honey I Shrunk the Doc — Project Context

> **Read `../constitution/constitution.md` first** for universal conventions.

## What is this?
A simple tool for combining photos and documents into one small, compressed PDF — built for non-technical users who need to upload documents to portals with file size limits.

## Product pitch
- Upload photos or PDFs, put them in order, pick a size, download one PDF
- No accounts, no cloud, no data leaves the device
- Works on mobile and desktop
- Simple enough for anyone

## Tech
- Single-file PWA: everything in `index.html` (HTML, CSS, vanilla JS)
- Dark theme with CSS variables
- Libraries loaded from CDN: PDF.js (rendering existing PDFs to canvas), jsPDF (creating output PDF)
- No build step, no server

## Repo
- GitHub: https://github.com/setugk/honey-i-shrunk-the-doc
- Branch: `main`
- Deployment: Cloudflare Pages (auto-deploy from main)
- URL: shrink.setugk.com (DNS TBD)

## File structure
```
Honey I Shrunk the Doc/
  index.html        # The entire app
  manifest.json     # PWA config
  icon-192.png      # App icon (192x192)
  icon-512.png      # App icon (512x512)
  .gitignore        # Ignores docs/
  context.md        # This file
  docs/
    build-log.md    # Version history
```

## Current version
v1.5

## Design tokens
```
--bg: #0a0a0b
--surface: #18181b
--surface-hover: #27272a
--text-primary: #ffffff
--text-secondary: #a1a1aa
--accent: #818cf8
--success: #4ade80
--danger: #f87171
--border: #3f3f46
--radius: 16px
```

## App flow
1. Upload zone (compact when files present) — camera button + add files button + drag/drop
2. File list — numbered thumbnails with ↑ ↓ reorder and × remove
3. Size selector — Small (~1MB), Medium (~2MB, default), Large (~4MB)
4. Create PDF button
5. Processing spinner with status text
6. Download section with file size shown

## Key technical decisions
- Images compressed via canvas (quality + maxWidth per preset)
- Existing PDFs rendered to canvas per page via PDF.js, then compressed as images
- jsPDF creates output PDF with compress:true flag
- Page dimensions match source aspect ratio (A4 width as base)
- All processing client-side, zero network requests after page load

## Compression presets
| Preset | JPEG Quality | Max Width |
|--------|-------------|-----------|
| Small  | 0.45        | 1200px    |
| Medium | 0.65        | 1800px    |
| Large  | 0.80        | 2400px    |

## Project-specific conventions
- No version constant in the app (no visible version to users)
- No localStorage (single-session tool, nothing persists)
- Icons are basic placeholders — replace with proper design when ready
