# PAL Tech Support Troubleshooting Guide

Internal support-team reference for PAL Lighting. Support reps use it live, on calls with customers. Maintained by the CX Manager (not a developer) entirely through Claude conversations — assume the user cannot read or write code, and never ask them to edit files by hand.

## Architecture

- `index.html` is the **entire application** — a client-rendered page driven by a `DATA` array of category/product objects defined inline. No build step, no dependencies, no other HTML/JS/CSS files.
- `source-manuals/` holds source PDFs and images, organized by category subfolders that roughly mirror the guide's categories. Cards link into it directly (paths with spaces are fine — the app runs `encodeURI` on links and image paths).
- `assets/` holds images extracted from manuals, referenced by cards.
- **Every file in both folders follows the naming convention in [NAMING-CONVENTION.md](NAMING-CONVENTION.md): `<product-or-sku-slug>_<content-descriptor>.<ext>`.** Name new files this way before wiring them into a card — don't leave generic names like `image_47.jpg` or `Scan001.pdf`. Read that file before naming anything if the pattern isn't obvious from nearby files in the same folder.
- Deploys via GitHub Pages from `main` on `PAL-CX/PAL-TS-GUIDE_v2` to https://pal-cx.github.io/PAL-TS-GUIDE_v2/ — a push to `main` is a production deploy, live within ~2 minutes.

## The update workflow (follow this every time)

1. **Never commit or push without the user's explicit approval.** The approval phrase is some form of "push and commit live" / "go ahead." Preview iterations are unlimited; publishing is gated.
2. **Preview before approval.** Copy `index.html` to a `_preview-*.html` file, make the edits there, serve locally (`python3 -m http.server`), screenshot the changed cards with headless Chrome (`/Applications/Google Chrome.app/Contents/MacOS/Google Chrome --headless --screenshot=...`), and send the user **tight crops of just the changed content** — not full pages. A small `_shot.html` iframe harness that drives the app's own search + card click works well for opening a specific card headlessly.
3. **After approval:** copy the preview over `index.html`, delete the preview/harness files, stage only the files that belong to the change (`index.html` + any new source-manual files it references), commit with a descriptive message, push to `origin main`.
4. New source documents the user drops into `source-manuals/` should be committed alongside the card changes that reference them.
5. When asked to check links/photos: verify against the **live site** (HTTP status of every `url:`/`src:`/`hero:` reference in the DATA array), not just the local filesystem — the difference between "file missing locally" and "file never pushed" matters.

## Writing style — hard rules

- **No AI/hype language anywhere in card content**: no "seamless," "robust," "leverage," "cutting-edge," "unlock," "elevate," "isn't just X, it's Y," no throat-clearing ("it's worth noting").
- **No maintainer meta-talk in the guide.** Notes about the guide's own gaps ("no photos exist yet," "someone should document X") belong in chat with the user, never in card content. Every note must help a rep on a live call.
- Plain, utilitarian, technical-writer voice. The reader is a support rep mid-call, often relaying steps to a homeowner over the phone.
- Homeowner-facing script content (where it exists) uses plain language a non-technical customer understands — no jargon.

## Content conventions

- Cards live in the `DATA` array grouped by category (`id: "cat-..."`). Reference-style cards (comparisons, charts, cheat sheets) sit alongside product cards in the relevant category.
- Card fields in use: `name`, `sku`, `status`, `tags`, `blurb`, `summary`, `links`, `facts`, `steps`, `warnings`, `notes`, `tables`/`table`, `images`, `hero`, `flowImage`. Copy the structure of an existing similar card rather than inventing new fields.
- Tags power the filter chips — reuse existing tags (check the filter row) before adding new ones.
- Keep image `alt` text and captions descriptive; captions should say what the rep is looking at and note when a diagram is a manufacturer drawing rather than a real photo.

## Git

- Remote `origin` = `PAL-CX/PAL-TS-GUIDE_v2` (production). Work directly on `main`.
- Stage precisely — the working tree often contains draft files (`_preview-*`, `_print-*`, `DRAFT-*`) that must stay uncommitted unless the user says otherwise.
- `.DS_Store` is gitignored.
