---
status: closed
last_updated: 2026-10-01
last_updated_by: auto — project-daily close
project_status: Amber
---

# Daily — 2026-10-01 (Thursday)

## Project Status

**Amber** (carried forward from 2026-09-30). Driver: **Reklamace**. Today's logistics meeting decides the supplier-data store (recommendation: AX-minimal + SharePoint Lists, [[ASM-214]]). The spec is due 2026-10-02 with the agreed decisions or open questions ([[ASM-185]], [[ASM-186]]), and the 2026-10-15–16 UAT is at risk. Listing was reset to enrichment-first (Magento out of the MVP, [[ASM-207]]).

## Current Priority

**Reklamace, 2026-10-01 logistics meeting**: walk through the data map and recommendation, Filip's email-agent demo, then a written recap of decisions and the spec by 2026-10-02.

## Action Items

- [ ] `carry-forward` `highest-prio` **Marek Pillár**: In parallel, draft the new (final) Reklamace spec with all product comments/requirements worked in. Leave the Excel's open decisions as open for now — from PM's plan, 2026-09-29 — partial 2026-09-29: first full draft `1. Feature Specs/3. Reklamace/3. Reklamace.docx` created via /product-client-spec; awaiting PM review — updated at close: working version is `3. Reklamace v3.docx` (PM review comments applied twice; v1/v2 deleted); still open until the 10-01 decisions are added
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Walk the logistics team through the options Excel at the meeting, then send it as a meeting recap for approval / consideration — due 2026-10-01 — from PM's plan, 2026-09-29
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Once the Excel is approved, add the AGREED decisions to the spec and send it to logistics / Petr Sláma for final approval. Target: spec with the knowledge base decided — due 2026-10-09 — from PM's plan, 2026-09-29
- [ ] `carry-forward` `follow-up` `mid-prio` **Marek Pillár**: Contact Filip Černý to walk through his growing pile of business-decision questions from Max/ViaPharma people; plan whether a direct meeting with them is needed — medium priority — from Filip Černý's Fakturace doprav backlog note, 2026-09-08
- [ ] `carry-forward` `follow-up` `low-prio` **Marek Pillár**: Data drift found on Maxie roadmap row "Přepojení na živého operátora při chybě nebo požadavku" — local roadmap data has it as Done, live Excel shows Planned. Not changed either way (out of scope for the estimates-routing task) — worth a quick check on which is correct — Marek's own note, 2026-09-09 — reprioritized via /todo review (2026-09-17)
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — **blocked: waiting on Honza Sovka's review first** — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] `carry-forward` `low-prio` **Marek Pillár / Tereza Foltýnová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — **deprioritized 2026-09-15**: no rush, will revisit sometime later this year — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
- [ ] `carry-forward` **Marek Pillár / Jindřich Tůma**: By end of this week, prepare a work-in-progress AI Platform spec/roadmap with open questions to show Dudaško — sequencing: design phase (~1 week), admin/role-views phase (~2-3 weeks), agentic-workflow follow-up conversation tentatively November — from 2026-09-21-ai-platform-vision-discovery-dudasko — partial 2026-09-24: Phase 1 prototype shown and accepted by Dudaško; written spec/roadmap still open (2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko) — moved to the week of 2026-09-28 per PM (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the disambiguation-approach conflict with ASM-119 — confirm whether the ranked-candidate mechanism is being reversed or whether this was a narrower UI-presentation point — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal
- [x] `carry-forward` **Marek Pillár / Jura Brázdil**: Reconcile the Blob storage/deployment blocker conflict with ASM-088 — confirm current dependency status on Dr. Max infra/BDC — from 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal — resolved 2026-10-01: BigHub deploys on the test environment itself (~2 weeks to automated run under VPN); production still depends on BDC ([[ASM-129]]) (2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors)
- [ ] `carry-forward` `mid-prio` **Marek Pillár**: Get Filip Černý to confirm/reconcile the 5 code-vs-spec contradictions found in today's Fakturace doprav code audit (kiosk auth, document versioning, AR pairing, temperature-log OCR gap, multi-vehicle silent overwrite) — [[ASM-131]], [[ASM-132]], [[ASM-133]], [[ASM-134]], [[ASM-135]] — before the spec is finalized or shared further — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, below Reklamace in priority (2026-09-25)
- [ ] `carry-forward` **Marek Pillár**: Confirm with P. Sláma whether the AR-pairing-key dependency (ZOPV/OPL) is already resolved in code — [[ASM-133]] — and update the Závislosti section accordingly — from today's redline review, 2026-09-23 — moved to the week of 2026-09-28 per PM, with the Fakturace contradictions (2026-09-25)
- [ ] `carry-forward` **Marek Pillár / Jura Brázdil**: Check whether ElevenLabs barge-in can pick up the interrupting context and respond to it, and report back to Mertová — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] `carry-forward` **Marek Pillár**: Add a KPI measurement-method column to the BQ tracker and collect measurement methods from every business owner — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Collect and prioritize department AI-initiative backlogs (logistics, marketing via Marek Dvořák, others) in BQ tracker format — target end of November 2026 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] `carry-forward` **Marek Pillár**: Get email sign-off on BQ figures from Marek Šimoník (after vacation) and Simona Mertová — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko — partial 2026-09-29: Šimoník agreed on the call to confirm by email, incl. the 2 annualized columns for Dudaško; chase if not in by end of week (2026-09-29-order-prediction-dashboard-v2-review)
- [ ] `carry-forward` **Marek Pillár**: Talk with Jindřich Tůma about the capacity pool: is he inside the 3 FTE or extra, and what does his September capacity table show ([[ASM-167]]) — from 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
- [ ] `carry-forward` **Marek Pillár**: Ask Tomáš Dudaško whether the cross-department AI-initiative tracker can be shared with other departments ([[ASM-179]]) — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table
- [ ] `carry-forward` **Marek Pillár / Tereza Foltýnová**: Review her draft table together (Wed/Thu) before the 2026-10-02 session — from 2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table — scheduled 2026-09-30 at Max (2026-09-29-management-meeting-debrief-reklamace-thursday-plan)
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: After the Thursday session, email logistics the agreed decisions for confirmation and send the Reklamace spec with agreed changes or yellow-highlighted open questions ([[ASM-185]], [[ASM-186]]) — due 2026-10-02 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
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
- [x] `carry-forward` `highest-prio` **Marek Pillár**: Send the email recap of the Listing meeting to Petr Neuman and Michaela Vdovicynová — due 2026-09-30 — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy — done (confirmed by PM 2026-10-01)
- [ ] `carry-forward` **Marek Pillár**: Rewrite the Listing spec and roadmap: Magento out of the MVP, enrichment first, food-supplements batch + export ([[ASM-207]], [[ASM-208]]) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `carry-forward` **Marek Pillár / Filip Černý**: Describe the scraping variant precisely for Dr. Max legal (process, sources, human review) and hand it to Petr Neuman — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `carry-forward` **Marek Pillár / Filip Černý**: Research third-party scraping/extraction services and a cost breakdown (hundreds vs. tens of thousands of SKUs), incl. a human-assisted URL variant — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `carry-forward` **Marek Pillár / Filip Černý**: Find out what happened to the earlier scraping legal check (via Alana Sihelská / Lukáš Szücs) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [x] `carry-forward` `highest-prio` **Marek Pillár**: Send the data map to logistics as a friendly prep email (read if time allows, discuss tomorrow; soft tone for Sláma) — due 2026-09-30 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review — done (confirmed by PM 2026-10-01)
- [ ] `task` `highest-prio` **Marek Pillár**: Send Radim Švarc the TEO/OCR platform/initiative proposals for the spring 2027 cycle; review with him early next week, then consult Tomáš Burda — due 2026-10-02 — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors

## Key Events

**TEO/OCR sync** ([2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors](../../meetings/external/2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors.md)): The offline autumn route works. Termetal and Rakun are processed (Rakun: 84 protocols, 18 flagged fields, no silent errors), and Míša calls it "a huge help". Cost is ~0.5–2 Kč per page (~1 Kč on average) and was accepted; the platform will add per-use-case cost tracking and spending caps. Next: Spedos autumn, a smaller vendor, then air conditioning. The test environment should run automatically in ~2 weeks, while production depends on BDC. Marek sends spring proposals via Radim, then Burda. Next sync is 2026-10-14 13:00 ([[ASM-218]]–[[ASM-222]]).

**Session summary (close)**: The TEO/OCR sync confirmed the offline autumn route delivers real value at ~1 Kč per page, with next vendors and the spring proposals (via Radim, then Burda) queued ([[ASM-218]]–[[ASM-222]]). The Slovak prep email and the final data map went to logistics ahead of the Reklamace meeting, and the Listing recap went to Neuman and Vdovicynová. The 30. 9. daily was closed and today's created. Still open: the logistics meeting outcome, the written recap, and the spec by 2026-10-02.

## Audit Log

[AUTO] project-daily — created today's daily; closed 2026-09-30 first; carried forward 41 unchecked items; status Amber and priority carried forward (2026-10-01)
[AUTO] project-assumptions — added ASM-218–ASM-222; update notes on ASM-129, ASM-165, ASM-130, ASM-120, ASM-127, from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors (2026-10-01)
[AUTO] project-knowledge — TEO/OCR entry: autumn offline batches, costs, air-conditioning protocols, volume, from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors (2026-10-01)
[AUTO] project-stakeholders — updated STK-041, STK-042, STK-026, STK-025, from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors (2026-10-01)
[AUTO] project-daily — 1 action item added (spring proposals to Radim); Blob-storage reconcile item resolved, from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors (2026-10-01)
[AUTO] meetings/index — added 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors (2026-10-01)
[AUTO] project-lessons — added LL-75 (match-failure flags can reveal upstream data errors), from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors (2026-10-01)
[MANUAL] project-daily — 2 action items marked done per PM: data-map prep email to logistics, Listing recap to Neuman/Vdovicynová (2026-10-01)
[AUTO] project-daily — closed 2026-10-01: session summary written; no further items resolved from session evidence; staleness items already carried (no change); status re-derived Amber (unchanged); priority unchanged (Reklamace meeting recap + spec by 2026-10-02); lesson already captured today (LL-75) (2026-10-01)
