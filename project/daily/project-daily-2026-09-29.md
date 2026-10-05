---
status: closed
last_updated: 2026-09-29
last_updated_by: auto — project-daily close
project_status: Amber
---

# Daily — 2026-09-29 (Tuesday)

## Project Status

**Amber** (carried forward from 2026-09-25). Driver: **Reklamace**. Only part of the spec exists, the supplier-data / knowledge-base decision is open ([[ASM-169]]), and Petr Sláma disputes the reframe ([[ASM-181]]). The 2026-10-15–16 UAT start is at risk. Secondary: the 5 Fakturace doprav code-vs-spec contradictions are still open ([[ASM-131]]–[[ASM-135]]).

## Current Priority

**Reklamace spec (set by PM, 2026-09-29).** Four steps:
1. The options Excel is 100% ready for the Thursday 2026-10-01 logistics meeting.
2. In parallel, draft the final spec.
3. Once the Excel is approved, add the agreed decisions to the spec.
4. Send the spec to logistics / Sláma for final approval.

Target: a plan/spec with the knowledge base decided by the end of next week (2026-10-09).

## Action Items

- [ ] `task` `highest-prio` **Marek Pillár**: Have the Reklamace options Excel 100% ready. It covers every possible variant/option with a reasoned pro/con for each, ideally priced in MD — due 2026-10-01 (Thursday logistics meeting) — from PM's plan, 2026-09-29 — partial 2026-09-29: data-source map drafted ("marek sheet" in `Mapa_zdroju_a_umisteni_dat_reklamace 1 - marek sheet.xlsx`); sent to Filip Černý for a check; MD pricing still open
- [ ] `task` `highest-prio` **Marek Pillár**: In parallel, draft the new (final) Reklamace spec with all product comments/requirements worked in. Leave the Excel's open decisions as open for now — from PM's plan, 2026-09-29 — partial 2026-09-29: first full draft `1. Feature Specs/3. Reklamace/3. Reklamace.docx` created via /product-client-spec; awaiting PM review — updated at close: working version is `3. Reklamace v3.docx` (PM review comments applied twice; v1/v2 deleted); still open until the 10-01 decisions are added
- [ ] `task` `highest-prio` **Marek Pillár**: Walk the logistics team through the options Excel at the meeting, then send it as a meeting recap for approval / consideration — due 2026-10-01 — from PM's plan, 2026-09-29
- [ ] `task` `highest-prio` **Marek Pillár**: Once the Excel is approved, add the AGREED decisions to the spec and send it to logistics / Petr Sláma for final approval. Target: spec with the knowledge base decided — due 2026-10-09 — from PM's plan, 2026-09-29
- [ ] `carry-forward` `follow-up` `mid-prio` **Marek Pillár**: Contact Filip Černý to walk through his growing pile of business-decision questions from Max/ViaPharma people; plan whether a direct meeting with them is needed — medium priority — from Filip Černý's Fakturace doprav backlog note, 2026-09-08
- [ ] `carry-forward` `follow-up` `low-prio` **Marek Pillár**: Data drift found on Maxie roadmap row "Přepojení na živého operátora při chybě nebo požadavku" — local roadmap data has it as Done, live Excel shows Planned. Not changed either way (out of scope for the estimates-routing task) — worth a quick check on which is correct — Marek's own note, 2026-09-09 — reprioritized via /todo review (2026-09-17)
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — **blocked: waiting on Honza Sovka's review first** — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] `carry-forward` `low-prio` **Marek Pillár / Tereza Foltová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — **deprioritized 2026-09-15**: no rush, will revisit sometime later this year — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [x] `carry-forward` **Marek Pillár**: Review the new Reklamace brief (`3. Reklamace.docx`) — confirm/correct business-value figures (currently sourced from the 2026-09-15 Tereza Foltová interview, flagged as potentially overstated), assign domain-expert/business-owner sign-off, and resolve open questions (label-OCR engine choice, e-mail-draft feature scope, whether a local case-status dashboard is wanted — **answered 2026-09-25: no, killed, see [[ASM-172]]**) — from cz-ai-logistics codebase read, 2026-09-16 — superseded 2026-09-29: the brief no longer exists on disk; value figures (BQ tracker), owner (Spilka) and open questions are covered in the new spec `3. Reklamace v3.docx`
- [ ] `carry-forward` **Marek Pillár / Jindřich Tůma**: By end of this week, prepare a work-in-progress AI Platform spec/roadmap with open questions to show Dudaško — sequencing: design phase (~1 week), admin/role-views phase (~2-3 weeks), agentic-workflow follow-up conversation tentatively November — from 2026-09-21-ai-platform-vision-discovery-dudasko — partial 2026-09-24: Phase 1 prototype shown and accepted by Dudaško; written spec/roadmap still open (2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko) — moved to the week of 2026-09-28 per PM (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the disambiguation-approach conflict with ASM-119 — confirm whether the ranked-candidate mechanism is being reversed or whether this was a narrower UI-presentation point — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the Blob storage/deployment blocker conflict with ASM-088 — confirm current dependency status on Dr. Max infra/BDC — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` `mid-prio` **Marek Pillár**: Get Filip Černý to confirm/reconcile the 5 code-vs-spec contradictions found in today's Fakturace doprav code audit (kiosk auth, document versioning, AR pairing, temperature-log OCR gap, multi-vehicle silent overwrite) — [[ASM-131]], [[ASM-132]], [[ASM-133]], [[ASM-134]], [[ASM-135]] — before the spec is finalized or shared further — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, below Reklamace in priority (2026-09-25)
- [ ] `carry-forward` **Marek Pillár**: Confirm with P. Sláma whether the AR-pairing-key dependency (ZOPV/OPL) is already resolved in code — [[ASM-133]] — and update the Závislosti section accordingly — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, with the Fakturace contradictions (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Check whether ElevenLabs barge-in can pick up the interrupting context and respond to it, and report back to Mertová — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Marek Pillár**: Add a KPI measurement-method column to the BQ tracker and collect measurement methods from every business owner — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Collect and prioritize department AI-initiative backlogs (logistics, marketing via Marek Dvořák, others) in BQ tracker format — target end of November 2026 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Get email sign-off on BQ figures from Marek Šimoník (after vacation) and Simona Mertová — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko — partial 2026-09-29: Šimoník agreed on the call to confirm by email, incl. the 2 annualized columns for Dudaško; chase if not in by end of week (2026-09-29-order-prediction-dashboard-v2-review)
- [ ] `carry-forward` **Marek Pillár**: Talk with Jindřich Tůma about the capacity pool: is he inside the 3 FTE or extra, and what does his September capacity table show ([[ASM-167]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [x] `carry-forward` **Marek Pillár**: Work up the Reklamace documentation to near-final depth, collect questions for Tereza Foltová, Jana Egrmaierová and Petr Spilka, and set up follow-up sessions as needed ([[ASM-177]]) — from 2026-09-25-tereza-foltova-reklamace-focus-logistics-initiatives-table — superseded 2026-09-29 by the 4-step Reklamace plan above ([[ASM-184]])
- [ ] `carry-forward` **Marek Pillár**: Ask Tomáš Dudaško whether the cross-department AI-initiative tracker can be shared with other departments ([[ASM-179]]) — from 2026-09-25-tereza-foltova-reklamace-focus-logistics-initiatives-table
- [ ] `carry-forward` **Marek Pillár / Tereza Foltová**: Review her draft table together (Wed/Thu) before the 2026-10-02 session — from 2026-09-25-tereza-foltova-reklamace-focus-logistics-initiatives-table — scheduled 2026-09-30 at Max (2026-09-29-management-meeting-debrief-reklamace-thursday-plan)

- [x] `task` **Marek Pillár**: Send the expanded Reklamace options Excel to Filip Černý for a technical-feasibility check — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` `highest-prio` **Marek Pillár**: Get the Reklamace spec draft to Filip Černý by end of day — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` `highest-prio` **Marek Pillár**: Set up a Marek / Filip Černý / Jindřich Tůma sync on the options Excel before Thursday — due before 2026-10-01 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan — agreed with Filip for 2026-09-30 afternoon (~15:00–16:00), online, covering the data map + demo (2026-09-29-reklamace-email-agent-demo-review-filip)
- [ ] `task` `highest-prio` **Marek Pillár**: After the Thursday session, email logistics the agreed decisions for confirmation and send the Reklamace spec with agreed changes or yellow-highlighted open questions ([[ASM-185]], [[ASM-186]]) — due 2026-10-02 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` **Marek Pillár**: Meet Tereza Foltová at Max to review the initiatives she collected since Friday — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` **Marek Pillár**: Run the Listing workshop with Petr Neuman and Michaela Vdovicynová — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` `mid-prio` **Marek Pillár**: Define each later phase's value driver ("system seller") with each initiative owner via discovery; give logistics outlook anchor points next week; coordinate capacity with Jindřich Tůma before promising anything ([[ASM-190]]) — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` `low-prio` **Marek Pillár**: Put blockers / personal time into the calendar so Jindřich Tůma can plan meetings around it — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` **Marek Pillár**: Send a four-point summary of the internal sync to the BigHub business group (for Ján Kabát and Jan Sovka) — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `task` `highest-prio` **Marek Pillár**: Work Filip Černý's comments into the data-map Excel ("marek sheet"): merge overlapping rows, reconsider the feature-like row, remove source references — due 2026-09-30 morning — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] `task` **Marek Pillár**: Check whether logistics specified expectations for the first supplier email / time saving — from 2026-09-29-reklamace-email-agent-demo-review-filip
- [ ] `task` `low-prio` **Marek Pillár**: Review Marek Šimoník's collected order-prediction V2 backlog (incl. model-accuracy reporting, email digest) with him before year-end, so BigHub has a plan ready for January ([[ASM-191]]) — due 2026-12 — from 2026-09-29-order-prediction-dashboard-v2-review
- [ ] `task` **Marek Pillár**: Contact Jiří Trajer about receipt data (expedition number + product codes) and per-product profitability; define and analyse the data table ([[ASM-197]]) — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `task` **Marek Pillár**: Once there's a first version, specify the profitability-based recommendation with Luboš Vosmek (3-tier model and/or receipt-based learning, incl. the legal "no AI" question) — due start of 2027 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `task` **Marek Pillár**: Agree with Jindřich Tůma where the MaxBuddy backlog is tracked (not in DevOps today, [[ASM-202]]) and get the 2026-09-29 items into it — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `task` **Marek Pillár**: Confirm the real MaxBuddy rollout date with Jura Brázdil and align Vosmek's "within days" expectation ([[ASM-203]]) — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `task` **Marek Pillár**: Send the recap email of the MaxBuddy backlog call to Luboš Vosmek and Jura Brázdil — due 2026-09-29 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] `staleness` `low-prio` Review project-assumptions — ~18 Open items without a status change for >14 days (e.g. ASM-006, ASM-023–037, ASM-043, ASM-052–064, ASM-087)
- [ ] `staleness` `low-prio` Review product-brief — >14 days since last_updated (2026-09-02)
- [ ] `staleness` `low-prio` Review project-stakeholders — 284 `-tbd-` fields (threshold 5)
- [ ] `staleness` `low-prio` Review client-overview — 13 `-tbd-` fields (threshold 5)

## Key Events

**Reklamace data-source map**: Built the "marek sheet" tab of the Reklamace data-map Excel. It covers 18 supplier/case fields with their current source, target store (Excel / AX / Confluence / SharePoint Lists), notes and sources. Where the 09-24/09-25 meetings conflicted with the May spec comments (spec 3.5), the newer meetings won. PM rejected a broader yellow-highlighted cross-reference pass across all meetings, so it was rolled back. The final version has broader, context-rich open questions for logistics and a highlighted result paragraph: AX holds account/address/main contact; everything else goes to one secured store (SharePoint Lists or Confluence, Excel not recommended); decision at the 10-01 meeting, spec by 10-09, AX API fields and claims-worker view before UAT on 10-15/16. Sent to Filip Černý for a check.

**Reklamace spec draft**: Created the `/product-client-spec` skill, which captures how past specs were built: intake, a register resolving every comment, newest source wins, the roadmap mirrored 1:1, colour annotations. Used it for the first full draft of `3. Reklamace.docx`, which is phase-based (Fáze 0–5) per Tereza's request. It resolves all 33 spec-3.5 comments, mirrors all 26 roadmap rows, and uses light purple for open items from the data map. PM decisions: the Zentiva email sequence becomes Fáze 1.1b after UAT; storage = Azure Blob (Filip to confirm); approvers are Spilka + Sláma with Žůrek informed. A code audit of `cz-ai-logistics` turned up gaps flagged orange: the rozvozový list only fills the recipient, the email draft isn't in the code, the letterhead is a single warehouse, the generate-doc bug is still there, and the odběratel field is missing.

**Internal sync — management-meeting debrief & Reklamace Thursday plan** ([2026-09-29-management-meeting-debrief-reklamace-thursday-plan](../../meetings/internal/2026-09-29-management-meeting-debrief-reklamace-thursday-plan.md)): Jindřich's management meeting went well: the BQ benefits table was well received and BDC communication was raised (BDC is now reaching out). He flagged quiet competitive pressure from Deloitte ([[ASM-187]]). Reklamace is the only real problem. The 10-01 agenda is fixed (Filip's email-thread demo, options Excel with BigHub's recommendation, spec by 10-02), and decisions will be confirmed in writing, with the spec treated as a contract ([[ASM-185]], [[ASM-186]]). Status stays **Amber**.

**Order-prediction dashboard v2 review with Šimoník** ([2026-09-29-order-prediction-dashboard-v2-review](../../meetings/external/2026-09-29-order-prediction-dashboard-v2-review.md)): Juraj demoed the v2 build (hierarchical channel view, run-rate projection, 30-min/1-h toggle, logistics chart following the selected series), and it was very well received. Still open: per-day budget and per-channel revenue split, both waiting on Šimoník's Excel ([[ASM-192]]), and the per-day × per-warehouse export for logistics shift planning ([[ASM-111]]). Final acceptance targeted for end of October; the client's "V2" talk is in Jan/Feb 2027 ([[ASM-191]]). Mobile access is not a blocker and the email digest goes to V2 ([[ASM-193]]). Honza Maroušek merged into STK-021.

**TEO/OCR client proposal**: Built a Czech client version of Alana's TEO/OCR one-pager: `TEO-OCR - návrh dalšího postupu - klientská verze.docx`. It follows three phases ([[ASM-165]]): Excel for autumn 2026, a review app before spring 2027 (prototype first), and follow-on extensions (a problem report by supplier/branch/device, next-inspection tracking, SNOW auto-import). All 14 Jura/Alana comments were applied. The traffic-light confidence levels, the per-batch summary e-mail and the upfront accuracy figure were dropped, and the claim that every product was first built standalone was removed. Internal framing (Dudaško, the Reklamace parallel, ASM refs) was stripped. The original was not modified. PM then trimmed the docx, restyled it to the Listing client-version design, and built an 8-slide PDF deck (`TEO-OCR - návrh dalšího postupu - prezentace.pdf`). Both were sent to Alana and Jura for confirmation. Topic closed for now; next step waits on their reply.

**MaxBuddy backlog call with Vosmek** ([2026-09-29-maxbuddy-roadmap-backlog-vosmek](../../meetings/external/2026-09-29-maxbuddy-roadmap-backlog-vosmek.md)): First backlog conversation on Vosmek's wishlist, with Jura. Dudaško liked the BQ results. Priority to year-end is UX "beauty" work. The one blocker is a Farmis scanner-focus bug, which Farmis is fixing. Profitability offering will use absolute CZK profit (3-tier 7/2/1, or receipt-based learning); Marek to go to Jiří Trajer, target start of 2027. Seasonal logos start with Mikuláš. Coverage overview goes into the filling interface. Open gap: Vosmek expects rollout "within days" versus the AKS block.

**Session summary (close)**: A Reklamace-focused day, following the PM's 4-step plan ([[ASM-184]]).
- **Data map**: built the "marek sheet" data-source map, rolled back a cross-reference pass the PM rejected, and added broader open questions plus a result paragraph.
- **Spec**: created `/product-client-spec` and produced `3. Reklamace v3.docx` over three PM review rounds. It is phase-based (0–5), newest resolution stated as fact, source traces kept internal (grey), a single yellow for everything open, "Další postup" at the end of each phase, and KPIs taken exactly from the BQ tracker.
- **Meetings**: the management-meeting debrief fixed the 10-01 agenda and the spec-as-contract rule. Filip's email-agent demo is largely built and will be shown as a simple deck ([[ASM-204]]–[[ASM-206]]).
- **Tomorrow (09-30)**: data-map comments, Listing workshop at 11:00, Tereza at Max, Marek/Filip/Jindřich sync ~15–16h.

## Audit Log

[AUTO] project-daily — created today's daily; carried forward 18 unchecked PM-owned items from 2026-09-25 (closed); status Amber carried forward; priority set by PM to the Reklamace spec (2026-09-29)
[MANUAL] project-daily — added the PM's 4-step Reklamace spec plan as 4 highest-prio action items (2026-09-29)
[MANUAL] project-assumptions — added ASM-184 (Reklamace spec approval sequence, decided) (2026-09-29)
[MANUAL] project-daily — Reklamace near-final-documentation carry-forward marked superseded by the 4-step plan (ASM-184) (2026-09-29)
[MANUAL] project-daily — Reklamace options-Excel action item annotated (data-source map drafted, sent to Filip Černý for check); session summary added (2026-09-29)
[MANUAL] .claude/skills/product-client-spec — new skill + command wrapper; CLAUDE.md commands table updated (2026-09-29)
[MANUAL] 3. Reklamace.docx — created via /product-client-spec (OneDrive 1. Feature Specs/3. Reklamace/) (2026-09-29)
[AUTO] meetings — added 2026-09-29-management-meeting-debrief-reklamace-thursday-plan note (2026-09-29)
[AUTO] project-assumptions — added ASM-185–ASM-190; updated ASM-184 (spec sent by 10-02 with open questions) and ASM-169 (BigHub storage recommendation) from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan (2026-09-29)
[AUTO] project-stakeholders — updated STK-003, STK-004, STK-006, STK-010, STK-013, STK-016, STK-022, STK-034, STK-051 from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan (2026-09-29)
[AUTO] project-knowledge — added Deloitte and Spec-as-contract & change requests; updated BDC from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan (2026-09-29)
[AUTO] project-daily — added 9 PM-owned action items (1 already done), Key Event; annotated Tereza table review with 2026-09-30 from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan (2026-09-29)
[AUTO] project-lessons — added LL-68 from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan (2026-09-29)
[AUTO] meetings/index — added entry for 2026-09-29-management-meeting-debrief-reklamace-thursday-plan (2026-09-29)
[MANUAL] 3. Reklamace v2.docx — PM's 5 review comments + direct edits applied: supplier-data section marked as a meeting result, 'další postup' discovery notes on 1.1b/2/3/4/5 (phases 3–5 rewritten in product language), stale roadmap rows #17/#18/#29/#30/#33 removed, source-conflict appendix removed and resolutions written in as facts, all source/meeting attributions marked grey (internal); previous file with comments kept (2026-09-29)
[MANUAL] 3. Reklamace v3.docx — PM edits from v2 kept; KPIs taken exactly from BQ tracker (new_Přehled) per PM comment; purple merged into yellow; 'Další postup' moved to the end of each phase; every -tbd- given context with its row/paragraph yellow; v2 with PM comment kept (2026-09-29)
[AUTO] meetings — added 2026-09-29-order-prediction-dashboard-v2-review note (2026-09-29)
[AUTO] project-assumptions — added ASM-191–ASM-195; updated ASM-069 (client naming), ASM-110, ASM-111 from 2026-09-29-order-prediction-dashboard-v2-review (2026-09-29)
[AUTO] project-stakeholders — updated STK-019, STK-035, STK-009, STK-016; STK-036 merged into STK-021 (Jan Maroušek, identity confirmed by PM) from 2026-09-29-order-prediction-dashboard-v2-review (2026-09-29)
[AUTO] project-knowledge — enriched Order-Prediction Dashboard entry (v2 build, holiday/warehouse/adaptation patterns) from 2026-09-29-order-prediction-dashboard-v2-review (2026-09-29)
[AUTO] project-daily — added 1 PM-owned action item, annotated BQ sign-off item, Key Event from 2026-09-29-order-prediction-dashboard-v2-review (2026-09-29)
[AUTO] project-lessons — added LL-69 from 2026-09-29-order-prediction-dashboard-v2-review (2026-09-29)
[AUTO] meetings/index — added entry for 2026-09-29-order-prediction-dashboard-v2-review (2026-09-29)
[MANUAL] TEO-OCR - návrh dalšího postupu - klientská verze.docx — client version created from Alana_TEO-OCR-odporucania.docx via /product-client-spec (2026-09-29)
[MANUAL] TEO-OCR client proposal — docx restyled to Listing design + PDF deck created; sent to Alana Sihelská / Jura Brázdil for confirmation, topic closed (2026-09-29)
[MANUAL] 3. Reklamace v3.docx — duplicate roadmap rows #31/#32 removed (PM edits kept); superseded 3. Reklamace.docx and v2 deleted per PM, v3 is the working version (2026-09-29)
[AUTO] meetings — added 2026-09-29-maxbuddy-roadmap-backlog-vosmek note (2026-09-29)
[AUTO] project-assumptions — added ASM-196–ASM-203; updated ASM-027 (rollout expectation gap) from 2026-09-29-maxbuddy-roadmap-backlog-vosmek (2026-09-29)
[AUTO] project-stakeholders — updated STK-011, STK-026, STK-049, STK-031, STK-004, STK-010 from 2026-09-29-maxbuddy-roadmap-backlog-vosmek (2026-09-29)
[AUTO] project-knowledge — enriched MaxBuddy and Farmis entries; added eRezervace from 2026-09-29-maxbuddy-roadmap-backlog-vosmek (2026-09-29)
[AUTO] project-daily — added 5 PM-owned action items and a Key Event from 2026-09-29-maxbuddy-roadmap-backlog-vosmek (2026-09-29)
[AUTO] project-lessons — added LL-70 from 2026-09-29-maxbuddy-roadmap-backlog-vosmek (2026-09-29)
[AUTO] meetings/index — added entry for 2026-09-29-maxbuddy-roadmap-backlog-vosmek (2026-09-29)
[AUTO] project-assumptions — added ASM-204 (email-agent MVP approach), ASM-205 (more real threads needed, open), ASM-206 (10-01 demo format); update note on ASM-173, from 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[AUTO] project-knowledge — Reklamace entry: real supplier email-thread findings, from 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[AUTO] project-stakeholders — updated STK-006 (Filip Černý), STK-044 (Jana Egrmaierová), from 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[AUTO] project-daily — 2 action items added; Marek/Filip/Jindřich sync item annotated with the agreed slot, from 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[AUTO] meetings/index — added 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[AUTO] project-lessons — added LL-71 (scope LLM agents from real examples with a human fallback; demo with real inputs/outputs), from 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[MANUAL] 3. Reklamace v3.docx — Phase 1.1b: 4 bullets added (email-agent reply outcomes, hand-off to a person, next steps, more real threads needed in yellow); PM edits kept, from 2026-09-29-reklamace-email-agent-demo-review-filip (2026-09-29)
[AUTO] project-lessons — added LL-72 (client-facing spec: state the newest resolution as fact, keep provenance internal) (2026-09-29)
[AUTO] project-daily — closed 2026-09-29: session summary written; 1 action item resolved (old Reklamace brief superseded by v3), spec item annotated; staleness re-run added 4 low-prio items (assumptions, product-brief, stakeholders, client-overview); status re-derived Amber (unchanged); priority unchanged (Reklamace spec + 10-01 meeting) (2026-09-29)
