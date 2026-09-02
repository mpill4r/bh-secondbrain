---
last_updated: 2026-09-02
last_updated_by: auto — project-meeting routing (2026-09-02-aks-atlantis-infra-sync)
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
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| Added | 2026-09-01 |
| Status | Active |

The dosage-verification logic still exists dormant in the codebase and could be revived if Dr. Max later pursues certification.

Original infrastructure/model provisioning for MaxBuddy was done manually (ad hoc clicking), not via Terraform or other IaC tooling — surfaced 2026-09-02 when checking whether a redeployment was possible. No structured infra-as-code state exists for it; the people most involved in the original setup are no longer easily reachable, and exact names are uncertain due to transcription quality (see 2026-09-02-aks-atlantis-infra-sync). Consensus was to leave it alone since it currently works.

### Max / Maxi / Lexi

| Field | Value |
|-------|-------|
| Definition | Three BigHub-built chatbot/assistant products for Dr. Max, owned business-side by paní Mertová (STK-017). Max is the main chatbot (Call Center-facing tickets prioritized); Lexi is a knowledge-base assistant being rolled out to IT, Legal, and Brno accounting, with Call Center next — Lexi is co-owned with Tomáš Dudaško (STK-010, IT/budget side). Distinct from MaxBuddy (the pharmacy point-of-sale cross-sell product). |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync |
| Added | 2026-09-01 |
| Status | Active |

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

Active project streams as of 2026-09-01 (per 2026-09-01-dr-max-x-bighub-project-status-sync): MaxBuddy (live, incremental changes), Max chatbot, Maxi, Lexi, claims/reklamace knowledge-base consolidation, freight invoicing (fakturace doprav), e-commerce order prediction (řízení poptávky), listing, voicebot. Plus **Kontrola beden** (crate/box control) — identified but not yet started; next-step contact Jan Maroušek (STK-021) has never been actioned.

Per a BigHub roadmap sheet (2026-09-02), owners cross-checked against the above: MaxBuddy → Tomáš Dudaško (STK-010), E-Shop order forecast → Marek Šimoník (STK-019, confirms), Product listing → Petr Neuman (STK-023, new), Maxie/Max → Simona Mertova/Martová (STK-017, spelling unresolved), Lexie → Tomáš Dudaško (STK-010, conflicts with the transcript's Martová/Mertová attribution). Also surfaced: **TD revisions**, a project stream not seen in any transcript, owned by Tomáš Burda (STK-025); and two initiatives — "Receiving compliants in stock" and "Invoicing solution" — both owned by Rudolf Zurek (STK-024), which may or may not be the same initiatives as Reklamace and Fakturace doprav respectively. Conflicts recorded but not reconciled — see ASM-006.

**Dev-side (BigHub) ownership map**, per Juraj Kmec (2026-09-02) — distinct from the business-side ownership above: e-commerce/order prediction → Juraj Kmec (STK-009); listing → Filip Černý (STK-006); logistics umbrella (reklamace + freight invoicing, believed to be one combined use case) → Jura Brázdil (STK-026, unconfirmed — conflicts with an earlier attribution to "Kuba Turner," see ASM-007); shared LLM platform infra/governance (not itself a use case) → William Gago (STK-027), with Lukáš Starenko (STK-028) and Honza Zelený (STK-029) also involved in unclear capacities.

### Order-Prediction Dashboard (Řízení poptávky)

| Field | Value |
|-------|-------|
| Definition | The e-commerce order/demand-prediction dashboard owned by Juraj Kmec. Static, read-only React frontend ("like Power BI") deliberately built with no interactivity so it can't break Dr. Max infra. Tracks two predicted metrics: (1) **Revenue** — plan/target vs. actual vs. model prediction with confidence intervals and a probability-of-hitting-target readout; (2) **Logistics** — predicted new order counts by warehouse and shipping method, with a "time travel" feature comparing a historical model run against actual outcomes. Both have a same-day zoomed view with ~30 min live-data delay. Deployed on Dr. Max infra, VPN-gated, no external repo access without a Dr. Max account. |
| Source | 2026-09-02-order-prediction-dashboard-walkthrough |
| Added | 2026-09-02 |
| Status | Active |

v1 considered done as of 2026-09-02; first live business demo 2026-09-03 (demoed by Juraj Kmec directly). Before this, the business had no live visibility — data was pulled manually from Excel exports ~2 days stale. No phase 2/3/4 roadmap defined yet; will be shaped after demo feedback and a 1-2 week trial by Marek Šimoník (STK-019, e-commerce lead).

### Axapta

| Field | Value |
|-------|-------|
| Definition | Dr. Max's legacy warehouse management system — a repurposed, warehouse-specific fork of Microsoft Dynamics. Relevant to the warehouse/claims automation stream, which requires custom-built APIs to integrate with it. |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-02-logistics-listing-team-sync |
| Added | 2026-09-01 |
| Last updated | 2026-09-02 |
| Status | Active |

Reklamace document flow (as of 2026-09-02): contract config in Axapta is complete; the system generates a PDF and stores it to Azure. Two distinct PDFs exist — **"rozvozový list"** (generated by BigHub) and **"návratka"** (generated by Accepta, client-side). Email-sending is the next unbuilt step — the plan is to pull the file from Azure and attach/send as a pre-filled draft (never auto-sent, see [[ASM-010]]); whether this calls the Microsoft Graph API's draft-creation endpoint directly is not yet specified.

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
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-logistics-listing-team-sync, 2026-09-02-aks-atlantis-infra-sync |
| Added | 2026-09-01 |
| Last updated | 2026-09-02 |
| Status | Needs confirmation |

Reklamace end-to-end testing (2026-09-02) surfaced a related cluster issue: a certificate only validates on one node pool, not others — temporarily worked around, needs a permanent fix. Also currently consuming much of Vladislav Tvarůžek's (STK-016) time, delaying Lukáš Starenko's (STK-028) environment access request.

Per a separate 2026-09-02 infra sync, access is actively closing out: node pools already exist, VPN address configuration underway, namespaces being corrected. Optimistic ETA today (2026-09-02) or tomorrow morning (2026-09-03); firewall/permission requests now take ~1 hour once submitted (down from ~2 weeks), owned by Dr. Max's Network Team. A separate item referred to as "AKSO" was mentioned alongside AKS in that sync — unclear whether it's a distinct workstream or a transcription artifact.

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
