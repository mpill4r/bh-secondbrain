---
status: closed
last_updated: 2026-09-25
last_updated_by: auto — project-daily close
project_status: Amber
---

# Daily — 2026-09-25 (Friday)

## Project Status

**Amber** (re-derived at close, unchanged). Drivers unchanged since 2026-09-24: the CC domain-expert continuity gap ([[ASM-091]]), and the disputed infra/DB access on the new cluster ([[ASM-164]]), which gates the Max chatbot's internal go-live phases ([[ASM-100]]), the MaxBuddy rollout and the first AI Platform release. There is no confirmation yet of Jura's DB-access retest. Today added a new Reklamace risk, still open: the supplier-data fields Axapta won't carry have no agreed home, and the rozvozový list fields are missing from the API contract. Positive signals continue: Dudaško's sentiment, and a clear phased path for TEO/OCR.

## Current Priority

**Heading into the week of 2026-09-28:**
- The 2026-09-29 management meeting: support Jindřich's "PR" value stories ([[ASM-160]]).
- The 2026-10-01 logistics meeting: the supplier-data options table ([[ASM-169]]) and Filip's email-agent demo ([[ASM-173]]).
- The Vosmek MaxBuddy wishlist call.
- Still open and carried: the Part A/B split with Tereza Foltýnová, starting the KPI measurement column in the BQ tracker ([[ASM-159]]), the MVP-vs-full-product scoping mismatch, and Filip's 5 Fakturace doprav code-vs-spec contradictions ([[ASM-131]]–[[ASM-135]]).
- TEO/OCR: consolidate Jura's comments and hold the informal call with Radim Švarc ([[ASM-165]], [[ASM-166]]).
- Watch: Jura's DB-access retest result ([[ASM-164]]).

## Action Items

- [ ] `carry-forward` `staleness` `low-prio` Review project-stakeholders — 96+ `-tbd-` fields (exceeds threshold of 5)
- [ ] `carry-forward` `staleness` `low-prio` Review client-overview — 14 `-tbd-` fields (exceeds threshold of 5)
- [ ] `carry-forward` `task` `mid-prio` **PM**: Generate & review project-weekly (overdue from Friday 2026-09-04) — /project-weekly
- [ ] `carry-forward` `follow-up` `mid-prio` **Marek Pillár**: Contact Filip Černý to walk through his growing pile of business-decision questions from Max/ViaPharma people; plan whether a direct meeting with them is needed — medium priority — from Filip Černý's Fakturace doprav backlog note, 2026-09-08
- [ ] `carry-forward` `task` `low-prio` **Jindřich Tůma / Marek Pillár**: Read through Tomáš Dudaško's AI-platform requirements Excel in full — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] `carry-forward` `follow-up` `low-prio` **Marek Pillár**: Data drift found on Maxie roadmap row "Přepojení na živého operátora při chybě nebo požadavku" — local roadmap data has it as Done, live Excel shows Planned. Not changed either way (out of scope for the estimates-routing task) — worth a quick check on which is correct — Marek's own note, 2026-09-09 — reprioritized via /todo review (2026-09-17)
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — **blocked: waiting on Honza Sovka's review first** — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] `carry-forward` `low-prio` **Marek Pillár / Tereza Foltýnová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — **deprioritized 2026-09-15**: no rush, will revisit sometime later this year — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] `carry-forward` **Marek Pillár**: Review the new Reklamace brief (`3. Reklamace.docx`) — confirm/correct business-value figures (currently sourced from the 2026-09-15 Tereza Foltýnová interview, flagged as potentially overstated), assign domain-expert/business-owner sign-off, and resolve open questions (label-OCR engine choice, e-mail-draft feature scope, whether a local case-status dashboard is wanted — **answered 2026-09-25: no, killed, see [[ASM-172]]**) — from cz-ai-logistics codebase read, 2026-09-16
- [ ] `carry-forward` `highest-prio` **Jindřich Tůma / Marek Pillár**: Resolve which timeline items were mis-scoped as MVP when they actually belong to the full product — **highest-prio for Thursday, 2026-09-24**, per PM — from 2026-09-17-lexie-max-maxie-weekly-sync — reprioritized via /todo review (2026-09-22)
- [ ] `carry-forward` `staleness` `low-prio` Review product-brief — exceeds 14-day staleness threshold, though 0 `-tbd-` fields
- [ ] `carry-forward` `staleness` `low-prio` Review project-assumptions — 8 open items exceed the 14-day-without-status-change threshold (ASM-035, ASM-033, ASM-030, ASM-029, ASM-028, ASM-027, ASM-025, ASM-023 — all last touched 2026-09-04/07)
- [ ] `carry-forward` **Marek Šimoník**: Review, edit, and confirm the completed order-prediction (Řízení poptávky) BQ Excel — full edit rights granted — from 2026-09-18-business-quantification-order-prediction-simonik
- [ ] `carry-forward` **Marek Pillár / Jindřich Tůma**: By end of this week, prepare a work-in-progress AI Platform spec/roadmap with open questions to show Dudaško — sequencing: design phase (~1 week), admin/role-views phase (~2-3 weeks), agentic-workflow follow-up conversation tentatively November — from 2026-09-21-ai-platform-vision-discovery-dudasko — partial 2026-09-24: Phase 1 prototype shown and accepted by Dudaško; written spec/roadmap still open (2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko)
- [ ] `carry-forward` **Jindřich Tůma**: Schedule a follow-up session to properly work through the AI adoption campaign draft/strategy — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] `carry-forward` **Jindřich Tůma**: Align with the relevant expert-group lead ("osmec") as BigHub's actual contact point for post-rollout adoption feedback, rather than the training center — for MaxBuddy this is confirmed as Luboš Vosmek (STK-011), resolved 2026-09-22 — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] `carry-forward` **Alana Sihelská**: Check with Vladislav Tvarůžek/BDC before tomorrow's meeting whether anyone has actually tested the AKS node-pool connectivity issue Jura reported last Friday — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] `carry-forward` **Jura Brázdil**: Check whether TEO/OCR's TEST-environment Blob storage can be self-provisioned on the platform ahead of a full deploy, without breaking anything — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] `carry-forward` **Jura Brázdil**: Continue tuning OCR bounding-box/crop accuracy and complete the candidate-list disambiguation approach for dates and addresses; re-run against full spring/autumn batches — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] `carry-forward` **Jindřich Tůma**: Schedule the Reklamace alignment meeting with Tomáš Dudaško and the head of logistics (plus Jan Sovka for historical context); include Marek on this and all future reklamace-thread meetings — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] `carry-forward` **Jindřich Tůma**: Coordinate with Honza Kabát on the Microsoft/Azure backlog-costing request and next steps, looping in Friday's Dudaško outcome — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] `carry-forward` **Jindřich Tůma**: Decide how to get his own Fireflies workspace access (join Marek's shared workspace vs. separate paid account) and confirm the approach with Marek — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] `carry-forward` **Radim Švarc / Michaela Albrechtová**: Verify the "Bezručova" (Mělník) branch entry missing from the číselník — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Radim Švarc / Michaela Albrechtová**: Push vendors to fill in complete addresses on protocols; return incomplete ones for completion rather than have BigHub guess the branch — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Jura Brázdil**: Give SPEDOS additional pipeline attention and send an export by end of this week (2026-09-25) — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Jura Brázdil**: Run the first offline batch (incl. JSON output) against the real Thermetal autumn-2026 protocols Míša sent — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Jura Brázdil**: Answer Radim's open question on BigHub's batch-creation logic for documents arriving via his twice-weekly Blob storage push — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [x] `carry-forward` **Marek Pillár**: Look into the Excel-only review-output issue — Radim's downstream review/correction workflow is entirely manual spreadsheet work with no AI assistance in that step; explore whether a better alternative exists — due 2026-09-24 — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal — resolved at close: direction agreed in 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics (Excel stays for the autumn 2026 cycle; non-Excel review solution to be built before spring 2027; follow-ups tracked separately) (2026-09-25)
- [ ] `carry-forward` **Radim Švarc**: Send back "correct" excel/json corrections to BigHub in a format agreed with Jura, so accuracy can be tracked over time — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the disambiguation-approach conflict with ASM-119 — confirm whether the ranked-candidate mechanism is being reversed or whether this was a narrower UI-presentation point — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the Blob storage/deployment blocker conflict with ASM-088 — confirm current dependency status on Dr. Max infra/BDC — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Get Filip Černý to confirm/reconcile the 5 code-vs-spec contradictions found in today's Fakturace doprav code audit (kiosk auth, document versioning, AR pairing, temperature-log OCR gap, multi-vehicle silent overwrite) — [[ASM-131]], [[ASM-132]], [[ASM-133]], [[ASM-134]], [[ASM-135]] — before the spec is finalized or shared further — from today's redline review, 2026-09-23
- [ ] `carry-forward` **Marek Pillár**: Confirm with P. Sláma whether the AR-pairing-key dependency (ZOPV/OPL) is already resolved in code — [[ASM-133]] — and update the Závislosti section accordingly — from today's redline review, 2026-09-23
- [ ] `carry-forward` **Jindřich Tůma**: Schedule the Reklamace continue-or-close decision meeting with Tomáš Dudaško, Rudolf Žůrek, Petr Spilka, and Jan Žižka — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Jindřich Tůma**: Escalate the AKS/BDC request-turnaround bottleneck (6-7 week queue behind Vláďa) at Tuesday's (2026-09-29) management meeting, up to CEO level if needed — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Jindřich Tůma**: Raise the rozvozový list free-text data-source gap at the next logistics status meeting — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Jindřich Tůma / Filip Černý**: Push Petr Sláma on the fakturace doprav API-contract revision — Filip to brief Jindřich on the technical specifics beforehand — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Filip Černý**: Finish the fakturace doprav backlog entry in the board/Kanban — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Jindřich Tůma**: Reach out to Petr Ondráček directly via Teams for the order-prediction per-channel budget Excel, since Marek Šimoník is on vacation — needed before the 2026-09-29 follow-up — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Filip Černý**: Continue chasing Petr Sláma / Jana Egrmaierová for formal written testing feedback on Reklamace — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] `carry-forward` **Jura Brázdil**: Fix the visible-but-empty admin-section gaps for non-admin accounts (reflow layout or add an explicit disabled/tooltip state) — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] `carry-forward` **Jura Brázdil**: Seal the MCP server registration security gap (secret/header leakage to any agent reading server descriptions) before further build-out — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] `carry-forward` **Jura Brázdil**: Give Jindřich a realistic-constraints summary of the Dr. Max requirements/backlog Excel, ahead of a fuller scoping conversation — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] `carry-forward` **Jura Brázdil**: Update X-Manager ticket statuses and add written replies to each ticket commented on — due 2026-09-24 — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Request access to Dr. Max's test order database (find the right infra contact) and connect Max to it — due 2026-09-24 — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Prepare a model cost projection for Max (needs expected traffic from Dr. Max) and add a model switcher to the test page — due next weekly sync (2026-10-01) — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Wire prescription (Rx) drug stock lookup without an e-recept — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Remove free-text feedback from the end-conversation screen for the public version; fix the text-copying bug in the feedback field — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Resend the Max analytics dashboard URL (outstanding since 2026-09-17) — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Create an X-Manager ticket for package-leaflet display with a highlighted section (e.g. dosage) — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Kateřina Kadlecová / Dr. Max CC team**: Send the exact wording of Max's opening message, including the AI Act disclosure — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Kateřina Kadlecová / Dr. Max CC team**: Shorten the tone prompt to comma-separated keywords — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Kateřina Kadlecová**: Write the bubble-placement change (intro text down above the bubbles, chat-style) into the X-Manager ticket — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Kateřina Kadlecová**: Get Dr. Max IT to enable mobile and geolocation testing on work devices — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Kateřina Kadlecová / Dr. Max CC team**: Send public methodologies as PDFs, starting with order tracking/reservations — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Lucie Fendrichová**: Provide order-status definitions and customer messaging, incl. combinations with specific carriers — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Dr. Max CC team**: Test the "show X more" carousel fix on mobile phones — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jindřich Tůma**: Gather Maxie/Atlantis materials and schedule a joint meeting with Simona Mertová, Honza Zelený and Tecl (Atlantis) to align on replicating the existing IVR Maxí solution — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jindřich Tůma**: Find out whether ElevenLabs licences and voices are paid within the project or by Dr. Max; set up an ElevenLabs Q&A if needed — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Check whether ElevenLabs barge-in can pick up the interrupting context and respond to it, and report back to Mertová — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Simona Mertová**: Send Marek the requested email confirmation — due 2026-09-25 — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Jura Brázdil**: Test DB access from the new cluster right after the meeting and report whether Tvarůžek's "done" is accurate — due 2026-09-24 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Jura Brázdil / Jindřich Tůma**: Share the prototype link (with PIN) with Tomáš Dudaško — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Jindřich Tůma**: Prepare "PR" value stories per live or near-live initiative for the 2026-09-29 project meeting; preview with Dudaško — due 2026-09-29 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Add a KPI measurement-method column to the BQ tracker and collect measurement methods from every business owner — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: With Tereza Foltýnová, agree the logistics Part A (finish Reklamace/Fakturace doprav specs) / Part B (new AI initiatives in tracker format) split — due 2026-09-25 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Collect and prioritize department AI-initiative backlogs (logistics, marketing via Marek Dvořák, others) in BQ tracker format — target end of November 2026 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Get email sign-off on BQ figures from Marek Šimoník (after vacation) and Simona Mertová — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Jindřich Tůma / Jura Brázdil**: Plan the first AI Platform release in detail (new-cluster deploy, MaxBuddy migration, chatbot deploy, security fixes, frontend wiring; ~4 weeks after DB access) — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Jindřich Tůma**: Keep Dudaško regularly updated on which department's AI-initiative backlog is in progress — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Marek Pillár**: Consolidate Jura Brázdil's comments into a phased TEO/OCR proposal: Excel for autumn 2026, non-Excel review solution before spring 2027, longer-term vision after ([[ASM-165]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [ ] **Marek Pillár**: Informal, non-committal call with Radim Švarc: gauge openness to building beyond Excel; map the full TEO process, follow-on use cases (e.g., next-service-due tracking) and per-cycle manual effort ([[ASM-166]], [[ASM-168]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [ ] **Marek Pillár**: Talk with Jindřich Tůma about the capacity pool: is he inside the 3 FTE or extra, and what does his September capacity table show ([[ASM-167]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [ ] **Jindřich Tůma**: Find out from Tomáš (assumed Dudaško) how much of the ~3 FTE annual budget has accumulated unused since May ([[ASM-167]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [ ] **Jindřich Tůma**: Send Filip Černý the Reklamace supplier-attribute table — due 2026-09-25 — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Review the supplier-attribute table and add input per section; write up the 3 Excel-on-SharePoint risks in business language plus a 4th "open unknowns" point ([[ASM-169]]) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Research SharePoint Lists (security, audit trail, automated reads) and send Jindřich a short write-up ([[ASM-169]]) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Jindřich Tůma**: Research Confluence as a Reklamace supplier-data store (fit, licensing) ([[ASM-169]]) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Jindřich Tůma**: Get editor/viewer counts for the supplier data via Jana Egrmaierová — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Build the ~1 MD Reklamace email-agent demo (text files, not Outlook) — due before 2026-10-01 ([[ASM-173]]) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Send Jindřich the Teams discussion link on the rozvozový list fields missing from the Axapta contract ([[ASM-174]]) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Jindřich Tůma**: Put the supplier-data options and the complete Axapta requirement list into the Reklamace spec; prepare materials for the 2026-10-01 logistics meeting — due 2026-10-01 — from 2026-09-25-reklamace-supplier-data-source-options

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
