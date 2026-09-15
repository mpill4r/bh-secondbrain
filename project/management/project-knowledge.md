---
last_updated: 2026-09-15
last_updated_by: auto — project-meeting routing
owner: Marek Pillár
---

# Project Knowledge

## Domain Terminology

### Second Brain

| Field | Value |
|-------|-------|
| Definition | This harness instance — a personal knowledge system for Marek's thoughts, ideas, and todos, not a commercial product |
| Source | PM input (project-initiation) |
| Added | 2026-09-01 |
| Status | Active |

## Client Jargon

> No formal client for Second Brain itself. Entries below are Dr. Max/BigHub account terminology that surfaces through Marek's day-job content — kept here since that's where project-specific jargon belongs in this template.

### MaxBuddy

| Field | Value |
|-------|-------|
| Definition | BigHub-built product for Dr. Max pharmacies. Originally a pharmacist dosage-verification assistant (pulled after legal flagged it as requiring medical device certification); the surviving, shipped feature is AI-driven point-of-sale cross-sell ("psí prodeje" — upsell suggestions) generated from basket contents, rolling out to all ~600 Dr. Max pharmacies. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-07-ai-portfolio-roadmap-scope-review |
| Added | 2026-09-01 |
| Last updated | 2026-09-07 |
| Status | Active |

The dosage-verification logic still exists dormant in the codebase and could be revived if Dr. Max later pursues certification.

**Regulatory detail (2026-09-03)**: the dosage-checking feature was meant to flag outdated dosing against the latest SPC (package leaflet) guidance — motivated by legislation shifting dosing-error liability onto prescribing doctors. ~6 months into development, this was found to make the product a regulated medical device requiring certification: any pipeline where patient data goes in and an LLM-derived recommendation comes out is prohibited without it ("no blackbox: patient data in, drug advice out"). Pivoted instead to upsell/cross-sell recommendations, which combine pharmacological knowledge but are reviewed and approved by an expert panel rather than generated per-patient by an LLM. BigHub is separately pushing (with SOS support) for anonymized receipt-data access to base upsell recommendations on actual purchase patterns — permitted, since anonymized data carries no patient-specific medical inference. This same "display official content, never generate medical advice" pattern was reused for the Max chatbot's SPC-leaflet guardrail — see [[ASM-020]].

A related, already-running system: SPC-change monitoring, collecting periodic diffs to drug package leaflets (running ~2 months as of 2026-09-03). ~99% of changes are noise (phrasing/formatting/grammar); dosage-paragraph changes are flagged critical. An AI re-sorting pass is planned before results are shared with Dr. Max, since signal-to-noise isn't good enough yet.

**Deployment strategy (2026-09-03)**: MaxBuddy runs on 30 of ~600 pharmacies. Dr. Max originally wanted full rollout within 14 days; Jura Brázdil determined this was unsafe (best case, MaxBuddy crashes; worst case, it takes down the pharmacies' payroll/POS system) given no adequate 1:1 test environment (single e-recept item only, ~16s DB response time). This triggered the AKS infrastructure effort started in July. Rollout plan: the same ~20-30 pilot pharmacies (chosen for younger, more technically flexible pharmacists) serve as a permanent canary environment — new versions validated there live first, then rolled to the remaining ~580.

**Platform consolidation**: MaxBuddy started standalone. Once the new AKS sandbox is live, Jura Brázdil takes over the shared AI platform (built by Viliam Gago, STK-027) and migrates MaxBuddy onto it alongside the Max chatbot and Lexie.

Original infrastructure/model provisioning for MaxBuddy was done manually (ad hoc clicking), not via Terraform or other IaC tooling — surfaced 2026-09-02 when checking whether a redeployment was possible. No structured infra-as-code state exists for it; the people most involved in the original setup are no longer easily reachable, and exact names are uncertain due to transcription quality (see 2026-09-02-aks-atlantis-infra-sync). Consensus was to leave it alone since it currently works.

**2026-09-07 portfolio review**: the recommendation engine's real ceiling isn't technical — Dr. Max has never granted access to actual sales/margin data, so it can only use 4 data points (fixed supplier-defined cross-sell pairs, supplier argument text, live stock, active ingredient). Early analytics (still being sanity-checked before going to Luboš Vosmek, STK-011) show a striking adoption gap: the most-recommended product was shown ~18,000 times but purchased only 6 times, and komplexní péče "tiles" get almost no clicks since being tucked behind a UI element in the last release — likely needs pharmacist training/adoption work, not just model tuning. Full 600-pharmacy rollout blocked on new AKS access, ~1 month pessimistic estimate post-grant — see [[ASM-027]]. Dosage-calc features stay blocked pending Dr. Max's certification decision — see [[ASM-028]].

### Max / Maxie / Lexie

| Field | Value |
|-------|-------|
| Definition | Three BigHub-built chatbot/assistant products for Dr. Max, owned business-side by paní Mertová (STK-017), co-owned with Tomáš Dudaško (STK-010, IT/budget side). **Max** is the customer-facing chatbot embedded on the drmax.cz website (order status, pharmacy locator, e-recepty, medication/stock lookup — see full flow below); a **voice channel of the same capability is Maxie**, launching scoped to order-status only via IVR. **Lexie (Lucie)** is the internal knowledge-base assistant being rolled out to IT, Legal, and Brno accounting, now in Call Center testing — currently blocked on 3 bugs, see below. Distinct from MaxBuddy (the pharmacy point-of-sale cross-sell product) — corrected 2026-09-03; an earlier entry incorrectly described Max as "Call Center-facing." |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-10-lexie-max-maxie-weekly-sync |
| Added | 2026-09-01 |
| Last updated | 2026-09-10 |
| Status | Active |

**Important scope correction (2026-09-04)**: the underlying AI platform (chatbot + RAG infrastructure) is **shared BigHub infrastructure reused across multiple clients**, not Dr. Max-exclusive — also deployed for Brněnská komunikace (Brno communications), with variants in progress for Kooperativa (accounting) and Unica (legal). Dr. Max is one deployment of a centralized "core" platform/repo, not a bespoke build. Frontend direction: one standardized template by default, custom per client only on explicit request — see [[ASM-025]]. Whether Honza Sovka retains product ownership of the platform across all clients (vs. Marek owning Dr. Max only) is unresolved — see [[ASM-026]].

**Max chatbot (2026-09-03)**: demoed live to strong Dr. Max reception. Four button-driven functions plus free-text LLM chat: order status (order number + email, or number alone with auto-detection, returns tracking link); pharmacy locator (by device location or city, shows hours/route/call button); e-recepty (handles prescribed/not-yet-issued, multi-item, already-issued, and expired states); medication/stock lookup (searches Dr. Max's public API, AI-reranks variants by form rather than pack size, checks live stock across 561 pharmacies). Refuses medical-advice questions (e.g. dosing safety), redirecting instead to the official SPC leaflet via the same API built for MaxBuddy — see [[ASM-020]]. Has a working usage-analytics dashboard (currently synthetic data pre-launch). Deployment: staged rollout via a public/testing version-switch mechanism (URL param or config flag), allowing fast, low-risk version releases without a full redeploy.

**Lexie (Lucie) — blocked on 3 bugs (2026-09-03)**: (1) feedback button broken specifically on long/large responses, confirmed reproducible; (2) autocomplete/suggestion popup ("našeptávač") to be removed entirely — pops up unpredictably, including mid-response, obscuring the answer an operator is relaying; (3) configurable fixed/canned status messages needed outside the prompt, for outage-style announcements. GPT model upgraded 5.1→5.4 on 2026-09-02 by Viliam Gago. All Lexie work paused until fixed — see [[ASM-021]].

**Lexie ticket triage (2026-09-04)**: root cause found for the feedback-button bug — thumbs aren't real buttons, they sit on an action area overlapped by the "regenerate response" control on long messages, so double-clicking selects text instead. Viliam Gago fixing same-day, alongside the status-announcement banner (admin-editable, not auto-detected) and a response-links fix already in test. Two other tickets: document-rename-not-reflecting-in-Lexie (indexer lag vs. a possible diacritics issue, unresolved) and test-user creation (auth architecture unresolved — 2FA on real Dr. Max accounts makes ad hoc role-testing painful; punted to Lukáš Szücs). A "Product Scope" ticket (Kateřina Kadlecová's MVP/roadmap ask) is now owned by Marek. RAG mechanics confirmed: Lexie indexes Dr. Max's SharePoint periodically via an embedding pipeline into a vector DB, with clickable source citations.

**Lexie ticket triage (2026-09-10)**: of the original 3 blockers, the feedback-button bug is confirmed fixed and testing has resumed — see [[ASM-058]]. Configurable fixed/canned status messages are in progress as ticket 150 ("ready for dev"), which surfaced a new permission-scope error ("cesty mimo působnost vašeho oddělení nelze nastavit") already logged with a screenshot. Našeptávač removal is now tracked as its own dedicated, higher-priority ticket, still outstanding. Document-rename-not-reflecting-in-Lexie is still untested by the client as of this date. The X-Manager Kanban view (grouped by scope: MVP/Full Version/Nice to Have, with a hide-empty-columns toggle) was confirmed as satisfying the client's standing roadmap-visibility ask — see [[ASM-059]].

**Lexie design gap (2026-09-10)**: Mertová flagged Lexie looks noticeably less polished than the newer Max chatbot. Design authority sits one level up at the AI-platform level (owned by Tomáš Dudaško) — an individual app can't diverge from the platform's eventual unified design without risking rework. BigHub is centralizing all Dr. Max apps under one platform entry point first; per-app design cascades down from that once agreed. Near-term: a bounded design-compromise ticket for Lexie, not a full redesign — see [[ASM-060]].

**Lexie test-account mechanics (2026-09-10)**: permissions are controlled entirely by Dr. Max's own Entra ID groups (max.bt.cz), not configurable by BigHub. For role-based testing across Lexie's 4 CC sub-departments (call centre agent, back office agent, testing, and a fourth — each needing a distinct document-access scope), two technical options were identified: (A) 4 separate accounts requiring logout/login to switch, or (B) 1 account in all relevant Entra groups with an in-app role switcher BigHub would build. Dr. Max prefers option B, but a single account in every group simultaneously doesn't actually exercise real role-restriction behavior, and whether multiple concurrent testers sharing one account would conflict is unresolved — see [[ASM-063]].

**Maxie (voicebot, 2026-09-03)**: built by Honza Zelený (STK-029), sharing infrastructure with the Max chatbot. Technical blocker (missing SIP trunk) resolved via an Atlantis meeting the prior Thursday; a request list is with Dr. Max's BDC infra team (contact: Vladislav Tvarůžek, STK-016), prioritized after the new AKS work — targeting ~14 days to technical readiness. Scope starts at order-status only via a fixed IVR branch, expanding as Dr. Max's IVR is updated — see [[ASM-022]].

**Process notes**: all three products' X-Manager feature requests should route through Simona Mertová as single point of contact — see [[ASM-018]]. Production-readiness bar is functional correctness against agreed scope, not full polish — see [[ASM-019]]. In-chat feedback mechanism (Max) is a star/emoji rating, no free text — see [[ASM-017]].

**2026-09-07 portfolio review**: confirmed Max and Maxie run on one shared LLM core/prompt engine, differing only by channel (web chat UI vs. voice/IVR) — intentional shared architecture, not incidental overlap. Max's production integration currently runs on Dr. Max's public website API, scraped rather than officially provided — flagged as a risk before a full public launch, see [[ASM-029]]. Maxie today mirrors 3 of the chatbot's core scenarios (hours, order status, e-recept); reklamace/return flows aren't built yet, shared build with the chatbot once done. Dr. Max runs its own fixed decision-tree IVR today and plans to replace branches with the dynamic LLM version one at a time — which branch goes first is Dr. Max's call, not yet decided.

### TEO / OCR (pharmacy service-protocol extraction)

| Field | Value |
|-------|-------|
| Definition | **TEO is Dr. Max's technical department** (not a project acronym — clarified 2026-09-07, Jura had been calling this the "OCR project" informally). The project itself is a BigHub effort (owner: Jura Brázdil) automating extraction from TEO's mandatory pharmacy equipment service-inspection/revision-repair protocols (automatic doors, air conditioning, etc.) — currently manually retyped into Excel by staff. "OCR" is a working name, not literally OCR-only — the pipeline is LLM-based extraction over scanned/photographed, often handwritten, documents. |
| Source | 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-15-business-quantification-teo-ocr |
| Added | 2026-09-03 |
| Last updated | 2026-09-15 |
| Status | Active |

Scope narrowed to one category first: automatic doors, two vendors — extracting door type, faults, branch address, and follow-up requests via a ~16-prompt pipeline. Currently in a second feasibility-measurement round (first round handled cleanly-extractable data; second tackles free-text notes). Target: production-ready for Dr. Max's November inspection cycle. Will move onto the shared AI platform (alongside MaxBuddy, Max, Lexie) once the new AKS sandbox is available.

**2026-09-07 portfolio review**: the "not yet present in the roadmap tracker" gap flagged 2026-09-03 is now resolved — added as the TEO_OCR sheet + a Portfolio entry. Status as of this review: still a local feasibility prototype on Jura's machine, not deployed anywhere; deliberately piloted on 2 suppliers/document formats for uniform inputs before expanding — see [[ASM-034]] (possibly the same underlying scope as the automatic-doors/two-vendor framing above, generalized in description — not confirmed either way). 5 fixed columns extract reliably; 3 more fields are open-ended, often handwritten "findings" text — harder, success rate still unknown. No shared storage/service exists yet to deliver extracted data to — currently framed as Dr. Max's responsibility to build. ServiceNow export/import and query-back features not started, tentatively Full Version, blocked on Dr. Max sharing asset/location data. New contacts: Radim Švarc (STK-041, building his own app that will call BigHub's OCR API directly — integration boundary still undefined) and Michaela Albrechtová (STK-042). Cross-project synergy identified with Fakturace doprav's similar mixed-format document problem — see [[ASM-035]].

**Ownership (2026-09-15)**: Business owner is Tomáš Burda (STK-025), head of the technical department — his "TD revisions" roadmap entry plausibly refers to this same initiative, pending his own confirmation. Radim Švarc (STK-041) is the domain expert/daily working contact, not the owner.

**Business value & volume (2026-09-15, Business Quantification interview + Dr. Max's own technical presentation)**: External service vendors perform inspections at pharmacies and email scanned PDF service documents (no OCR layer) to Dr. Max's technical department — a single document can contain up to ~100 individual inspections. A technician manually reads and transcribes: cost-center/branch number, address, date, equipment type/count, order number, service company, and technician-written defect notes — then manually re-enters all of it into ServiceNow. Volume: ~250 documents/week (seasonal — higher in autumn during door/climate-control service season, lower in summer, averaging out annually). Time cost: ~40 hours (~5 MD) per month, sourced from a prior estimate Radim had given to Lukáš Síč, cross-checked against a historical sample of protocols on a network drive. Per-MD/hourly cost rate not yet available — Tomáš Burda to provide; an ~3 000 Kč/day figure from the logistics quantification was referenced only as an illustrative placeholder, not a TEO-specific rate.

**Proposed automated architecture (Dr. Max's own presentation, 2026-09-15)**: vendors redirect documents to a dedicated intake email (example: `revize@drmax.cz`) or a shared network drive; an automated service (proposed: Microsoft PowerAutomate) captures emails and saves attachments; files are sent to an AI extraction tool via API (proposed stack: Python orchestration + BigHub's internal model, or Claude directly); extracted data populates a shared Excel with uncertain/mismatched fields flagged for review; the technician checks the Excel before ServiceNow import, either manually (mechanism being prepared by a BDC contact, "Wágner" — STK-047, low-confidence) or via simulated-click automation (undecided). Notably, Dr. Max's own team already tested **Claude directly against a 100-page sample document**, successfully producing a full row-level extraction with uncertain rows flagged — informal client-side validation ahead of any formal BigHub pipeline. The presentation closes with a direct, unanswered question to BigHub: is this pipeline feasible, and what's a realistic delivery timeline? See `documents/client/2026-09-15-teo-ocr-technical-process-presentation.md`.

**KPI framing (2026-09-15, open)**: Marek proposed an example time/FTE-saved KPI (~80 hours saved within 3 months ≈ half an FTE); Radim pushed back, preferring a document-count/correction-rate metric (share of imported documents read correctly with no manual correction needed) as a better proxy for real impact — not yet finalized.

### Reklamace (claims) — business objective & phasing

| Field | Value |
|-------|-------|
| Definition | Business origin and quantification for the Reklamace initiative, captured via the Business Quantification interview format. Today's process is paper-heavy and fragmented: separate systems that don't automatically communicate, staff photographing claim evidence to WhatsApp and manually forwarding it, and per-warehouse/per-person knowledge scattered across personal Excel sheets and notebooks with no shared source of truth — flagged originally by an external audit (Ableneo). The goal is not primarily error reduction (staff know the repetitive process well) but reducing the friction/cognitive load of a fragmented manual flow. |
| Source | 2026-09-15-business-quantification-reklamace-fakturace-doprav |
| Added | 2026-09-15 |
| Status | Active |

**Owner**: Petr Spilka (STK-014), tentatively also domain expert — Jana Egrmaierová (STK-044) floated as a possible alternative, unconfirmed.

**Business value (Fermi estimate, unconfirmed)**: ~4 people × ~2 hours/day saved ≈ 1 FTE. A wage-cost figure (~3000, unit/currency unclear from the source transcript) was mentioned but needs verification with Petr Spilka.

**KPIs**: Primary — end-to-end process time (baseline needed pre-launch, no existing measurement tool today; target threshold not cleanly settled between "50% faster" and "~25% faster"). Secondary — post-launch (≥3 months) satisfaction survey, ~66% target (majority of a 6-7 person sample). Document/claim error rate was explicitly discussed and rejected as a KPI — see [[ASM-072]].

**Phasing**: Ships in 5 phases (0 through 4/5); the full ~1 FTE saving only materializes once all phases are live — see [[ASM-072]]. Documentation should label phases explicitly (e.g. Phase 0 = Příprava/preparation, Phase 1 = příjmové reklamace/receiving claims) since staff currently confuse "příjmové" (receiving) vs. "dodavatelské" (supplier) claim types.

### Reklamace "OCR" (SP/MS štítky)

| Field | Value |
|-------|-------|
| Definition | What's built today for Reklamace's SP/MS label flows is **barcode scanning, not OCR** — reading a printed barcode down to an identifying number. Real OCR (reading handwritten batch/expiry text) is a separate, unbuilt need for the warehouse (skladové) reklamace flow, where labels carry handwritten batch/expiry information rather than a scannable code. |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| Added | 2026-09-07 |
| Status | Active |

Naming confusion source: Honza's original spec notes used "OCR" loosely for both, which is why the roadmap tracker initially conflated them. Tracked separately now — see the '"Opravdový" OCR' (real OCR) backlog row on the Reklamace roadmap sheet.

### Fakturace doprav (freight invoicing) document types

| Field | Value |
|-------|-------|
| Definition | Document types the Fakturace doprav kiosk portal classifies and extracts per delivery route ("trasa," identified by an AR number): **ZOPV** ("záznam o provozu vozidla," vehicle-operation record — driver name, plate, delivery date, kilometers driven, typically the richest data source); **rozvozový list** (delivery/route list, usually multi-page); **noční závoz** (night-delivery confirmation, can have multiple per route); **OPIATY** (narcotic-substance handover document); **POPLSOL** (a warehouse-transfer document — only needs matching to the correct route, no further data extraction). |
| Source | 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| Added | 2026-09-10 |
| Status | Active |

Documents are classified primarily by barcode where present; barcodes aren't guaranteed on every document (per Petr Sláma), but a computer-printed AR number always is — handwritten-only AR numbers are treated as unacceptable input. ViaPharma is independently building a new standardized, pre-filled ZOPV form (with Petr Sláma's team) that should eliminate most illegible-handwriting cases at the source, leaving only kilometers driven as a manual field (drivers are paid by distance, which can vary from the fixed route distance).

### Fakturace doprav — business objective & KPIs

| Field | Value |
|-------|-------|
| Definition | Business origin and quantification for Fakturace doprav, captured via the Business Quantification interview format on 2026-09-15 — where it appeared on the roadmap tracker under the generic label "fakturace od dodavatelů" (see [[ASM-006]] for the naming disambiguation). Today's process places a heavy manual burden on transport/logistics office staff, who manually collect, verify, and compile driver-submitted delivery documents by hand, currently causing overtime. Goal: scan/automate as much as possible via the drivers themselves, framed not as headcount reduction but as freeing existing staff from repetitive manual work. |
| Source | 2026-09-15-business-quantification-reklamace-fakturace-doprav |
| Added | 2026-09-15 |
| Status | Active |

**Owner / domain expert**: Jan Žižka (STK-015) — hadn't seen the tracker yet as of this call.

**Business value (Fermi estimate, flagged as possibly too large by the client herself)**: ~16 hours/day (2 people × 8 hours) → a potential annual saving in the range of ~1.5 million (currency not stated). Source figure: an earlier Ableneo estimate of ~90 hours/month of relevant manual work, 40–60% considered automatable. Needs verification with Jan Žižka before being treated as reliable.

**Scope**: Savings are entirely office/administrative-side — driver time and cost are explicitly out of scope, since drivers aren't ViaPharma/Dr. Max employees. A driver satisfaction check was floated as a soft secondary signal only, not a hard KPI — see [[ASM-072]].

**KPIs**: Primary — total administrative time-fund reduced by ~40%, measured in aggregate (not per-headcount, since staff time isn't cleanly separable by task). Document error rate was explicitly discussed and rejected as a KPI, same reasoning as Reklamace — see [[ASM-072]].

### AI Listing Tool (Dr. Max)

| Field | Value |
|-------|-------|
| Definition | Internal e-commerce PIM (Product Information Management) and AI catalog-enrichment platform for Dr. Max pharmacy/health e-commerce content managers. Three core functions: (1) **audit & validate catalog health** — scores each product listing against regulatory/categorization criteria; (2) **automate content generation** — GenAI produces structured product descriptions, meta text, and taxonomy attributes; (3) **configure category standards ("Listovací minima")** — per-category rules covering AI prompt instructions, character limits, allowed attribute values, and a blacklist of non-compliant medical claims. |
| Source | 2026-09-11-ai-listing-tool-demo-walkthrough |
| Added | 2026-09-11 |
| Status | Active |

Demoed screen flow: category selection → product catalog table (per-product SKÓRE health/completeness score, STAV workflow status, PROBLÉMY validation badges) → product detail dual-pane AI generation editor (diff view, one-click "Generovat", version history with rollback) → category rules configuration ("Listovací minima": 6 description fields with per-field AI prompts, 2 meta-description fields with fixed character ranges, a 28-attribute product parameter taxonomy with per-attribute auto/manual toggle, and the compliance blacklist — see the Regulatory & Compliance entry below). Confirms the tool's current live scale: 72 products in the single pilot category ("Proteiny / Doplňky stravy"), consistent with the "hardcoded to 1 category" scope noted elsewhere ([[ASM-032]]). Only two product-level workflow statuses were observed (*Import*, *Rozpracováno*) — full status lifecycle unconfirmed.

## Data Model Concepts

## Regulatory & Compliance

### Listing — non-compliant medical claim blacklist

| Field | Value |
|-------|-------|
| Definition | The AI Listing Tool enforces a per-category blacklist of non-compliant curative/medical claim phrases (e.g. "léčí", "hojí", "terapeutický", "léčivý", "uzdravuje", "zmírňuje příznaky") as part of its "Listovací minima" category-standards configuration, blocking AI-generated content from using this language. |
| Source | 2026-09-11-ai-listing-tool-demo-walkthrough |
| Added | 2026-09-11 |
| Status | Needs confirmation |

Unclear whether this blacklist is signed off by Dr. Max or a BigHub-authored draft pending client review — relevant given this account's broader pattern of BigHub building ahead of confirmed client sign-off (e.g. the still-undefined category/parameter system, see the Farmis/Magento entry above).

## Naming Conventions

## Vendor & Partner Context

### BigHub

| Field | Value |
|-------|-------|
| Definition | Company where Marek Pillár works as a PM |
| Source | PM input (project-initiation) |
| Added | 2026-09-01 |
| Last updated | 2026-09-04 |
| Status | Active |

Other BigHub clients referenced (2026-09-04) as also running the shared AI/chatbot platform used for Dr. Max's Max/Maxie/Lexie: **Brněnská komunikace** (Brno communications), **Kooperativa** (accounting department variant), **Unica** (legal department variant, still in progress). No named individual contacts captured for these accounts yet.

### AI platforma (new initiative)

| Field | Value |
|-------|-------|
| Definition | **Confirmed 2026-09-08**: this is the same shared BigHub AI/chatbot platform already powering Max Chatbot/Maxie/Lexie for Dr. Max (see "Shared AI/chatbot platform" below) — not a separate, new system. Tomáš Dudaško (STK-010) wants visible investment in it: unified test/production environments, improved UX/visual polish, and consolidation of all Dr. Max BigHub projects onto it. Test environment link: https://aiplatform-prod.cz.dr-max.global/login — Marek's own access not yet confirmed. |
| Source | PM input 2026-09-08; 2026-09-08-ai-platform-strategy-history-with-jan-sovka; 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |
| Added | 2026-09-08 |
| Last updated | 2026-09-08 |
| Status | Active |

Deliberately kept out of the 9-product roadmap set (`product-roadmap-portfolio-full.xlsx`) for now, per PM instruction, until scoped. Agreed 3-phase delivery plan: (1) UX rework into one consolidated landing page, (2) migrate existing projects onto the platform on both test and production, (3) build Dudaško's backlog (from his requirements Excel) into an admin/reporting layer. See also "BigHub's shared-platform strategy (retired)" and "AI platform — current technical state" below.

### BigHub's shared-platform strategy (retired)

| Field | Value |
|-------|-------|
| Definition | ~1.5 years ago, BigHub's internal strategy was to build one unified AI platform as a "passive revenue" B2B product — a single core, white-labeled and wrapped per client — sold to clients (including Dr. Max) on a shared roadmap, common feature releases, and unified admin/cost reporting. It never got internal traction or investment (no team was ever properly resourced to build it as a real product) and was formally killed in an internal management evaluation **~4 months ago (~2026-05)**. Current strategy: fully custom builds per client, optionally inspired by each other's code, increasingly via AI-assisted ("vibe coding") development — no shared product roadmap. The underlying codebase is deployed across Dr. Max, Brněnská komunikace, Kooperativa, and Unica (heavily modified). **Sensitivity**: the Kooperativa deployment is built heavily around Kooperativa-specific needs (integrates with something referred to as "XLET" — unconfirmed) — avoid Kooperativa traces being visible if the platform is demoed to Dr. Max. |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka |
| Added | 2026-09-08 |
| Status | Active — historical context |

### AI platform — current technical state

| Field | Value |
|-------|-------|
| Definition | Per Jura Brázdil (2026-09-08), the platform's actual current build is much earlier-stage than its "2 years of development" history suggests: in practice it equals **one implemented product — a RAG/document-retrieval system**. MaxBuddy is **not** yet in the platform's own namespace (blocked on the new AKS environment since early August 2026). Known infra issues: a **shared database/DB server with zero isolation between use cases** (e.g. MaxBuddy's process could technically reach into Listing's data), and a **single shared admin account** across all use cases. The role-based permission system (Entra ID-based) that exists today was built specifically for the RAG chatbot (Lexie) — it is **not** a general, platform-wide capability yet, despite earlier framing (2026-09-08, Jan Sovka) suggesting broader maturity. |
| Source | 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |
| Added | 2026-09-08 |
| Status | Active |

### Alfred

| Field | Value |
|-------|-------|
| Definition | BigHub's internal client-knowledge system concept (working name) — centrally logs client interactions, agreements, and specs so future conversations carry full context; envisioned to act as an in-call co-pilot and eventually feed prepared context to developers for agentic development. Currently just a vision plus a small functional prototype. Stays a BigHub-owned internal asset — never handed to clients, even as accounts mature. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| Added | 2026-09-01 |
| Status | Active |

### Dr. Max / ČLH (Česká lékárna holding)

| Field | Value |
|-------|-------|
| Definition | BigHub client account. Czech pharmacy chain, part of Penta, official entity ČLH. ~40 billion CZK revenue in Czech, ~10% (~4 billion CZK) from the e-shop. Grew via acquisitions; a global group called BDC oversees local entities, which retain significant autonomy. Numbers/ROI-driven account culture due to Penta ownership. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| Added | 2026-09-01 |
| Last updated | 2026-09-01 |
| Status | Active |

Active project streams as of 2026-09-01 (per 2026-09-01-dr-max-x-bighub-project-status-sync): MaxBuddy (live, incremental changes), Max chatbot, Maxie, Lexie, claims/reklamace knowledge-base consolidation, freight invoicing (fakturace doprav), e-commerce order prediction (řízení poptávky), listing, voicebot. Plus **Kontrola beden** (crate/box control) — identified but not yet started; next-step contact Jan Maroušek (STK-021) has never been actioned.

Per a BigHub roadmap sheet (2026-09-02), owners cross-checked against the above: MaxBuddy → Tomáš Dudaško (STK-010), E-Shop order forecast → Marek Šimoník (STK-019, confirms), Product listing → Petr Neuman (STK-023, new), Maxie/Max → Simona Mertova/Martová (STK-017, spelling unresolved), Lexie → Tomáš Dudaško (STK-010, conflicts with the transcript's Martová/Mertová attribution). Also surfaced: **TD revisions**, a project stream not seen in any transcript, owned by Tomáš Burda (STK-025); and two initiatives — "Receiving compliants in stock" and "Invoicing solution" — both owned by Rudolf Zurek (STK-024), which may or may not be the same initiatives as Reklamace and Fakturace doprav respectively. Conflicts recorded but not reconciled — see ASM-006.

**Dev-side (BigHub) ownership map**, per Juraj Kmec (2026-09-02) — distinct from the business-side ownership above: e-commerce/order prediction → Juraj Kmec (STK-009); listing → Filip Černý (STK-006); logistics umbrella (reklamace + freight invoicing, believed to be one combined use case) → Jura Brázdil (STK-026, unconfirmed — conflicts with an earlier attribution to "Kuba Turner," see ASM-007); shared LLM platform infra/governance (not itself a use case) → William Gago (STK-027), with Lukáš Starenko (STK-028) and Honza Zelený (STK-029) also involved in unclear capacities. Amended 2026-09-03: Jakub Turner (STK-007) is also actively engaged in reklamace-app backend work (auth, Axapta integration), alongside Brázdil — the two ownership attributions aren't mutually exclusive after all, see [[ASM-007]].

### Order-Prediction Dashboard (Řízení poptávky)

| Field | Value |
|-------|-------|
| Definition | The e-commerce order/demand-prediction dashboard owned by Juraj Kmec. Static, read-only React frontend ("like Power BI") deliberately built with no interactivity so it can't break Dr. Max infra. Tracks two predicted metrics: (1) **Revenue** — plan/target vs. actual vs. model prediction with confidence intervals and a probability-of-hitting-target readout; (2) **Logistics** — predicted new order counts by warehouse and shipping method, with a "time travel" feature comparing a historical model run against actual outcomes. Both have a same-day zoomed view with ~30 min live-data delay. Deployed on Dr. Max infra, VPN-gated, no external repo access without a Dr. Max account. |
| Source | 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-15-order-prediction-dashboard-follow-up |
| Added | 2026-09-02 |
| Last updated | 2026-09-15 |
| Status | Active |

v1 considered done as of 2026-09-02; first live business demo 2026-09-03 (demoed by Juraj Kmec directly). Before this, the business had no live visibility — data was pulled manually from Excel exports ~2 days stale. Formally accepted by the client as "version 1" on 2026-09-15 — see [[ASM-069]].

**Live demo outcome (2026-09-03)**: Very positive reception from Šimoník. A real 8-minute site outage (2026-08-24, 09:20–09:28) correctly showed as a dip in the live chart — a strong, organic trust-building validation moment. Model is calibrated for a 14-day horizon (reliable) with unguaranteed extrapolation beyond that (deliberately shown without confidence intervals). Trained purely on recognized/invoiced revenue, not blended with order-backlog signals — see [[ASM-016]]. Known gap: doesn't yet account for marketing campaigns (the one promo/campaign CSV on file is ~2 months stale) — likely explanation for recent Brno under-prediction (a campaign started 2026-08-29). Small feature backlog: order-count toggle on the breakdown table, D-7 and day-of-week-aligned D-365 historical overlay lines, split warehouse/shipping-method filters, clearer tooltip text distinguishing "probability of hitting today's target" from "% of month-end target expected." Review process for the testing phase: verify data accuracy → request UX changes → tune model accuracy last, see [[ASM-014]]. Phase-1 primary users are Šimoník and Petr Ondráček (STK-035); a separate logistics need (month-ahead view) deferred to a later phase, see [[ASM-015]].

**2026-09-07 portfolio review**: Order Service data now flows through DataHub rather than a direct connection (architecture clarification, not a scope change). Production deployment is technically live already, but the *test* environment is undersized on the old AKS node pool and throwing out-of-memory errors — production itself runs fine, waiting on the new AKS to fix test capacity. Christmas prediction quality flagged as a known open risk since training data has no prior Christmas season to learn from — see the new "Spresňovanie modelovania" backlog item. Campaign recommendation model and automated campaign generation discussed as possibly Full Version but no firm call made — both genuinely hard analytics problems needing dedicated scoping, see [[ASM-030]].

**Terminology (2026-09-15)**: Three distinct figures now appear together on dashboard views and must be kept separate — **budget** (Dr. Max's annual plan, set every August for the following year), **forecast** (Dr. Max's own internal re-budgeting exercise, redone after months 3, 5, and 7 against year-end expectations — running ~3-6% below the original 2026 budget as of this date), and **predikce** (the model's own output — the only one of the three BigHub computes). Budget/forecast are supplied externally by Dr. Max (a "2026 forecast" column added to the existing data feed); see [[ASM-070]].

**Order-count comparison methodology (2026-09-15)**: A same-weekday historical comparison feature uses **T-7** (7 days back) and **T-364** (not a literal D-365) specifically to preserve day-of-week alignment across a full year, including leap years — the model counts by week (52), not by raw day offset, so it doesn't drift even in a leap year.

**Pharmacy reservations as strategic differentiator (2026-09-15)**: "Rezervace v lékárnách" (pharmacy reservations — click & collect at one of ~600 physical Dr. Max pharmacies) are dramatically cheaper fulfillment than warehouse-based click & collect: a pharmacist simply holds a product on a shelf, versus Dr. Max carrying full warehouse pick/pack/return cost. Dr. Max is actively pushing this channel (a new in-app "reserve at pharmacy" button, alongside add-to-cart) and considers it a key e-commerce USP. On the dashboard, reservations need to be broken out from the general order aggregate as their own top-line category, further split per warehouse (Nučice, Brno) for logistics staffing — see [[ASM-071]]. This surfaced a design gap in the existing "Metrix" (warehouse × delivery-method matrix) view: reservations don't map cleanly onto either axis (a reservation is conceptually both a "warehouse" and a "delivery method" in the current model), needing a redesign.

**Delivery cadence (2026-09-15)**: The dashboard's initial build is formally accepted as "version 1"; further requests batch into "version 2," and once that ships, subsequent requests batch into "version 3," on a roughly quarterly cadence rather than continuous ad hoc releases — see [[ASM-069]].

### Axapta

| Field | Value |
|-------|-------|
| Definition | Dr. Max's legacy warehouse management system — a repurposed, warehouse-specific fork of Microsoft Dynamics. Relevant to the warehouse/claims automation stream, which requires custom-built APIs to integrate with it. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| Added | 2026-09-01 |
| Last updated | 2026-09-10 |
| Status | Active |

Reklamace document flow (as of 2026-09-02): contract config in Axapta is complete; the system generates a PDF and stores it to Azure. Two distinct PDFs exist — **"rozvozový list"** (generated by BigHub) and **"návratka"** (generated by Accepta, client-side). Email-sending is the next unbuilt step — the plan is to pull the file from Azure and attach/send as a pre-filled draft (never auto-sent, see [[ASM-010]]); whether this calls the Microsoft Graph API's draft-creation endpoint directly is not yet specified.

**Reklamace mobile app** (demoed 2026-09-03 by Filip Černý): operator scans a shipping label → app looks up the product via Accepta's endpoint → operator confirms/adjusts quantity → photographs any damage, optional note → submits → app returns a reklamace number written to Axapta. A second flow, "receipt with reservation," follows the same pattern and also writes to Axapta. Auth for the testing phase is hardcoded per-user logins (not yet Entra ID/OAuth — see [[ASM-012]]); the API is being extended to include an "odběratel" (recipient/customer) field so Dr. Max's side has full visibility into who a claim is for.

**Jump Server** (BigHub → Dr. Max direct log access, including the Mongo archive): proposed roughly a month before 2026-09-03, has "definitely not moved" since — no clear owner assigned on either side as of 2026-09-03. Distinct from the AKS/VPN access blockers tracked elsewhere; this specifically concerns read access into Dr. Max's own logs/Mongo rather than infrastructure provisioning.

**State ownership for Fakturace doprav** (clarified 2026-09-10 by Jan Žižka): Axapta — not the BigHub app — is the sole source of truth for route/document status. The app holds no state of its own and simply forwards scanned documents to Axapta as they arrive, whenever they arrive; Axapta reconciles documents submitted across multiple separate scan sessions for the same route, and a route row must appear in Axapta the moment its first document lands (so ViaPharma has reaction time to chase a slow carrier before month-end close). This corrected an earlier misunderstanding where the app was being built to track its own completion state and push a manual-review/ready-for-invoicing status to Axapta — see [[ASM-053]].

### BDC

| Field | Value |
|-------|-------|
| Definition | Global group overseeing Dr. Max's local entities across countries. Local entities (like the Czech one) retain significant autonomy; some infrastructure is global (managed via BDC), some local — creates approval bottlenecks, e.g. infra access requests (AKS, voicebot) that span multiple BDC teams. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-dr-max-x-bighub-project-status-sync |
| Added | 2026-09-01 |
| Status | Active |

### Atlantis

| Field | Value |
|-------|-------|
| Definition | Infrastructure/access vendor involved in provisioning access (`prostupy`) for Dr. Max systems — relevant to the voicebot project's infra blocker. Runs on Dr. Max's own datacenter hardware (their VMs) but is administered as a vendor service by Atlantis's own staff (contact: Tecl, STK-033), including public addresses/comms. Currently serves as the central PBX for the entire Dr. Max call center and all T-Mobile data lines — every inbound call routes through this existing SIP connection; adding further SIP lines is not expected to be technically difficult. Will connect directly to **ElevenLabs** (voice AI provider) for the voicebot; a new public IP/domain needs configuring for that integration, owned end-to-end by Atlantis. |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-aks-atlantis-infra-sync |
| Added | 2026-09-01 |
| Last updated | 2026-09-02 |
| Status | Active |

### AKS

| Field | Value |
|-------|-------|
| Definition | Infrastructure/access component referenced as a recurring blocker for the order-prediction and voicebot streams — access approvals span multiple BDC teams. Likely "Azure Kubernetes Service" given the Microsoft/Azure context elsewhere in the account, but not stated explicitly in source. |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-logistics-listing-team-sync, 2026-09-02-aks-atlantis-infra-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |
| Added | 2026-09-01 |
| Last updated | 2026-09-04 |
| Status | Needs confirmation |

Reklamace end-to-end testing (2026-09-02) surfaced a related cluster issue: a certificate only validates on one node pool, not others — temporarily worked around, needs a permanent fix. Also currently consuming much of Vladislav Tvarůžek's (STK-016) time, delaying Lukáš Starenko's (STK-028) environment access request.

Per a separate 2026-09-02 infra sync, access is actively closing out: node pools already exist, VPN address configuration underway, namespaces being corrected. Optimistic ETA today (2026-09-02) or tomorrow morning (2026-09-03); firewall/permission requests now take ~1 hour once submitted (down from ~2 weeks), owned by Dr. Max's Network Team. A separate item referred to as "AKSO" was mentioned alongside AKS in that sync — unclear whether it's a distinct workstream or a transcription artifact.

**Node-pool cost issue (2026-09-04)**: Jura Brázdil flagged idle AKS node pools that are actively costing money while unused. Two ways out: BDC deletes the idle pools immediately, or every project gets redeployed with a node selector (non-trivial, cross-project work). Unresolved as of 2026-09-04 — Jindřich Tůma to pursue with BDC.

### Farmis / Magento

| Field | Value |
|-------|-------|
| Definition | Client-side systems relevant to the listing project. Magento appears to be (part of) the e-commerce platform; Farmis is a separate system with a functionality gap under analysis (assigned to Jan Sovka) before listing work proceeds — also the source of a Farmis release that broke a MaxBuddy dependency, causing two recent outages. |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-logistics-listing-team-sync |
| Added | 2026-09-01 |
| Last updated | 2026-09-02 |
| Status | Needs confirmation |

Listing's core blocker (reconfirmed 2026-09-02) is not code but Dr. Max's undefined category/parameter system (e.g. how to categorize something like bottled water) — a POC/demo exists for one narrow category, but extending to all categories is stuck pending client-side decisions. Per Filip Černý, further development isn't worth pursuing until this is delivered. See [[ASM-011]] for the agreed Discovery-first path forward.

### Planning Wizard

| Field | Value |
|-------|-------|
| Definition | A Dr. Max-side initiative not previously seen in this account — mentioned only in passing as something that displaced Vladislav Tvarůžek's (STK-016) bandwidth for ~2 days, delaying AKS/Atlantis work. Nature and ownership otherwise unknown. |
| Source | 2026-09-02-aks-atlantis-infra-sync |
| Added | 2026-09-02 |
| Status | Needs confirmation |

### ElevenLabs

| Field | Value |
|-------|-------|
| Definition | Third-party voice AI provider (text-to-speech/speech-to-text) that Atlantis will connect to directly for the Dr. Max voicebot project. |
| Source | 2026-09-02-aks-atlantis-infra-sync |
| Added | 2026-09-02 |
| Status | Active |

## Seasonal & Cyclical Patterns

## Project Conventions

### Effort estimate convention (MD)

| Field | Value |
|-------|-------|
| Definition | Effort estimates are always abbreviated as "MD" (man-days), never spelled out, in any language. Hour-based estimates convert to MD as: 1-3h → 0.5 MD, 4h+ → 1 MD. In the roadmap Excel, the "Estimate - Optimistic" column takes the lower bound of any range and "Estimate - Pessimistic" takes the upper bound; flat single-point estimates go in both columns unchanged. Waiting/external-dependency periods (e.g. a certification process, an infra-access grant) are not effort estimates and are excluded from MD sums — only actual work effort counts. **When a developer gives a single MD figure with no explicit range** (as Filip Černý did for Reklamace/Fakturace doprav/Listing, 2026-09-09), treat that figure as the pessimistic value and compute optimistic as 50% of it — this is a per-instance PM instruction, not a universal default, so confirm it applies before reusing it for a different developer's estimates. |
| Source | PM input, 2026-09-08; extended 2026-09-09 |
| Added | 2026-09-08 |
| Last updated | 2026-09-09 |
| Status | Active |

### VBS (work-breakdown-structure) framework

| Field | Value |
|-------|-------|
| Definition | Jindřich Tůma's preferred project work-breakdown-structure framework: a tree breakdown of a project (e.g. "infrastructure" → "Azure setup," "Azure access," "licensing"), held at multiple granularities — coarse for business-facing roadmap timelines (e.g. "infrastructure — 14 days," no ticket-level detail), fine-grained for actual estimation and time tracking against individual tickets. Used both for estimating a project and for reporting on it (tracking overruns against the original breakdown). |
| Source | 2026-09-02-roadmap-tracking-and-listing-onboarding-sync, 2026-09-02-logistics-listing-team-sync |
| Added | 2026-09-02 |
| Status | Active |

In a separate 2026-09-02 sync, Jindřich reiterated the plan for a shared coordination platform combining both a technical and a **business** Kanban (not just ticket tracking) — replacing informal tracking currently scattered across tools like "X-manager." Goal: every sync references the same board; 15-20 min standups; target operational next week.

### Communication channels & X-Manager coverage gap

| Field | Value |
|-------|-------|
| Definition | Confirmed 2026-09-03: X-Manager (BigHub's formal ticketing tool, access granted ~1 month prior) currently has essentially nothing in it for MaxBuddy — it's only used for the new chatbot/REX platform. MaxBuddy itself still runs via email and Teams, with a weekly Wednesday sync. Screenshots of X-Manager tickets get informally cross-posted to the "LLM Platforma" Teams chat rather than tracked centrally. |
| Source | 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |
| Added | 2026-09-03 |
| Status | Active |

Relevant Teams channels: **BigHubInfrastructureChat** (in Dr. Max's Teams — general BigHub-dev infra coordination; members include Viliam Gago, Jura Brázdil, "Duri"); **MaxBuddy.DVH x BigHub** (coordination with the Data Warehouse/DVH team specifically); **Dr. Max LLM Platforma** (general LLM-platform coordination and informal X-Manager screenshot sharing — also where Marek was added 2026-09-02). Channel history is not retroactively visible to members added after the fact.

### "Old wise man" discovery approach

| Field | Value |
|-------|-------|
| Definition | Jan Sovka's discovery methodology for new client engagements: (1) start with long-tenured people who understand the *why* behind existing processes before proposing change; (2) gather input from both directions — management priorities/KPIs and the people actually doing the work, since ground-level reality often differs from what management believes; (3) validate specs with clickable/prototype mockups before or alongside writing them, which surfaces edge cases and gets much stronger stakeholder buy-in than a text brief alone. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| Added | 2026-09-01 |
| Status | Active |

## Historical Context

---

## Entry Format

```markdown
### {Term or Concept Name}

| Field | Value |
|-------|-------|
| Definition | {Clear, concise definition in project context} |
| Source | {document-slug, meeting-slug, PM input, or web research with citation} |
| Added | {YYYY-MM-DD} |
| Last updated | {YYYY-MM-DD — only present if updated after initial add} |
| Status | Active / Needs confirmation / Superseded |

{Optional: 1-2 sentences of additional context — usage notes, relationship to other terms, caveats.}
```
