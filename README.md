# BEA 2026 Shared Task 2 — Pre-Recording Presentation

HTML (reveal.js) slides for the BEA 2026 pre-recording video accompanying the paper
**"Multi-Strategy Rubric-Based Short Answer Scoring for German"** (Jonas Gwozdz, Andreas Both — WSE Research, HTWK Leipzig).

- **Venue:** 21st Workshop on Innovative Use of NLP for Building Educational Applications (BEA) @ ACL 2026
- **Shared Task 2:** Rubric-based Short Answer Scoring for German (ALICE-LP-1.0)
- **Result:** #2 on three of four official tracks (#3 on Track 4), 9 teams
- **Slot:** Fri 3 July 2026, 15:00–16:30 CEST · Poster #147 (virtual)
- **Video deadline:** 4 June 2026 (Underline upload, ≤ 10 min)
- **Paper code:** https://github.com/WSE-research/bea2026-german-asag

## View / present

Just open `index.html` in a browser (no build step — reveal.js loads from CDN).

- Navigate with **arrow keys** / Space.
- **Speaker view (with the script + timer):** press **S**.
- **PDF export:** open `index.html?print-pdf` then print to PDF (A4 landscape, background graphics on).

To serve locally (recommended for recording, avoids any file:// quirks):

```bash
python -m http.server 8000   # then open http://localhost:8000
```

## Recording (≤ 10 min)

1. Open the speaker view (**S**) on a second screen, or read from `SCRIPT.md`.
2. Record the main window. Target ≈ 9:00 (see the timing table in `SCRIPT.md`).
3. Export and upload to Underline by the deadline.

## Styling — HTWK corporate design

Slides follow the official **HTWK Leipzig corporate design** (Gestaltungsrichtlinie v1.0/2018): house fonts
Source Sans / Serif / Code Pro, the official Farbklima, the black logo with its Schutzzone, and the "Tape" key
visual (two bars from the logo's **H**) in HTWK Gelb, with muted HTWK Blau for data (the CD's recommendation for
scientific work).

The theme `css/htwk-reveal.css` and `assets/htwk-logo-h-black.svg` are **copies** of the reusable
`htwk-branding` skill (the source of truth lives in Jonas's PhD vault). To update branding, change it in the
skill first, then re-copy here.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The deck (9 slides + embedded speaker notes) |
| `css/htwk-reveal.css` | HTWK reveal.js theme |
| `assets/htwk-logo-h-black.svg` | Official HTWK logo (horizontal, black) |
| `SCRIPT.md` | Human-readable speaker script with timings |
