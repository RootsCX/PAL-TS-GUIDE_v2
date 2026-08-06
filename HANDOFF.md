# PAL Troubleshooting Guide — Handover Guide

**For:** Incoming CX Manager, PAL Lighting
**From:** Cory Bradley (collaborator on the GitHub repo through September)
**What this covers:** How to keep the team's troubleshooting guide updated using Claude, without writing any code.

---

## 1. What you're inheriting

The troubleshooting guide is a single web page the support team uses on live calls:

- **Live site:** https://pal-cx.github.io/PAL-TS-GUIDE_v2/
- **Where it lives:** a GitHub repository called `PAL-TS-GUIDE_v2` (you're now the owner)
- **The folder you were given** is a working copy of that repository. Everything in it syncs to GitHub, and GitHub automatically publishes it to the live site. When a change is "pushed," the live site updates itself within a minute or two. There is no separate publishing step and nothing else to maintain.

Inside the folder, only two things matter to you:

| Item | What it is |
|---|---|
| `index.html` | The entire guide — every card, every note. **Claude edits this, you never do.** |
| `source-manuals/` | The library of PDFs, manuals, and photos, organized in folders by product category. **This is the only place you'll add files yourself.** |
| `NAMING-CONVENTION.md` | How every file in `source-manuals/` and `assets/` is named — e.g. `treo-max-plus-v2_product-photo.jpg`. Skim it once; Claude follows it automatically when adding files, so you mostly just need to know it exists. |
| `FILE-INDEX.md` | One-line description of every file already in the repo — what it is, not just what it's named. Useful when you're not sure whether a document already exists before asking Claude to find or add one. |

You will never open or edit `index.html` directly. You describe changes to Claude in plain English, review screenshots, and approve. That's the whole job.

---

## 2. One-time setup (do this once, ~15 minutes)

1. **Install the Claude desktop app** (claude.ai/download) and sign in. You'll use Claude Code — the mode that can work with folders on your computer.
2. **Open the guide folder in Claude.** Start a session and point it at the folder you were given. Claude will automatically read the project instructions file (`CLAUDE.md`) inside the folder and know how everything works — you don't have to explain anything.
3. **Connect GitHub so pushes work from chat.** Paste this into your first Claude session:

   > Help me sign in to GitHub from this computer so you can push changes for me. I own the repo PAL-CX/PAL-TS-GUIDE_v2. Walk me through it one step at a time — I'm not a developer.

   Claude will walk you through a one-time login (it uses a tool called the GitHub CLI — you'll approve the login in your web browser once). After that, your computer stays authorized: **you will not need to log in to GitHub again** for day-to-day updates. Claude commits and pushes for you from chat, with your approval each time.

That's it. From here on, every update is just a conversation.

---

## 3. The two ways updates come in — and what to do with each

This is the most important habit to build. Updates arrive from the team in two forms:

### A. Someone hands you a document (PDF, manual, spec sheet, photos)

**Drop the file into `source-manuals/` first, then tell Claude.**

1. Put the file in the right category subfolder (e.g., a new driver manual goes in `source-manuals/Drivers and Controllers/`, a bubbler doc in `source-manuals/Water Features/Bubblers/`). Make a new subfolder if the product doesn't have one — Claude can help you pick the right spot.
2. Then tell Claude what it is and what you want:

   > I just added the new [product] install manual to source-manuals under [folder]. Read it and update that product's card — pay attention to [whatever the team flagged].

Claude will read the document, propose the changes, and show you previews.

### B. Someone shares a tip, correction, or field observation (no document)

**Just tell Claude in chat. No file needed.**

Examples of things that are chat-only:

- "The team says the reset on the PCR-2Z is actually 5 seconds, not 3 — fix that card."
- "Reps keep getting calls where the remote won't pair after a power outage — add that scenario to the PCZ-2 card."
- "A tech told us the app rejects 5GHz WiFi — make sure that's called out."

Rule of thumb: **if there's a source document, it goes in the folder so future updates can reference it. If it's just knowledge from the team, it goes straight into chat.** Never type up a Word doc just to hold a tip — that's what the conversation is for.

---

## 4. The update routine (every time)

Every update follows the same five steps. Claude knows this routine — you just have to hold the line on step 3.

1. **Describe the change** (and drop in any files per section 3).
2. **Claude shows you preview screenshots** of exactly what changed — cropped to just the changed part, from a local test build. Nothing is live yet.
3. **You review and approve** — or ask for revisions. Iterate as many times as you want; nothing goes live while you iterate.
4. **Say "push and commit live."** Those words are the approval. Claude publishes, and the live site updates in a minute or two.
5. **Spot-check the live site** if the change was important — open the card on your phone the way a rep would.

**The one rule that keeps this safe: nothing gets published until you explicitly say so.** Claude is instructed to never commit or push without your go-ahead. If a session ever seems to be skipping the preview step, stop and ask for previews — that's your safety net.

---

## 5. Keeping the guide's voice right

The guide is a tool reps read mid-call. The writing rules (Claude has these baked in, but you're the enforcer):

- Plain, utilitarian language. Short sentences. No marketing tone, no "seamless," no "robust," no filler.
- Every note must help the rep **on the call**. Internal to-dos ("we should get photos of this board") stay in your chats with Claude — never in the guide.
- When you get feedback that something reads wrong, tell Claude and also say: **"remember this"** — Claude keeps a memory across sessions and will apply the correction going forward.

---

## 6. Useful prompts to keep handy

| Situation | What to say |
|---|---|
| Routine content fix | "On the [card name] card, change X to Y. Show me a preview." |
| New document arrived | "I added [file] to source-manuals/[folder]. Update the [product] card from it." |
| Broken link/photo report | "A rep says the photos on the [card] card aren't loading. Check every link and image against the live site and tell me what's actually broken." |
| Before publishing | "Show me tight screenshots of just the changes." |
| Publishing | "Push and commit live." |
| New product line | "We're launching [product]. Here are the docs in source-manuals/[folder] — draft a new card and show me." |
| Health check (monthly, good habit) | "Verify all PDF links and images on the live site are working." |

---

## 7. Open items I'm leaving you

Loose ends worth knowing about — ask Claude about any of these and it can pick them up:

1. **Custom Strip call script + edge-case matrix** — a homeowner-facing call script and a technical failure matrix were drafted and reviewed as PDFs (with Jason), but were **never merged into the guide**. The draft files are in the repo folder (`_preview-strip-matrix.html`, `_print-callscript.html`, `_print-matrix.html`, `DRAFT-custom-strip-edge-case-matrix.md`). Decide: merge them in, or keep them PDF-only.
2. **Bubbler SKU naming** — the exploded-parts diagrams on the LED Bubbler card are labeled from the source PDFs, but whether "V2" is a distinct hardware revision was never confirmed with PAL engineering.
3. **Custom Strip cut increment** — PAL's own install guide contradicts itself (50mm on one page, 99mm on another). Unresolved; needs an answer from PAL.
4. **Edge-case failure matrix** — still marked draft; never validated by PAL engineering.
5. **`source-manuals/PALCatalog.pdf`** — the full product catalog sits in the folder but isn't committed to GitHub. Commit it if you want it in the repo permanently.

---

## 8. Timeline

- **Now:** You own the GitHub repository; I'm a collaborator if you need anything.
- **September:** My collaborator access ends with my contract. Before then, do at least one full update cycle end-to-end (change → preview → approve → push) while I'm still reachable, so any setup snag gets caught early.
