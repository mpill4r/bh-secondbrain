---
last_updated: 2026-09-07
type: internal
attendees: [Marek Pillár, Jindřich Tůma, Jura Brázdil, Filip Černý, Jakub Turner, Lukáš Starenko, Juraj Kmec]
tldv_link:
---

# AI Portfolio & Roadmap Scope Review

**Date**: 2026-09-07
**Attendees**: Marek Pillár (Product/PM, drove the review), Jindřich Tůma (PM, opening framing only — left before the second half), Jura Brázdil (Dev — MaxBuddy, Max Chatbot, Maxie, TEO), Filip Černý (Dev — Reklamace, Fakturace doprav, Listing), Jakub Turner (Dev — Reklamace, Fakturace doprav, part 1 only), Lukáš Starenko (Dev — Reklamace document generation, part 1 only), Juraj Kmec (Data Scientist — Řízení poptávky)
**Type**: internal
**Recording**: N/A (transcript provided as two parts, no tldv link)
**Previous session**: N/A — new thread
**Meeting prep**: N/A

## TL;DR

Marek and Jindřich walked the dev team line-by-line through the newly-assembled AI portfolio/roadmap spreadsheet (sourced from Jindřich's GitHub export, Max/Maxie specs, and Honza Sovka's notes) to validate phase (MVP/Full Version/Backlog) and status for every initiative — MaxBuddy, Max Chatbot, Maxie, Lexie, Reklamace, Fakturace doprav, Řízení poptávky, Listing, and TEO — ahead of presenting a consolidated roadmap this week. Several duplicate tracker rows were identified for removal, two new blockers surfaced (Dr. Max's poor product-variant data for Listing; Dr. Max not yet defining a supplier-instructions knowledge base for Reklamace), and domain experts/business owners were confirmed per initiative to close out remaining open questions. Jindřich stepped out partway through for another meeting; Marek continued the review solo with Juraj Kmec, Filip Černý, and Jura Brázdil.

## Key Discussion Points

### Process framing (Jindřich Tůma, opening)

Two-part plan going forward: (1) stand up a proper Kanban tool (Jira or Azure DevOps, test environment being set up on Max's side) — one board per project, weekly-ish status cadence, single source of truth for what's being worked on and what's blocked; (2) hold the client to the *originally specified* first-version scope rather than scope-creeping mid-project — deliver a "starting version," then scale via releases. Today's review exists because the original specs were split across multiple people (Alana, Honza Sovka) who aren't fully available now, so the team needs to jointly re-validate what each project's spec actually said before a timeline/estimate can be built.

### MaxBuddy (Jura Brázdil)

Live in Farmis for ~1 year. Core complexní péče (complex-care) recommendation flow is fully integrated, but only ever uses four data points: fixed supplier-defined cross-sell pairs, supplier-authored argument text, live stock data, and active ingredient (for e-recept cases with no specific product). The real ceiling on this feature isn't technical — **Dr. Max has never granted access to actual sales/margin data**, so MaxBuddy can't learn from what actually converts; Jura has asked repeatedly. Early analytics (still being sanity-checked) show a striking adoption gap: the most-recommended product was shown ~18,000 times but purchased only 6 times, and complexní péče "tiles" get almost no clicks since being tucked behind a UI element in the last release — likely needs pharmacist training/adoption work, not just model tuning.

Rows 12–17 (dosage calculation, verification, traffic-light display, etc.) are **fully blocked** on Dr. Max's own decision on whether to pursue medical-device certification — Jura flagged that if/when that happens, BigHub will likely also need to prepare the codebase for an audit (logging, auditability). Full 600-pharmacy rollout is blocked on the new AKS environment; Jura's pessimistic estimate is ~1 month of work after Vláďa grants access, likely faster. Canary rollout plan (20 pilot pharmacies first) already matches the confirmed MVP scope. No other backlog beyond full rollout — a live-data dashboard integration was BigHub's own idea, not something Dr. Max asked for, and stays backlog.

### Max Chatbot & Maxie (Jura Brázdil)

Core scenarios (pharmacy hours, order status, e-recept reading) are live, but currently wired to **Dr. Max's public website API — scraped, not an official integration**. Jura flagged this as a real risk before a full public launch (no guarantee it won't silently drift/break) and recommends switching to an officially-provided integration first. Reklamace/return flows for the chatbot haven't been scoped with Dr. Max at all yet. FAQ isn't implemented — trivial once infra is unblocked. Product recommendations work but don't use Dr. Max's actual on-site algorithm (no access granted). WhatsApp/Messenger and discount-code generation are backlog, undiscussed with the client.

Maxie shares the same LLM core/prompting as the chatbot, differing only by channel (voice/IVR vs. web chat) — confirmed by Jura as intentional, not incidental overlap. Historically blocked on Eleven Labs public-exposure infra (Honza Zelený's area), believed close to resolved. Dr. Max today runs a fixed decision-tree IVR and plans to replace branches with the dynamic LLM version one at a time — which branch goes first is still their call.

### Lexie (brief, Viliam Gago not present)

Essentially all requirements accounted for; currently in testing. Viliam (on vacation, back ~Tuesday) shipped ~5 ticket fixes Friday — action for Marek/Jindřich to notify the Dr. Max CC team to retest.

### Reklamace (Filip Černý, Jakub Turner, Lukáš Starenko)

MS-label and SP-label flows: done, demoed Thursday. Photo documentation: mostly done, missing the supplier-specific instructions knowledge base — **data not yet provided by Dr. Max** (Tereza was expected to deliver it today; Filip believes this has already been discussed with them across 2–3 status calls, contrary to Marek's initial read that it was uncommunicated). Axapta case creation + photo-linking: confirmed working, tested with Kopecký. Document generation (Lukáš Starenko): functionally done, mid-decision on sync-vs-async architecture for returning a link to the generated file. Draft email to supplier: in development (Jakub). Auto-send email: not started, tied to the draft-email item, unclear whether it's MVP or a later "phase 1.1." Warehouse (skladové) reklamace: **real OCR for handwritten labels doesn't exist yet** — what's been built so far is barcode scanning, not OCR; flagged as new, nontrivial backlog work. Error-state handling: partially covered — Filip will self-audit against the original spec and consolidate gaps as feature requests if the client raises them. Two-way Axapta integration: done, tested. Currently only deployed to test — handoff to Tereza Foltová and (name uncertain in transcript) "Egermajerová" for review this week; full production still pending.

Two structural findings: the "3 UCs" dev-infra/fileshare tracker item is stale/unneeded (document sharing is already solved via Azure Blob Storage, not a literal fileshare — naming confusion from an older note) and should be dropped or rewritten; several tracker rows (email doc generation, O365 integration, "dosud vyvinutých funkcí") are duplicates of already-tracked items and were marked for removal. Jakub Turner flagged that **logging/monitoring/alerting is a genuine gap** — currently logs only inside the AKS container with no cross-project convention yet; needs solving before general release.

### Fakturace doprav (Filip Černý, Jakub Turner)

Overall still early — "chybí toho jako milion" (a ton is still missing) — and Dr. Max hasn't seen much of it yet. Filip wants to sync with them for a first feedback round. Digitalizace podkladů: not done, currently manual file upload only, no scanner integration. Document-type processing: done except temperature-logger data (next phase) and GPS (later phase, handled Axapta-side). Completeness check: done. Km/data validation: BigHub just forwards scanned km, Axapta does the actual comparison — confirmed done on BigHub's side; temperature-log correctness explicitly **not** MVP. Axapta record creation: blocked — Dr. Max hasn't built their side yet; BigHub is ready. Driver confirmation: not started, Filip's own backlog. Deviation flagging: effectively done (Axapta owns the decision, BigHub just relays data).

### Řízení poptávky / order-prediction dashboard (Juraj Kmec)

Virtual warehouse dashboard: functionally working, in review with Marek Šimoník — expect polish requests as usage continues, first reaction positive. Minor "unresolved orders %" display bug traced to a client-side data-sync issue, not the model — low priority. ML forecasting model: working, still validating; Christmas prediction quality is a known open risk since the training data has no prior Christmas season. Historical reference lines (last week/last year overlay): backlog — technically feasible but nontrivial, and blocked in part on a fresh campaign-data export from Petr Ondráček (current export ~2 months stale). Campaign recommendation model and automated campaign generation: discussed as potentially **Full Version**, but Juraj was explicit these are genuinely hard analytics problems in their own right — "automated campaign generation" as the client described it (fully autonomous Christmas-campaign creation) isn't realistic as scoped; no firm phase call was made, both stay Nice to Have/Backlog until a proper scoping conversation happens, more likely an optimizer/recommender than true automation.

Data sources: mostly connected — Dr. Max's data warehouse plus Blob storage for predictions/processed data; Order Service now flows through DataHub rather than a direct connection (architecture clarification, not a gap). Confirmed done, no other known sources pending. Dev-infra "3 UCs" item: same stale framing as Reklamace's — can be deleted. Production deployment: **technically live already**, but the *test* environment is currently undersized on the old AKS node pool and throwing out-of-memory errors — production itself runs fine; waiting on the new AKS to fix test capacity.

### Listing (Filip Černý)

Content generation, search/filter parameter recommendations, missing-data identification, and the draft-generate/edit/approve flow: all done. Category/structure recommendation: **not done, and Filip flagged this was likely never actually agreed as in-scope** — it depends on Dr. Max's own messy/unspecific category system, which isn't BigHub's to fix; proposal is to leave it out and treat any future ask as a feature/change request rather than a gap. External-source enrichment (scraping sites like Notino): mostly built technically but **paused before broader test rollout over legal uncertainty** around scraping — may need an official API or middleman instead. Magento write-back: not done — blocked because Dr. Max hasn't specified how they want data imported (Excel upload? DB writes?); closer to backlog than blocker since it's roughly half a day of work once the method is defined, but Dr. Max hasn't prioritized answering. Confirmed Phase 2 / Full Version: listing net-new products (vs. just improving existing ones).

Two new items surfaced: (1) **product-variant data quality** — Dr. Max's own variant data is poor, blocking a planned "variant system update" feature, waiting on them; (2) **multi-category support** — the current demo is hard-coded to one category; real scope could span roughly 500–2,000+ categories depending on how granular Dr. Max wants listing rules, entirely open and Dr. Max's call. Proposed rollout approach (Petr Neuman's suggestion): start with a deliberately small, non-pharma category set (foods, supplements, sporting goods) rather than a large/complex one, to avoid skewing early AI output.

### TEO (Jura Brázdil)

Clarified: **TEO is a Dr. Max department name** (technical department), not a project acronym — Jura had been calling this the "OCR project" informally. The work is OCR of technical-department revision/repair protocol documents. Still a local prototype on Jura's own machine, feasibility-testing stage, not deployed anywhere. Deliberately piloted on just 2 suppliers/document formats first for more uniform inputs before considering expansion. 5 fixed columns extract reliably; 3 more fields are open-ended, often handwritten "findings" text — harder, in progress, overall success rate still unknown. The sample Excel Dr. Max provided as a template didn't even match their real input data. Document volume isn't an issue — multi-protocol PDFs are already auto-split; handwriting vs. printed text is the real difficulty. No shared storage/service exists yet to deliver extracted data to — currently framed as Dr. Max's responsibility to build, not a BigHub blocker. ServiceNow export/import and the "upcoming revisions" query-back feature: not started, tentatively Full Version, also blocked on Dr. Max sharing asset/location data BigHub has no way to know today.

**Cross-project synergy surfaced live**: Filip Černý noted TEO's mixed printed/handwritten/checkbox document problem closely resembles Fakturace doprav's document-extraction problem — he and Jura agreed to a short knowledge-sharing session comparing approaches.

### Domain experts / stakeholders confirmed

- **Overall roadmap sign-off**: Honza Sovka (Alana also worked on the original specs and may have context)
- **Řízení poptávky**: Marek Šimoník (e-commerce) + Petr Ondráček (logistics/warehouse) — both attended the original scoping meeting
- **Listing**: Petr Neuman — Jindřich has already promised him a discovery session
- **Reklamace**: Petr Sláma ("manažer"-type) and Jan Kopecký (technical) as primary contacts; a BDC-side technical contact referred to as "Kopčík"/Zábojník (not directly Dr. Max, unconfirmed employment status); Tereza Foltová and a name transcribed as "Egermajerová" as the actual business/end users
- **Fakturace od dodavatelů**: Jan Žižka — works with "Honza," seniority/hierarchy unclear, Filip has never spoken with him directly; area described as still "in diapers" (very early)
- **Max Chatbot / Maxie**: Simona Mertová — also files most X-Manager tickets; multiple other people involved too
- **Lexie**: covered by the same Max/Maxie/Lexie CC-team contacts, no separate list needed
- **TEO**: Radim Švarc + Michaela Albrechtová

## Decisions Made

- MaxBuddy's MVP scope is finalized at the 20-pharmacy pilot; rows 12–17 (dosage-calc features) stay formally blocked pending Dr. Max's medical-device certification decision.
- Max Chatbot and Maxie share one LLM core/prompt engine, differing only by channel — confirmed intentional shared architecture.
- Campaign recommendation model and automated campaign generation (Řízení poptávky) were discussed as potentially Full Version, but no firm phase call was made — Juraj flagged both as genuinely hard analytics problems needing their own scoping conversation first; they stay Nice to Have/Backlog until that happens.
- Listing's category/structure recommendation is confirmed out of agreed scope — treated as a future feature request, not a tracked gap.
- Listing category rollout will start with a small, non-pharma category set rather than a large/complex one.
- Several duplicate tracker rows (Reklamace: email doc generation, O365 integration, "dosud vyvinutých funkcí"; both Reklamace and Řízení poptávky: stale "3 UCs" dev-infra/fileshare items) are marked for removal from the roadmap.
- TEO is understood as the Dr. Max department name behind the OCR-protocols project, piloted deliberately on 2 suppliers first.

## Action Items

- [ ] **Jura Brázdil**: Send the cleaned-up MaxBuddy analytics deck to Luboš Vosmek — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Marek Pillár / Jindřich Tůma**: Notify the Dr. Max CC team to retest Lexie after Viliam's Friday fixes — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Filip Černý**: Self-audit Reklamace error-state handling against the original spec and consolidate gaps — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Marek Pillár / Jindřich Tůma**: Email Petr Ondráček directly for a fresh campaign/promo data export (current one ~2 months stale) — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Filip Černý**: Sync with Dr. Max on Fakturace doprav for a first feedback round — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Filip Černý / Jura Brázdil**: Hold a short knowledge-sharing session comparing TEO's and Fakturace doprav's document-extraction approaches — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Marek Pillár / Jindřich Tůma**: Route the finished roadmap to Honza Sovka for sign-off — from 2026-09-07-ai-portfolio-roadmap-scope-review
- [ ] **Jakub Turner**: Define a cross-project logging/monitoring/alerting convention (currently AKS-container-only) — from 2026-09-07-ai-portfolio-roadmap-scope-review

## Open Questions

- Reklamace/Fakturace od dodavatelů stakeholder hierarchy is unclear — Petr Sláma, Jan Kopecký, and Jan Žižka's actual seniority/reporting lines are unconfirmed.
- Whether the auto-send-supplier-email item for Reklamace is MVP or a later "phase 1.1" is still undecided.
- Listing's target category count and rollout granularity (roughly 500–2,000+) is entirely open, pending Dr. Max.
- Legal status of external-source scraping (e.g. Notino) for Listing enrichment is unresolved — may need an official API/middleman instead.

## Sentiment & Tone

Productive, working-session tone throughout — a genuine line-by-line validation rather than a status theater exercise. The dev team pushed back constructively where the pre-filled tracker didn't match reality (Filip on Listing's category-recommendation scope, Jura on MaxBuddy's data-access ceiling, several duplicate-row callouts), and Marek/Jindřich took the corrections without friction. A recurring undertone across nearly every project: **BigHub is frequently blocked waiting on Dr. Max** — for supplier data, category definitions, variant data, asset/location data, or simply a decision — more so than on BigHub's own execution. Team energy stayed high through a long (~90+ min combined) session; Jindřich apologized for stepping out early, and the meeting closed warmly ("moc se omlouvám za to dlouhý mitting, ale pomohlo to").

## Routing Log

Confirmed 2026-09-07 (all items). Written:
- **project-stakeholders**: added STK-041 (Radim Švarc), STK-042 (Michaela Albrechtová), STK-043 ("Kopčík"/Zábojník, low-confidence), STK-044 ("Egermajerová", low-confidence); enriched STK-034 (Petr Sláma), STK-015 (Jan Žižka), STK-002 (Jan Sovka)
- **project-assumptions**: ASM-027 (MaxBuddy AKS rollout blocker), ASM-028 (MaxBuddy certification blocker), ASM-029 (Max Chatbot/Maxie unofficial-API risk), ASM-030 (Řízení poptávky campaign items, no firm phase), ASM-031 (Listing category/structure out of scope), ASM-032 (Listing category rollout sequencing), ASM-033 (Listing scraping legal risk), ASM-034 (TEO 2-supplier pilot), ASM-035 (TEO/Fakturace doprav synergy)
- **project-knowledge**: updated MaxBuddy, Max/Maxie/Lexie, TEO/OCR (renamed from "OCR"), Order-Prediction Dashboard entries; added new Reklamace OCR-vs-barcode entry
- **project-daily** (2026-09-07): all 8 action items from this meeting written to Action Items
