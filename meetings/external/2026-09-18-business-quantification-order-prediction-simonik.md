---
last_updated: 2026-09-18
type: external
attendees: [Marek Pillár, Marek Šimoník]
tldv_link:
---

# Business Quantification Call with Marek Šimoník — Order Prediction (Řízení poptávky)

**Date**: 2026-09-18
**Attendees**: Marek Pillár (BigHub, running the interview), Marek Šimoník (Dr. Max — Head of E-commerce, business owner of Řízení poptávky/order prediction)
**Type**: external
**Recording**: N/A (Marek recorded the call himself; transcript export only)
**Previous session**: N/A — first Business Quantification interview for this initiative. Related prior context: [2026-09-03-order-prediction-dashboard-live-demo](2026-09-03-order-prediction-dashboard-live-demo.md), [2026-09-15-order-prediction-dashboard-follow-up](2026-09-15-order-prediction-dashboard-follow-up.md)
**Meeting prep**: N/A

## TL;DR

Fourth Business Quantification interview in the Tomáš Dudaško OKR series — this one covering the order-prediction dashboard (Řízení poptávky). Šimoník confirmed as business owner (with Petr Ondráček staying domain expert, not co-owner), and the call landed two concrete, conservative KPIs: analyst control-time reduced from ~5h/week to 2h/week (long-term), and catching at least one serious issue/month via the dashboard. No new feature backlog surfaced — Q4 will be the real stress test before any further roadmap conversation.

## Key Discussion Points

### Business Owner & Domain Expert

Marek opened by asking Šimoník to confirm business ownership and asked whether there's also a domain expert who could stand in for him on vision/roadmap/testing if his calendar is full. Šimoník named Petr Ondráček (his subordinate/analyst) as domain expert — the person who knows the underlying data sources best and, until now, built the manual reports by hand — but explicitly noted Ondráček "úplně nemá ten přesah jako strategický" (doesn't have the strategic view) `[translated from Czech]`. When Marek offered to let Ondráček take business ownership instead, Šimoník declined: "Klidně to nechme takhle, úplně ideálně" (Let's just leave it as is, that's ideal) `[translated from Czech]` — he stays sole business owner.

### Origin & Pain Point

Asked what frustration originally motivated the initiative, Šimoník was clear it wasn't about errors: "asi to nebylo o chybách, spíš to bylo o zpoždění" (it probably wasn't about mistakes, it was more about delay) `[translated from Czech]` — specifically the lack of flexibility to react to e-shop order/revenue performance in near-real-time. Asked whether the pain would have gotten worse without a fix, he said no — it would just have stayed "furt stejně špatný" (just as bad, permanently), not escalating.

### Business Value #1 — Analyst Time Savings

Current state: the analyst (Ondráček) spends roughly **1 hour/day (~20 hours/month)** manually pulling together multiple Excels and Power BI reports each morning to reconstruct "what happened yesterday." Šimoník was explicit this is today's baseline, not a target — near-term, the analyst will keep doing this in parallel as a trust-building double-check on the new dashboard. Long-term, he believes this could be eliminated entirely once report recipients trust the live dashboard enough to look at it directly.

### Business Value #2 — Reaction / Outage-Prevention Value

Harder to quantify, but demonstrated with a concrete example: using the dashboard's historical data to judge safe vs. unsafe windows for IT/product releases or planned outages. Pressed for a number, Šimoník gave a deliberately conservative estimate: **~100–200 orders/month "saved"** (not lost to an undetected issue) at **~1,000 Kč average order value**, i.e. **~100,000–200,000 Kč/month**. He was explicit about not wanting to overstate this: "nechci zas asi kreslit vzdušný zámky... budu rád, když to jako nastane ta situace, ale pokud se bavíme o těch 100 tisících, tak si dovedu představit, že to může být ono" (I don't want to build castles in the air... but if we're talking about the ~100k, I can believe that) `[translated from Czech]`. On a broader annual, company-wide basis — factoring in the logistics multiplier below — he believes it could reach "miliony korun" (millions of Kč) per year, a looser upside framing he kept explicitly separate from the conservative monthly figure.

### Logistics Multiplier (Adjacent, Not Owned by Šimoník)

Šimoník flagged that a related dashboard extension for the logistics team — using the same order-forecast data to plan warehouse shifts (staff up or send people home based on forecasted volume) — is already "asi 90% připraveno" (about 90% ready), needing some data cleanup. This would meaningfully multiply the dashboard's value, but it sits under the Director of Logistics, a separate department Šimoník doesn't manage and was careful not to speak for: "nejsem ten, který ani ty směny plánuje, ani nemám pod sebou ty lidi" (I'm not the one who plans shifts, nor do I manage those people) `[translated from Czech]`.

### KPI #1 — Control/Verification Time Reduction

Baseline and target were negotiated live on the call. Marek proposed framing it as a % reduction in the analyst's report-verification time; after some back-and-forth on daily vs. weekly framing, they landed on: baseline **~5 hours/week** (consistent with the ~20h/month, ~1h/day figure above) → target **2 hours/week**. Šimoník called this "conservative" and framed it as roughly a 50% cut in his own words, though the actual numbers agreed are closer to 60%. Explicitly **not** a near-term KPI — the analyst keeps doing this work in parallel for now.

### KPI #2 — Outage / Serious-Issue Detection Cadence

Marek initially proposed a conservative stretch goal of catching at least one predicted outage every 6 months. Šimoník pushed for something more ambitious: at least one "serious issue" per **month** — not necessarily a critical bug, could be web-side or logistics-related.

### Backlog / Future Wishlist

Asked for any backlog or wishlist beyond what's already agreed, Šimoník was direct: "úplně upřímně zatím nemám nic... nemám v šuplíku jako další vývoj" (honestly I don't have anything else — no further development in the drawer) `[translated from Czech]`, beyond what was already fed back in the 2026-09-15 follow-up. His plan: get the currently-agreed scope delivered in the next 2–3 weeks, use Q4's seasonal peak as the real stress test, and revisit future direction with Marek around year-end/Q4 based on how that goes.

### Listing Project — Resourcing Ask

Off-topic but notable: Šimoník clarified logistics doesn't report to him, but he does own the marketplace team (where a colleague works on Listing, led client-side by Petr Neuman). He asked that BigHub prioritize dev capacity on Listing over further order-prediction work. Marek confirmed this is already BigHub's top priority — waiting on Neuman's KPI Excel sign-off before starting Discovery next week — a point of genuine, unprompted alignment on both sides.

## Decisions Made

- Marek Šimoník confirmed as sole business owner of the order-prediction dashboard; Petr Ondráček confirmed as domain expert (not co-owner) — he lacks the strategic view needed for business ownership.
- KPI #1 committed: reduce analyst control/verification time from ~5 hours/week to 2 hours/week — a long-term target, explicitly not applicable near-term.
- KPI #2 committed: catch at least one "serious issue" (web or logistics) per month via the dashboard, once mature — more ambitious than Marek's initial 6-month proposal.
- Business value #2 (reaction/outage-prevention) quantified at ~100,000–200,000 Kč/month, explicitly flagged as conservative.
- No new feature backlog for now — current scope stands; next roadmap conversation deferred to Q4/year-end after the seasonal stress test.
- BigHub's dev-capacity priority stays on the Listing project over further order-prediction work — already the existing plan, no change needed.

## Action Items

- [ ] **Marek Pillár**: Fill in and send the Business Quantification/KPI Excel for order prediction (Řízení poptávky) to Marek Šimoník today, per Tomáš Dudaško's EOD deadline — due 2026-09-18 — from 2026-09-18-business-quantification-order-prediction-simonik
- [ ] **Marek Šimoník**: Review, edit, and confirm the completed order-prediction BQ Excel — full edit rights granted — from 2026-09-18-business-quantification-order-prediction-simonik
- [ ] **Marek Pillár**: Reconnect with Marek Šimoník around Q4/year-end to discuss the order-prediction dashboard's next-phase roadmap, once the current scope has been stress-tested through the seasonal peak — from 2026-09-18-business-quantification-order-prediction-simonik

## Open Questions

- Whether the ~90%-built logistics shift-planning dashboard extension is on BigHub's roadmap at all, or being built independently for/by the Logistics department — Šimoník doesn't own or speak for that team, so this needs a separate conversation with Logistics leadership if BigHub wants visibility into it.
- Petr Ondráček's stakeholder record (STK-035) currently describes him as a "logistics-side contact... co-primary user" — today's call describes him as Šimoník's own e-commerce-team analyst and the person who built the manual reports. Flagged for correction in routing review below.

## Sentiment & Tone

Warm, relaxed, and low-friction throughout — clearly an established, comfortable working relationship (informal tone, jokes about having a full hour blocked vs. needing only half of it). Šimoník was consistently the one pumping the brakes on optimistic framing rather than Marek: he repeatedly chose conservative numbers over ambitious ones ("určitě lepšie dať nižšie číslo a prekonať ho" — better to lowball and beat it — was Marek's framing, and Šimoník ran with it throughout), explicitly resisted inflating the outage-prevention value ("nechci kreslit vzdušné zámky"), and was careful to scope his commitments precisely (declining to speak for Logistics, distinguishing "aktuální stav" from "cíl" multiple times when Marek's questions blurred the two). This mirrors the pattern from this week's other Business Quantification calls (Mertová, Foltýnová, Vosmek) — business owners pushing back constructively on inflated framing rather than accepting whatever number makes the pitch look best. On the one substantive KPI negotiation (control-time reduction), Šimoník moved from an initial looser "50%" framing to a concrete, slightly-more-aggressive 5h→2h commitment without hesitation once Marek anchored the conversation in real numbers. No tension or friction anywhere in the call.

## Routing Log

- **project-stakeholders**: Enriched STK-019 (Marek Šimoník — confirmed sole ownership, KPIs, backlog status, logistics-dashboard flag, Last interaction → 2026-09-18). Corrected STK-035 (Petr Ondráček — role corrected from "logistics-side contact" to Šimoník's own e-commerce-team analyst/domain expert).
- **project-assumptions**: Added ASM-106 (business ownership confirmed), ASM-107 (control-time KPI 5h→2h/week), ASM-108 (≥1 serious issue/month KPI), ASM-109 (~100–200k Kč/month reaction value), ASM-110 (no new backlog, revisit Q4), ASM-111 (logistics shift-planning dashboard extension, Open).
- **project-daily**: 3 action items added to 2026-09-18's daily.
- **meetings/index**: Entry added.
- **External Excel**: `businessQuantificationWorskop.xlsx` (`E-commerce BQ` sheet, row 2) filled with this call's content; row 4 added as a new, separately-tracked initiative for the logistics shift-planning dashboard extension. `BQ_Final.xlsx` (`All Products (Updated)` sheet) later built from the consolidated data, including a derived "Year Expenses / Savings" column.
- **project-lessons**: Triggered autonomously — see project-lessons.md for any captured entries (LL-046 captured during the same-day BQ_Final.xlsx work, not from this meeting directly).
