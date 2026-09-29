---
last_updated: 2026-09-29
type: external
attendees: [Marek Šimoník, Petr Ondráček, Juraj Kmec, Marek Pillár]
recording_link:
---

# Order-Prediction Dashboard — v2 Feedback Review with Marek Šimoník

**Date**: 2026-09-29
**Attendees**: Marek Šimoník (Dr. Max, Head of E-commerce, business owner), Petr Ondráček (Dr. Max, e-commerce analyst / domain expert, in the same room as Šimoník), Juraj Kmec (BigHub, data scientist / dashboard owner, presenter), Marek Pillár (BigHub, PM)
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-09-15-order-prediction-dashboard-follow-up](2026-09-15-order-prediction-dashboard-follow-up.md) (also see [2026-09-18-business-quantification-order-prediction-simonik](2026-09-18-business-quantification-order-prediction-simonik.md))
**Meeting prep**: N/A

> **Transcript note**: Jindřich Tůma was expected but never joined. Speaker diarization was corrected at PM's confirmation: the Slovak lines labelled "Juraj Kmec" at 16:30–17:46 and 27:09 were Marek Pillár; the Czech logistics lines labelled "Juraj Kmec" at 22:13 and 29:25–31:00 were Petr Ondráček. Short Czech interjections around 08:06–08:21 are also most likely Ondráček (same room as Šimoník), not Marek Pillár.

## TL;DR

Juraj Kmec walked Šimoník (just back from a week's holiday) through the v2 build that answers the 2026-09-15 feedback: a hierarchical channel view, a run-rate ("při současném tempu") projection, a 30-min/hour toggle, and a logistics chart that follows the selected series. Almost all of it landed well. Two items are still open. The **budget Excel** from Šimoník blocks the per-day budget and the per-channel split of recognized revenue. The **per-day, per-warehouse export** is for logistics shift planning. Both sides agreed to close the requirements with a **final acceptance by end of October**, then use the dashboard through the season, collect ideas, and talk about a V2 extension in Jan/Feb 2027. Mobile/non-VPN access is not a blocker; the email digest idea goes to V2.

## Key Discussion Points

### What landed from the 2026-09-15 feedback

Juraj Kmec said he had worked in nearly all of the previous session's feedback, except the items that depend on Šimoník's budget Excel. Progress against the 2026-09-15 action items:

| 2026-09-15 item | Status 2026-09-29 |
|---|---|
| E-com aggregate + three top-line categories (e-com / pharmacy reservations / marketplace) with drill-down | **Done**: hierarchical selector; sub-charts follow the selected level (e-com → warehouses → delivery methods). Loading is a bit slow; Juraj says it could be sped up |
| 30-min vs. hourly granularity toggle | **Done** |
| Budget / forecast / predikce on one view | **Partly**: "target" is renamed to "budget". Per-day budget values wait on Šimoník's Excel |
| Run-rate projection ("at the current pace") | **Done, new**: Šimoník called it the thing he's happiest about. It replaces his own manual calculation |
| Logistics chart per warehouse / delivery method, reservations split out | **Done**: the chart follows the selected series. Removing "pharmacy pickup" recalculates the numbers and charts |
| Metrix-to-Excel export | **Workaround**: a Chrome extension Šimoník sent works. Juraj forgot the planned "copy" button and will add it. The real logistics need turned out to be a *per-day* export (see below) |
| Mobile / non-VPN access | **Scoped, not promising**: Dr. Max security is not keen (see below) |
| Business Overview page | Only small changes ("today" first, budget naming) |
| "Rozpad" (breakdown) tab | Unchanged. Šimoník: "the first three [tabs] are ideal". Rozpad isn't used yet |

Šimoník on the top-level view: "I think this is absolutely ideal, it's exactly what we wanted… the top view is what we want most. The warehouses are more for logistics, but also for us, and then there's the very detailed one, in case we ever wanted to know." [translated from Czech]

### Holiday behaviour (yesterday, 2026-09-28, was a public holiday)

- Pharmacy reservations jumped today. Šimoník explained that reservations are driven by the "pick up within 15 minutes" promise. On a holiday that promise isn't shown because many pharmacies are closed, so demand shifts to the next day.
- Recognized revenue ("uznané tržby") for the holiday was about 1.2M Kč versus ~15M on a normal Monday (−93% YoY). Šimoník: "that's correct". The model already expected almost nothing to be booked for the holiday, similar to a weekend. Juraj noted that the holiday estimate itself behaved oddly and he didn't invest time into it.
- Today's run-rate showed ~19,600, about 21% above the prediction. Šimoník put this down to the first day after a holiday.

### Recognized revenue split by channel — waiting on the Excel

Šimoník asked why recognized revenue is still shown for the whole e-shop including OTC. Juraj has held it back so it can be done together with the budget Excel, which has per-channel targets, to avoid doing the work twice. The agreed split is **orders (e-com) / pharmacy reservations / marketplace**. It will **not** go down to delivery methods: "that doesn't even exist anymore" on the revenue side. Šimoník also won't give logistics the marketplace view. It will work like the created-orders view, filtered dynamically by the selected channel.

### Logistics: per-day export for shift planning

Petr Ondráček raised the export for logistics, which is not done yet. The need is the forecast **per day and per warehouse** for the coming week. Jan (Honza) Maroušek plans shifts on Wednesday–Friday for the following week, so he can call in temporary workers (brigádníci). A 7-day sum "doesn't make much sense" to them. They need daily figures ("Tuesday this many, Wednesday this many"). Šimoník suggested reusing the existing next-days table with a day picker, so the numbers are the chart's daily columns. A list at the bottom that can be pulled out through the Chrome extension is "more than enough". The view currently covers 14 days (today, 29 Sep, through 12 Oct). Juraj: "we still owe this one". He now has a clear picture and will add it.

Šimoník also mentioned a possible future view built around logistics' **cut-off times**. Logistics should specify it themselves.

### Delivery-method breakdown under a warehouse

Šimoník had asked a colleague in logistics whether the per-warehouse delivery-method sub-breakdown is needed and has no answer yet. Juraj: keep it. If nobody uses it, removing it gains nothing. Both accept that finer granularity is noisier: with ~50–300 orders a day at 30-minute resolution, ±10 orders can mean ±100%.

Warehouse context from Šimoník: **Nučice** mainly serves pharmacy pickup (orders shipped to pharmacies). **Brno** serves part of the Moravian pharmacies but mainly the parcel carriers (PPL, DODO, Česká pošta), so it has up to ~6 delivery methods.

### Operational decisions the model can't see

Petr Ondráček raised that last week logistics moved Zásilkovna volume from Brno to Nučice. This shifts the per-warehouse split sharply, and there is no channel to tell the model. Šimoník's view was that this is chicken-and-egg by design: the forecast is supposed to *trigger* exactly these decisions (e.g. "Brno can't handle next week, move some to the more elastic Nučice"). He is fine with the model not knowing what logistics will do. Juraj added that the model adapts after about 2 days when a channel shifts. History shows reality running above the prediction for a few days until the estimate caught up.

### Model accuracy reporting

Šimoník asked whether there will be a way to report how accurate the model is. He doesn't want a daily metric. He wants something like a monthly average deviation ("the model typically differs by ±3%"), possibly as a **success criterion**. He specifically wants the accuracy of the *daily* predictions, not only the month-end total, which naturally gets better toward the end of the month. Juraj already has an internal (not business-facing) task planned for this. Every model prediction is stored, so the "time travel" comparison against actuals is possible. He was waiting for enough history to build up.

Marek Pillár suggested Šimoník add it to his own requirements list, discuss it with Marek, and check with Juraj what can be measured, so the effort matches a once-a-month need and isn't overbuilt. Šimoník: even a single Excel export would do.

Petr Ondráček framed the value from the logistics side: Honza Maroušek could see what was planned for Brno and Nučice, what he changed (e.g. the Zásilkovna move), and what actually happened, and learn cause and effect for future decisions.

Šimoník's own sense: the run-rate projection is very accurate from about 10–11 a.m. Day +1 is easiest to forecast. Two weeks out is harder, but the forecast updates daily.

### Mobile / non-VPN access and an email digest

- Juraj reported that the infra/security team was "not exactly enthusiastic" about VPN-less mobile access. Vláďa (infra) said on a weekly status call that security leans stricter. Jindřich Tůma is to give the fuller update.
- Šimoník floated a fallback: a scheduled email, or an agent that takes the data at about 12–1 p.m. and sends the day's outlook (e.g. three screens). Juraj said it's technically feasible, but email support takes real work, so it's **V2 scope** to agree with Jindřich.
- Šimoník was clear it is **not a blocker for acceptance**, just nicer to use. The mobile side is partly Dr. Max's own internal problem (their security team, a VPN on a personal phone). A locked-down company phone isn't attractive to him ("I'd end up with two phones").
- Marek Pillár linked it to the **AI Platform**, which he and Tomáš Dudaško are working on. All BigHub apps for Dr. Max go under one role-based platform with its own reporting, cost tracking and access overview. Access will quite likely work without VPN, via an entry point such as SharePoint. Šimoník had heard the same from Dr. Max's IT director and liked the idea of unified access.

### Wrap-up, acceptance timeline and V2

- Šimoník owns sending the budget Excel (today, tomorrow at the latest). BigHub then finishes the budget, the per-channel revenue split and the logistics export.
- Šimoník will propose dates with the Excel for a **last follow-up in ~2–3 weeks** for the final assessment, with **final acceptance by end of October**.
- After that, Dr. Max will use the dashboard as much as possible through the season and keep a side list of ideas. A **"version 2" extension** can be discussed in January/February.
- Juraj flagged **Christmas** as the hard modelling case. He plans to tune the model for it. Normal-period predictions are reasonable.
- Marek Pillár asked Šimoník to collect that backlog and review it **before the end of the year**, not leave it for January, so BigHub can have a plan ready by January. He acknowledged Šimoník's steer that BigHub's current focus is Listing, but wants this project to keep moving too.

### BQ / KPI sign-off

Marek Pillár asked Šimoník for an email confirmation of the KPI figures. Šimoník had confirmed them verbally within an hour after their call, but Marek has since added two columns for Tomáš Dudaško: annualized savings/gain, derived from Šimoník's own numbers. He needs a written "agreed" in email ("five minutes of your time"). Šimoník: "we'll do that."

## Decisions Made

- **Final acceptance by end of October 2026**: once the budget Excel items and the logistics per-day export are delivered, a last follow-up in ~2–3 weeks gives the final acceptance of the requirements gathered so far. After that, Dr. Max uses the dashboard through the season and collects ideas for a "V2" extension discussed in Jan/Feb 2027. *(Naming overlaps with [[ASM-069]], see Open Questions.)*
- **Recognized revenue split level**: orders (e-com) / pharmacy reservations / marketplace. Not by delivery method. Implemented together with the budget Excel.
- **Mobile/non-VPN access is not an acceptance blocker**. The email/agent daily digest is an idea for V2, to be scoped with Jindřich Tůma. The AI Platform is the likely long-term path to VPN-less access.
- **Delivery-method sub-breakdown under a warehouse stays**, even while logistics hasn't confirmed they need it.
- **The model doesn't need to know about operational decisions** (e.g. moving carrier volume between warehouses). Šimoník accepts that the forecast triggers such decisions and then drifts from actuals until it catches up.
- **Model accuracy reporting stays lightweight**: a monthly view of daily-prediction deviation (even an Excel export) is enough. It isn't needed daily and shouldn't be overbuilt. It goes on Šimoník's requirements list.

## Action Items

- [ ] **Marek Šimoník**: Send the budget Excel (per-day, per-channel budget) to Juraj Kmec — due 2026-09-30 at the latest — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Marek Šimoník**: With the Excel, propose dates for the final follow-up / acceptance meeting (~2–3 weeks out, acceptance by end of October) — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Marek Šimoník**: Reply by email confirming the BQ KPI figures, including the two new annualized columns — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Juraj Kmec**: After the Excel arrives, add per-day budget values and split recognized revenue by channel (e-com / reservations / marketplace) — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Juraj Kmec**: Build the logistics per-day export (forecast by day × warehouse for the coming days, with a day picker) for shift planning — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Juraj Kmec**: Add the missed "copy" button on the Metrix/table view — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Juraj Kmec**: Turn both transcripts (2026-09-15 and today) into tasks — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Juraj Kmec**: Run the planned internal model-accuracy evaluation once enough history exists — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Jindřich Tůma**: Give Šimoník the infra/security update on mobile/non-VPN access, and scope the email-digest idea as V2 — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Marek Šimoník**: Get logistics' answer on whether the per-warehouse delivery-method breakdown is needed, and let logistics specify any cut-off-time-based view — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Marek Šimoník**: Collect the V2 backlog (incl. model-accuracy reporting) — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Marek Pillár**: Review Šimoník's collected V2 backlog with him before year-end, so a plan is ready for January — due 2026-12 — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] **Marek Pillár**: Chase Šimoník's email sign-off on the BQ figures (annualized columns) if not in by end of week — from 2026-09-29-order-prediction-dashboard-v2-review

## Open Questions

- **Version naming vs. [[ASM-069]]**: on 2026-09-15 the build was accepted as "v1" and the feedback batch became "v2". Today Šimoník talks about a *final acceptance* at end of October and a *"version 2"* extension in Jan/Feb. In practice, today's batch is the "v2" of ASM-069, and the Jan/Feb extension would be ASM-069's "v3". Which labels should BigHub use with the client?
- Does the per-day logistics export cover what [[ASM-111]] (the "~90% ready" logistics shift-planning extension) described, or is that still a separate piece of work?
- Does logistics need the delivery-method sub-breakdown per warehouse? Šimoník is waiting on a colleague.
- Items from 2026-09-15 not mentioned today: the "data as of" timestamp label, renaming the T-7/T-364 comparison, reservation-specific historical comparison, pre-summed totals on Business Overview. Status unknown.
- Model accuracy as a formal success criterion: what threshold (Šimoník's example was ±3%) and what measurement method? This ties into the BQ tracker's KPI-measurement-method column.

## Sentiment & Tone

Warm and positive, with a clear shift from "working session" to "closing out". Šimoník opened with unprompted praise ("super", "I'm really happy it's there") for the run-rate projection and the hierarchical view. He apologized twice for the late Excel and took ownership of it as the main blocker, which BigHub waved off graciously. He repeatedly defused his own asks ("I'm just brainstorming", "I definitely don't want this to be a blocker for acceptance", "not something I'd check daily"). Together with his instinct to not overbuild the accuracy report, this reads as a business owner protecting BigHub's scope, not piling on.

Relationship signals:
- **Trust in the model is growing but not yet quantified.** Šimoník trusts the intraday run-rate from experience. He is now asking for an accuracy number to *rely on*, which is a natural next step and a good fit for the BQ success criteria.
- **Ondráček is the logistics voice in the room.** He raised the Zásilkovna move and the per-day export, and turned Honza Maroušek's shift planning into a concrete requirement. That makes logistics a real second user group.
- **Šimoník is already thinking beyond this dashboard.** He knew about the unified AI platform from Dr. Max's IT director and welcomed it. That is positive cross-validation for the platform initiative.
- **One soft signal**: Šimoník has told Marek Pillár that BigHub should focus on Listing. Marek pushed, politely, for this project not to stall after acceptance. Watch whether V2 gets real attention from Dr. Max after October or quietly fades.
- Jindřich Tůma's absence had no visible effect. Juraj ran the session confidently on his own.

## Routing Log

- **project-assumptions**: Added ASM-191 (Decided): final acceptance by end of October, client "V2" in Jan/Feb 2027. ASM-192 (Decided): recognized revenue split by channel. ASM-193 (Decided): mobile access not a blocker, email digest in V2. ASM-194 (Decided): model not fed operational decisions. ASM-195 (Open): model-accuracy reporting. Updated ASM-069 (client naming: "final acceptance" = our v2, client "V2" = our v3), ASM-110 (timing made concrete) and ASM-111 (per-day × per-warehouse shift-planning export).
- **project-stakeholders**: Updated STK-019 (Šimoník), STK-035 (Ondráček), STK-009 (Kmec), STK-016 (Vláďa). STK-036 ("Honza") merged into STK-021 Jan Maroušek, identity confirmed by PM; role updated to logistics shift planner.
- **project-knowledge**: Enriched the "Order-Prediction Dashboard (Řízení poptávky)" entry with the v2 build, holiday effects, warehouse roles, model adaptation, granularity noise and accuracy-data notes.
- **project-daily**: 1 PM-owned action item added (year-end V2 backlog review). The existing BQ sign-off item was annotated. Non-PM action items stay in this note only.
- **project-lessons**: LL-69 (forecast-triggered decisions vs. accuracy measurement).
