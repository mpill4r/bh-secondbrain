---
last_updated: 2026-09-04
last_updated_by: auto — project-meeting routing (2026-09-04-ai-platform-standup-xmanager-lexi-demo)
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
| Source | 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |
| Added | 2026-09-01 |
| Last updated | 2026-09-03 |
| Status | Active |

The dosage-verification logic still exists dormant in the codebase and could be revived if Dr. Max later pursues certification.

**Regulatory detail (2026-09-03)**: the dosage-checking feature was meant to flag outdated dosing against the latest SPC (package leaflet) guidance — motivated by legislation shifting dosing-error liability onto prescribing doctors. ~6 months into development, this was found to make the product a regulated medical device requiring certification: any pipeline where patient data goes in and an LLM-derived recommendation comes out is prohibited without it ("no blackbox: patient data in, drug advice out"). Pivoted instead to upsell/cross-sell recommendations, which combine pharmacological knowledge but are reviewed and approved by an expert panel rather than generated per-patient by an LLM. BigHub is separately pushing (with SOS support) for anonymized receipt-data access to base upsell recommendations on actual purchase patterns — permitted, since anonymized data carries no patient-specific medical inference. This same "display official content, never generate medical advice" pattern was reused for the Max chatbot's SPC-leaflet guardrail — see [[ASM-020]].

A related, already-running system: SPC-change monitoring, collecting periodic diffs to drug package leaflets (running ~2 months as of 2026-09-03). ~99% of changes are noise (phrasing/formatting/grammar); dosage-paragraph changes are flagged critical. An AI re-sorting pass is planned before results are shared with Dr. Max, since signal-to-noise isn't good enough yet.

**Deployment strategy (2026-09-03)**: MaxBuddy runs on 30 of ~600 pharmacies. Dr. Max originally wanted full rollout within 14 days; Jura Brázdil determined this was unsafe (best case, MaxBuddy crashes; worst case, it takes down the pharmacies' payroll/POS system) given no adequate 1:1 test environment (single e-recept item only, ~16s DB response time). This triggered the AKS infrastructure effort started in July. Rollout plan: the same ~20-30 pilot pharmacies (chosen for younger, more technically flexible pharmacists) serve as a permanent canary environment — new versions validated there live first, then rolled to the remaining ~580.

**Platform consolidation**: MaxBuddy started standalone. Once the new AKS sandbox is live, Jura Brázdil takes over the shared AI platform (built by Viliam Gago, STK-027) and migrates MaxBuddy onto it alongside the Max chatbot and Lexie.

Original infrastructure/model provisioning for MaxBuddy was done manually (ad hoc clicking), not via Terraform or other IaC tooling — surfaced 2026-09-02 when checking whether a redeployment was possible. No structured infra-as-code state exists for it; the people most involved in the original setup are no longer easily reachable, and exact names are uncertain due to transcription quality (see 2026-09-02-aks-atlantis-infra-sync). Consensus was to leave it alone since it currently works.

### Max / Maxie / Lexie

| Field | Value |
|-------|-------|
| Definition | Three BigHub-built chatbot/assistant products for Dr. Max, owned business-side by paní Mertová (STK-017), co-owned with Tomáš Dudaško (STK-010, IT/budget side). **Max** is the customer-facing chatbot embedded on the drmax.cz website (order status, pharmacy locator, e-recepty, medication/stock lookup — see full flow below); a **voice channel of the same capability is Maxie**, launching scoped to order-status only via IVR. **Lexie (Lucie)** is the internal knowledge-base assistant being rolled out to IT, Legal, and Brno accounting, now in Call Center testing — currently blocked on 3 bugs, see below. Distinct from MaxBuddy (the pharmacy point-of-sale cross-sell product) — corrected 2026-09-03; an earlier entry incorrectly described Max as "Call Center-facing." |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |
| Added | 2026-09-01 |
| Last updated | 2026-09-04 |
| Status | Active |

**Important scope correction (2026-09-04)**: the underlying AI platform (chatbot + RAG infrastructure) is **shared BigHub infrastructure reused across multiple clients**, not Dr. Max-exclusive — also deployed for Brněnská komunikace (Brno communications), with variants in progress for Kooperativa (accounting) and Unica (legal). Dr. Max is one deployment of a centralized "core" platform/repo, not a bespoke build. Frontend direction: one standardized template by default, custom per client only on explicit request — see [[ASM-025]]. Whether Honza Sovka retains product ownership of the platform across all clients (vs. Marek owning Dr. Max only) is unresolved — see [[ASM-026]].

**Max chatbot (2026-09-03)**: demoed live to strong Dr. Max reception. Four button-driven functions plus free-text LLM chat: order status (order number + email, or number alone with auto-detection, returns tracking link); pharmacy locator (by device location or city, shows hours/route/call button); e-recepty (handles prescribed/not-yet-issued, multi-item, already-issued, and expired states); medication/stock lookup (searches Dr. Max's public API, AI-reranks variants by form rather than pack size, checks live stock across 561 pharmacies). Refuses medical-advice questions (e.g. dosing safety), redirecting instead to the official SPC leaflet via the same API built for MaxBuddy — see [[ASM-020]]. Has a working usage-analytics dashboard (currently synthetic data pre-launch). Deployment: staged rollout via a public/testing version-switch mechanism (URL param or config flag), allowing fast, low-risk version releases without a full redeploy.

**Lexie (Lucie) — blocked on 3 bugs (2026-09-03)**: (1) feedback button broken specifically on long/large responses, confirmed reproducible; (2) autocomplete/suggestion popup ("našeptávač") to be removed entirely — pops up unpredictably, including mid-response, obscuring the answer an operator is relaying; (3) configurable fixed/canned status messages needed outside the prompt, for outage-style announcements. GPT model upgraded 5.1→5.4 on 2026-09-02 by Viliam Gago. All Lexie work paused until fixed — see [[ASM-021]].

**Lexie ticket triage (2026-09-04)**: root cause found for the feedback-button bug — thumbs aren't real buttons, they sit on an action area overlapped by the "regenerate response" control on long messages, so double-clicking selects text instead. Viliam Gago fixing same-day, alongside the status-announcement banner (admin-editable, not auto-detected) and a response-links fix already in test. Two other tickets: document-rename-not-reflecting-in-Lexie (indexer lag vs. a possible diacritics issue, unresolved) and test-user creation (auth architecture unresolved — 2FA on real Dr. Max accounts makes ad hoc role-testing painful; punted to Lukáš Szücs). A "Product Scope" ticket (Kateřina Karlecová's MVP/roadmap ask) is now owned by Marek. RAG mechanics confirmed: Lexie indexes Dr. Max's SharePoint periodically via an embedding pipeline into a vector DB, with clickable source citations.

**Maxie (voicebot, 2026-09-03)**: built by Honza Zelený (STK-029), sharing infrastructure with the Max chatbot. Technical blocker (missing SIP trunk) resolved via an Atlantis meeting the prior Thursday; a request list is with Dr. Max's BDC infra team (contact: Vladislav Tvarůžek, STK-016), prioritized after the new AKS work — targeting ~14 days to technical readiness. Scope starts at order-status only via a fixed IVR branch, expanding as Dr. Max's IVR is updated — see [[ASM-022]].

**Process notes**: all three products' X-Manager feature requests should route through Simona Mertová as single point of contact — see [[ASM-018]]. Production-readiness bar is functional correctness against agreed scope, not full polish — see [[ASM-019]]. In-chat feedback mechanism (Max) is a star/emoji rating, no free text — see [[ASM-017]].

### OCR (pharmacy service-protocol extraction)

| Field | Value |
|-------|-------|
| Definition | New, early-stage BigHub project (owner: Jura Brázdil) automating extraction from mandatory pharmacy equipment service-inspection protocols (automatic doors, air conditioning, etc.) — currently manually retyped into Excel by staff. "OCR" is a working name, not literally OCR-only — the pipeline is LLM-based extraction over scanned/photographed, often handwritten, documents. |
| Source | 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |
| Added | 2026-09-03 |
| Status | Active |

Scope narrowed to one category first: automatic doors, two vendors — extracting door type, faults, branch address, and follow-up requests via a ~16-prompt pipeline. Currently in a second feasibility-measurement round (first round handled cleanly-extractable data; second tackles free-text notes). Target: production-ready for Dr. Max's November inspection cycle. Will move onto the shared AI platform (alongside MaxBuddy, Max, Lexie) once the new AKS sandbox is available. Not yet present in the BigHub roadmap Excel/portfolio tracker as of 2026-09-03 — a gap, not yet reconciled.

## Data Model Concepts

## Regulatory & Compliance

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
| Source | 2026-09-02-order-prediction-dashboard-walkthrough |
| Added | 2026-09-02 |
| Status | Active |

v1 considered done as of 2026-09-02; first live business demo 2026-09-03 (demoed by Juraj Kmec directly). Before this, the business had no live visibility — data was pulled manually from Excel exports ~2 days stale. No phase 2/3/4 roadmap defined yet; will be shaped after demo feedback and a 1-2 week trial by Marek Šimoník (STK-019, e-commerce lead).

**Live demo outcome (2026-09-03)**: Very positive reception from Šimoník. A real 8-minute site outage (2026-08-24, 09:20–09:28) correctly showed as a dip in the live chart — a strong, organic trust-building validation moment. Model is calibrated for a 14-day horizon (reliable) with unguaranteed extrapolation beyond that (deliberately shown without confidence intervals). Trained purely on recognized/invoiced revenue, not blended with order-backlog signals — see [[ASM-016]]. Known gap: doesn't yet account for marketing campaigns (the one promo/campaign CSV on file is ~2 months stale) — likely explanation for recent Brno under-prediction (a campaign started 2026-08-29). Small feature backlog: order-count toggle on the breakdown table, D-7 and day-of-week-aligned D-365 historical overlay lines, split warehouse/shipping-method filters, clearer tooltip text distinguishing "probability of hitting today's target" from "% of month-end target expected." Review process for the testing phase: verify data accuracy → request UX changes → tune model accuracy last, see [[ASM-014]]. Phase-1 primary users are Šimoník and Petr Ondráček (STK-035); a separate logistics need (month-ahead view) deferred to a later phase, see [[ASM-015]].

### Axapta

| Field | Value |
|-------|-------|
| Definition | Dr. Max's legacy warehouse management system — a repurposed, warehouse-specific fork of Microsoft Dynamics. Relevant to the warehouse/claims automation stream, which requires custom-built APIs to integrate with it. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo |
| Added | 2026-09-01 |
| Last updated | 2026-09-03 |
| Status | Active |

Reklamace document flow (as of 2026-09-02): contract config in Axapta is complete; the system generates a PDF and stores it to Azure. Two distinct PDFs exist — **"rozvozový list"** (generated by BigHub) and **"návratka"** (generated by Accepta, client-side). Email-sending is the next unbuilt step — the plan is to pull the file from Azure and attach/send as a pre-filled draft (never auto-sent, see [[ASM-010]]); whether this calls the Microsoft Graph API's draft-creation endpoint directly is not yet specified.

**Reklamace mobile app** (demoed 2026-09-03 by Filip Černý): operator scans a shipping label → app looks up the product via Accepta's endpoint → operator confirms/adjusts quantity → photographs any damage, optional note → submits → app returns a reklamace number written to Axapta. A second flow, "receipt with reservation," follows the same pattern and also writes to Axapta. Auth for the testing phase is hardcoded per-user logins (not yet Entra ID/OAuth — see [[ASM-012]]); the API is being extended to include an "odběratel" (recipient/customer) field so Dr. Max's side has full visibility into who a claim is for.

**Jump Server** (BigHub → Dr. Max direct log access, including the Mongo archive): proposed roughly a month before 2026-09-03, has "definitely not moved" since — no clear owner assigned on either side as of 2026-09-03. Distinct from the AKS/VPN access blockers tracked elsewhere; this specifically concerns read access into Dr. Max's own logs/Mongo rather than infrastructure provisioning.

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
