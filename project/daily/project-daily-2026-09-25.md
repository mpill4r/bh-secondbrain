---
status: closed
last_updated: 2026-09-25
last_updated_by: auto — project-daily close
project_status: Amber
---

# Daily — 2026-09-25 (Friday)

## Project Status

**Amber** (re-scoped at close per PM: status now measures only PM-actionable streams). Driver: **Reklamace**. The continue-or-close decision is still open, and only part of the process is specified (phases 3–5 not at all). Petr Sláma disputes the reframe ([[ASM-181]]), and the October 15–16 full-UAT start is at risk given how much of the spec is missing. Marek owns the documentation from today ([[ASM-177]]). Secondary: the 5 Fakturace doprav code-vs-spec contradictions are unresolved and now queued behind Reklamace ([[ASM-131]]–[[ASM-135]]).

*Watch (owned by others, no PM action):* DB access on the new cluster, which gates the end-of-September Max go-live phases ([[ASM-100]], [[ASM-164]]); the replacement for Kadlecová ([[ASM-091]]).

## Current Priority

**Heading into the week of 2026-09-28:**
- The 2026-09-29 management meeting: support Jindřich's "PR" value stories ([[ASM-160]]).
- The 2026-10-01 logistics meeting: the supplier-data options table ([[ASM-169]]) and Filip's email-agent demo ([[ASM-173]]).
- The Vosmek MaxBuddy wishlist call.
- Still open and carried: the Part A/B split with Tereza Foltýnová, starting the KPI measurement column in the BQ tracker ([[ASM-159]]), the MVP-vs-full-product scoping mismatch, and Filip's 5 Fakturace doprav code-vs-spec contradictions ([[ASM-131]]–[[ASM-135]]).
- TEO/OCR: consolidate Jura's comments and hold the informal call with Radim Švarc ([[ASM-165]], [[ASM-166]]).
- Watch: Jura's DB-access retest result ([[ASM-164]]).

## Action Items

- [x] `carry-forward` `staleness` `low-prio` Review project-stakeholders — 96+ `-tbd-` fields (exceeds threshold of 5) — dropped per PM via day-review Q&A (2026-09-25)
- [x] `carry-forward` `staleness` `low-prio` Review client-overview — 14 `-tbd-` fields (exceeds threshold of 5) — dropped per PM via day-review Q&A (2026-09-25)
- [x] `carry-forward` `task` `mid-prio` **PM**: Generate & review project-weekly (overdue from Friday 2026-09-04) — /project-weekly — done: W39 weekly generated and confirmed (2026-09-25)
- [ ] `carry-forward` `follow-up` `mid-prio` **Marek Pillár**: Contact Filip Černý to walk through his growing pile of business-decision questions from Max/ViaPharma people; plan whether a direct meeting with them is needed — medium priority — from Filip Černý's Fakturace doprav backlog note, 2026-09-08
- [x] `carry-forward` `task` `low-prio` **Jindřich Tůma / Marek Pillár**: Read through Tomáš Dudaško's AI-platform requirements Excel in full — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka — dropped per PM (2026-09-25)
- [ ] `carry-forward` `follow-up` `low-prio` **Marek Pillár**: Data drift found on Maxie roadmap row "Přepojení na živého operátora při chybě nebo požadavku" — local roadmap data has it as Done, live Excel shows Planned. Not changed either way (out of scope for the estimates-routing task) — worth a quick check on which is correct — Marek's own note, 2026-09-09 — reprioritized via /todo review (2026-09-17)
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — **blocked: waiting on Honza Sovka's review first** — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] `carry-forward` `low-prio` **Marek Pillár / Tereza Foltýnová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — **deprioritized 2026-09-15**: no rush, will revisit sometime later this year — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] `carry-forward` **Marek Pillár**: Review the new Reklamace brief (`3. Reklamace.docx`) — confirm/correct business-value figures (currently sourced from the 2026-09-15 Tereza Foltýnová interview, flagged as potentially overstated), assign domain-expert/business-owner sign-off, and resolve open questions (label-OCR engine choice, e-mail-draft feature scope, whether a local case-status dashboard is wanted — **answered 2026-09-25: no, killed, see [[ASM-172]]**) — from cz-ai-logistics codebase read, 2026-09-16
- [x] `carry-forward` `highest-prio` **Jindřich Tůma / Marek Pillár**: Resolve which timeline items were mis-scoped as MVP when they actually belong to the full product — **highest-prio for Thursday, 2026-09-24**, per PM — from 2026-09-17-lexie-max-maxie-weekly-sync — reprioritized via /todo review (2026-09-22) — closed as stale per PM: never itemized, not raised since 2026-09-17 ([[ASM-104]]) (2026-09-25)
- [x] `carry-forward` `staleness` `low-prio` Review product-brief — exceeds 14-day staleness threshold, though 0 `-tbd-` fields — dropped per PM via day-review Q&A (2026-09-25)
- [x] `carry-forward` `staleness` `low-prio` Review project-assumptions — 8 open items exceed the 14-day-without-status-change threshold (ASM-035, ASM-033, ASM-030, ASM-029, ASM-028, ASM-027, ASM-025, ASM-023 — all last touched 2026-09-04/07) — dropped per PM via day-review Q&A (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jindřich Tůma**: By end of this week, prepare a work-in-progress AI Platform spec/roadmap with open questions to show Dudaško — sequencing: design phase (~1 week), admin/role-views phase (~2-3 weeks), agentic-workflow follow-up conversation tentatively November — from 2026-09-21-ai-platform-vision-discovery-dudasko — partial 2026-09-24: Phase 1 prototype shown and accepted by Dudaško; written spec/roadmap still open (2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko) — moved to the week of 2026-09-28 per PM (2026-09-25)
- [x] `carry-forward` **Marek Pillár**: Look into the Excel-only review-output issue — Radim's downstream review/correction workflow is entirely manual spreadsheet work with no AI assistance in that step; explore whether a better alternative exists — due 2026-09-24 — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal — resolved at close: direction agreed in 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (Excel stays for the autumn 2026 cycle; non-Excel review solution to be built before spring 2027; follow-ups tracked separately) (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the disambiguation-approach conflict with ASM-119 — confirm whether the ranked-candidate mechanism is being reversed or whether this was a narrower UI-presentation point — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the Blob storage/deployment blocker conflict with ASM-088 — confirm current dependency status on Dr. Max infra/BDC — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` `mid-prio` **Marek Pillár**: Get Filip Černý to confirm/reconcile the 5 code-vs-spec contradictions found in today's Fakturace doprav code audit (kiosk auth, document versioning, AR pairing, temperature-log OCR gap, multi-vehicle silent overwrite) — [[ASM-131]], [[ASM-132]], [[ASM-133]], [[ASM-134]], [[ASM-135]] — before the spec is finalized or shared further — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, below Reklamace in priority (2026-09-25)
- [ ] `carry-forward` **Marek Pillár**: Confirm with P. Sláma whether the AR-pairing-key dependency (ZOPV/OPL) is already resolved in code — [[ASM-133]] — and update the Závislosti section accordingly — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, with the Fakturace contradictions (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Check whether ElevenLabs barge-in can pick up the interrupting context and respond to it, and report back to Mertová — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Marek Pillár**: Add a KPI measurement-method column to the BQ tracker and collect measurement methods from every business owner — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [x] `carry-forward` **Marek Pillár**: With Tereza Foltýnová, agree the logistics Part A (finish Reklamace/Fakturace doprav specs) / Part B (new AI initiatives in tracker format) split — due 2026-09-25 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko — done: agreed in 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
- [ ] `carry-forward` **Marek Pillár**: Collect and prioritize department AI-initiative backlogs (logistics, marketing via Marek Dvořák, others) in BQ tracker format — target end of November 2026 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Get email sign-off on BQ figures from Marek Šimoník (after vacation) and Simona Mertová — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [x] **Marek Pillár**: Consolidate Jura Brázdil's comments into a phased TEO/OCR proposal: Excel for autumn 2026, non-Excel review solution before spring 2027, longer-term vision after ([[ASM-165]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics — closed per PM (done / no longer needed) (2026-09-25)
- [x] **Marek Pillár**: Informal, non-committal call with Radim Švarc: gauge openness to building beyond Excel; map the full TEO process, follow-on use cases (e.g., next-service-due tracking) and per-cycle manual effort ([[ASM-166]], [[ASM-168]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics — closed per PM (done / no longer needed) (2026-09-25)
- [ ] **Marek Pillár**: Talk with Jindřich Tůma about the capacity pool: is he inside the 3 FTE or extra, and what does his September capacity table show ([[ASM-167]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [ ] **Marek Pillár**: Work up the Reklamace documentation to near-final depth, collect questions for Tereza Foltýnová, Jana Egrmaierová and Petr Spilka, and set up follow-up sessions as needed ([[ASM-177]]) — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table
- [ ] **Marek Pillár**: Ask Tomáš Dudaško whether the cross-department AI-initiative tracker can be shared with other departments ([[ASM-179]]) — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table
- [ ] **Marek Pillár / Tereza Foltýnová**: Review her draft table together (Wed/Thu) before the 2026-10-02 session — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table

## Key Events

PM set the AI Initiative tracker (sheet `new_Přehled`) as the source of truth for business quantification. Reconciled the harness against it: MaxBuddy's value settled at 81M Kč/yr ([[ASM-140]] closed); Listing's conversion figure corrected from +1 pp to +0.1 pp, with cost/item 230→130→100 Kč ([[ASM-123]]); Reklamace clarified as 425k Kč for phase 1 only; Rudolf Žůrek set as Kontrola beden owner. The BQ knowledge entry now carries the authoritative per-initiative table, the KPI baselines for the measurement column, and the 55-idea backlog with 4 new idea-owner stakeholders.

**Session summary (close)**: Friday covered four things.
- **Tracker as source of truth**: the PM set the AI Initiative tracker (`new_Přehled`) as the business-quantification source of truth, and the harness was reconciled to it.
- **Reference document for Dr. Max**: produced a Czech reference document of the 9 running AI initiatives (`AI-iniciativy-prehled-2026-09-25.docx`, BigHub spec house style, no money/KPIs). After PM feedback it went through several iterations: dashboard-style PDF → Dr. Max-green Word → reference document ("what does this initiative do/solve"). The PM corrected MaxBuddy's stage to "being deployed" (Nasazování), not a finished solution. The tracker still says Deployed/Řešení, and that is not yet reconciled.
- **TEO/OCR (Alana 1:1)**: settled phasing for TEO/OCR: Excel for the autumn cycle, a non-Excel review solution before spring 2027.
- **Reklamace supplier data (Jindřich/Filip)**: set up the Reklamace supplier-data options approach for next Thursday's logistics meeting.

## Audit Log

[AUTO] project-daily — created today's daily, carrying forward all 70 unchecked items from 2026-09-24's close; project_status (Amber) and priority carried forward (2026-09-25)
[MANUAL] project-knowledge — "Business Quantification tracker" rewritten against the tracker (source of truth): authoritative per-initiative values/owners/KPI baselines, ideas backlog; Kontrola beden owner note (2026-09-25)
[MANUAL] project-assumptions — ASM-140 Decided (MaxBuddy 81M Kč/yr); ASM-123 corrected (Listing +0.1 pp, 230→130→100 Kč, 34.12M); ASM-125 annotated with the tracker value ranking (2026-09-25)
[MANUAL] project-stakeholders — updated STK-012, STK-019, STK-024, STK-025, STK-031, STK-049 (roles per tracker; STK-012/STK-031 flagged as possible duplicates); added STK-053 (Miroslav Tlustý), STK-054 (Martin Panzner), STK-055 (Jana Kneiflová), STK-056 (Jan Štangel) (2026-09-25)
[AUTO] project-assumptions — added ASM-165 (TEO Excel for autumn / non-Excel before spring 2027), ASM-166 (Radim-first path to Burda), ASM-167 (~3 FTE capacity pool, open), ASM-168 (TEO discovery gap, open); ASM-130 update note, from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (2026-09-25)
[AUTO] project-knowledge — TEO/OCR entry: twice-yearly cadence and phasing, volume-model conflict flagged; new Seasonal entry "TEO/OCR service-protocol cycles"; new Project Conventions entry "BigHub capacity pool (Dr. Max)", from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (2026-09-25)
[AUTO] project-stakeholders — updated STK-004, STK-003, STK-007, STK-041, STK-025, STK-010; added STK-057 (Kuba Vodička, low confidence), from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (2026-09-25)
[AUTO] project-daily — 4 action items added, from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (2026-09-25)
[AUTO] project-lessons — added LL-060 (check process cadence before proposing mid-cycle change), LL-061 (inbound use cases skip discovery), from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (2026-09-25)
[AUTO] meetings/index — added 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (2026-09-25)
[AUTO] project-assumptions — added ASM-169 (supplier-data options with risks, client chooses), ASM-170 (non-Axapta store extends Axapta via supplier account), ASM-171 (main-contact concept kept), ASM-172 (case timeline dashboard killed), ASM-173 (email-agent demo), ASM-174 (rozvozový list Axapta fields missing from contract, open), ASM-175 (claims-worker display gap, open), ASM-176 (unhoused supplier fields, open); update notes on ASM-122, ASM-139, ASM-143, from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] project-knowledge — Reklamace entry: Axapta-as-single-source claim narrowed; supplier-attribute map, two-person claim flow, email flow added; new Naming Conventions entry "Reklamace supplier-data naming" (Instrukce, účet dodavatele, SharePoint Lists), from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] project-stakeholders — updated STK-006 (Filip Černý), STK-007 (Jakub Turner), STK-034 (Petr Sláma), STK-044 (Jana Egrmaierová), from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] client-overview — Ways of Working: informal agreements harden into commitments (Excel narrative), from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] project-daily — 8 action items added; Reklamace-brief carry-forward annotated (case-status dashboard answered), from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] project-lessons — added LL-062 (find the real driver behind a legacy-tool preference), LL-063 (frame interim demos as non-commitments), LL-064 (map every output-document field to its source before signing an API contract), from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] meetings/index — added 2026-09-25-reklamace-supplier-data-source-options, from 2026-09-25-reklamace-supplier-data-source-options (2026-09-25)
[AUTO] project-daily — closed 2026-09-25: session summary written; 1 action item resolved from session evidence (TEO Excel-only review gap → phased direction agreed); staleness re-run (no new items; existing stakeholders/client-overview/product-brief/assumptions items still apply); status re-derived Amber (unchanged); priority re-derived for the week of 2026-09-28; lessons already captured today (LL-060–064), nothing new (2026-09-25)
[MANUAL] project-daily — day-review Q&A: 4 staleness reminders dropped; Dudaško Excel read dropped; MVP-scoping item closed as stale (ASM-104); TEO consolidation + Radim call closed; Part A/B split done; Fakturace contradictions + Sláma AR check and AI Platform WIP spec moved to week of 2026-09-28 (Fakturace downgraded highest→mid) (2026-09-25)
[MANUAL] project-assumptions — ASM-104 closed as stale per PM (2026-09-25)
[MANUAL] project-knowledge — BQ tracker table: MaxBuddy stage set to Nasazování per PM; tracker's Deployed/Řešení flagged as out of date (2026-09-25)
[AUTO] project-assumptions — added ASM-177 (Part A/B split), ASM-178 (SharePoint logistics table, 10-02 validation), ASM-179 (tracker sharing, open), ASM-180 (Fakturace doprav spec ownership, open); update note on ASM-161, from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
[AUTO] project-knowledge — Reklamace spec-coverage paragraph; Project Conventions: logistics initiatives table, external-account email, from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
[AUTO] project-stakeholders — updated STK-001, STK-013, STK-014, STK-044, from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
[AUTO] client-overview — Ways of Working: spec-first expectation vs. agile delivery, from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
[AUTO] project-daily — 6 action items added; Part A/B split action item marked done, from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
[AUTO] meeting-index — added 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table (2026-09-25)
[AUTO] project-assumptions — added ASM-181 (Sláma original-vision claim, open), ASM-182 (shared test phone + login), ASM-183 (two-address shipments, open); update notes on ASM-122, ASM-139, ASM-171, from 2026-09-24-viapharma-reklamace-knowledge-base-standoff (2026-09-25)
[AUTO] project-knowledge — Reklamace knowledge-base standoff paragraph (Jana's procedure flags, Sláma's savings view), from 2026-09-24-viapharma-reklamace-knowledge-base-standoff (2026-09-25)
[AUTO] project-stakeholders — updated STK-006, STK-007, STK-013, STK-014, STK-034 (sentiment Neutral leaning Champion → Neutral), STK-044, from 2026-09-24-viapharma-reklamace-knowledge-base-standoff (2026-09-25)
[AUTO] client-overview — Ways of Working: written client comments treated as the record, from 2026-09-24-viapharma-reklamace-knowledge-base-standoff (2026-09-25)
[AUTO] project-daily — 5 action items added, from 2026-09-24-viapharma-reklamace-knowledge-base-standoff (2026-09-25)
[AUTO] meeting-index — added 2026-09-24-viapharma-reklamace-knowledge-base-standoff (late routing; committed 2026-09-24 unrouted) (2026-09-25)
[AUTO] project-knowledge — Naming Conventions: AI-initiatives roadmap table conventions, from 2026-09-14-ai-initiatives-roadmap-table-alignment (routed late as superseded) (2026-09-25)
[AUTO] meeting-index — added 2026-09-14-ai-initiatives-roadmap-table-alignment; 2 prep files (2026-09-14, 2026-09-17); 3 notes from 2026-09-01 re-marked "Superseded — not routed" (2026-09-25)
[AUTO] document-index — added 4 unindexed internal documents (2026-09-11 Max chatbot spec; 2026-09-21 AI Platform design brief, UX benchmark brief, sitemap) (2026-09-25)
[MANUAL] harness-artifacts-index — registered 4 non-routing reference artifacts: listing-specifikace, ai-initiatives-okr-framework, ai-platform-claude-design-brief, action-items-archive (2026-09-25)
[AUTO] project-lessons — added LL-065 (map undefined phases under agile), LL-066 (resolve every written client spec comment), LL-067 (named owner defuses a negative narrative), from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table and 2026-09-24-viapharma-reklamace-knowledge-base-standoff (2026-09-25)
[MANUAL] project-weekly — generated and confirmed internal weekly 2026-W39 (2026-09-25)
[MANUAL] project-daily — status re-scoped to PM-actionable streams only (Amber, driver now Reklamace; infra and Kadlecová moved to a watch note); 64 action items owned by others moved to action-items-archive, only PM-owned items tracked going forward (2026-09-25)
[MANUAL] project-weekly — W39 Project Status and Action Items sections updated to the PM-scope rule (2026-09-25)
