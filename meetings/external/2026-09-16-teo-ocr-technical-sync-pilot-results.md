---
last_updated: 2026-09-16
type: external
attendees: [Tomáš Burda, Jura Brázdil, Alana Sihelská, Michaela Albrechtová]
tldv_link:
---

# TEO/OCR Technical Sync — Blind Pilot Results & Blob Storage Planning

**Date**: 2026-09-16
**Attendees**: Tomáš Burda (Dr. Max — head of technical department, STK-025), Jura Brázdil (BigHub — TEO/OCR developer, STK-026), Alana Sihelská (BigHub, standing in for Jindřich Tůma, STK-004), Michaela Albrechtová (Dr. Max — TEO/OCR contact, STK-042, identity inferred from a conference-room speaker label and Burda addressing her as "Míša" — confirmed by PM)
**Type**: external
**Recording**: Alana asked Burda to record locally for Jindřich Tůma, since she couldn't record from her own account — no tldv link provided
**Previous session**: No prior instance of this specific technical-sync thread exists in the harness — attendees reference a working session "last week" that set up this test (send a real 2025 vendor dataset, run the pipeline blind without touching it) which was not itself captured here. Related business-context session: [2026-09-15-business-quantification-teo-ocr](2026-09-15-business-quantification-teo-ocr.md)
**Meeting prep**: N/A

## TL;DR

BigHub ran the TEO/OCR pipeline blind against a real 2025 dataset (140 protocols, the 2 pilot vendors) with no manual tuning, and walked Dr. Max through the results live: accuracy came in a few points above the previously measured 91%/94% benchmarks, device type/order number/service company all hit 100%, and roughly a third of protocols got flagged for human review — though several flags turned out to be false positives on genuinely legible data. Concrete next steps: BigHub is migrating its platform to new AKS node pools and will self-provision Blob storage for a TEST environment (no infra-team dependency to create it), Burda reviewed BigHub's technical/API documentation and is starting Dr. Max-side build work the next day, and Michaela's ServiceNow-import form is nearly done and expected live this week or early next. Next joint sync: Tuesday next week, ~14:00.

## Key Discussion Points

### Blind validation results on real 2025 data

Jura screen-shared the extraction output (still Excel-like at this stage) from running the pipeline, untouched, against the agreed real 2025 dataset for the 2 pilot vendors. Positive: equipment type, order number ("zakázka"), and service company all came back 100% — "z tím není vůbec žádný problém" [translated from Czech: "there's no problem with that at all"]. One clear bug: a single missing address extraction that Jura hasn't yet root-caused — he confirmed it's a genuine failure, not a data-quality issue, and will investigate further. The recurring weak spot remains handwritten fields — branch/cost-center numbers and inspection dates.

Of 140 protocols, 47 (~a third) were flagged for human review. Jura and Michaela both noted several flags were false positives on data that reads unambiguously to a human eye ("tady sedmnáctka je podle mě za mě úplně jasná" [translated: "this '17' looks completely unambiguous to me"]) — meaning the real review burden may be lower than the raw flag rate suggests, though this wasn't quantified further. One genuine catch: the system correctly flagged a case where BigHub's own team had mistranscribed a date (wrote "11" instead of the correct "17") during pipeline setup — confirming the review-flagging mechanism does catch real errors, not just noise. Branch-count reconciliation was close but imperfect: 376 extracted vs. 356 actual — described as "poměrně svěžná" [translated: "a fairly decent match"], not investigated further in this call.

Overall measured accuracy on this real blind dataset came in a few percentage points *above* what was measured on the original test set — Jura flagged this could partly be luck rather than a guaranteed improvement, and didn't want to over-claim it.

### Bugs found during review

Michaela caught two issues Jura wasn't aware of:
1. **Duplicated defects/findings text** — the free-text "závady a nedostatky" (defects/shortcomings) field is being written out twice in the output for every record. Jura hadn't noticed this and will investigate.
2. **A missed review flag** — protocol #136 had a genuine date error that wasn't flagged orange for review (should have been) — a real "silent error" instance, i.e. exactly the failure mode the production spec's accuracy tables are designed to track and minimize.

Jura separately noted he's been focused on getting the bounding-box crops (the visual reference to the original document for each extracted value) precisely aligned — flagged one example where a crop was slightly off and didn't quite capture the relevant text (an EPS reference).

### Delivery architecture: Blob storage, node pools, and test environment

Today the pipeline runs entirely locally/offline; inference is currently run manually through Kubernetes. Jura is in the process of migrating the platform project to new AKS node pools with adequate compute capacity, and as part of that will provision Blob storage on the existing platform — described as free and fully self-service, with **no need to involve Vladislav Tvarůžek (STK-016) or the BDC infra team to create it**. The only possible infra dependency is a single, simple external network-access grant if Radim Švarc needs programmatic access to the storage from outside — Jura expects that to be quick if needed at all.

Once the Blob storage exists, BigHub will deploy to a **TEST environment** (not yet production — further provisioning is still needed before prod). The test environment is deliberately built to accept flexible, real-world input — zip files with nested folders, PDFs, images — matching how vendors actually submit documents today, rather than requiring a specific clean format upfront. Jura also flagged this is designed with an eye toward eventually supporting a shared-mailbox intake model later, without requiring a rebuild.

### Dr. Max-side technical review & build kickoff

Burda reviewed BigHub's technical documentation (the API contract "MDčko") — he hadn't had time to go through it in full detail yet, but what he saw looked good ("vypadá to dobře... musím říct, že to vypadá fajn"). He plans to start building on Dr. Max's side starting the next day and expects the two workstreams (BigHub's pipeline/storage work, Dr. Max's ServiceNow-side build) to proceed independently for now, syncing again once BigHub has the test environment ready.

### Vendor/supplier name-matching requirement

Michaela reiterated that extracted service-company names must exactly match the supplier list Dr. Max already sent BigHub — down to punctuation and spacing (e.g. a missing space or period in "s.r.o." would break the ServiceNow import match). Jura confirmed the extraction logic already constrains service-company, branch, and equipment-type fields to the literal text as-is (rather than a normalized/paraphrased version) for exactly this reason, and will double-check this holds consistently.

### Scope for autumn 2026 service season

Burda confirmed the current committed autumn-service scope is 2 vendors only ("Racun" and "Thermetal" — spelling per PM's supplier list should be treated as authoritative over this transcript's phonetic rendering), with no current ambition to add more. He then floated the idea of adding one additional, larger vendor (referenced only as "PEDOS" — name uncertain, possibly a mis-transcription) given inspections continue into October and smaller vendors represent modest volume (10-20 documents) compared to the current two (50-70 each). Jura said this is now relatively cheap to do — his pipeline is reusable, and processing 2 more vendors (dev + test) is roughly a day's work — and is open to it if Dr. Max sends sample documents when they have time. Not decided in this call.

### Multi-branch / multi-protocol document splitting

Confirmed working as previously agreed: a single physical document covering many branches (Burda's example: one protocol covering 30 different branches) correctly splits into one row per branch/inspection. Where a single document covers 2 devices at the same branch (e.g. two automatic doors), the system keeps this to one row with an equipment-count column rather than splitting it — splitting into separate rows only happens when they are genuinely two separate physical documents/protocols. Michaela confirmed this matches what they'd discussed and agreed in the prior (uncaptured) session.

### Dr. Max-side ServiceNow import status

Michaela reported the ServiceNow-import form/pipeline on Dr. Max's side is nearly complete: form built, links functional, tested in the test environment with bugs fixed, aside from one cosmetic non-blocking issue (a chart component built by "Wágner," BDC, STK-047, not rendering/linking correctly — described as "something extra," not core functionality). The import mechanism itself is capable of writing to the target table. She expects this deployed live this week (today is Wednesday) or, at the latest, early next week.

### Resourcing risk flagged privately by Burda (post-meeting, to Alana)

After Jura and Michaela dropped off, Burda raised a concern with Alana: the people on "Radim's side" who did the antivirus/security-review work BigHub had requested are now essentially finished with that specific ask, and risk being reassigned to other work if Burda doesn't line up a clear next task for them soon. He characterized the ball as now mainly being on Dr. Max's side and committed to prioritizing this in his own schedule, hoping to have something concrete to show by next Tuesday.

## Decisions Made

- Proceed with a TEST-environment deployment next (not production yet) — pending BigHub's Blob storage provisioning.
- Blob storage for TEST will be self-provisioned by BigHub on the existing platform, with no infra-team (BDC/Vladislav Tvarůžek) involvement needed to create it.
- Autumn 2026 service-season scope stays at 2 vendors for now; adding a 3rd, larger vendor is under consideration but not committed.
- Next joint technical sync: Tuesday next week (~2026-09-23), ~14:00 — Wednesday didn't work for Dr. Max's side this cycle.

## Action Items

- [ ] **Jura Brázdil**: Investigate the duplicated defects/findings text-field bug — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Jura Brázdil**: Root-cause the single missing-address extraction failure from the blind 2025-dataset run — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Jura Brázdil**: Investigate protocol #136's missed review flag (unflagged date error) — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Jura Brázdil**: Fix bounding-box crop alignment issues (e.g. the EPS-reference example) — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Jura Brázdil**: Migrate the platform project to new AKS node pools and provision Blob storage for the TEST environment — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Jura Brázdil**: Confirm whether Vladislav Tvarůžek's involvement is needed for Radim Švarc's external programmatic storage access, and request if so — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Tomáš Burda**: Begin Dr. Max-side build work against BigHub's API contract, starting 2026-09-17 — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Tomáš Burda**: Have something concrete on the Dr. Max-side build to show by next Tuesday (~2026-09-23) — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Michaela Albrechtová / Tomáš Burda**: Send sample documents for a possible 3rd/larger vendor ("PEDOS," name uncertain) if pursuing the expanded autumn scope — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Michaela Albrechtová**: Deploy the ServiceNow-import form to production (this week or early next week at the latest) — from 2026-09-16-teo-ocr-technical-sync-pilot-results
- [ ] **Marek Pillár / Alana Sihelská**: Confirm the correct spelling of the two pilot vendor names ("Racun"/"Thermetal" per this transcript) against the supplier list already sent — from 2026-09-16-teo-ocr-technical-sync-pilot-results

## Open Questions

- Whether "PEDOS" is a real vendor name or a transcription artifact — needs confirmation before treating it as a scope candidate.
- Root cause of the missing-address extraction failure and the protocol #136 missed-flag — both open engineering investigations.
- Whether the branch-count discrepancy (376 extracted vs. 356 actual) reflects a systematic issue or a handful of edge cases — not investigated in this call.
- Exact identity confirmation for "Michaela Albrechtová" as the Dr. Max-side speaker in this transcript (PM confirmed during routing, but the transcript itself never states her name directly).
- Whether Radim Švarc's team being "essentially done" and at reassignment risk should be escalated further, or is being adequately handled by Burda's own internal prioritization.

## Sentiment & Tone

Collegial, technical, and detail-oriented — this reads as a working engineering sync rather than a business/relationship conversation. Burda and Michaela both engaged substantively with the extraction results (not passively accepting a demo), catching two real bugs and pushing back gently on Jura's framing of certain review flags as necessary. No friction; Burda's closing remark about keeping Radim's team resourced reads as proactive relationship management on Dr. Max's side, not a complaint. Slight uncertainty at the very start about whether "pan Vorda" [likely Tomáš Burda in Alana's initial framing] would join at all — resolved positively once the meeting got going.

## Routing Log

- **project-knowledge**: TEO/OCR entry updated with blind real-world validation results (accuracy, bugs found) and delivery progress (self-provisioned storage, TEST environment, Dr. Max-side build kickoff, vendor-scope discussion, SNOW-import status).
- **project-assumptions**: Added ASM-088 (Decided — TEST-environment Blob storage self-provisioned, no BDC dependency) and ASM-089 (Open — whether to add a 3rd autumn-scope vendor).
- **project-stakeholders**: Enriched STK-025 (Tomáš Burda), STK-026 (Jura Brázdil), STK-004 (Alana Sihelská), STK-042 (Michaela Albrechtová — identity confirmed by PM), STK-047 ("Wágner").
- **project-daily**: 11 action items added to 2026-09-16.
- **meeting-index**: Entry added.
