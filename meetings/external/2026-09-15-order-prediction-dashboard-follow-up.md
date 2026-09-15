---
last_updated: 2026-09-15
type: external
attendees: [Juraj Kmec, Jindřich Tůma, Marek Pillár, Marek Šimoník, Petr Ondráček]
tldv_link:
---

# [Ext] AI Predikce obj: Follow-Up

**Date**: 2026-09-15
**Attendees**: Juraj Kmec (BigHub, data scientist / dashboard owner, presenter), Jindřich Tůma (BigHub, running the call), Marek Pillár (BigHub, PM — mostly listening), Marek Šimoník (Dr. Max, Head of E-commerce), Petr Ondráček (Dr. Max, logistics)
**Type**: external
**Recording**: N/A (fireflies.ai transcript)
**Previous session**: [2026-09-03-order-prediction-dashboard-live-demo](2026-09-03-order-prediction-dashboard-live-demo.md) (also see [2026-09-02-order-prediction-dashboard-walkthrough](../internal/2026-09-02-order-prediction-dashboard-walkthrough.md))
**Meeting prep**: N/A

## TL;DR

First structured client feedback session on the order-prediction dashboard since its 2026-09-03 live demo — Marek Šimoník and Petr Ondráček worked through detailed, mostly UX-level feedback (data grouping, historical comparison views, mobile access, terminology) rather than raising trust or accuracy concerns. Several previously-backlogged items (T-7/T-364 historical overlay) are now built and were demoed live. The session closed with Jindřich Tůma proposing to formally accept the current build as "version 1" and move to a structured, batched change-request cadence for v2/v3 — Šimoník agreed. Jan Sovka was expected but did not join.

## Key Discussion Points

### Mobile / non-VPN access

Šimoník flagged that the dashboard is currently only reachable on Dr. Max's internal network or via VPN — no mobile access without VPN, which he called "dosáhle důležitá věc" (a genuinely important thing) once the rest is otherwise working well. Juraj Kmec acknowledged this needs a deliberate security trade-off, not a pure technical fix — loosening access somewhat while keeping it reasonably secured is "poměrně běžná věc, kterou se apky používají" (a fairly standard requirement for apps). Jindřich Tůma confirmed BigHub owns reviewing this with the infra/security side: "Marko, absolutně validní požadavek. Musíme to poběrat s tím infra... To není problém." [translated from Czech]

### Budget / forecast / predikce terminology and data model

Šimoník walked through his own detailed notes on the "new orders" view. Key points:
- Proposed renaming the "new orders" card to "vytvořené objednávky" (created orders) for internal terminology clarity — a naming-only change.
- Dr. Max already maintains budget and forecast figures at daily granularity, tied to recognized revenue ("uznané tržby"): an annual budget is set every August for the following year, then re-forecast after months 3, 5, and 7 ("forecasting") against year-end expectations. This year's forecast is running ~3–6% below the original (more optimistic) budget, as the market hasn't grown as expected.
- He wants budget, forecast, and today's expected revenue ("predikce" — the model's own output) all viewable together at the same daily granularity, alongside revenue recognized so far — explicitly asked to keep the three terms distinct: **budget** and **forecast** are Dr. Max's own business planning figures (supplied externally, e.g. via Excel), **predikce** is specifically what the model computes.
- Juraj confirmed Alana had already sent a "2026 forecast" column alongside the existing e-commerce data feed; data will need to keep arriving at least weekly through year-end, with a new delivery arrangement to be worked out for January onward (open question — see below).
- Juraj will add budget/forecast/predikce (and "uznané zatím") together on the same chart, replacing the need to compute this by hand — which Šimoník had been doing live on a calculator during the call as a sanity check, and it broadly lined up with the dashboard's own predikce figure.

### Historical / comparison views

- **T-7 / T-364 comparison — delivered**: In direct response to a request Šimoník relayed from Petr Ondráček at the previous call, Juraj confirmed he finished building a same-weekday historical comparison the day before this meeting — using T-7 and T-364 (not a literal D-365) specifically so day-of-week alignment holds even across a leap year. He demoed it live on screen share, with absolute order counts shown alongside the percentage comparison (e.g. "2000 objednávek realizovaných plus 10%"). Petr Ondráček separately confirmed his own math on the 52-week/leap-year edge case checks out. Still needs a more user-friendly name than its current internal/dev name ("julicevýho" — a placeholder Juraj wants to replace).
- Šimoník asked for a "data as of [timestamp]" label directly on the graph, instead of having to hunt for the latest-data date — Juraj confirmed this is a quick, low-effort addition.
- Petr Ondráček separately asked for the same T-7/T-8 and historical-year comparison to be broken out specifically for reservations (see below), not just aggregate order counts, plus a user-selectable 30-minute vs. hourly granularity toggle (needed for BDC outage reporting, which is conventionally done in whole-hour blocks) — Juraj confirmed this is buildable ("skalendržit").

### Channel grouping: e-com, marketplace, rezervace

Šimoník asked for a cleaner top-level grouping: an aggregated "e-com" total (summing the Nučice/Ostrava/Brno warehouses) shown alongside reservations and marketplace as three top-line categories, rather than needing to add up three warehouse tiles himself; drill-down into individual warehouses should stay available underneath. Juraj agreed this is a sensible aggregation to add on top of the existing warehouse-level tiles.

### Pharmacy reservations as a strategic differentiator

Petr Ondráček flagged that pharmacy reservations ("rezervace v lékárnách") get folded into the general new-orders aggregate today and need to be split out as their own category — both for his own reporting and because logistics needs to plan warehouse staffing separately from reservation volume. Šimoník gave the business context: pharmacy reservations are considered Dr. Max's key e-commerce USP — leveraging ~600 physical pharmacies as pickup points is dramatically cheaper than warehouse-based click & collect (a pharmacist just holds a product on a shelf vs. Dr. Max carrying full fulfillment/return cost), and a new in-app "reserve at pharmacy" button (in addition to add-to-cart) is being actively pushed to accelerate this. Marek Pillár asked whether pharmacy staff headcount could become a constraint; Šimoník said no — reservations are markedly less labor-intensive than click & collect.

### Logistics handoff — warehouse-level reservation/pickup breakdown

Šimoník handed the second half of the call to logistics topics, noting he'd already shared an early preview with Jan ("Honza") Maroušek but not yet the fuller version. The core ask (Šimoník, confirmed by Marek Pillár for his own spec-writing purposes): split reservation/pickup data into four parts — pharmacy reservation *and* warehouse click-and-collect, each separately for the Nučice and Brno warehouses — because Honza Maroušek plans warehouse staffing per site and currently has no visibility into pharmacy-reservation volume broken out by warehouse.

This surfaced a design issue with the existing "Metrix" (a warehouse × delivery-method matrix view): pharmacy reservation is architecturally treated as if it were both a warehouse and a delivery method in the current matrix, which Juraj Kmec acknowledged is conceptually paradoxical ("ten sklad bude vlastně paradoxní, jako rezervace v lékárnách je jakoby sklad. A zároveň je to dopravní metoda."). Juraj proposed possibly splitting it into two independent selectors (warehouse, delivery method) instead of one combined matrix, and will think through the redesign — no committed design yet. Petr Ondráček also asked whether the Metrix could be exported to Excel; Juraj said it's technically possible but needs an effort estimate, and that Honza Maroušek is the one with the actual export requirement (cadence/format still needs to be confirmed directly with him).

### Business Overview page — minor UX polish

Šimoník's last item: extend the same three-channel breakdown (e-com/marketplace/rezervace) to the Business Overview page, and show summed totals directly on-screen (e.g. a pre-computed "15 milionů" total) rather than requiring the viewer to mentally add two figures together (his example: 8.3 + 7.9). Juraj confirmed this is a straightforward addition.

### "Rozpad" (breakdown) feature — deprioritized, revisit later

Šimoník admitted he hasn't yet reviewed the "rozpad" breakdown feature in detail and has no feedback on it yet. Juraj noted it was the lowest-priority item from the start, so this is fine — open to repurposing that space for new tabs based on future ideas rather than polishing it as originally scoped.

### Process cadence — formal v1 acceptance

Jindřich Tůma proposed formalizing the delivery cadence: treat the currently delivered build as an acceptable "version 1" now, given it already reflects the intended non-final UX direction and real data; future requests (today's feedback included) become "version 2," to be delivered together rather than piecemeal; from v2 onward, further requests batch into v3, ideally on a quarterly-ish cadence rather than continuous ad hoc pushes. Framed this partly as a BigHub-internal reporting need ("na nás je zase zvěra dupáno" [translated from Czech] — internal pressure to show delivered value on schedule), not as a constraint on the client's ability to keep giving feedback. Šimoník agreed and formally signed off on v1 as delivered, "acceptance nahoru," looking forward to v2. Point of contact on BigHub's side for ongoing coordination is confirmed to remain Lukáš Síč, with Jindřich covering directly when needed.

### Capacity / prioritization question — deferred

Marek Pillár asked directly what BigHub's capacity/prioritization plan looks like — whether the team will stay focused on e-commerce/order-prediction alone for another four months, or balance it against other pipeline projects. Jindřich Tůma did not give a concrete answer on the call and said he'd follow up separately.

### Separate ask: business-value/KPI recap session

At the start of the call, Marek Pillár asked Marek Šimoník to schedule a separate session to revisit and recap the dashboard's product value and KPIs (unrelated to today's feature-feedback agenda). Šimoník said Wednesday/Thursday don't work (a hotel conference), Friday is more likely, and will send concrete dates — not yet done as of this call.

## Decisions Made

- The dashboard's current build is formally accepted by Marek Šimoník as "version 1"; today's feedback (and any further requests) becomes the batched scope for "version 2," with subsequent requests batching into "version 3" on a roughly quarterly cadence going forward, rather than continuous piecemeal releases.
- Mobile/non-VPN access to the dashboard is a validated, BigHub-owned follow-up to scope with Dr. Max infra/security — not dismissed as out of scope.
- The revenue-prediction model's own output will be consistently called "predikce" going forward, kept terminologically distinct from Dr. Max's own "budget" and "forecast" planning figures, to avoid confusion as more views combine all three.
- Pharmacy reservations ("rezervace v lékárnách") will be broken out as their own top-line category, separate from e-com/marketplace, and further split per-warehouse for logistics staffing purposes — reflecting their strategic importance as a differentiator, not just a reporting nicety.

## Action Items

- [ ] **Juraj Kmec / Jindřich Tůma**: Scope mobile / non-VPN dashboard access with Dr. Max infra and security — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Add budget, forecast, and predikce (plus revenue recognized so far) together on the same daily-granularity view, replacing manual calculation — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Marek Šimoník / Dr. Max**: Confirm the ongoing data-delivery arrangement for the "2026 forecast" column beyond year-end (weekly cadence through December confirmed; January onward still needs a storage/delivery decision) — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Rename the newly-built T-7/T-364 historical comparison feature to a user-friendly label (currently an internal placeholder name) — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Add a "data as of [timestamp]" label directly on the dashboard graph — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Build a 30-minute vs. hourly granularity selector for the "today" view (needed for BDC outage reporting) — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Extend T-7/T-8 and historical-year comparison views to reservations specifically, not just aggregate order counts — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Add an aggregated top-level "e-com" total (summing Nučice/Ostrava/Brno warehouses) alongside reservations and marketplace as three top-line categories, keeping per-warehouse drill-down available — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Redesign the warehouse × delivery-method "Metrix" view so pharmacy reservations aren't modeled as if they were simultaneously a warehouse and a delivery method; split reservation/pickup data per warehouse (Nučice, Brno) for logistics staffing use — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Scope effort for a Metrix-to-Excel export feature — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Petr Ondráček**: Confirm with Jan ("Honza") Maroušek the exact export cadence/format he needs from the Metrix view (one-time vs. recurring) — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Juraj Kmec**: Extend the Business Overview page with the same e-com/marketplace/rezervace channel breakdown, and show pre-summed totals directly rather than requiring manual addition — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Marek Šimoník**: Send available dates (likely Friday) for a separate session to recap the dashboard's business value/KPIs with Marek Pillár — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Jindřich Tůma**: Follow up on BigHub's capacity/prioritization plan for the e-commerce/order-prediction stream vs. other pipeline projects — from 2026-09-15-order-prediction-dashboard-follow-up
- [ ] **Jindřich Tůma**: Schedule the next sync after Marek Šimoník returns from a full week off — from 2026-09-15-order-prediction-dashboard-follow-up

## Open Questions

- Identity confirmation: is "Honza Maroušek," the logistics warehouse planner referenced repeatedly in this meeting, the same person as STK-021 (Jan Maroušek, previously recorded only as the Kontrola beden contact) and/or STK-036 ("Honza," the low-confidence logistics contact flagged on 2026-09-03 as wanting a month-ahead dashboard view)? Names and the warehouse-planning role strongly suggest a match, but not explicitly confirmed on this call.
- Exact scope and effort of the Metrix redesign (splitting warehouse and delivery-method into independent selectors) — not yet designed, just agreed as a direction.
- Whether several 2026-09-03 backlog items (double-number display bug, tooltip clarity between target-probability metrics, revenue/order-count toggle, refreshed campaign/promo data) are still outstanding — none were explicitly revisited in this meeting, so their status is unconfirmed rather than resolved.

## Sentiment & Tone

Continued high engagement and trust, but a notable shift in register from the 2026-09-03 demo: that call was about validating the dashboard's core trustworthiness (the outage-correlation moment); this one was a working session with detailed, constructive, occasionally granular UX/data-modeling feedback — Šimoník arrived with his own written notes and worked through them systematically, and both he and Petr Ondráček engaged with real business context (the pharmacy-reservation strategy, warehouse staffing needs) rather than surface complaints. No friction or pushback anywhere in the transcript. Jindřich Tůma's v1-acceptance proposal landed smoothly — Šimoník's agreement was immediate and warm ("Úplně ideálně"), suggesting the relationship is comfortable enough to move from ad hoc iteration to a more formal cadence without it reading as BigHub pulling back. The one soft signal worth tracking: Marek Pillár's direct capacity/prioritization question went unanswered on the call — worth a real follow-up rather than letting it drop, since it was asked plainly by a Dr. Max-side stakeholder about whether other pipeline projects will compete for the same team's time.

## Routing Log

- **project-assumptions**: Added ASM-069 (Decided) — v1 acceptance + v2/v3 batched cadence; ASM-070 (Decided) — "predikce" naming convention; ASM-071 (Decided) — pharmacy reservations as strategic differentiator, to be broken out per warehouse.
- **project-stakeholders**: Enriched STK-009 (Juraj Kmec), STK-003 (Jindřich Tůma), STK-019 (Marek Šimoník — last interaction updated), STK-035 (Petr Ondráček — last interaction updated), STK-002 (Jan Sovka — noted as expected but absent). Flagged a possible (unconfirmed) identity match between this meeting's "Honza/Jan Maroušek" and existing entries STK-021 (Jan Maroušek) and STK-036 ("Honza") — not merged, needs PM verification.
- **project-knowledge**: Enriched "Order-Prediction Dashboard (Řízení poptávky)" entry with the budget/forecast/predikce terminology model, the T-7/T-364 leap-year-safe comparison methodology, the pharmacy-reservation business rationale, and the v1-acceptance/delivery-cadence note.
- **project-daily**: 15 action items added to 2026-09-15's daily.
