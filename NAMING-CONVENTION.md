# File Naming Convention — `assets/` and `source-manuals/`

Applied to every file in `assets/` (199 files) and `source-manuals/` (173 files) in August 2026. New files should follow this same pattern so the folders stay searchable and self-explanatory without opening the guide.

## The pattern

```
<product-or-family-slug>_<content-descriptor>.<ext>
```

One underscore, always — it separates *what product this is* from *what this file actually shows*. Everything else is hyphens, all lowercase, no spaces.

**Examples:**
- `pcr-1z-sm_labeled-board-diagram.jpg` — PCR-1Z-SM driver, a labeled board diagram
- `treo-max-plus-v2_product-photo.jpg` — Treo Max+ (V2), the product photo
- `custom-strip_safe-cut-point-diagram.jpg` — applies across the whole Custom Strip family, not one SKU
- `waterblade_install-instructions.pdf` — Waterblade, the install instructions PDF

## Choosing the product slug

1. **Use the SKU** when the file is tied to one specific part number: `pcr-2dmx`, `64-pctwf03`.
2. **Use the product name** when there's no clean single SKU or the card covers a SKU family: `treo-mini-plus-v2`, `sonar-retro-bulb`.
3. **Use the product family** when one file is genuinely shared across many cards (common with Custom Strip diagrams — the same cross-section or cut-point diagram appears on 9 different SKU cards): `custom-strip`, `perimeter-strip-kit`.

When in doubt, match whatever the guide's own `alt` text already calls the product — it's almost always already right there in `index.html`.

## Content descriptor vocabulary

Keep it to these recurring terms so files sort and scan predictably:

| Descriptor | Use for |
|---|---|
| `product-photo` | A real photo of the product |
| `hero-photo` | The photo used as the card's header/tile image |
| `install-guide`, `install-instructions` | Full install manual PDFs |
| `owners-manual` | Owner-facing manual PDFs |
| `spec-sheet` | Spec sheet PDFs |
| `sales-sheet`, `sell-sheet`, `brochure` | Marketing PDFs |
| `cloning-reference` | DIP switch / cloning tables |
| `dip-table`, `board-diagram` | Diagrams from a manual, not real photos |
| `wiring-diagram` | Wiring/connection diagrams |
| `dimensions-diagram` | Dimension/measurement diagrams |
| `install-diagram` | Step diagrams for a specific install scenario |
| `product-guide` | General reference PDF that isn't strictly an install guide |

If a file is one of a numbered series (e.g. multi-page install instructions, or several similar diagrams for the same product), add `-1`/`-2`/`-a`/`-b` etc. at the end rather than inventing a new descriptor for each.

## Two exceptions

- **`assets/PAL-Lighting.png`** — the site logo, referenced directly in `index.html`'s HTML header, not the `DATA` array. Left as-is; it was already clearly named and touching it isn't worth the churn.
- **Files prefixed `unused-`** — about 60 files in `assets/` aren't linked from any card (leftovers from the original PDF/manual extraction). They're named the same way but with `unused-` glued onto the front of the product slug, e.g. `unused-bubbler_product-photo.jpg`. That prefix means: *nothing in the guide currently points at this file.* Before deleting any of them, search `index.html` for the file to confirm — some may be worth linking into a card someday rather than deleting.

## Folder structure

Unchanged. Only filenames were touched — `source-manuals/` keeps its per-product folders (some with spaces in the names, which is fine; the app already handles that). Don't feel obligated to also "clean up" folder names to match this convention — that's a separate, much bigger change that would touch every path in the guide for no real benefit.

## When you add a new file

1. Drop it in the right `source-manuals/` subfolder (create one if the product is new).
2. Rename it to `<product-slug>_<descriptor>.<ext>` before or after — either works, just do it before telling Claude to build the card, so the reference gets written correctly the first time.
3. Tell Claude what it is. It'll wire up the card and confirm the path resolves before anything goes live.
