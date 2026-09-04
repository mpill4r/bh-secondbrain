---
last_updated: 2026-09-03
type: external
attendees: [Jindřich Tůma, Jan Sovka, Juraj Kmec, Marek Šimoník, Petr Ondráček]
tldv_link:
---

# Order-Prediction Dashboard — Live Demo with Marek Šimoník

**Date**: 2026-09-03
**Attendees**: Jindřich Tůma (BigHub, running the call), Jan Sovka (BigHub), Juraj Kmec (BigHub, presenter/dashboard owner), Marek Šimoník (Dr. Max, Head of E-commerce), Petr Ondráček (Dr. Max, logistics — joined ~15 min in)
**Type**: external
**Recording**: N/A
**Previous session**: N/A directly, but this is the live client-facing follow-up to the internal walkthrough on 2026-09-02 (2026-09-02-order-prediction-dashboard-walkthrough), and references an earlier session Jindřich believes happened in June (predates this harness, not captured)
**Meeting prep**: N/A

## TL;DR

Juraj Kmec demoed the order-prediction dashboard live with real production data to its actual business owner, Marek Šimoník, for the first time. Reception was strongly positive — a real 8-minute site outage correctly showing up as a dip in the live chart was a standout trust-building moment. Šimoník raised sharp, well-informed questions (revenue-vs-order-backlog dynamics, a Brno campaign the model doesn't yet know about) and got dashboard access on the spot; Jan Sovka set a three-layer review process (data accuracy → display/UX → model accuracy) to keep the group from prematurely fixating on forecasting precision.

## Key Discussion Points

### Access and rollout mechanics

Login is Dr. Max email + manual whitelist — currently just Šimoník and Ondráček plus BigHub project staff. Both sides agreed a lightweight manual process (emailing additional addresses to Juraj to whitelist) is sufficient at this volume; no need to over-engineer self-service access yet. Jindřich committed to sending the access email (URL + login instructions, forwardable to further users) within 30 minutes of the call.

### Business Overview page — validated well

Juraj walked through the revenue-vs-target-vs-model-prediction view, with a time-travel selector to replay historical model runs against actual outcomes. August's model tracked reality closely. The standout moment: an 8-minute site outage on 2026-08-24 (09:20–09:28) showed up as a visible dip in the live/"today" chart — Šimoník immediately recognized and confirmed it, calling it "an extremely good indicator" and explicitly the kind of validation he wanted to see. Jan Sovka clarified a key distinction that had confused Šimoník in earlier internal reviews: **new orders** hit the shop the moment they're placed, while **recognized revenue** only books when invoiced — meaning, e.g., Sundays show many new orders but tiny recognized revenue (pharmacies/pickup points closed). This resolved a live question Šimoník had about Sunday-shaped data.

### Warehouse/method filtering — delivered on a prior request

The dashboard now supports filtering the "today" view by warehouse (e.g. Prague vs. Brno) and shipping method — a request from an earlier (June) session. Šimoník confirmed this was exactly what he'd asked for. One display bug surfaced live: the "expected new orders today" figure appeared to show two overlapping/confusing numbers rather than a clear total + already-realized split — Juraj to investigate and fix.

### Prediction accuracy discussion

Reviewing yesterday's actual vs. predicted order counts, Brno has been running consistently under-predicted recently. Šimoník identified the likely cause: a marketing campaign started 2026-08-29 that the model has no visibility into — Petr Ondráček's previously-supplied campaign/promo CSV is roughly two months stale. Juraj confirmed the model currently just ignores missing campaign data rather than accounting for it, and asked for a refreshed file. Šimoník also asked a substantive modeling question: does the revenue forecast account for a current warehouse backlog (orders created/packed but not yet shipped, due to the warehouse currently running behind), or is it purely based on already-invoiced revenue? Juraj confirmed it's trained purely on recognized revenue — tested blending in order-backlog data early on, but the revenue-only model performed better. The model self-corrects over a few days via a nightly (midnight) recalibration, but Juraj wants to verify exactly how it behaves against a live backlog spike like the current one before confirming it's fully accounted for.

Juraj was explicit about calibration limits: the model is reliable within a 14-day horizon; beyond that, figures are extrapolated and deliberately shown without confidence intervals, since they aren't trustworthy that far out. Šimoník agreed this scope is reasonable and doesn't need to change.

### Metric clarity — target-probability vs. month-completion

Jan Sovka flagged a box on the homepage that combines two different metrics in a way that initially confused him: the "probability of hitting 100%+ of today's target" (useful for deciding whether to push a same-day campaign) is distinct from "% of month-end target expected" (a business-level KPI). He argued both metrics earn their place but need clearer separation/labeling — Juraj to tighten the explanatory tooltips.

### Feature backlog raised during the demo

Several small, non-urgent requests surfaced, to be formalized into a written backlog rather than actioned ad hoc:
- Toggle the bottom breakdown table between revenue and order-count views (currently revenue-only)
- Add historical overlay lines to the "today" chart: same weekday last week (D-7) and same weekday last year (offset by a few days from exact D-365 to preserve day-of-week alignment)
- Split the combined warehouse+shipping-method selector into two independent filters (already on Juraj's own roadmap)
- Incorporate fresh campaign/promo data once Ondráček provides it

### Process and scope framing

Jan Sovka proposed a three-layer review order for the coming weeks: **(1)** verify the underlying numbers/filters are correct against Dr. Max's own source data — a check only the client can fully do; **(2)** request display/UX changes (extra KPIs, different breakdowns); **(3)** only then assess and tune model accuracy. Explicit rationale: avoid the group getting stuck relitigating forecast precision before the more basic layers are settled — today's accuracy is considered "good enough" to build on. Separately, Jan Sovka set scope expectations: Šimoník and Ondráček are the dashboard's primary users for the current phase; a separate logistics contact ("Honza" — identity unclear, needs verification) raised different needs (a month-ahead view rather than day/14-day) and was deliberately placed into a later phase (2/3/4), not phase 1.

### Cadence and feedback channel

Since Šimoník is away for part of next week, the plan is an in-person sync at Dr. Max's site later next week (Thursday or Friday) — Jindřich and Juraj will bring a written notes/handout of BigHub's own dashboard observations to review together, while Šimoník and Ondráček explore/test the live dashboard independently in the meantime. Feedback should be funneled through one channel rather than arriving ad hoc from multiple users — Jindřich will maintain the backlog and check whether a shared platform can be used; for now, feedback goes by email.

### Marek Pillár's role (introduced in absentia)

Jan Sovka introduced Marek Pillár's role to Šimoník even though Marek wasn't on this call — framing him as the team's dedicated, product/business-background owner for this e-commerce stream going forward, working alongside Jindřich, replacing Jan Sovka's own hands-on involvement.

## Decisions Made

- Dashboard access rollout stays manual (email-based whitelist) at current scale — no need for self-service yet.
- Review priority order going forward: verify data accuracy first, then request display/UX changes, then address model-accuracy tuning last.
- Šimoník and Ondráček are the dashboard's primary users for the current phase; the other logistics stakeholder's differing (month-ahead) needs are deferred to a later phase.
- The revenue-prediction model stays trained purely on recognized/invoiced revenue (not blended with order-backlog signals) — empirically outperforms the blended approach tested earlier.

## Action Items

- [ ] **Jindřich Tůma**: Send dashboard access email (URL + login instructions, forwardable) — due within 30 min of the call, 2026-09-03 — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Marek Šimoník / Petr Ondráček**: Send additional user email addresses for dashboard whitelisting — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Juraj Kmec**: Investigate and fix the confusing double-number display under "expected new orders today" — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Juraj Kmec**: Verify how the model's nightly recalibration responds to a live order-vs-invoice backlog spike (current Brno/warehouse situation) — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Petr Ondráček**: Send refreshed campaign/promo data (previous file ~2 months stale) so the model can account for the 2026-08-29 Brno campaign and future promos — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Juraj Kmec**: Backlog — add order-count toggle to the breakdown table, split warehouse/shipping-method filters, add D-7 and day-of-week-aligned D-365 historical overlay lines, tighten tooltip text distinguishing the two target-probability metrics — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Jindřich Tůma**: Determine whether a shared platform (vs. email) can be used to capture Dr. Max's dashboard feedback/backlog — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Jindřich Tůma / Juraj Kmec**: Prepare a written notes/handout of BigHub's own dashboard observations ahead of next week's in-person sync — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Jindřich Tůma**: Schedule the in-person follow-up sync at Dr. Max's site next week (Thursday or Friday) — from 2026-09-03-order-prediction-dashboard-live-demo
- [ ] **Marek Šimoník / Petr Ondráček**: Explore/test the live dashboard over the next 1-2 weeks and compile feedback ahead of the in-person sync — from 2026-09-03-order-prediction-dashboard-live-demo

## Open Questions

- Who is the "Honza" Jan Sovka mentioned as a separate logistics contact with different (month-ahead) dashboard needs, deferred to a later phase? Not clearly the same person as Jan Maroušek (STK-021, Kontrola beden) — needs verification before merging or creating a confident stakeholder record.
- Whether a shared platform (vs. email) can carry the Dr. Max feedback/backlog process — Jindřich still investigating.

## Sentiment & Tone

Very positive and high-trust. Marek Šimoník was visibly enthusiastic — multiple unprompted compliments ("this is exactly what I wanted to see," "overall this looks great"), and his questions were sharp and constructive rather than skeptical, engaging seriously with the model's methodology rather than just its UI. The outage-correlation moment functioned as a strong, organic trust-building demonstration — Šimoník cited it as exactly the kind of validation he needed. Jan Sovka's framing (three-layer review order, deliberate phase-2+ deferral for the other logistics contact) reads as proactive scope protection, keeping a technically engaged client from pulling the team into premature model-tuning debates. No friction or resistance surfaced anywhere in the call.

## Routing Log

- **project-stakeholders**: Added STK-035 (Petr Ondráček, new), STK-036 ("Honza", low-confidence); enriched STK-002 (Jan Sovka), STK-003 (Jindřich Tůma), STK-009 (Juraj Kmec), STK-019 (Marek Šimoník — filled several `-tbd-` fields, sentiment set to Champion).
- **project-assumptions**: Added ASM-014 (Decided) — dashboard review order; ASM-015 (Decided) — phase-1 user scope; ASM-016 (Decided) — revenue-only model design.
- **project-knowledge**: Enriched Order-Prediction Dashboard entry with demo outcome, calibration limits, campaign-data gap, feature backlog.
- **project-daily**: Added 10 action items.
