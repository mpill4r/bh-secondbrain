---
last_updated: 2026-09-02
type: internal
attendees: [Marek Pillár, Juraj Kmec]
tldv_link:
---

# Order Prediction Dashboard Walkthrough with Juraj Kmec

**Date**: 2026-09-02
**Attendees**: Marek Pillár (AI Analyst), Juraj Kmec (Data Scientist — predictive model, Dr. Max/BigHub-side)
**Type**: internal
**Recording**: N/A
**Previous session**: N/A
**Meeting prep**: N/A

## TL;DR

Juraj gave Marek a live demo of the e-commerce order-prediction (řízení poptávky) dashboard the day before its first live business demo, and clarified ownership across the ~9 Dr. Max streams: Juraj owns e-commerce/order prediction, Jura Brázdil (not Jakub Turner, as Marek initially misremembered) owns both reklamace (complaints) and freight invoicing under a shared "logistics" umbrella, Filip Černý owns listing, and Vilo/William Gago owns the shared LLM platform infrastructure. Juraj will demo the dashboard himself tomorrow directly to the business (e-commerce lead "Marek" Šimoník); Marek Pillár is not presenting.

## Key Discussion Points

### Project ownership map (data science / dev side)

Juraj walked through how the ~4 known Data Science / Gen AI use cases split up: he owns e-commerce order prediction; Filip Černý owns listing; Jura Brázdil (surname clarified — not Jakub Turner, whom Marek had confused with "the guy with the dog at the team building," which was actually Jura) is believed to own both reklamace (complaints — automatically parsing driver scan records into complaint tickets) and freight invoicing (fakturace dopravy), which Juraj believes are "the same use case" or at least closely related under a shared "logistics" umbrella — he was explicit this is not certain: *"To ma úplně neber za slovo"* [translated from Slovak: "don't take that as gospel"]. Separately, there is a shared LLM platform / governance layer (not itself a use case) with contact **William Gago** ("Vilo") from BigHub, plus **Lukáš Starenko** and **Honza Zelený** also active in the "Dr. Max LLM Platforma" chat, though their exact roles are unclear even to Juraj. Marek was added to that chat during the call.

### Dashboard demo

The dashboard is a static, read-only "BI-style" view (Juraj's words: *"len čisto akože statický dashboard ala Power BI"* [translated from Slovak: "just a purely static dashboard, kind of like Power BI"]) built on a React frontend, deliberately static/safe so it can't break Dr. Max infra. It tracks two predicted metrics:
- **Revenue**: plan (business target line) vs. actual vs. model prediction with confidence intervals, plus a probability-of-hitting-target readout — currently showing a stark 8% probability of hitting today's target, which Juraj acknowledged looks "depressing" but is the actual model output.
- **Logistics**: predicted new order counts by warehouse and shipping method, with a "time travel" feature to compare a historical model run's prediction against what actually happened.

Both metrics also have a same-day zoomed view (live data, ~30 min delay) and can be filtered per warehouse/shipping method (e.g. Nučice = main Prague warehouse, plus Ostrava, Brno). Data consistency across warehouses is not verified — Marek flagged that Honza had mentioned warehouse-to-warehouse reporting is inconsistent (paper vs. Excel vs. internal systems); Juraj said the data looks consistent from where he sits but couldn't rule out inconsistency "behind the curtain," and expects the large warehouses at least to be reliable.

### Origin and current state

Before this dashboard, the business had no live visibility — they were pulling data manually from Excel exports that were already ~2 days stale, with no way to check same-day performance. The dashboard's v1 is now considered done: it was shown to the business roughly a month ago in an earlier, non-live form; the team then spent about a month hardening infra, and it goes live in front of the business tomorrow for the first time in its deployed form. No phase 2/3/4 roadmap exists yet — that will be shaped after tomorrow's demo feedback and after the e-commerce lead ("Marek" Šimoník) spends a week or two using it, followed by a feedback/adjustment loop.

### Demo logistics

Juraj will run tomorrow's demo himself — he has run all previous demos on this stream and is the only one with full context on how it evolved. Marek Pillár is attending but not presenting, and has nothing specific to ask going in.

### Documentation

Juraj has a fairly thorough repo README/doc set, admittedly "optimized for Claude and GPT" but usable, that Marek doesn't yet have direct access to (it's on Dr. Max's Azure DevOps, pending Marek's Dr. Max account setup). Juraj will zip and send it directly in the meantime. It includes a product brief / business use-case document with explicit business questions.

## Decisions Made

- Juraj will send Marek a zip of the e-commerce project's documentation (README + business use-case doc) directly, ahead of Marek getting Azure DevOps access.
- Juraj demos tomorrow's live business session himself; Marek Pillár attends without presenting.

## Action Items

- [ ] **Juraj Kmec**: Zip and send the e-commerce order-prediction project documentation (README, business use-case doc) to Marek — from order-prediction-dashboard-walkthrough
- [ ] **Marek Pillár**: Reach out to William Gago (Vilo) re: the shared LLM platform stream — from order-prediction-dashboard-walkthrough
- [ ] **Marek Pillár**: Get onboarded to Dr. Max Azure DevOps for e-commerce project doc access (pending Dr. Max account, requested today per prior daily) — from order-prediction-dashboard-walkthrough

## Open Questions

- Are reklamace (complaints) and freight invoicing (fakturace dopravy) actually one combined use case under Jura Brázdil, or two separate ones? Juraj was explicit he isn't sure.
- What exactly do William Gago, Lukáš Starenko, and Honza Zelený each own within the shared LLM platform stream?
- Is warehouse-level data collection actually standardized, or does it vary by warehouse (paper vs. Excel vs. system) as Honza previously suggested?

## Sentiment & Tone

Relaxed, collegial working session between peers — Juraj was open about uncertainty ("don't take that as gospel," "I don't know exactly what he does") rather than overstating his knowledge, which read as trustworthy. Some self-deprecating candor about the dashboard's discouraging 8%-probability reading. Slight end-of-call time pressure on both sides (Juraj had another meeting, Marek had one in 5 minutes) but no friction.

## Routing Log

- **project-stakeholders**: Added STK-026 (Jura Brázdil), STK-027 (William Gago), STK-028 (Lukáš Starenko), STK-029 (Honza Zelený, low-confidence); enriched STK-009 (Juraj Kmec — dashboard status).
- **project-assumptions**: Added ASM-007 (Open) — Jura Brázdil vs. Kuba Turner reklamace ownership conflict.
- **project-knowledge**: Added dev-side ownership map to Dr. Max/ČLH entry; added Order-Prediction Dashboard entry.
- **project-daily**: Added 3 action items (Juraj: send docs; Marek: reach out to William Gago; Marek: get Azure DevOps access) plus ASM-007 reconciliation item.
