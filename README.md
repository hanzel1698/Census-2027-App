# HLO 2027 — Enumerator Data-Collection App

An **offline-first, mobile-first web app** for enumerators of the **Census of India 2027, Phase I (Houselisting & Housing Census)**. It turns the official 34-question HLO schedule into a fast, one-tap-per-question flow that runs on the enumerator's own smartphone — exactly the workflow described in the Instruction Manual included in this repository.

**Run it:** open `index.html` in any browser, or host the repo on any static server / GitHub Pages. It is a PWA — once opened, it installs to the home screen and **works fully offline** in the field. All data stays on the device until exported.

## Why it's fast for an enumerator

- **One question per screen, one tap to answer** — selecting a coded option auto-advances to the next question. A typical residential household takes well under two minutes.
- **Automatic skip logic straight from the manual** (Chapter 5):
  - Locked house → jumps directly to Q34 Mobile number (§5.1.15)
  - Vacant (code 0) / non-residential (codes 3–9) → actual use + mobile only
  - Institutional household → household no. **999**, asks only up to Q11, skips Q8 (§5.1.35)
  - Q21 Type of latrine only when Q20 is exclusive/shared; Q25 fuel skipped when "No cooking"
  - Q29 Laptop auto-filled **Yes** when internet is on laptop/computer (§5.1.84)
- **Auto-numbering:** Line number (Q1), 4-digit Census House number (Q3) and Household number (Q9) are auto-generated; **REPEAT** buttons for building & census house exactly as in the manual (§5.1.1).
- **Multi-household census houses:** "Add another household — same census house" repeats the numbers and **auto-fetches floor/wall/roof (Q4–6)** from the first household (§5.1.8).
- **Built-in validations:** married couples ≤ persons − 1 (Q16 rule), 10-digit mobile format, persons ≥ 1, mandatory actual-use / vacancy-reason text.
- **Manual guidance on every question** — a collapsible ⓘ panel with the condensed instruction (treated vs untreated tap water, shared vs public latrine, 100 m urban / 500 m rural water-distance rule shown automatically per your block's area type, LPG connection vs main fuel independence, dwelling-room definition, etc.).
- **PREVIOUS / JUMP / NEXT** navigation and a review screen before confirming each census house (§5.1.92) — tap any review row to fix it.
- **Self-Enumeration aware:** asks SE status first, records the SE ID and tags SE-verified records for supervisor review (§5.1.4–5.1.7).

## Home-screen functions (mirroring the official HLO app, §5.3)

| Button | What it does |
|---|---|
| **Houselist Entry** | Start a new census house / household |
| **Updation Data** | List, edit or delete unsynced records (complete & incomplete) |
| **Edit Already Synced Data** | Correct synced records — tagged for re-sync/review |
| **View Summary** | Progress vs layout-map expectations, use-of-house breakdown, households, population |
| **Sync** | Locks completed records as synced |
| **Mark as Complete** | Confirmation checkbox + finger **signature**, then locks the HLB (§5.1.93–94) |
| **Export / Backup** | CSV of all 34 questions per record; full JSON backup & restore |

## Files

- `index.html` — the entire app (no build step, no dependencies)
- `sw.js`, `manifest.webmanifest` — offline cache + installability (PWA)
- `ilide.info-english-census-manual-2027-pr_….pdf` — official Instruction Manual (source of all question codes: **Annexure IV**, and skip rules: **Chapter 5**)

> Note: this is an independent field tool. Data collected with it should be handed over via the CSV/JSON export; it does not connect to CMMS servers.
