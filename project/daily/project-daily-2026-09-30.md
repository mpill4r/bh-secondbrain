---
status: closed
last_updated: 2026-09-30
last_updated_by: auto — project-daily close
project_status: Amber
---

# Daily — 2026-09-30 (Wednesday)

## Project Status

**Amber** (carried forward from 2026-09-29). Driver: **Reklamace**. The supplier-data store decision is open until the 2026-10-01 logistics meeting ([[ASM-169]]), the spec (`3. Reklamace v3.docx`) goes out with open questions by 2026-10-02 ([[ASM-185]], [[ASM-186]]), and the 2026-10-15–16 UAT start is at risk. Watch: Deloitte's parallel AI initiatives at Dr. Max ([[ASM-187]]).

## Current Priority

**Reklamace, ahead of the 2026-10-01 logistics meeting.** Today:
- Finalize the data-map Excel with Filip's comments.
- Listing workshop with Petr Neuman at 11:00.
- Meet Tereza at Max.
- Marek / Filip / Jindřich sync ~15:00–16:00 (data map + email-agent demo).

## Action Items

- [x] `carry-forward` `highest-prio` **Marek Pillár**: Have the Reklamace options Excel 100% ready. It covers every possible variant/option with a reasoned pro/con for each, ideally priced in MD — due 2026-10-01 (Thursday logistics meeting) — from PM's plan, 2026-09-29 — partial 2026-09-29: data-source map drafted ("marek sheet" in `Mapa_zdroju_a_umisteni_dat_reklamace 1 - marek sheet.xlsx`); sent to Filip Černý for a check; MD pricing still open — done 2026-09-30: `Final_Mapa_zdroju_a_umisteni_dat_reklamace.xlsx` (options with pros/cons + BigHub recommendation); MD pricing not included
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: In parallel, draft the new (final) Reklamace spec with all product comments/requirements worked in. Leave the Excel's open decisions as open for now — from PM's plan, 2026-09-29 — partial 2026-09-29: first full draft `1. Feature Specs/3. Reklamace/3. Reklamace.docx` created via /product-client-spec; awaiting PM review — updated at close: working version is `3. Reklamace v3.docx` (PM review comments applied twice; v1/v2 deleted); still open until the 10-01 decisions are added
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Walk the logistics team through the options Excel at the meeting, then send it as a meeting recap for approval / consideration — due 2026-10-01 — from PM's plan, 2026-09-29
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: Once the Excel is approved, add the AGREED decisions to the spec and send it to logistics / Petr Sláma for final approval. Target: spec with the knowledge base decided — due 2026-10-09 — from PM's plan, 2026-09-29
- [ ] `carry-forward` `follow-up` `mid-prio` **Marek Pillár**: Contact Filip Černý to walk through his growing pile of business-decision questions from Max/ViaPharma people; plan whether a direct meeting with them is needed — medium priority — from Filip Černý's Fakturace doprav backlog note, 2026-09-08
- [ ] `carry-forward` `follow-up` `low-prio` **Marek Pillár**: Data drift found on Maxie roadmap row "Přepojení na živého operátora při chybě nebo požadavku" — local roadmap data has it as Done, live Excel shows Planned. Not changed either way (out of scope for the estimates-routing task) — worth a quick check on which is correct — Marek's own note, 2026-09-09 — reprioritized via /todo review (2026-09-17)
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Capture live comments from both meetings in the Figma export of the roadmap, then export as PNG/PDF and email back to attendees with what gets agreed — **blocked: waiting on Honza Sovka's review first** — from 2026-09-09-logistics-cc-roadmap-presentation-prep
- [ ] `carry-forward` `low-prio` **Marek Pillár / Tereza Foltová**: Schedule a follow-up session to cover the remaining ~9 initiatives from the Business Quantification prep template — **deprioritized 2026-09-15**: no rush, will revisit sometime later this year — from 2026-09-15-business-quantification-reklamace-fakturace-doprav
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
- [ ] `carry-forward` **Marek Pillár**: Ask Tomáš Dudaško whether the cross-department AI-initiative tracker can be shared with other departments ([[ASM-179]]) — from 2026-09-25-tereza-foltova-reklamace-focus-logistics-initiatives-table
- [ ] `carry-forward` **Marek Pillár / Tereza Foltová**: Review her draft table together (Wed/Thu) before the 2026-10-02 session — from 2026-09-25-tereza-foltova-reklamace-focus-logistics-initiatives-table — scheduled 2026-09-30 at Max (2026-09-29-management-meeting-debrief-reklamace-thursday-plan)
- [x] `carry-forward` `highest-prio` **Marek Pillár**: Get the Reklamace spec draft to Filip Černý by end of day — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan — done: Filip confirmed he has the spec (2026-09-30)
- [x] `carry-forward` `highest-prio` **Marek Pillár**: Set up a Marek / Filip Černý / Jindřich Tůma sync on the options Excel before Thursday — due before 2026-10-01 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan — agreed with Filip for 2026-09-30 afternoon (~15:00–16:00), online, covering the data map + demo (2026-09-29-reklamace-email-agent-demo-review-filip) — done: held 2026-09-30 (2026-09-30-reklamace-thursday-prep-data-map-demo-review)
- [ ] `carry-forward` `highest-prio` **Marek Pillár**: After the Thursday session, email logistics the agreed decisions for confirmation and send the Reklamace spec with agreed changes or yellow-highlighted open questions ([[ASM-185]], [[ASM-186]]) — due 2026-10-02 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` **Marek Pillár**: Meet Tereza Foltová at Max to review the initiatives she collected since Friday — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [x] `carry-forward` **Marek Pillár**: Run the Listing workshop with Petr Neuman and Michaela Vdovicynová — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan — done 2026-09-30 (2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy)
- [ ] `carry-forward` `mid-prio` **Marek Pillár**: Define each later phase's value driver ("system seller") with each initiative owner via discovery; give logistics outlook anchor points next week; coordinate capacity with Jindřich Tůma before promising anything ([[ASM-190]]) — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` `low-prio` **Marek Pillár**: Put blockers / personal time into the calendar so Jindřich Tůma can plan meetings around it — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] `carry-forward` **Marek Pillár**: Send a four-point summary of the internal sync to the BigHub business group (for Ján Kabát and Jan Sovka) — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [x] `carry-forward` `highest-prio` **Marek Pillár**: Work Filip Černý's comments into the data-map Excel ("marek sheet"): merge overlapping rows, reconsider the feature-like row, remove source references — due 2026-09-30 morning — from 2026-09-29-reklamace-email-agent-demo-review-filip — done 2026-09-30: PM resolved 7 comments; Claude applied the 5 PM-answered threads in the new sheet "marek sheet v2" (changes highlighted yellow) and replied "Resolved by Claude" in each thread
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
- [x] `task` **Marek Pillár**: Process the Listing meeting with Petr Neuman (upload the transcript or notes) and send a recap — due 2026-09-30 — from 2026-09-30-listing-neuman-discovery-kickoff-meeting-prep — done: processed as 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `task` `highest-prio` **Marek Pillár**: Send the email recap of the Listing meeting to Petr Neuman and Michaela Vdovicynová — due 2026-09-30 — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `task` **Marek Pillár**: Rewrite the Listing spec and roadmap: Magento out of the MVP, enrichment first, food-supplements batch + export ([[ASM-207]], [[ASM-208]]) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `task` **Marek Pillár / Filip Černý**: Describe the scraping variant precisely for Dr. Max legal (process, sources, human review) and hand it to Petr Neuman — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `task` **Marek Pillár / Filip Černý**: Research third-party scraping/extraction services and a cost breakdown (hundreds vs. tens of thousands of SKUs), incl. a human-assisted URL variant — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] `task` **Marek Pillár / Filip Černý**: Find out what happened to the earlier scraping legal check (via Alana Sihelská / Lukáš Szücs) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [x] `task` `highest-prio` **Marek Pillár**: Fix the AX column in the data map ("possible, not agreed" instead of ?/—); review the sheet and the result paragraph for errors, incl. the "minimal AX development" wording — due 2026-09-30 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review — done: final file `Mapa_zdroju_a_umisteni_dat_reklamace – final.xlsx` (one sheet); AX column relabelled "Možné – nedomluveno", pros/cons overview + new result at the bottom, changes tracked as red strikethrough
- [ ] `task` `highest-prio` **Marek Pillár**: Send the data map to logistics as a friendly prep email (read if time allows, discuss tomorrow; soft tone for Sláma) — due 2026-09-30 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review

## Key Events

**Reklamace Thursday prep** ([2026-09-30-reklamace-thursday-prep-data-map-demo-review](../../meetings/internal/2026-09-30-reklamace-thursday-prep-data-map-demo-review.md)): The three-way sync aligned on the data map. Store columns mean feasibility; AX blockers are political. The recommendation for 10-01 is AX-minimal plus a SharePoint List, sent today as a soft prep email. Filip's deck is approved with keyword highlighting. Infra requests move to ServiceNow, and one shared Entra registration will provide the UAT login ([[ASM-213]]–[[ASM-217]]).

**Listing reset with Petr Neuman** ([2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy](../../meetings/external/2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy.md)): Magento is out of the MVP. A Magento import changes only one column at a time, and CZ is moving to a global PIM ~9 months out. The focus shifts to enrichment: the next batch is food supplements (~2,000 SKUs) with an export for the parameter specialist, and every SKU is still human-reviewed ([[ASM-207]]–[[ASM-212]]). Scraping goes to Dr. Max legal via Neuman as a secondary goal.

**Data-map Excel — review round**: The PM resolved Filip's comments himself and answered 5 threads with instructions. Claude applied them in a duplicated sheet "marek sheet v2", with 26 changed cells highlighted yellow:
- the follow-up email process reframed as a new feature (scope expansion, ~10 MD), with its instructions moved into Poznámky;
- open questions added for the standard/specific flag and the photo-instruction data;
- the missing AX fields reframed from a BigHub error to an open question;
- the result rewritten per Filip: AX supplies only the supplier account and existing case data (reklamace no., RD, issue date), and everything supplier-specific goes into one Instrukce/KB table (SharePoint Lists), with pros before cons;
- the PM's own text polished and the remaining source lines removed.

The original sheet is unchanged, and the threaded comments were preserved with Claude replies.

**Session summary (close)**: Reklamace was still the focus.
- **Reklamace data map**: the 5 answered comment threads went into "marek sheet v2", with Claude replies. The PM's edits and the three-way sync (feasibility columns, AX-minimal + SharePoint Lists recommendation) then produced the single-sheet `Final_Mapa_zdroju_a_umisteni_dat_reklamace.xlsx`, all changes accepted, and a Slovak prep email for 10-01.
- **Listing reset with Neuman**: Magento is out of the MVP; food supplements (~2,000 SKUs) + export come first ([[ASM-207]]–[[ASM-212]]).
- **Filip's email-agent deck**: finalised.
- **Track record**: the history of the Zentiva follow-up email sequence was reconstructed (Sláma's May comments were never answered).

## Audit Log

[AUTO] project-daily — created today's daily; carried forward 40 unchecked items from 2026-09-29 (closed); status Amber and priority carried forward (2026-09-30)
[MANUAL] Mapa_zdroju_a_umisteni_dat_reklamace 1 - marek sheet.xlsx — new sheet "marek sheet v2" (26 cells changed, yellow); 5 comment threads answered "Resolved by Claude" and marked done; original sheet untouched (2026-09-30)
[AUTO] meetings/index — added prep 2026-09-30-listing-neuman-discovery-kickoff-meeting-prep (2026-09-30)
[AUTO] project-daily — 1 action item added (Listing meeting recap), from 2026-09-30-listing-neuman-discovery-kickoff-meeting-prep (2026-09-30)
[AUTO] project-assumptions — added ASM-207–ASM-212; ASM-065, ASM-067, ASM-032 superseded; update notes on ASM-073, ASM-033, ASM-068, from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy (2026-09-30)
[AUTO] project-knowledge — AI Listing Tool entry: Listing reset (Magento import limitation, global PIM, supplier data, legislative groups, vendor portal), from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy (2026-09-30)
[AUTO] project-stakeholders — updated STK-023, STK-048, STK-006; added STK-058 ("Maruška", low confidence), from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy (2026-09-30)
[AUTO] project-daily — 5 action items added; Listing-meeting processing item closed, from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy (2026-09-30)
[AUTO] meetings/index — added 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy (2026-09-30)
[AUTO] project-lessons — added LL-73 (verify legacy import mechanics before committing MVP write-back), from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy (2026-09-30)
[AUTO] project-assumptions — added ASM-213–ASM-217; update notes on ASM-170, ASM-174, ASM-205, ASM-206, ASM-188, ASM-182, ASM-122, from 2026-09-30-reklamace-thursday-prep-data-map-demo-review (2026-09-30)
[AUTO] project-knowledge — Reklamace entry: email-agent prototype (first-email text, reply states), from 2026-09-30-reklamace-thursday-prep-data-map-demo-review (2026-09-30)
[AUTO] project-stakeholders — updated STK-034, STK-016, STK-026, STK-006, from 2026-09-30-reklamace-thursday-prep-data-map-demo-review (2026-09-30)
[AUTO] project-daily — 2 action items added; 2 items closed (spec to Filip, three-way sync), from 2026-09-30-reklamace-thursday-prep-data-map-demo-review (2026-09-30)
[AUTO] meetings/index — added 2026-09-30-reklamace-thursday-prep-data-map-demo-review (2026-09-30)
[AUTO] project-lessons — added LL-74 (options matrices: separate feasibility from agreement), from 2026-09-30-reklamace-thursday-prep-data-map-demo-review (2026-09-30)
[MANUAL] Mapa_zdroju_a_umisteni_dat_reklamace – final.xlsx — new single-sheet final data map from PM's v2 + 2026-09-30 sync decisions (ASM-213/214/215): feasibility legend, AX column "Možné – nedomluveno", presentation-ready pros/cons per option, new result; replaced text kept as red strikethrough, original solution texts archived at the bottom (2026-09-30)
[MANUAL] Final_Mapa_zdroju_a_umisteni_dat_reklamace.xlsx — all tracked changes accepted (35 cells), archive rows removed, intended formatting restored (semantic fills, header styles, bold, row heights); PM edits (E9, F29) kept (2026-09-30)
[AUTO] project-daily — closed 2026-09-30: session summary written; 2 action items resolved (options Excel → final data map; Listing workshop held); staleness items already carried (no change); status re-derived Amber (unchanged); priority unchanged (Reklamace 10-01 meeting + spec by 10-02); lessons already captured today (LL-73, LL-74) (2026-09-30)
