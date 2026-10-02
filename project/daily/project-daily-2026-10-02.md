---
status: closed
last_updated: 2026-10-02
last_updated_by: auto — project-daily close
project_status: Amber
---

# Daily — 2026-10-02 (Friday)

## Project Status

**Amber** (carried forward from 2026-10-01). Driver: **Reklamace**. The 10-01 logistics meeting unlocked the standoff: Sláma's May comment was accepted, Excel is out, and supplier data is converging on one SharePoint List keyed by supplier account ([[ASM-223]], [[ASM-228]]). Still pending: Sláma's column-J feedback (early week of 10-05), a named Dr. Max owner for the List ([[ASM-215]]), and the knowledge-base decision by 2026-10-09 ([[ASM-184]]). Phase 1 testing was extended by a week ([[ASM-227]]); the effect on the 10-15–16 UAT is unconfirmed.

## Current Priority

**Reklamace, Monday 2026-10-05 10:00 meeting + recap/spec**: prepare the in-person "next steps" meeting with Jindřich (Žůrek, Dudaško, Spilka, Tereza; likely a value/continuation question, [[ASM-242]]), then accept/reject v5 and send logistics the 10-01 recap + spec with the open questions (supplier store, avízo, labels sample). Shifted at close from "recap + spec by 10-02": the spec work ran through v4/v5 today, and the Monday meeting surfaced as the bigger risk.

## Action Items

- [ ] `carry-forward` `highest-prio` **Marek Pillár**: In parallel, draft the new (final) Reklamace spec with all product comments/requirements worked in. Leave the Excel's open decisions as open for now — from PM's plan, 2026-09-29 — partial 2026-09-29: first full draft `1. Feature Specs/3. Reklamace/3. Reklamace.docx` created via /product-client-spec; awaiting PM review — updated at close: working version is `3. Reklamace v3.docx` (PM review comments applied twice; v1/v2 deleted); still open until the 10-01 decisions are added — partial 2026-10-02: internal v4 with 10-01 outcomes + contract facts created; PM review pending, then client version
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Once the Excel is approved, add the AGREED decisions to the spec and send it to logistics / Petr Sláma for final approval. Target: spec with the knowledge base decided — due 2026-10-09 — from PM's plan, 2026-09-29
- [ ] `carry-forward` `follow-up` `mid-prio` **Marek Pillár**: Contact Filip Černý to walk through his growing pile of business-decision questions from Max/ViaPharma people; plan whether a direct meeting with them is needed — medium priority — from Filip Černý's Fakturace doprav backlog note, 2026-09-08
- [ ] `carry-forward` `follow-up` `low-prio` **Marek Pillár**: Data drift found on Maxie roadmap row "Přepojení na živého operátora při chybě nebo požadavku" — local roadmap data has it as Done, live Excel shows Planned. Not changed either way (out of scope for the estimates-routing task) — worth a quick check on which is correct — Marek's own note, 2026-09-09 — reprioritized via /todo review (2026-09-17)
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — **blocked: waiting on Honza Sovka's review first** — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] `carry-forward` `low-prio` **Marek Pillár / Tereza Foltýnová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — **deprioritized 2026-09-15**: no rush, will revisit sometime later this year — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] `carry-forward` **Marek Pillár / Jindřich Tůma**: By end of this week, prepare a work-in-progress AI Platform spec/roadmap with open questions to show Dudaško — sequencing: design phase (~1 week), admin/role-views phase (~2-3 weeks), agentic-workflow follow-up conversation tentatively November — from 2026-09-21-ai-platform-vision-discovery-dudasko — partial 2026-09-24: Phase 1 prototype shown and accepted by Dudaško; written spec/roadmap still open (2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko) — moved to the week of 2026-09-28 per PM (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the disambiguation-approach conflict with ASM-119 — confirm whether the ranked-candidate mechanism is being reversed or whether this was a narrower UI-presentation point — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` `mid-prio` **Marek Pillár**: Get Filip Černý to confirm/reconcile the 5 code-vs-spec contradictions found in today's Fakturace doprav code audit (kiosk auth, document versioning, AR pairing, temperature-log OCR gap, multi-vehicle silent overwrite) — [[ASM-131]], [[ASM-132]], [[ASM-133]], [[ASM-134]], [[ASM-135]] — before the spec is finalized or shared further — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, below Reklamace in priority (2026-09-25)
- [ ] `carry-forward` **Marek Pillár**: Confirm with P. Sláma whether the AR-pairing-key dependency (ZOPV/OPL) is already resolved in code — [[ASM-133]] — and update the Závislosti section accordingly — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, with the Fakturace contradictions (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Check whether ElevenLabs barge-in can pick up the interrupting context and respond to it, and report back to Mertová — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Marek Pillár**: Add a KPI measurement-method column to the BQ tracker and collect measurement methods from every business owner — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Collect and prioritize department AI-initiative backlogs (logistics, marketing via Marek Dvořák, others) in BQ tracker format — target end of November 2026 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Get email sign-off on BQ figures from Marek Šimoník (after vacation) and Simona Mertová — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko — partial 2026-09-29: Šimoník agreed on the call to confirm by email, incl. the 2 annualized columns for Dudaško; chase if not in by end of week (2026-09-29-order-prediction-dashboard-v2-review)
- [ ] `carry-forward` **Marek Pillár**: Talk with Jindřich Tůma about the capacity pool: is he inside the 3 FTE or extra, and what does his September capacity table show ([[ASM-167]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [x] `carry-forward` **Marek Pillár**: Ask Tomáš Dudaško whether the cross-department AI-initiative tracker can be shared with other departments ([[ASM-179]]) — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table — done 2026-10-02: master shared read-only with departments (2026-10-02-logistics-initiatives-green-field-cenarky-analysis)
- [x] `carry-forward` **Marek Pillár / Tereza Foltýnová**: Review her draft table together (Wed/Thu) before the 2026-10-02 session — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table — scheduled 2026-09-30 at Max (2026-09-29-management-meeting-debrief-reklamace-thursday-plan) — superseded 2026-10-02: list rebuilt from a green field (2026-10-02-logistics-initiatives-green-field-cenarky-analysis)
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: After the Thursday session, email logistics the agreed decisions for confirmation and send the Reklamace spec with agreed changes or yellow-highlighted open questions ([[ASM-185]], [[ASM-186]]) — due 2026-10-02 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan — partial 2026-10-01: meeting held, direction converging (Excel out, one SharePoint List keyed by supplier account, [[ASM-228]]); recap + spec still to send (2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review) — not sent 2026-10-02: spec v5 ready for PM accept/reject first; recap + spec to go early week of 10-05
- [ ] `carry-forward` **Marek Pillár**: Meet Tereza Foltýnová at Max to review the initiatives she collected since Friday — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` `mid-prio` **Marek Pillár**: Define each later phase's value driver ("system seller") with each initiative owner via discovery; give logistics outlook anchor points next week; coordinate capacity with Jindřich Tůma before promising anything ([[ASM-190]]) — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Put blockers / personal time into the calendar so Jindřich Tůma can plan meetings around it — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` **Marek Pillár**: Send a four-point summary of the internal sync to the BigHub business group (for Ján Kabát and Jan Sovka) — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` **Marek Pillár**: Check whether logistics specified expectations for the first supplier email / time saving — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Review Marek Šimoník's collected order-prediction V2 backlog (incl. model-accuracy reporting, email digest) with him before year-end, so BigHub has a plan ready for January ([[ASM-191]]) — due 2026-12 — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] `carry-forward` **Marek Pillár**: Contact Jiří Trajer about receipt data (expedition number + product codes) and per-product profitability; define and analyse the data table ([[ASM-197]]) — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `carry-forward` **Marek Pillár**: Once there's a first version, specify the profitability-based recommendation with Luboš Vosmek (3-tier model and/or receipt-based learning, incl. the legal "no AI" question) — due start of 2027 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `carry-forward` **Marek Pillár**: Agree with Jindřich Tůma where the MaxBuddy backlog is tracked (not in DevOps today, [[ASM-202]]) and get the 2026-09-29 items into it — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `carry-forward` **Marek Pillár**: Confirm the real MaxBuddy rollout date with Jura Brázdil and align Vosmek's "within days" expectation ([[ASM-203]]) — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `carry-forward` **Marek Pillár**: Send the recap email of the MaxBuddy backlog call to Luboš Vosmek and Jura Brázdil — due 2026-09-29 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `carry-forward` `staleness` `low-prio` Review project-assumptions — ~18 Open items without a status change for >14 days (e.g. ASM-006, ASM-023–037, ASM-043, ASM-052–064, ASM-087)
- [ ] `carry-forward` `staleness` `low-prio` Review product-brief — >14 days since last_updated (2026-09-02)
- [ ] `carry-forward` `staleness` `low-prio` Review project-stakeholders — 284 `-tbd-` fields (threshold 5)
- [ ] `carry-forward` `staleness` `low-prio` Review client-overview — 13 `-tbd-` fields (threshold 5)
- [ ] `carry-forward` **Marek Pillár**: Rewrite the Listing spec and roadmap: Magento out of the MVP, enrichment first, food-supplements batch + export ([[ASM-207]], [[ASM-208]]) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `carry-forward` **Marek Pillár / Filip Černý**: Describe the scraping variant precisely for Dr. Max legal (process, sources, human review) and hand it to Petr Neuman — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `carry-forward` **Marek Pillár / Filip Černý**: Research third-party scraping/extraction services and a cost breakdown (hundreds vs. tens of thousands of SKUs), incl. a human-assisted URL variant — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `carry-forward` **Marek Pillár / Filip Černý**: Find out what happened to the earlier scraping legal check (via Alana Sihelská / Lukáš Szücs) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [x] `carry-forward` `highest-prio` **Marek Pillár**: Send Radim Švarc the TEO/OCR platform/initiative proposals for the spring 2027 cycle; review with him early next week, then consult Tomáš Burda — due 2026-10-02 — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors — partial 2026-10-02: proposal (`TEO-OCR - návrh dalšího postupu - klientská verze.docx`) emailed to Radim; awaiting his response, then review with him and consult Burda — done 2026-10-02: client proposal emailed to Radim (see Key Events); review with him early next week, then Burda
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Put the 10-01 outcomes into the new Reklamace spec — email-agent flow + additions (CC, PDF archive to Axapta, alternative drafts), SharePoint List direction, problem-types open point, and explicit written answers to Sláma's open May comments ([[ASM-223]], [[ASM-224]], [[ASM-225]], [[ASM-228]]) — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review — partial 2026-10-02: outcomes, contract facts and avízo context in v4/v5 (tracked changes); written answers to Sláma's May comments still to check before sending
- [ ] `carry-forward` **Marek Pillár**: Chase Petr Sláma's column-J feedback on the data map early in the week of 2026-10-05, so the knowledge base is decided by 2026-10-09 ([[ASM-184]], [[ASM-229]]) — from 2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review
- [ ] `task` **Marek Pillár**: Generate & review project-weekly today — /project-weekly
- [ ] **Tereza Foltýnová / Petr Spilka**: Finish the logistics initiatives list (green field) in the SharePoint copy with brief benefits per item, cenařky included and prioritized; ask Marek when unsure — next Wednesday session if ready — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Petr Spilka**: Email the hourly rate for the cenařky savings calculation — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Marek Pillár**: Clean the master AI-initiative tracker (rows from 13 down) so stale rows don't confuse departments ([[ASM-230]]) — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Jindřich Tůma**: Ask Tomáš Dudaško whether non-AI automation can be funded from the AI-initiative budget ([[ASM-233]]) — due 2026-10-02 — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Jindřich Tůma**: Once the logistics list is agreed, say when BigHub can start each item, based on capacity — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Marek Pillár**: If cenařky is prioritized, plan the on-site analysis for a high-traffic window (Nov–Dec or March) with Spilka ([[ASM-232]]) — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Jura Brázdil**: Add a model switcher on the Max test page (GPT-5 mini vs. "Luna") ([[ASM-234]]) — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Discuss Max/Maxie model costs and the allowed spend range (incl. hybrid escalation budget) with Tomáš Dudaško — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Add per-IP throttling to Max ([[ASM-235]]) — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Ticket and fix the geolocation timeout on "find nearest pharmacy" — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Lucie Fendrichová**: Ticket the route bug (origin always Prague; navigates to another shop at the same address) with examples — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Test courier tracking numbers from staging orders — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Šárka Andělová / Dr. Max CC team**: Run the SPC leaflet display past Legal (section jump; no patient data; unmodified SÚKL leaflets) and report back — due 2026-10-06 — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Rebuild order status and carrier answers on the three X-Manager source tables; human carrier names; check API for payment status and order history ([[ASM-237]]) — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Marek Pillár**: Offer CC async review of the order-status source tables before the final set goes to Jura — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Write the order-process methodology (changing delivery, what to offer, when to escalate) as a separate document — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil / Viliam Gago**: Review what a back-office Lexie agent needs (own SharePoint, Entra groups, Dr. Max permission) and report the steps ([[ASM-238]]) — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Confirm whether a role-switching test user for Lexie is possible — due next weekly sync — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Deploy Max for testing on drmax-space.cz and ask Vladislav Tvarůžek about starting the network/certificate work for drmax.cz ([[ASM-236]]) — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Hold the Atlantis/BDC Maxie meeting and push for delivery of the setup within that week ([[ASM-188]]) — due 2026-10-05 — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Simona Mertová**: Name the main CC contact replacing Kateřina Kadlecová from the end of October ([[ASM-091]]) — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] `task` `highest-prio` **Marek Pillár / Jindřich Tůma**: Prepare the Monday 10:00 in-person Reklamace "next steps" meeting (Žůrek, Dudaško, Spilka, Tereza) — likely value/continuation question ([[ASM-242]]); stakeholder read in the 1:1 note — due 2026-10-05 — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo
- [ ] `task` **Marek Pillár**: Read Jan's forwarded March 2026 logistics use-case email before Monday — due 2026-10-05 — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo
- [ ] `task` **Marek Pillár**: Ask logistics which suppliers need the okamžité avízo, their notice deadline, and in which phase; and whether the automatic send is an accepted exception ([[ASM-240]]) — from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo

## Key Events

**Reklamace spec v4**: `3. Reklamace v4.docx` was created from v3 (v3 kept). 10-01 outcomes were applied as tracked changes (author Claude):
- Testing extension (+1 week).
- Supplier-data direction: one SharePoint List, Excel out.
- CC to the shared claims mailbox.
- PDF thread archive on the AX claim (1.1a).
- Alternative drafts per recipient and Sláma's May comment as the accepted 1.1b direction.
- Problem types and the UX-feedback rule.
- Axapta ERP/WMS correction.

Contract facts from the new swaggers were applied: RD `case_number` is already in the contract, the rozvozový list is triggered by `claim_case_closed` and returns `document_link`, and only the issue date is missing. Everything in the data-map Excel is marked purple as open until the map is accepted. All 27 Filip comments were kept, worked into the text and answered with threaded recommendations (26 replies).

**TEO/OCR spring proposal sent to Radim Švarc**: Marek emailed `TEO-OCR - návrh dalšího postupu - klientská verze.docx` to Radim. The email was in Slovak, formal, and framed as a recommendation. It asks Radim to review the proposal and, if it makes sense, to agree how to take it to Tomáš Burda (Radim stays the entry point, [[ASM-166]]). It summarizes the three phases: Excel unchanged for autumn 2026, a review app before spring 2027 starting with a clickable prototype, and later extensions. It argues for building on the Dr. Max AI platform rather than a standalone app:
- Per-use-case cost visibility and spending caps, which answers Burda's cost concern ([[ASM-220]]).
- Continuous accuracy from returned corrections.
- One place for monitoring, access and user management.
- Reuse: a new vendor is about a day's work, and the approach could be offered for other document types.

The reuse argument was limited to sourced facts. Awaiting Radim's response.

**Reklamace spec v5**: The PM reviewed v4, and 22 of 26 comment threads were resolved. `3. Reklamace v5.docx` resolves the remaining open threads as tracked changes with replies:
- Fáze 2 open question on the label sample (printed vs. handwritten, 10–30 labels).
- Příjem s výhradou wording ("Jinak se tento flow nepoužije").
- Purple note in the Axapta cell about the supplier-data direction and the contract mismatch.

The immediate-avízo thread is left open and unchanged per PM. 6 earlier tracked changes from v4 still await the PM's accept/reject.

**1:1 with Jan Sovka** ([2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo](../../meetings/internal/2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo.md)): Jan steps back from logistics and won't join Monday's Reklamace meeting, leaving it to Marek and Jindřich as a clean break ([[ASM-241]]). He gave a read on the attendees (Žůrek calls the shots; Spilka may posture), forwarded logistics' March 2026 use-case email, and explained okamžité avízo: a nightly automatic notice after příjem s výhradou for suppliers that need ~24 h notice, not blocking testing ([[ASM-240]]).

**Session summary (close)**: A heavy Reklamace day. The new Axapta / inbound API contracts were saved, and spec v4 then v5 were built as tracked changes. All 27 Filip comments were answered, data-map items are marked purple, and the avízo section now carries Jan Sovka's explanation. The 1:1 with Jan set up Monday's meeting without him and gave a stakeholder read on Žůrek and Spilka. The parallel session processed the cenařky green-field reset and the Lexie/Max sync, and the TEO/OCR spring proposal went to Radim. Status stays **Amber**: Monday may question whether Reklamace continues, and the supplier store, its owner and the recap email are still open. Not routed: the Reklamace app UX walkthrough document (summary saved, routing awaiting PM). Not done: today's weekly (W40).

## Audit Log

[AUTO] project-daily — created today's daily; 2026-10-01 already closed; carried forward 40 unchecked items; status Amber and priority carried forward; Friday weekly nudge added (2026-10-02)
[MANUAL] documents/index — saved 2 Logistika API contracts raw (Axapta Integration API v0.9.10, Claims Platform Inbound API v0.4.0) to documents/internal/2026-10-02-logistika-reklamace-api-contracts/, not yet ingested — reserved for logistics context enrichment (2026-10-02)
[MANUAL] 3. Reklamace v4.docx — updated via /product-client-spec: 10-01 meeting outcomes + API contracts (v0.9.10 / inbound v0.4.0) as tracked changes, data-map items purple, 27 Filip comments answered (2026-10-02)
[AUTO] project-assumptions — added ASM-230, ASM-231, ASM-232, ASM-233; ASM-179 resolved; update on ASM-187 from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis (2026-10-02)
[AUTO] project-knowledge — new Cenařky entry; Reklamace value caveat from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis (2026-10-02)
[AUTO] project-stakeholders — updated STK-014, STK-013, STK-003 from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis (2026-10-02)
[AUTO] client-overview — Ways of Working: parallel Duo AI channel in logistics from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis (2026-10-02)
[AUTO] project-daily — 6 action items added; 2 closed (tracker sharing, pre-10-02 draft review) from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis (2026-10-02)
[AUTO] project-lessons — LL-78 from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis (2026-10-02)
[MANUAL] 3. Reklamace v5.docx — remaining comment threads resolved via tracked changes + replies (3 threads); avízo thread kept open per PM (2026-10-02)
[AUTO] project-assumptions — added ASM-234 to ASM-239; updates on ASM-091, ASM-188, ASM-100 (slipped), ASM-203 from 2026-10-02-lexie-max-maxie-weekly-sync (2026-10-02)
[AUTO] project-knowledge — Max/Maxie: model costs, order-status sources, SPC leaflet legal stance from 2026-10-02-lexie-max-maxie-weekly-sync (2026-10-02)
[AUTO] project-stakeholders — updated STK-037, STK-045, STK-050, STK-046 (name corrected to Veronika Strmisková), STK-017, STK-026 from 2026-10-02-lexie-max-maxie-weekly-sync (2026-10-02)
[AUTO] project-daily — 15 action items added from 2026-10-02-lexie-max-maxie-weekly-sync (2026-10-02)
[AUTO] project-lessons — LL-79 from 2026-10-02-lexie-max-maxie-weekly-sync (2026-10-02)
[AUTO] project-assumptions — added ASM-240–ASM-243, from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[AUTO] project-stakeholders — updated STK-024, STK-014, STK-002, STK-003, STK-010; added STK-060; moved STK-059 to External, from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[AUTO] project-knowledge — Reklamace: okamžité avízo; logistics initiatives: March 2026 source email, from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[AUTO] client-overview — Ways of Working: logistics decision-making, from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[AUTO] project-daily — 3 action items added, from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[AUTO] meetings/index — added 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[AUTO] project-lessons — added LL-80, from 2026-10-02-jan-sovka-1on1-monday-reklamace-meeting-okamzite-avizo (2026-10-02)
[MANUAL] 3. Reklamace v5.docx — okamžité avízo section updated with Jan Sovka's context (purpose, ~24 h notice, automatic-send exception to confirm, questions for logistics) as tracked changes; reply added in the avízo thread (kept open) (2026-10-02)
[AUTO] project-daily — closed 2026-10-02: session summary written; 1 item resolved (TEO/OCR proposal to Radim), 2 progress notes (spec, recap); staleness items already carried (no change); status re-derived Amber (unchanged); priority shifted to the 2026-10-05 Reklamace meeting + recap/spec; lessons already captured today (LL-78–LL-80) (2026-10-02)
