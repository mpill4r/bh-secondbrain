---
last_updated: 2026-09-11
last_updated_by: manual — conversational
---

# Meeting Prep — AI Initiatives Business Quantification (FigJam working session)

**Meeting**: Monday 2026-09-14, with Tereza Foltýnová (STK-013)
**Purpose**: Define, together with business owners, how much and what each Žůrek/logistics AI initiative saves or brings (Kč, time, FTE, etc.) — live in FigJam.

---

## Step 1 — Context extracted (11 initiatives)

| Initiative | Description | Business owner | Goal / problem | Existing quantitative claims | Stage |
|---|---|---|---|---|---|
| **Reklamace** | Automation of creating and recording supplier complaints — evidence, photo documentation, supplier communication, audit trail | Rudolf Žůrek (domain expert: Petr Sláma) | Eliminate manual claim processing across ~4 quality staff | Baseline: 4 staff × 2h/day = 8h/day. Time savings **by phase**: Intake claims 45%, email agent 5%, warehouse claims 10%, Phase 3 10%, Phase 4+5 30%. Internal benefit estimate: 90 000 Kč | In Testing, 20% complete, MVP mostly done |
| **Fakturace od dodavatelů** | OCR processing/automation of supplier invoices at line-item level, feeding Axapta | Rudolf Žůrek (domain expert: Jan Žižka) | Automate manual supplier-invoice entry | Internal benefit estimate: 450 000 Kč (highest of the three) — no time/FTE baseline documented anywhere | In Development, 10% complete, described internally as "still in diapers" — very early |
| **Kontrola beden** | Automated crate/box content control (inspection table + packing line) via camera, compared against WMS | Rudolf Žůrek (domain expert: Jan Maroušek — flagged once before as "never actioned") | Reduce manual crate-content checking | None — no baseline, no benefit estimate anywhere | Idea — feature sheet completely empty |
| Automatické objednávky dle sezónnosti a počasí | Automatic reordering based on seasonality/weather | — (Sklad/Logistika, unassigned) | — | None | Idea — title only |
| Alokace zboží mezi sklady | Goods allocation between warehouses | — | — | None | Idea — title only |
| Kamera na lince – kontrola obsahu bedny | Line camera for box-content QA | — | — | None — possibly the same idea as Kontrola beden | Idea — title only |
| Inteligentní rádce pro vedoucího skladu | AI advisor for warehouse manager | — | — | None | Idea — title only |
| Konsolidace / rozdělování balíčků (master data) | Package consolidation/splitting, master data | — | — | None | Idea — title only |
| Balancování skladových zásob vč. lékáren | Stock balancing across warehouses incl. pharmacies | — | — | None | Idea — title only |
| Supply chain – komplexní AI/Copilot strategie | Comprehensive AI/Copilot strategy for supply chain | — | — | None | Idea — title only |
| Sklad – vychystávací strategie (AI decision engine) | AI decision engine for warehouse picking strategy | — | — | None | Idea — title only |

**Open question worth raising with Terka directly**: whether "Fakturace od dodavatelů" and "Fakturace doprav" (a different, already-tracked freight-invoicing project) are the same initiative or genuinely distinct — flagged since 2026-09-02, reconfirmed 2026-09-07, never resolved with the people involved (see [[ASM-006]]).

---

## Step 2 — FigJam template design

### Legend (color key — top-left of the board)

- 🟢 Green — confirmed by business owner
- 🟡 Yellow — estimate / rough figure, not yet confirmed
- 🔴 Red — unknown / needs discovery

### Per-initiative card (one frame per initiative)

```
┌─────────────────────────────────────┐
│ [INITIATIVE NAME]                    │
│ Business owner: [name]               │
│                                       │
│ Why this matters:                    │
│ [1-2 sentence business goal]         │
│                                       │
│ Value type:  □ Kč  □ Time  □ FTE     │
│              □ Quality  □ Risk       │
│              □ Other: ____           │
│                                       │
│ Baseline (today):                    │
│ [current state, quantified if poss.] │
│                                       │
│ Expected impact:                     │
│ [target number + unit]               │
│                                       │
│ How we'll measure it:                │
│ [method / cadence]                   │
│                                       │
│ Confidence: 🟢 🟡 🔴                  │
│                                       │
│ Open questions / assumptions:        │
│ [parking-lot notes]                  │
└─────────────────────────────────────┘
```

### Board layout (left to right)

1. **Legend + instructions** (single frame, far left)
2. **Section: In Progress** — Reklamace, Fakturace od dodavatelů
3. **Section: Idea Stage** — Kontrola beden + the warehouse/logistics idea cluster
4. **Parking lot** — a wide sticky-note zone for cross-cutting open questions (e.g. the Fakturace od dodavatelů/Fakturace doprav overlap)
5. **Summary / rollup** (far right) — a simple table auto-tallying: total confirmed Kč, total confirmed time/FTE saved, count of initiatives by confidence color, count still fully unknown

### On the 8 bare-title ideas

Eight nearly-empty cards would clutter the board and none are vetted initiatives yet — just single-line brainstorm titles with no owner or objective. Recommendation: one consolidated "Warehouse/Logistics idea backlog" card listing all 8 as bullet points, rather than 8 individual card frames — unless Terka specifically wants to work through them one by one. Both options pre-filled below.

---

## Step 3 — Pre-filled cards (copy-paste ready into FigJam)

### Card: Reklamace
- **Business owner**: Rudolf Žůrek
- **Why this matters**: Automate manual complaint processing currently eating ~8h/day across the quality team
- **Value type**: ☑ Time ☑ FTE ☑ Kč
- **Baseline**: 4 quality staff × 2h/day = 8h/day total 🟢
- **Expected impact**: 45% time savings on intake claims (largest single phase); additional 5–30% across other phases — see phase breakdown 🟢
- **Measurement method**: TBD — ask in call
- **Confidence**: 🟢 (baseline + phased savings already documented in the dev spec)
- **Open questions**: Do these phase percentages need re-validating with current staffing, or still accurate?

### Card: Fakturace od dodavatelů
- **Business owner**: Rudolf Žůrek
- **Why this matters**: Automate manual entry of supplier invoices into Axapta
- **Value type**: ☑ Kč (unconfirmed) — TBD for time/FTE
- **Baseline**: 🔴 TBD — ask in call (no current manual-effort baseline documented anywhere)
- **Expected impact**: 🔴 TBD — ask in call
- **Measurement method**: 🔴 TBD — ask in call
- **Confidence**: 🔴 (nothing confirmed; area described internally as "still in diapers")
- **Open questions**: Is this the same initiative as "Fakturace doprav" (freight invoicing), or genuinely distinct? Never confirmed.

### Card: Kontrola beden
- **Business owner**: Rudolf Žůrek
- **Why this matters**: Reduce manual crate-content checking via camera + WMS comparison
- **Value type**: 🔴 TBD — ask in call
- **Baseline**: 🔴 TBD — ask in call
- **Expected impact**: 🔴 TBD — ask in call
- **Measurement method**: 🔴 TBD — ask in call
- **Confidence**: 🔴 (nothing scoped yet; the named contact for this has never been followed up with)
- **Open questions**: Who's the right contact now? Is this the same as "Kamera na lince – kontrola obsahu bedny" below?

### Option A — consolidated card: Warehouse/Logistics idea backlog
- **Business owner**: 🔴 TBD — ask in call
- **Why this matters**: 🔴 TBD — ask in call
- **Items to triage together**: automatic reordering by seasonality/weather · stock allocation between warehouses · box-content camera QA · AI advisor for warehouse manager · package consolidation/splitting · cross-warehouse stock balancing · supply-chain AI/Copilot strategy · AI picking-strategy engine
- **Confidence**: 🔴 (all 8 are title-only, no owner or detail exists)

### Option B — 8 individual stub cards (if Terka wants to work through them one by one)
Same fields as above, each with owner/goal/baseline/impact/measurement all marked 🔴 TBD — only the initiative name differs per card.

---

**Sources**: `product-roadmap-portfolio-full.xlsx` (Portfolio, Reklamace, Fakturace od dodavatelů, Kontrola beden, Řízení skladu - backlog sheets), `project-stakeholders.md` (STK-021 Jan Maroušek, STK-015 Jan Žižka), `project-assumptions.md` ([[ASM-006]]), `project-knowledge.md`, and the Reklamace dev spec (`Logistika - 2026-06_Reklamace_Specifikace_3.5.docx`) for the phase-level time-savings baseline.
