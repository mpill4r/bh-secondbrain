---
last_updated: 2026-09-15
type: external
attendees: [Marek Pillár, Tereza Foltýnová]
tldv_link:
---

# Business Quantification Call with Tereza Foltýnová — Reklamace & Fakturace Doprav

**Date**: 2026-09-15
**Attendees**: Marek Pillár (BigHub, running the interview), Tereza Foltýnová (ViaPharma CZE — logistics/claims data consolidation)
**Type**: external
**Recording**: N/A (pasted transcript, no timestamps beyond MM:SS speaker tags)
**Previous session**: N/A directly (first live execution of the Business Quantification workshop) — see [2026-09-14-ai-initiatives-business-quantification-prep](../prep/2026-09-14-ai-initiatives-business-quantification-prep.md)
**Meeting prep**: [2026-09-14-ai-initiatives-business-quantification-prep](../prep/2026-09-14-ai-initiatives-business-quantification-prep.md)

## TL;DR

First live run of the Business Quantification workshop (the 6-field OKR-card interview script from `ai-initiatives-okr-framework.md`) — but only 2 of the ~11 prepped initiatives were covered (Reklamace, and the freight-invoicing item labeled "fakturace od dodavatelů" on the roadmap) before Tereza had to hop to another call. Both cards got real, if uncertain, numbers — Tereza pushed back constructively on an initial Fakturace doprav estimate that felt too large rather than accepting it, and both explicitly deferred final figures to the actual business owners (Petr Spilka, Jan Žižka) for confirmation. A likely resolution surfaced for a long-standing naming ambiguity: the roadmap's "fakturace od dodavatelů" line appears to actually be the freight/transport invoicing initiative (Fakturace doprav), not a separate supplier-invoicing stream.

## Key Discussion Points

### Process setup

Marek is building his own working version of the initiative-tracking sheet, to be reconciled later with Tomáš Dudaško's master Excel; Tereza will review the final version against her own tracker for consistency, and Marek will send her either the document or the call recording afterward. Marek explicitly framed the "I don't know" answer as acceptable throughout — unknowns get flagged as estimates, not treated as blockers, matching the interview script's opening norm-setting line.

### Reklamace — Objective (JTBD)

Tereza explained the origin of the Reklamace initiative: an external firm (Ableneo) auditing ViaPharma's processes flagged that the claims process was paper-heavy and fragmented — separate systems that don't automatically communicate, staff photographing claim evidence to WhatsApp and manually forwarding it, and knowledge scattered per warehouse and even per individual staff member (personal Excel sheets/notebooks, no shared source of truth). She was explicit that this wasn't really about *error rates* — staff know the repetitive process well from memory — but about reducing the friction and cognitive load of a fragmented, multi-step manual flow: "pojďme to prostě hodit do nějakého lepšího kabátu, než aby opravdu každá holka měla jako svůj sešit" [translated from Czech: "let's just put this into a better shape, rather than every person having their own personal notebook"].

### Reklamace — Business Value & KPIs

- **Owner**: Petr Spilka (confirmed — matches existing record).
- **Domain expert**: Tentatively Petr Spilka again, with Jana Egrmaierová floated as a possible alternative — Tereza wants to confirm this with Spilka directly before finalizing.
- **Business value (Fermi estimate, explicitly unconfirmed)**: ~4 people, each saving ~2 hours/day → ~8 hours/day ≈ 1 FTE. Tereza was clear this is an estimate grounded in an earlier internal analysis, not invented on the spot, but not a hard measurement either. A wage-cost figure (~3000, unit/currency unclear from the transcript — likely a per-unit "mzdový náklad" reference) was mentioned but needs verification.
- **Primary KPI**: End-to-end process time (current vs. post-launch) — there's no existing tool to measure this today, so a baseline measurement is needed before launch and a comparable measurement after. The exact success threshold wasn't cleanly landed on in the call — Marek floated "50% faster," then recalculated toward "~25% faster" based on the 2-of-N-hours framing; this needs tightening, not treated as decided.
- **Secondary KPI**: A post-launch (≥3 months) user satisfaction survey among affected staff, using a small-sample usability-testing rule of thumb (6–7 people; majority — e.g. 4 of 6/7 — satisfied counts as success, i.e. a ~66% target).
- **Explicitly rejected as a KPI**: document/claim error rate — Marek raised it, but both agreed attribution would be unclear (illegible handwriting vs. driver error vs. other causes) and it would effectively require driver education rather than measuring the tool itself — dropped from this round.
- **Phasing note**: Reklamace ships in 5 phases (0 through 4/5 per the dev roadmap — the exact numbering was somewhat garbled in the transcript); the full ~1 FTE saving only materializes once **all** phases are live. Tereza asked for the phases to be made explicit in the documentation (e.g. Phase 0 = Příprava/preparation, Phase 1 = příjmové reklamace/receiving claims) because people currently confuse "příjmové" (receiving) vs. "dodavatelské" (supplier) claim types.

### Fakturace doprav ("fakturace od dodavatelů" on the roadmap) — Objective (JTBD)

Tereza described a heavy manual burden on the transport/logistics office staff, who manually collect, verify, and compile driver-submitted delivery documents by hand — currently causing overtime. The goal is to scan/automate as much of this as possible via the drivers themselves. She was explicit the framing isn't headcount reduction so much as freeing existing staff from repetitive manual work to do their actual jobs: "spíš těm lidem jako rozvázání ruce" [translated from Czech: "more like freeing people's hands"].

### Fakturace doprav — Business Value & KPIs

- **Owner / domain expert**: Jan Žižka (heard phonetically as "Honza Hiška" in the transcript — matches the existing Jan Žižka / STK-015 record). He hasn't seen the tracking table yet; Tereza will confirm with him directly.
- **Business value (Fermi estimate, explicitly flagged as possibly too large)**: ~16 hours/day (2 people × 8 hours) → a potential annual saving in the range of ~1.5 million [currency not stated, presumably Kč]. Tereza pushed back on this number herself as feeling too ambitious and wants to re-verify it with Žižka before it's treated as reliable. Source: an earlier Ableneo estimate of ~90 hours/month of relevant manual work, with 40–60% considered automatable.
- **Scope clarification**: These savings are entirely on the office/administrative side — drivers are explicitly *not* ViaPharma/Dr. Max employees ("řidiči ty vůbec nejsou naši"), so driver time is out of scope for the cost/FTE calculation. A driver satisfaction check was floated as a soft, secondary nice-to-have (since the kiosk changes their workflow slightly), not a hard KPI — to be run past Žižka given his direct driver relationship.
- **Primary KPI**: Total administrative time-fund reduced by ~40% — Tereza was clear this has to be measured in aggregate (total hours spent on this work), not per-headcount, since the relevant staff's time isn't cleanly separable by task.
- **Explicitly rejected as a KPI**: Same as Reklamace — document error rate was raised and dropped for the same attribution reasons.

### Naming clarification

Tereza asked for a naming adjustment on the roadmap: append a domain qualifier so "fakturace od dodavatelů" reads as the transport/freight item ("doprava") and Reklamace reads as the "core sklady" (core warehouses) item — matching Dr. Max's internal Core/Ecom domain convention, which she said would reduce confusion since some initiative names currently read as too generic/interchangeable.

**This plausibly resolves a standing ambiguity** flagged earlier in `project-stakeholders` (STK-015, STK-024) and `project-assumptions` (ASM-006) about whether "fakturace od dodavatelů" (supplier invoicing) and "Fakturace doprav" (freight invoicing) are the same or different initiatives — the owner match (Jan Žižka) and Tereza's own "je to ta doprava" framing both point to these being the *same* initiative, tracked under a misleadingly generic label, not two separate streams. Flagged for PM confirmation rather than auto-resolved.

### Wrap-up and scope gap

The call ended earlier than planned — Tereza had another call to join — after covering only Reklamace and Fakturace doprav. The remaining ~9 initiatives from the prep template (the other Žůrek/logistics initiatives) were not discussed and still need their own session(s). Tereza also flagged she's unavailable starting this Friday (reason/duration unclear from the transcript) and may not be able to loop in Petr Spilka/Jan Žižka for review before then — possibly slipping to the following week.

## Decisions Made

- Document/claim error rate is explicitly excluded as a KPI for both Reklamace and Fakturace doprav — attribution to the tool vs. driver/staff behavior is too unclear to be a clean metric.
- Driver time and cost are out of scope for Fakturace doprav's business-value calculation — drivers aren't ViaPharma/Dr. Max employees; only office/administrative time counts toward the FTE/hours-saved figure.
- Reklamace's full projected FTE saving is contingent on all 5 delivery phases shipping, not any single phase — the documentation should make phase-by-phase scope explicit rather than implying the saving lands immediately.
- Both business-value estimates discussed today (Reklamace ~1 FTE, Fakturace doprav ~2 FTE/~1.5M annually) are provisional Fermi estimates pending confirmation from the actual business owners (Petr Spilka, Jan Žižka) — not to be treated as final numbers yet.

## Action Items

- [ ] **Tereza Foltýnová**: Confirm the Reklamace domain expert (Petr Spilka vs. Jana Egrmaierová) directly with Petr Spilka — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Tereza Foltýnová**: Verify the Reklamace business-value estimate (~1 FTE / ~2 hours saved per person per day, ~3000 wage-cost figure) with Petr Spilka — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Tereza Foltýnová**: Verify the Fakturace doprav business-value estimate (~16 hours/day, ~2 FTE, ~1.5M annual) with Jan Žižka — flagged by Tereza herself as feeling too large — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Marek Pillár**: Send today's captured Reklamace and Fakturace doprav cards to Tereza for review — due today, 2026-09-15 — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Tereza Foltýnová**: Loop in Petr Spilka and Jan Žižka to review/confirm names and content on the tracker — target end of this week (Friday), may slip to next week given her own availability — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Marek Pillár**: Add explicit phase labels (0 through 4/5, e.g. Phase 0 = Příprava, Phase 1 = příjmové reklamace) to the Reklamace documentation, distinguishing "příjmové" vs. "dodavatelské" claim types — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Marek Pillár**: Adjust initiative naming on the roadmap tracker to add domain qualifiers — "fakturace od dodavatelů" → clarify as transport/doprava, Reklamace → clarify as core sklady — matching the Core/Ecom convention — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] **Marek Pillár / Tereza Foltýnová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — from 2026-09-15-business-quantification-reklamace-fakturace-doprav

## Open Questions

- Is "fakturace od dodavatelů" (as tracked on Tomáš Dudaško's roadmap Excel) actually the same initiative as "Fakturace doprav" (freight invoicing, Jan Žižka)? Today's content strongly suggests yes, but it isn't a formal, explicit confirmation.
- What is the exact unit/currency behind the "~3000" wage-cost figure mentioned for Reklamace? The transcript is garbled at that point.
- What precise end-to-end time-reduction target should Reklamace's primary KPI use — the call floated both "50% faster" and "~25% faster" without settling on one.
- Is Jana Egrmaierová a Reklamace domain expert alongside or instead of Petr Spilka?
- Why and for how long is Tereza unavailable starting this Friday — does it affect the timeline for getting Spilka/Žižka's review?

## Sentiment & Tone

Positive, collaborative, and notably well-calibrated — Tereza pushed back on her own initiative's numbers rather than accepting an inflated estimate (explicitly flagging the 16-hours/day Fakturace doprav figure as feeling too ambitious and wanting to verify it before it's trusted), which is a strong signal of honest engagement with the quantification exercise rather than motivated reasoning toward a bigger business case. Marek's interview technique visibly worked as designed — sticking to JTBD-style "what" questions, resisting a weak KPI candidate (error rate) even when it would have been easy to just add it, and explicitly normalizing "I don't know" answers. No friction anywhere in the call. The one soft signal: the session ran short of its full scope (2 of ~11 initiatives) purely due to time/scheduling pressure on Tereza's side, not disengagement — worth planning a tighter follow-up cadence rather than assuming the remaining initiatives can be rushed into leftover time.

## Routing Log

- **project-assumptions**: Added ASM-072 (Decided) — error rate excluded as a KPI for both initiatives, driver time/cost excluded from Fakturace doprav's FTE calc, Reklamace's FTE saving contingent on all 5 phases. Updated ASM-006 — the invoicing-solution/Fakturace-doprav naming conflict moved from fully open to "leaning resolved" based on today's evidence.
- **project-stakeholders**: Enriched STK-013 (Tereza Foltýnová), STK-015 (Jan Žižka), STK-044 (Jana Egrmaierová — floated as a possible domain expert). Narrowed STK-014 (Petr Spilka)'s role description, which had overstated Fakturace doprav ownership against today's call and ASM-006.
- **project-knowledge**: Added "Reklamace (claims) — business objective & phasing" and "Fakturace doprav — business objective & KPIs" entries.
- **project-daily**: 8 action items added to 2026-09-15's daily; the original "run the Business Quantification call" item marked partially done rather than checked off.
