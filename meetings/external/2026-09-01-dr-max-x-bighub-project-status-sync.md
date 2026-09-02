---
last_updated: 2026-09-01
type: external
attendees: [Jindřich Tůma, Lukáš Szücs, Tereza Foltová, Jan Kabát, Marek Pillár]
tldv_link:
---

# Dr. Max x BigHub Sync — Project Status Walkthrough

**Date**: 2026-09-01, 15:00
**Attendees**: Jindřich Tůma (BigHub — new unified PM, ~half-time on-site), Lukáš Szücs (Dr. Max CZE — Project Manager), Tereza Foltová (ViaPharma CZE — vendor, logistics data), Ján "Jan" Kabát (BigHub — Head of Sales, key account owner @ Dr. Max, joined ~16 min in), Marek Pillár (BigHub — PM / AI Analyst, formally introduced during this call). Tomáš Dudaško was invited but absent.
**Type**: external (status sync — cross-team with Dr. Max/vendor attendees)
**Recording**: N/A (Fireflies transcript, PDF export)
**Previous session**: N/A — first captured instance of this specific joint status call; note this is distinct from the same-day BigHub-internal prep sync captured separately in `meetings/internal/2026-09-01-dr-max-business-sync.md` (different attendees and content — that one has no Dr. Max/vendor participants).
**Meeting prep**: N/A

## TL;DR

Recurring cross-team status call (previously run by Alana, now run by Jindřich) walking through all active Dr. Max project streams: logistics/claims knowledge-base consolidation (on Tereza/ViaPharma's side, in progress), freight invoicing (scope agreed with Jan Žižka, needs Petr Spilka's review by mid-September), e-commerce order prediction (built, demo Thursday, blocked-ish on AKS access), listing (blocked pending a Magento-vs-Farmis functionality analysis assigned to Honza Sovka), MaxBuddy (acceptance protocol sent for the delivered project; a live production incident this stays open; a new analytics-safety process agreed with Dr. Max's analytics team), Max/Maxi/Lexi chatbots (demo Thursday; Lexi being rolled out to Legal and Brno accounting; a design/logo blocker resolved by reusing the current look until Brno's tender concludes), and the voicebot (infra access list finally submitted to Atlantis/Vláďa Tvarušek, pending provisioning). Jindřich formally introduced Marek Pillár to the Dr. Max/ViaPharma side as the new BigHub AI Analyst who will be working the account alongside him; Dr. Max needs to provision him a client account/Teams access.

## Key Discussion Points

### Logistics — claims (reklamace) knowledge-base consolidation

Data now sits with Tereza Foltová's side (ViaPharma); she confirmed nothing is blocked on BigHub and test data/vendors have already been handed over — the delay risk, if any, is on her side working through ~15 rows of supplier-specific data. Jindřich clarified the project's scope now also includes standardizing the process across suppliers, not just this data pull: they expect ~90-95% of suppliers to converge on one unified process, with the rest handled as documented exceptions in the knowledge base. Tereza will flag which suppliers are non-standard/harder cases (referencing prior input from Petr Spilka) and aims to finish ahead of schedule.

### Logistics — freight invoicing (fakturace doprav)

Scope has been agreed with Jan Žižka (Dr. Max). Next step: **Petr Spilka** needs time to review what changed/didn't change in the reworked scope — expected mid-September. In parallel, Jindřich/Lukáš want to start a conversation with Dr. Max/Atlantis about a physical DHL-related location/site question (raised by "Kim") — Jan Sovka already has a contact for this — to see if it can be resolved in the same pass rather than duplicating effort. Jindřich asked to sit with Lukáš Szücs in person the next day at the Dr. Max office to go deeper.

Separately, Jindřich confirmed to Tereza that the timeline document he'd promised for this project will land this week, as committed.

### E-commerce — order prediction (predikce objednávek)

Build is complete; a demo/rehearsal with **Marek Šimoník** (Dr. Max) is scheduled for Thursday — delayed a week because Šimoník was on vacation. Lukáš flagged they'll again run into the **AKS** access issue: a new AKS instance was provisioned yesterday, and access/`prostupy` approvals span multiple BDC teams, so it has to go through a full access-request cycle again. Vláďa Tvarušek is reportedly handling most of it himself. Jindřich will visit Tvarušek in person the next day (he's based in Horoměřice) to try to speed up approvals — this access also blocks MaxBuddy's rollout to the remaining pharmacies, which they want completed by end of month, so there's shared urgency.

### E-commerce — Listing

No progress to report since the last status (when Alana was still running these calls) — Lukáš never got agenda space to present to **pan Žák**/at the management meeting. Jindřich's read: this is blocked pending a **Magento vs. Farmis functionality gap analysis**, following a meeting with pan Ondráček and pan Neumann, which Jindřich has assigned to **Honza Sovka** so the team doesn't build something that has to be re-architected once the analysis lands. Lukáš clarified the analysis needs to cover not just this specific case but the broader picture — listing isn't just 1P e-commerce products, but company-wide listing.

### MaxBuddy

A post-production package was deployed successfully, currently live on a small subset of branches — deliberately chosen because they have younger staff who are more receptive to change, making them a good test group. Early feedback is positive. An **acceptance protocol** was sent to Tomáš Dudaško (via Alana) to formally close out and accept the whole delivered project to date; going forward, incremental change packages (like this one) will each be accepted the same way.

A meeting with **pan Machát** (Dr. Max analytics) about an hour before this call surfaced a real risk: changes to the underlying data model (e.g. adding a column) as part of building out MaxBuddy risk breaking Dr. Max's company-wide analytics. Agreed approach going forward: the analytics team gets looped in at an appropriate point in the dev process — once a batch of backlog items is prioritized for the next release — to review and approve/adjust the affected data fields before it ships.

Lukáš separately flagged two Buddy outages in the last two weeks — root cause wasn't the BigHub application itself, but a Farmis release that broke a library/service dependency; he doesn't have full details but confirmed it happened. No concrete mitigation yet — Jindřich flagged it as an open question to revisit (how it was detected, whether it's preventable) and suggested reviewing further the next day in person.

### Max Chatbot / Maxi / Lexi

**Max chatbot**: demo scheduled Thursday; team is currently working through a ticket backlog, prioritized so that Call Center's user-facing requests (which Jindřich wants shown at the demo, so Call Center can validate them) go first, with infrastructure-only tickets held for a second batch after the demo.

**Lexi**: same status/approach as Max. Additionally, Lukáš (with the infra team) has prepared Lexi so that **Legal** and **Brno accounting (účtárna)** can start populating its knowledge base and testing it — coordination on rollout with those two departments is starting now, and they'll also canvass other departments for interest. Jindřich separately confirmed **IT (Petr Machán)** is already using it and speaks highly of it; any IT-specific feature requests will be incorporated over time, but current focus stays on Call Center. That makes IT, Legal, Brno accounting, and (once live) Call Center four departments in play for Lexi.

Recap of a separate meeting with **paní Martová** (Dr. Max) last week: (1) they agreed to add a justification column to the Max/Maxi/Lexi tracking tables — time saved, cost saved, etc. — so value can eventually be measured; (2) the chatbot's design/logo had been blocked because Dr. Max's Brno headquarters ran a separate tender for design/logo work company-wide. Resolved: BigHub will ship now using the current design/logo (following the Slovak precedent) so as not to block deployment, and apply the new branding in a later wave once Brno's tender concludes and a direction is chosen. Jindřich and Lukáš explained this trade-off to Martová directly and she agreed not to block the current release on it.

### Max VoiceBot

Prior test/rehearsal with Alana happened last week (pan Techl was on vacation). Per earlier guidance from **pan Žák**, if the timeline slips further the team is to raise a flag/stop point explicitly rather than let it drift silently. Update from Atlantis today: the required access/`prostupy` list was received, and Jindřich has forwarded it to **Vláďa Tvarušek** (infra); now waiting on provisioning. Some delay is expected since the AKS work is competing for the same infra attention, but there's no indication of any technical or approval blocker at this point.

### Marek's introduction to the client

Jindřich formally introduced Marek Pillár to the Dr. Max/ViaPharma side as BigHub's new hire, being trained by Jan Sovka, joining as **AI Analyst**, and working alongside Jindřich on the account going forward — describing them as building a team together. Jan Kabát added that he and Jindřich had already flagged to Tomáš Dudaško in an earlier 1:1 that they wanted to invest further in the relationship and that the Jindřich+Marek pairing is intended to be the key to unlocking the next phase — though this hadn't yet been broadcast more widely before today. Lukáš asked for Marek's name, surname, phone, and email so Dr. Max can provision him an account (Teams access etc.); Jindřich confirmed BigHub hadn't sent this yet and will sort it out; Jan Kabát offered to send Lukáš the details directly. Marek closed by thanking the group, noting his background across several agencies/larger companies, and said he'll spend the coming period getting up to speed on documents and meetings.

## Decisions Made

- Freight-invoicing and claims-consolidation projects proceed as scoped; freight-invoicing scope review by Petr Spilka targeted for mid-September.
- MaxBuddy: all future incremental change packages will be formally accepted the same way as the original delivered project (via acceptance protocol), rather than left informally open-ended.
- MaxBuddy/analytics: any change touching the shared data model must be reviewed by Dr. Max's analytics team (contact: pan Machát) at the point a release batch is prioritized, to avoid breaking company-wide analytics.
- Chatbot (Max/Maxi/Lexi) design/logo: ship now with the current design (Slovak precedent), apply Brno's new branding in a later wave once their tender concludes — do not block current deployment on it.
- Listing project is paused pending the Magento-vs-Farmis functionality gap analysis (assigned to Honza Sovka) before further build work.

## Action Items

- [ ] **Jindřich Tůma**: Sit with Lukáš Szücs in person (Dr. Max office) to go deeper on the freight-invoicing scope and the DHL/site question — due 2026-09-02
- [ ] **Jindřich Tůma**: Visit Vláďa Tvarušek in person (Horoměřice) to push AKS access approvals — due 2026-09-02
- [ ] **Jindřich Tůma**: Deliver the promised project timeline document to Tereza Foltová — due this week (~2026-09-05)
- [ ] **Honza Sovka**: Complete the Magento vs. Farmis functionality gap analysis for the listing project — from 2026-09-01-dr-max-x-bighub-project-status-sync
- [ ] **Jan Kabát**: Send Marek Pillár's account details (name, surname, phone, email) to Lukáš Szücs for Dr. Max/Teams provisioning — from 2026-09-01-dr-max-x-bighub-project-status-sync
- [ ] **Team**: Prepare for Thursday demos — order-prediction demo with Marek Šimoník, and Max chatbot demo (Call Center-facing tickets first) — due 2026-09-04 (Thursday)
- [ ] **Lukáš Szücs**: Coordinate with Legal and Brno accounting to onboard them onto Lexi (knowledge-base population + testing) — from 2026-09-01-dr-max-x-bighub-project-status-sync

## Open Questions

- Root cause and prevention plan for the two recent MaxBuddy outages caused by a Farmis release breaking a dependency.
- Whether AKS access approvals (spanning multiple BDC teams) will move faster than last time.
- Whether Petr Spilka's freight-invoicing scope review (mid-September) surfaces any changes to what's already agreed with Jan Žižka.

## Sentiment & Tone

Businesslike, well-run status meeting with a clear walking-the-board format — Jindřich runs it competently and has clearly absorbed the account since taking over from Alana, referencing prior context accurately and following up on earlier commitments (e.g. Tereza's timeline document) unprompted. The tone with Dr. Max/ViaPharma participants is warm and collaborative — Tereza is proactive and reassuring about not blocking BigHub; Lukáš is thorough and raises real operational issues (outages, access blockers) matter-of-factly rather than defensively. The MaxBuddy/analytics risk (Machát's finding) is handled constructively — surfaced early and immediately resolved into a concrete process, not left hanging. Marek's introduction lands warmly; Jan Kabát's framing ("this duo is the key") signals real organizational investment in the account, consistent with what Jan Sovka described in the earlier onboarding call. Marek's own closing remarks are confident and appropriately humble about the ramp-up ahead.

## Routing Log

- **project-stakeholders**: Added STK-012 (Lukáš Szücs), STK-013 (Tereza Foltová), STK-014 (Petr Spilka), STK-015 (Jan Žižka), STK-016 (Vláďa Tvarušek), STK-017 (Martová), STK-018 (Petr Machán), STK-019 (Marek Šimoník), STK-020 (Marie Hulešová), STK-021 (Jan Maroušek) to External Stakeholders; STK-022 (Sony Vu Hong) to Internal Team. Enriched STK-001, STK-002, STK-003, STK-004, STK-005, STK-009 (Juraj Kmec surname resolved) with role/title detail from the Who's Who reference card.
- **project-knowledge**: Added Max/Maxi/Lexi, BDC, Atlantis, AKS (Needs confirmation), Farmis/Magento (Needs confirmation); updated Dr. Max/ČLH entry with current active project-stream list including Kontrola beden (not yet started).
- **project-assumptions**: Added ASM-004 (analytics review required for MaxBuddy data-model changes, Decided) and ASM-005 (Open — Who's Who card reconciliation pending Marek's verification).
- **project-daily** (2026-09-01): Logged 7 open action items; checked off the carried "confirm Marek's Tuesday-status inclusion" item from the 2026-08-25 onboarding meeting as resolved by this call.

> Migration note: this meeting note was originally routed and processed on 2026-09-01 in the predecessor repo (`bh-secondBrain`), where meetings were kept in a single flat folder. Ported into this template on 2026-09-02 into `meetings/external/` and reclassified to the fixed `internal | client | external | milestone` type enum — `external` chosen because Second Brain has no formal client (see `client-overview.md`) and this call's non-BigHub attendees (Dr. Max, ViaPharma) make `internal` inaccurate; original free-form type: "status sync". Content and routing log unchanged.
