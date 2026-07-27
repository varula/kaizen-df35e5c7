## Goal
Produce a fully editable PowerPoint (`Kaizen_Event_Template.pptx`) that mirrors both pages of the uploaded PDF, using **Inter Tight** throughout and matching each page's theme.

## Deliverable
- One `.pptx` file, 2 slides, 16:9 at 13.333" × 7.5" (or 13.33 × 9.4 to preserve the tall page proportions — will use standard widescreen and lay content out to fit).
- Saved to `/mnt/documents/Kaizen_Event_Template.pptx` and surfaced via `<presentation-artifact>`.
- Every text element is a real editable text box (no rasterized images of text). Tables are real PPTX tables. Status pills, PDCA chips, MUDA tags are shapes with editable text.

## Slide 1 — "Kaizen Activity Board" (light theme, navy + amber)
Recreates PDF page 1:
- Navy header bar (`#0B1F3A`) with amber accent stripe: title **KAIZEN**, tagline "KAI · ZEN | CHANGE FOR THE BETTER", subtitle "Continuous Improvement Activity Board", plus right-side info box (KAIZEN No. K-2026-014 / REV 01 / SHEET 1/1).
- Section 1 · IDENTIFICATION: labeled fields grid (Unit/Factory, Line No., Date Opened, Product/Style, Operation, Target Close, Workstation ID, Machine, Buyer/PO) + Team row (Leader, Operator, IE, Quality, Mechanic).
- Current Status: 4 PDCA chips (Plan, Do, Check, Act) — Plan & Do filled amber, Check & Act grey.
- Section 2 · THEME: navy bar + statement.
- Section 3 · PROBLEM STATEMENT: 4 rows (What/Where/When/How much) with amber label chips. MUDA row with 7 tag pills (Motion, Waiting, Defect filled red; rest grey).
- Section 4 · SMART TARGET: real 7-column table (KPI, Baseline, Unit, Target, Unit, ∆ Improvement, Review) with the 6 KPI rows. Achievability / Relevance / Time-Bound lines. Sign-off row with 4 signature lines.
- Footer: PDCA / ECRS legend, form code, quote.

## Slide 2 — "Kaizen Activity Board — Sewing Line" (dark theme, amber + orange)
Recreates PDF page 2:
- Amber header bar with title + meta (Line, Styles, IE Manager, Month, Operators, Shifts).
- KPI strip: 4 stat cards (87% Line Efficiency, 3 Kaizens, 12 Ideas, 1.8% Defect Rate).
- Two-column body:
  - Left col: **Active Kaizens** card (4 items with status dots + owner + metric badges); **Before / After Evidence** with 2 dashed photo placeholders.
  - Right col: **PDCA Status** 2×2 mini-grid (Plan/Do/Check/Act with state badges); **Efficiency Trend — L4** bar chart (5 bars Feb→Jun, Jun highlighted amber); **Improvement Actions — This Week** numbered list.
- Bottom row: 3 cards — **Idea Submission Pipeline** (5-row table), **Defect Reduction Tracker** (4 defect rows + total), **Kaizen Milestone Schedule** (5 dated milestones with status dots).
- Footer: Posted by / Next update / Gap GIS · Bureau Veritas / Armana Apparels.

## Typography & theme
- Font family: **Inter Tight** for all text (title, body, labels, table cells). Registered on each run via pptxgenjs `fontFace`. Weights: 700 for titles/labels, 600 for KPI numbers, 500 semibold for subheads, 400 for body.
- Slide 1 palette: bg `#FFFFFF`, panels `#F5F6F8`, navy `#0B1F3A`, amber `#F5A623`, red `#D8232A`, green `#2E9E5B`, muted grey `#6B7280`.
- Slide 2 palette: bg `#111418`, panel `#1B1F24`, border `#2A2F36`, amber `#F5A623`, blue `#3B82F6`, green `#22C55E`, red `#EF4444`, muted `#8B93A1`.

## Implementation
1. Build a Node script `/tmp/build_kaizen.mjs` using `pptxgenjs`.
2. Set layout to `LAYOUT_WIDE` (13.333 × 7.5"). Use precise inch coordinates for every block.
3. Register Inter Tight via Google Fonts CSS in `pres.theme = { headFontFace: "Inter Tight", bodyFontFace: "Inter Tight" }` and per-shape `fontFace: "Inter Tight"`. (Viewers without Inter Tight installed fall back to system UI — acceptable; text remains editable.)
4. Write to `/mnt/documents/Kaizen_Event_Template.pptx`.
5. QA: convert to PDF with LibreOffice → `pdftoppm` → view both slide images. Check overlap, clipping, alignment; iterate until clean. Also `python -m markitdown` to verify text content.
6. Emit `<presentation-artifact path="Kaizen_Event_Template.pptx" mime_type="application/vnd.openxmlformats-officedocument.presentationml.presentation">`.

## Out of scope
- No new app UI, routes, or backend changes. This is a document-generation task only.
