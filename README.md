# My Digital Memories

A digital memory & scrapbook for anyone who loves collecting gifts and cards from friends, memorabilia from trips, and the small paper things that are easy to lose. Letters, postcards, receipts, tickets, photos, notes, stickers — kept in one place, browsable, and viewable in an interactive 3D flip.

**[Live demo →](#)** *(add your GitHub Pages URL here once deployed)*

---

## Features

- **Add keepsakes** with a front photo, optional back photo, date, who it's from, location, and notes
- **Interactive 3D card viewer** — drag any item to spin it and see the back; the flip UI automatically hides for items that only have a front
- **HEIC support** — iPhone photos convert in-browser automatically, no app or plugin needed
- **Background eraser** — tap the background in a photo to remove it, fully offline; items with a removed background render as free-floating cutouts (drop shadow following the actual shape) instead of sitting in a photo frame
- **Categories & filtering** — Letter, Postcard, Receipt, Ticket, Photograph, Note, Sticker, Other; filter chips only appear once you have enough items to need them (>8)
- **Sort & reorder** — by date added, date received, or drag your own custom order
- **Soft sound cues** on add / delete / flip
- **Everything runs client-side** — no server, no account, no API keys

## How it works

This is a single self-contained `index.html` file — no build step, no dependencies to install. Everything is inlined:

- **UI & logic** — vanilla JS, no framework
- **HEIC → JPEG conversion** — [`libheif-js`](https://github.com/catdad-experiments/libheif-js), bundled inline so it works offline
- **Background removal** — a canvas-based flood-fill "magic wand": tap a pixel, it erases contiguous similar-colored pixels around it (adjustable sensitivity), fully offline — no AI model, no network call
- **3D card** — CSS 3D transforms (`perspective` / `rotateY`) driven by the Pointer Events API
- **Storage** — the browser's `localStorage`, wrapped in a small shim so the exact same code also runs unmodified inside Claude's artifact environment (which provides its own storage API)
- **Fonts** — Recoleta (display) + Inter (UI), both embedded as base64 so the page needs zero external requests to render

## Deploying your own copy

1. Put `index.html` in the root of your repo (not a subfolder)
2. Commit and push to your main branch
3. In the repo: **Settings → Pages → Source: "Deploy from a branch"** → pick `main` and `/ (root)` → Save
4. Your live URL will be `https://your-username.github.io/your-repo-name/`

No build tooling, no environment variables, no config needed.

## Running locally

Just open `index.html` directly in a browser — double-click it, or:

```bash
open index.html        # macOS
start index.html        # Windows
```

## Known limitations

- **Storage is per-browser, not synced.** Data lives in that browser's `localStorage` on that one device. Clearing browser data or switching browsers/devices means a fresh, empty archive. There's no account system and no backend — this is a local-first prototype, not a multi-device app (yet — see Roadmap).
- **It's public once deployed.** Anyone with the link can open the page and add their own items, but nobody's data is shared with anyone else — each visitor gets their own separate local copy.
- **Recoleta font is a demo/trial build.** It only covers a limited glyph set. Get the fully licensed file from Latinotype before treating this as a finished brand asset.
- **Background eraser is heuristic, not AI.** It works well on flat items with a fairly uniform background (like a receipt on a solid backdrop) and less well on busy or gradient backgrounds (wrinkled fabric, shadows) — you may need a few taps and a sensitivity adjustment.
- **Storage quota.** `localStorage` typically caps around 5–10MB per browser. Since photos are compressed before saving, this comfortably fits dozens of items, but very large collections may eventually need a real backend.

## Roadmap

Pulled from the original brand brief, roughly in order:

**v1**
- Folders (create/organize items into folders)
- Tags & filtering
- Favorites
- "Locked" items (things you only want to see when you choose to)

**v2**
- A 3D "memory box" you can open on a set date, years later
- Reminders ("you received this a year ago")

## Credits

Brand, logo, color system, and product direction by [you]. Built with Claude.
