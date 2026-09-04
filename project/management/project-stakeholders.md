---
last_updated: 2026-09-04
last_updated_by: auto — project-meeting routing (2026-09-04-ai-platform-standup-xmanager-lexi-demo)
owner: Marek Pillár
---

# Project Stakeholders

## Internal Team

### STK-001

| Field | Value |
|-------|-------|
| ID | STK-001 |
| Name | Marek Pillár |
| Aliases | — |
| Role | PM (sole user) |
| Location | -tbd- |
| Status | Active |
| Joined | 2026-09-01 |
| Left | — |
| Notes | Owner and sole user of this second brain. Works as a PM at BigHub. Formal role on the Dr. Max account: AI Analyst, working alongside Jindřich Tůma. Formally introduced to the ViaPharma logistics team on 2026-09-03 (previously introduced only to core Dr. Max/vendor contacts, 2026-09-01). On 2026-09-03, received a project handoff from Jura Brázdil (specs, technical docs, session logs) for MaxBuddy/chatbot/OCR — building a personal sub-repo/harness to process this material with Claude, echoing the "umbrella + per-project harnesses" architecture idea from 2026-09-02. Got partial VPN access working (MaxBuddy admin interface reachable; other resources still blocked) — fully resolved 2026-09-04. On 2026-09-04, scope explicitly confirmed as Dr. Max exclusively (at least the first month) — not the broader cross-client AI platform; owns the "Product Scope" X-Manager ticket from Kateřina Karlecová. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

### STK-002

| Field | Value |
|-------|-------|
| ID | STK-002 |
| Name | Jan Sovka |
| Aliases | Honza |
| Role | Original consultant / account owner-manager, Dr. Max (BigHub) — Marek's direct superior/line manager. ~10% allocated, escalation support. |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Onboarded Marek onto the Dr. Max account. Currently ~10% allocated to the account, aiming to increase involvement now that Marek is on board. Weekly 1:1s with Marek. Proposed a 5-supplier pilot approach for the reklamace supplier-data rollout (~4 hours, unblocks quickly before scaling to ~280 suppliers). Covering the 2026-09-03 logistics test session for Jindřich Tůma (out for a medical appointment) and recording it for later review. On 2026-09-03, ran the recurring BigHub↔ViaPharma logistics status call in Jindřich's/Alana's absence; owes Petr Sláma (STK-034) a concrete two-sided freight-invoicing timeline, and still hasn't closed his carried-forward task to talk to Jan Žižka about DHL overlap. Also attended the order-prediction dashboard live demo (2026-09-03) — proposed a three-layer review order (data accuracy → display/UX → model accuracy) and set phase-1 scope (Šimoník/Ondráček as primary users, a separate logistics contact deferred to a later phase). Present (mostly quiet) at the Max chatbot demo (2026-09-03). Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |

### STK-003

| Field | Value |
|-------|-------|
| ID | STK-003 |
| Name | Jindřich Tůma |
| Aliases | Jindra |
| Role | Marek's project manager on the Dr. Max account; new unified PM, BigHub↔Dr. Max coordination lead — ~half-time on-site |
| Location | -tbd- |
| Status | Active |
| Joined | 2026-08-18 (approx. — started "the previous week" per 2026-08-25 meeting) |
| Left | — |
| Notes | Holds the single coordination role spanning both BigHub and Dr. Max sides, replacing the previous split PM setup. Splits time ~50/50 between BigHub and Dr. Max. Works alongside Marek on account ownership (~30% Jindřich / ~70% Marek per Jan Sovka's framing). On 2026-09-02, proposed a VBS (work-breakdown-structure) framework for project detail tracking, agreed to simplify the business-facing roadmap sheet to Ideas/Active only, and pushed for specs to carry an explicit business-signed hypothesis + acceptance-criteria section before build starts. Still hasn't scheduled Marek's introduction to Tomáš Dudaško as of that date. Also reiterated the shared Kanban-platform plan (technical + business board, 15-20 min standups, target next week) in a separate 2026-09-02 team sync; out for a medical appointment the morning of 2026-09-03, with Jan Sovka (STK-002) covering the logistics test session in his place. Ran the order-prediction dashboard live demo with Marek Šimoník (2026-09-03), representing Alana/Lukáš Szücs on that workstream; owns sending dashboard access, deciding whether a shared platform can carry Dr. Max's feedback backlog (currently email), and scheduling an in-person follow-up at Dr. Max's site next week. Also ran the Max chatbot demo (2026-09-03) — asked that all X-Manager feature requests for Max/Lexie/Maxie route through Mertová as single point of contact; asked Mertová for lightweight business-case/time-savings metrics per initiative; committed to a weekly Thursday sync starting next week (testing results, tickets, first roadmap showing) and to fixing 3 blocking Lexie bugs by Tue/Wed. On 2026-09-04, finally got X-Manager access after "fighting for 10 days"; ran an internal ticket-triage stand-up (getting the priority-3 Lexie fixes moving same-day, ahead of the Tue/Wed estimate); flagged an urgent AKS node-pool cost issue with BDC; will call Mertová to align MVP/harmonogram terminology and check with Honza Sovka whether he retains cross-client AI-platform ownership vs. Marek owning Dr. Max only. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-jindrich-marek-introduction, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync, 2026-09-02-logistics-listing-team-sync, 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

### STK-004

| Field | Value |
|-------|-------|
| ID | STK-004 |
| Name | Alana Sihelská |
| Aliases | — |
| Role | Outgoing Project Manager (BigHub), Dr. Max account — ~1 month handover |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Previously carried most of the client-side PM burden on Dr. Max. Transitioning out of day-to-day ownership as Marek and Jindřich take over; handed off context to Marek (call completed). Source: 2026-08-25-marek-onboarding-with-jan-sovka |

### STK-005

| Field | Value |
|-------|-------|
| ID | STK-005 |
| Name | Ján Kabát |
| Aliases | Honza Kabát |
| Role | Head of Sales (BigHub) — key account owner @ Dr. Max |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Primary day-to-day sales contact with Tomáš Dudaško on the client side. Formally introduced Marek to Dr. Max client contacts on 2026-09-01. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-dr-max-business-sync, 2026-09-01-dr-max-x-bighub-project-status-sync |

### STK-006

| Field | Value |
|-------|-------|
| ID | STK-006 |
| Name | Filip Černý |
| Aliases | — |
| Role | Developer — logistics + listing streams (Dr. Max) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Flagged as needing more product-level input, especially on the listing stream, where he's already bringing informal product judgment. On 2026-09-02, led the reklamace end-to-end API test (positive result, one temporary certificate/nodepool workaround in place) and took a firm position that further Listing development is pointless until Dr. Max delivers the category/parameter system ("we'll just burn money for nothing"). On 2026-09-03, delivered a live demo of the reklamace mobile app to ViaPharma — well received; owns adding the "odběratel" (recipient) field to the reklamace API. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-dr-max-listing-introduction, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo |

### STK-007

| Field | Value |
|-------|-------|
| ID | STK-007 |
| Name | Jakub Turner |
| Aliases | Kuba Turner |
| Role | Developer — MaxBuddy, architecture/infrastructure, and reklamace-app backend (auth, Axapta integration) (Dr. Max) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Surname confirmed as Turner (2026-09-02) — resolves the "Kuba Turner" mentioned in the 2026-09-01 listing-intro note, originally misattributed to reklamace; confirmed working on MaxBuddy instead (see ASM-007, Decided 2026-09-02). Update 2026-09-03: PM confirmed Turner is also actively engaged in reklamace-app backend work (OAuth/Entra ID auth design, hardcoded test-login issuance, Axapta write integration) alongside Jura Brázdil's (STK-026) ownership — both are true; see ASM-007 amendment. Source: 2026-08-25-marek-onboarding-with-jan-sovka; identity confirmed 2026-09-02; role expanded 2026-09-03-viapharma-logistics-status-reklamace-demo |

### STK-008

| Field | Value |
|-------|-------|
| ID | STK-008 |
| Name | Lukáš |
| Aliases | — |
| Role | Developer — architecture/infrastructure (Dr. Max, BigHub-side) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Surname not yet known. Note: distinct person from Lukáš Szücs (STK-012), who is Dr. Max's own client-side Project Manager — same first name, different organization. Source: 2026-08-25-marek-onboarding-with-jan-sovka |

### STK-009

| Field | Value |
|-------|-------|
| ID | STK-009 |
| Name | Juraj Kmec |
| Aliases | — |
| Role | Data scientist — predictive model (Dr. Max, BigHub-side) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Owns the e-commerce predictive model; opportunity to extend into a fuller application. Order-prediction dashboard v1 is done as of 2026-09-02, demoing live to the business 2026-09-03; static React BI-style view with no interactivity, ~30 min data delay. Demo on 2026-09-03 to Marek Šimoník (STK-019) landed very well — a real 8-minute outage correctly showing as a dip validated the model live. Model trained purely on recognized revenue (tested blending order-backlog data, revenue-only performed better); reliable within a 14-day horizon, extrapolated and unguaranteed beyond that. Owns a small feature backlog (order-count toggle, D-7/D-365 historical overlay, split warehouse/method filters, tooltip clarity) and needs to verify model responsiveness to the current Brno order-backlog spike. Source: 2026-08-25-marek-onboarding-with-jan-sovka; surname resolved via Who's Who reference card, 2026-09-01-dr-max-x-bighub-project-status-sync; dashboard status from 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-order-prediction-dashboard-live-demo |

### STK-022

| Field | Value |
|-------|-------|
| ID | STK-022 |
| Name | Sony Vu Hong |
| Aliases | Soňa |
| Role | Marketing (BigHub) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Owns/could own an adoption newsletter highlighting Dr. Max wins — not her core job, described as somewhat reluctant, needs support. Marek is connecting with her on this. Resolves the name "Soňa" referenced in the still-unrouted 2026-09-01-dr-max-business-sync note. Source: 2026-09-01-dr-max-x-bighub-project-status-sync (Who's Who reference card) |

### STK-026

| Field | Value |
|-------|-------|
| ID | STK-026 |
| Name | Jura Brázdil |
| Aliases | — |
| Role | Developer — owns reklamace (complaints), freight invoicing (fakturace dopravy), MaxBuddy, Max chatbot, and a new OCR project (Dr. Max, BigHub-side) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Confirmed by Marek (2026-09-02) as owning both reklamace and freight invoicing. Resolves a conflict with the 2026-09-01 listing-intro note, which had named "Kuba Turner" as building reklamace — Turner is instead associated with MaxBuddy. See ASM-007 (Decided). On 2026-09-03, demoed the Max chatbot live to strong client praise (order status, pharmacy locator, e-recepty, medication lookup, all LLM-backed with a medical-advice guardrail); also owns MaxBuddy (oldest project — pharmacist upsell tool, originally a dosage-checking product until a medical-device certification requirement froze that feature) and a new early-stage OCR project (pharmacy equipment service-protocol extraction, targeting Dr. Max's November inspection cycle). Taking over the shared AI platform infrastructure from Viliam Gago (STK-027) once the new AKS sandbox is ready, migrating MaxBuddy and Lexie onto it. On 2026-09-04, flagged an urgent AKS node-pool cost issue (idle pools costing money, needs BDC cleanup or a cross-project node-selector redeploy); proposed the AI platform's frontend stay a standardized template by default, customized per client only on explicit request. Source: 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

### STK-027

| Field | Value |
|-------|-------|
| ID | STK-027 |
| Name | Viliam Gago |
| Aliases | William Gago (as referenced in the 2026-09-02 transcript), Vilo |
| Role | Shared LLM/AI platform infrastructure contact (BigHub) — the platform is reused across multiple clients (Brněnská komunikace, Kooperativa, Unica), not Dr. Max-exclusive |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Owns the shared LLM platform work — common backend/infra shared across the Dr. Max AI use cases, not itself a use case. Marek was added to the "Dr. Max LLM Platforma" chat during the 2026-09-02 call. Marek reached out to him 2026-09-02 — resolved. Separately, in a 2026-09-02 AKS/Atlantis infra sync, asked whether legacy PTU/model infrastructure was set up manually or via Terraform (relevant to potential redeployment) — nobody present had a confident answer. That meeting's source attendee data tagged him "EXT" (external) despite his BigHub-internal placement here — flagged as an open question, not yet reconciled. Per Jura Brázdil (2026-09-03): built the shared AI platform infrastructure currently hosting the chatbot's document-search use case; still developing the Lexie platform as of 2026-09-03 (X-Manager ticket status unclear even to Jura); upgraded the GPT model 5.1→5.4 on 2026-09-02; handing platform ownership to Jura once the new AKS sandbox is ready. On 2026-09-04, demoed the Lexie admin/RAG interface live; committed to same-day fixes for the thumbs-up/down overlap bug, the status-announcement banner, and the response-links deploy; his future role is loosely defined (possibly ad hoc/cluster-level support later) but not yet transitioning; needs to clean up and hand off platform documentation. Source: 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-02-aks-atlantis-infra-sync, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

### STK-040

| Field | Value |
|-------|-------|
| ID | STK-040 |
| Name | "Duri" (name uncertain) |
| Aliases | — |
| Role | Member of the BigHub Infrastructure Teams channel — described by Jura Brázdil as one of "everyone who's building something," alongside Jura and Viliam Gago (STK-027) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Low-confidence entry — single mention, no role detail beyond channel membership. Kept per PM instruction to route everything; needs verification. Source: 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

### Inactive

{Inactive internal team members}

## External Stakeholders

### STK-010

| Field | Value |
|-------|-------|
| ID | STK-010 |
| Name | Tomáš Dudaško |
| Aliases | — |
| Organization | Dr. Max (ČLH — Česká lékárna holding) |
| Role | Head of IT — holds the BigHub budget, primary approver of proposed projects/business cases |
| Location | -tbd- |
| Influence | High |
| Sentiment | Neutral |
| Sentiment context | Currently "a bit frosty" — has been paying for months without seeing enough visible delivered value; expects results now that several streams are nearing production. |
| Communication preference | -tbd- |
| Expectations | Business cases and ROI justification for proposed work; visible delivery |
| Last interaction | 2026-08-25 |
| Status | Active |
| Notes | Named Owner/Customer for MaxBuddy and Lexie on the BigHub roadmap sheet (2026-09-02). Confirmed 2026-09-02 as the IT/budget-side owner of Lexie, co-owning alongside Mertová (STK-017), who holds the operational/product side — not a conflict, see ASM-006 (partially resolved). Source: 2026-08-25-marek-onboarding-with-jan-sovka, roadmap sheet 2026-09-02; resolved 2026-09-02 |

### STK-011

| Field | Value |
|-------|-------|
| ID | STK-011 |
| Name | Luboš Vosmek |
| Aliases | — |
| Organization | Dr. Max |
| Role | Regional director (one of 3); internal champion for MaxBuddy |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Champion |
| Sentiment context | MaxBuddy was his idea to push; benefits (or loses) directly based on whether it delivers the promised cross-sell uplift. Leads an "expert group" of senior pharmacists/branch leads, receptive to hands-on prototype testing. Per Jura Brázdil (2026-09-03): warm relationship, positive on the analytics work so far; has enough standing to get the notoriously slow DVH team to resolve requests in a day when he escalates personally. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

### STK-012

| Field | Value |
|-------|-------|
| ID | STK-012 |
| Name | Lukáš Szücs |
| Aliases | — |
| Organization | Dr. Max CZE |
| Role | Project Manager |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral |
| Sentiment context | Thorough, collaborative, raises operational issues (outages, access blockers) matter-of-factly. Per Jura Brázdil (2026-09-03): nominally "PM core" for MaxBuddy, but characterized candidly as more of a CC'd/copied presence than an actively driving one. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Distinct from STK-008 "Lukáš" (BigHub developer) — same first name, different person/org. On 2026-09-03, confirmed the Jump Server access request (BigHub direct access to Dr. Max logs/Mongo) still has "definitely not moved" after ~1 month silence; agreed to add Lukáš Starenko (STK-028) to the "CZE AXE BOOM AI" Teams group per Filip Černý's request. On 2026-09-04, assigned to figure out a workable test-user/auth approach for the Lexie platform (local service account vs. AD group role management) — low priority, unresolved as of that date. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

### STK-013

| Field | Value |
|-------|-------|
| ID | STK-013 |
| Name | Tereza Foltová |
| Aliases | — |
| Organization | ViaPharma CZE (vendor) |
| Role | Handles logistics/claims data consolidation |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral |
| Sentiment context | Proactive, reassuring about not blocking BigHub; working through ~15 rows of supplier-specific data. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Supplier Excel for the reklamace rollout still expected Monday, per her earlier commitment (reconfirmed 2026-09-02). On 2026-09-03: consolidating ~120 suppliers into a single structure, working three-deep on it (including Jana, despite being on vacation); original 2026-09-07 deadline at risk given the manual-verification load — committed to a status update Monday 2026-09-08 (~80% clean estimate). Also coordinating with Dr. Max accounting to add an Axapta reference number and customer-vs-vendor distinction to the same data; staying in Excel for now rather than moving to a database. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo |

### STK-014

| Field | Value |
|-------|-------|
| ID | STK-014 |
| Name | Petr Spilka |
| Aliases | — |
| Organization | Dr. Max |
| Role | Head of Logistics CORE — owns Reklamace (claims) and Fakturace doprav (freight invoicing) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Reviewing the reworked freight-invoicing scope, expected mid-September. Source: 2026-09-01-dr-max-x-bighub-project-status-sync |

### STK-015

| Field | Value |
|-------|-------|
| ID | STK-015 |
| Name | Jan Žižka |
| Aliases | — |
| Organization | Dr. Max |
| Role | Head of Transport — owns Fakturace doprav (freight invoicing) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Agreed the freight-invoicing scope with Lukáš Szücs. Source: 2026-09-01-dr-max-x-bighub-project-status-sync |

### STK-016

| Field | Value |
|-------|-------|
| ID | STK-016 |
| Name | Vladislav Tvarůžek |
| Aliases | Vláďa; previously recorded as "Tvarušek" — corrected 2026-09-02 per official attendee data |
| Organization | Dr. Max / BDC infra |
| Role | Infrastructure access approvals (prostupy) |
| Location | Horoměřice |
| Influence | -tbd- |
| Sentiment | Champion |
| Sentiment context | Proactively working the AKS access blocker (node pools already exist, VPN config underway), openly attributing a ~2-day delay to a competing priority ("Planning Wizard") rather than deflecting. Jindřich explicitly thanked him for prioritizing BigHub's requests. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-02 |
| Status | Active |
| Notes | Handles access approvals blocking the order-prediction (AKS) and voicebot streams. As of 2026-09-02: optimistic ETA for AKS access is today or tomorrow morning (2026-09-03); firewall/permission requests now take ~1 hour once submitted (down from ~2 weeks), owned by the Network Team. Also chasing the Atlantis-side contact ("Tecl") for the voicebot's public IP/domain needs. Also BigHub's primary day-to-day infra contact for MaxBuddy specifically (per Jura Brázdil, 2026-09-03) — distinct from Martin Hrášek (STK-038), the higher-tier BDC escalation contact. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-aks-atlantis-infra-sync, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

### STK-017

| Field | Value |
|-------|-------|
| ID | STK-017 |
| Name | Mertová (Simona) |
| Aliases | Martová (mis-transcribed spelling from the 2026-09-01 status-sync transcript — Marek confirmed "Mertová" as correct, 2026-09-02) |
| Organization | Dr. Max |
| Role | Owns Maxie/Max chatbot project (per roadmap sheet); also described as co-owning Max/Maxie/Lexie with Tomáš Dudaško (STK-010) — Marek confirmed (2026-09-02) this is not a conflict: Dudaško holds the IT/budget-side ownership of Lexie, Mertová the operational/product ownership. |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | Agreed to a value-tracking column on the Max/Maxie/Lexie tables and to not block current chatbot deployment over the Brno design/logo tender. |
| Communication preference | -tbd- |
| Expectations | Asked (2026-09-03) to be the single point of contact for X-Manager feature requests on Max/Lexie/Maxie; owes lightweight business-case/time-savings metrics per initiative, due early next week. |
| Last interaction | 2026-09-04 |
| Status | Active |
| Notes | Surname spelling resolved 2026-09-02 (Mertová correct, "Martová" was a transcription error) and Lexie co-ownership with Dudaško confirmed as non-conflicting — see ASM-006 (partially resolved). Present at the 2026-09-03 Max chatbot demo (introduced as present; no clearly attributed lines in the transcript — see that meeting's Open Questions). On 2026-09-04, sent a message (via Kateřina Karlecová, STK-037) that mixed up a harmonogram document from Honza Sovka with a separate MVP-definition ask — Jindřich calling to align terminology directly; will send an invite for a Thursday sync covering all her streams (Max, Maxie, etc.). Source: 2026-09-01-dr-max-x-bighub-project-status-sync, roadmap sheet 2026-09-02, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo; resolved 2026-09-02 |

### STK-018

| Field | Value |
|-------|-------|
| ID | STK-018 |
| Name | Petr Machán |
| Aliases | — |
| Organization | Dr. Max IT |
| Role | Active Lexie user |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Champion |
| Sentiment context | Speaks highly of Lexie; IT-specific feature requests will be incorporated over time. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Source: 2026-09-01-dr-max-x-bighub-project-status-sync |

### STK-019

| Field | Value |
|-------|-------|
| ID | STK-019 |
| Name | Marek Šimoník |
| Aliases | — |
| Organization | Dr. Max |
| Role | Head of E-commerce — owns Řízení poptávky (order/demand prediction) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Champion |
| Sentiment context | Enthusiastic, unprompted praise for the order-prediction dashboard demo ("this is exactly what I wanted to see"); engages with substance (raised a real modeling question about revenue-vs-order-backlog dynamics) rather than surface-level feedback. Treats a correctly-flagged real outage in the live data as a strong trust signal. |
| Communication preference | -tbd- |
| Expectations | Wants dashboard numbers independently verifiable against Dr. Max's own source data before UX/model requests; comfortable with a 14-day-reliable forecast horizon as long as it's clearly scoped. |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Confirmed as Owner/Customer of "E-Shop order forecast" (= Řízení poptávky) on the BigHub roadmap sheet (2026-09-02) — clean match, no conflict. Saw the order-prediction dashboard live for the first time 2026-09-03 (moved up from the originally-expected 2026-09-04) — reception very positive; flagged a 2026-08-29 Brno marketing campaign the model doesn't yet account for, and will explore/test the dashboard over 1-2 weeks ahead of an in-person follow-up next week. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, roadmap sheet 2026-09-02, 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-order-prediction-dashboard-live-demo |

### STK-020

| Field | Value |
|-------|-------|
| ID | STK-020 |
| Name | Marie Hulešová |
| Aliases | — |
| Organization | Dr. Max |
| Role | Head of Quality — owns Reklamace (claims) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Source: 2026-09-01-dr-max-x-bighub-project-status-sync (Who's Who reference card) |

### STK-021

| Field | Value |
|-------|-------|
| ID | STK-021 |
| Name | Jan Maroušek |
| Aliases | — |
| Organization | Dr. Max |
| Role | Contact for Kontrola beden (crate/box control) — a not-yet-started project stream |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Flagged as "never actioned" — nobody has followed up with him yet on Kontrola beden. Source: 2026-09-01-dr-max-x-bighub-project-status-sync (Who's Who reference card) |

### STK-023

| Field | Value |
|-------|-------|
| ID | STK-023 |
| Name | Petr Neuman |
| Aliases | Neumann (spelling used in two prior meeting notes — roadmap sheet spells it "Neuman", treated as more authoritative) |
| Organization | Dr. Max |
| Role | Owner/Customer — Product listing |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Previously mentioned only as "pan Neumann" — handles all listings, reports to a bigger boss; positively received a proposed hierarchical listing-minimum structure but the category system itself is still undelivered client-side (main blocker to clean integration). Confirmed as the formal listing owner via the BigHub roadmap sheet (2026-09-02). Per Jindřich Tůma (2026-09-02), there is a second listing business owner alongside him — name not yet known; both are described as approachable and willing to explain things directly. Source: 2026-09-01-dr-max-listing-introduction, 2026-09-01-dr-max-x-bighub-project-status-sync, roadmap sheet 2026-09-02, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync |

### STK-024

| Field | Value |
|-------|-------|
| ID | STK-024 |
| Name | Rudolf Zurek |
| Aliases | — |
| Organization | Dr. Max |
| Role | Owner/Customer — "Receiving compliants in stock" and "Invoicing solution" (per BigHub roadmap sheet) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | New name, first seen on the 2026-09-02 roadmap sheet. Unresolved overlap with existing records: "Invoicing solution" may be the same initiative as Fakturace doprav (freight invoicing), currently attributed to Jan Žižka (STK-015, scope owner) and Petr Spilka (STK-014, reviewer); "Receiving compliants in stock" may be the same initiative as Reklamace (claims), currently attributed to Marie Hulešová (STK-020). Recorded both per PM instruction — not yet reconciled. See ASM-006. Source: roadmap sheet 2026-09-02 |

### STK-025

| Field | Value |
|-------|-------|
| ID | STK-025 |
| Name | Tomáš Burda |
| Aliases | — |
| Organization | Dr. Max |
| Role | Owner/Customer — "TD revisions" |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | "TD revisions" is a project stream not previously mentioned in any processed meeting — nature of the initiative unknown beyond the name. Source: roadmap sheet 2026-09-02 |

### STK-028

| Field | Value |
|-------|-------|
| ID | STK-028 |
| Name | Lukáš Starenko |
| Aliases | — |
| Organization | -tbd- |
| Role | -tbd- |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Owns CZ AI logistics — specifically reklamace (complaints) document generation, taking over from Kuba Turner (STK-007), who no longer has time for it. Working on the Axapta contract config (done) and PDF generation (done); email-draft sending step not yet built. Still lacks a working test/production environment (in progress with Vláďa Tvarůšek, STK-016) and Teams/Swagger-group access. Also active in the "Dr. Max LLM Platforma" chat alongside William Gago (STK-027) and Honza Zelený (STK-029) in an unclear capacity. Update 2026-09-03: confirmed as the "our Lukáš" Filip Černý asked Lukáš Szücs (STK-012) to add to the "CZE AXE BOOM AI" Teams group — likely the resolution path for his still-open Teams/Swagger-group access item. Source: 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo |

### STK-029

| Field | Value |
|-------|-------|
| ID | STK-029 |
| Name | Honza Zelený |
| Aliases | Jan Zeleny (as tagged in the 2026-09-02 Fireflies attendee data) |
| Organization | -tbd- |
| Role | Involved in the Atlantis/ElevenLabs voicebot telephony integration (raised SIP port and T-Mobile details) — technical involvement beyond the LLM-platform chat presence previously recorded |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-02 |
| Status | Active |
| Notes | Active in the "Dr. Max LLM Platforma" chat alongside William Gago (STK-027) and Lukáš Starenko (STK-028); exact role unknown, not even to Juraj Kmec. Also present in a separate 2026-09-02 AKS/Atlantis infra sync, tagged "EXT" in that meeting's attendee data, raising the Atlantis/ElevenLabs SIP integration topic — role still not fully clear (Dr. Max-side, Atlantis-side, or BigHub-side). Low-confidence entry overall — flagged during routing as thin, kept per PM instruction to route everything. Per Jura Brázdil (2026-09-03): building Maxie (the voicebot), sharing infrastructure with the Max chatbot — same core capability, voice instead of text. Source: 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-02-aks-atlantis-infra-sync, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |

### STK-030

| Field | Value |
|-------|-------|
| ID | STK-030 |
| Name | Jiří Jankovič (name uncertain — transcript quality low) |
| Aliases | — |
| Organization | -tbd- |
| Role | -tbd- — a developer Marek called during his dev-outreach round; topic reportedly "Vady" (possibly Vláďa Tvarušek/AKS access), unconfirmed |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Low-confidence entry — name and role both uncertain from a garbled transcript passage. Kept per PM instruction to route everything; needs verification. Source: 2026-09-02-logistics-listing-team-sync |

### STK-031

| Field | Value |
|-------|-------|
| ID | STK-031 |
| Name | Lukáš Síč (name transcribed inconsistently — possibly "Vachá") |
| Aliases | — |
| Organization | -tbd- |
| Role | Controls Teams/Swagger-sharing access for the reklamace project |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Low-confidence entry — name spelling uncertain. Lukáš Starenko (STK-028) was pointed to him by Filip Černý to request access. Source: 2026-09-02-logistics-listing-team-sync |

### STK-032

| Field | Value |
|-------|-------|
| ID | STK-032 |
| Name | Jan Kopecký |
| Aliases | — |
| Organization | ViaPharma CZE |
| Role | Technical contact for reklamace endpoint testing and Axapta/reklamace backend dev — OAuth/Entra ID auth planning, raised the Jump Server access topic |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Champion |
| Sentiment context | Described by Filip Černý as responsive — "reacts quickly and adjusts things." Confirmed the reklamace end-to-end test found/created the expected cases correctly (2026-09-02). On 2026-09-03, proactively flagged a likely Entra ID integration friction point early rather than let it surface later, and pushed to keep the stalled Jump Server request moving in parallel with other access work. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Full name and organization resolved 2026-09-03 (previously "Kopecký", org unknown). Source: 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo |

### STK-033

| Field | Value |
|-------|-------|
| ID | STK-033 |
| Name | Tecl |
| Aliases | — |
| Organization | Atlantis (vendor) |
| Role | Technical contact for public IP/network configuration on the Atlantis voicebot-telephony integration |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Low-confidence entry — single mention, surname only, not yet contacted. Vladislav Tvarůžek (STK-016) is chasing him to configure the public IP/domain the voicebot integration needs. Source: 2026-09-02-aks-atlantis-infra-sync |

### STK-034

| Field | Value |
|-------|-------|
| ID | STK-034 |
| Name | Petr Sláma |
| Aliases | — |
| Organization | ViaPharma CZE |
| Role | Technical/process contact — freight-invoicing dev-timeline alignment, reklamace-app testing coordination |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral (leaning Champion) |
| Sentiment context | Detail-oriented and collaborative; pushes for concrete two-sided timelines to avoid dev misalignment, but flexible on exact dates ("just sometime next week is fine"). Praised the reklamace app demo unprompted, called it clean and simple. His interest in per-user test logins is about Axapta-log traceability, not security. |
| Communication preference | -tbd- |
| Expectations | Wants a realistic, mutually-aligned dev timeline for freight invoicing so his team isn't left waiting or rushing to catch up. |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | New contact, first appearance 2026-09-03. Source: 2026-09-03-viapharma-logistics-status-reklamace-demo |

### STK-035

| Field | Value |
|-------|-------|
| ID | STK-035 |
| Name | Petr Ondráček |
| Aliases | — |
| Organization | Dr. Max |
| Role | Logistics-side contact for the order-prediction dashboard — co-primary user alongside Marek Šimoník (STK-019) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Joined the 2026-09-03 dashboard demo ~15 min in. Previously supplied a manual promo/campaign CSV (now ~2 months stale) and manually-pulled "created orders" figures before the dashboard existed. Owes a refreshed campaign/promo data file so the model can account for the 2026-08-29 Brno campaign. Source: 2026-09-03-order-prediction-dashboard-live-demo |

### STK-036

| Field | Value |
|-------|-------|
| ID | STK-036 |
| Name | "Honza" (name uncertain — first name only) |
| Aliases | — |
| Organization | Dr. Max — logistics |
| Role | Logistics-side contact with dashboard needs distinct from Šimoník/Ondráček's (wants a month-ahead view rather than day/14-day) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | Month-ahead visibility rather than the current day/14-day dashboard scope. |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Low-confidence entry — single mention by Jan Sovka, surname and identity not confirmed. Not clearly the same person as Jan Maroušek (STK-021, Kontrola beden) — needs verification before merging. Deliberately placed into a later phase (2/3/4) of the order-prediction dashboard rather than phase 1. Source: 2026-09-03-order-prediction-dashboard-live-demo |

### STK-037

| Field | Value |
|-------|-------|
| ID | STK-037 |
| Name | Kateřina "Kačka" Karlecová |
| Aliases | Kačka |
| Organization | Dr. Max — Call Center |
| Role | CC team member testing Lexie (Lucie); detailed bug reporter, active UX voice on the Max chatbot's feedback-mechanism design |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral (leaning engaged) |
| Sentiment context | Detail-oriented and constructive — well-documented bug reports (video evidence attached to X-Manager tickets), proactive UX opinions grounded in her own prior chatbot data (star/emoji ratings over free text, green→red color order), and explicit concern for her operators' experience (avoiding "panic" from over-broad status visibility). |
| Communication preference | -tbd- |
| Expectations | Wants the 3 blocking Lexie bugs fixed before her team resumes testing; wants feature requests centralized through Mertová rather than scattered. |
| Last interaction | 2026-09-04 |
| Status | Active |
| Notes | Low/medium-confidence attribution — most or all of the "CZ-BRN-TIT-CCManager" transcript tag's lines are attributed to her based on being explicitly named and asked to summarize the team's blocking bugs, but this may also include lines from Simona Mertová (STK-017), who was introduced as present but has no clearly separate attribution. On 2026-09-04, created the X-Manager "Product Scope" ticket (MVP/roadmap ask, now owned by Marek) and sent Jindřich a message that mixed up terminology between a harmonogram document and an MVP-definition ask. Source: 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

### STK-038

| Field | Value |
|-------|-------|
| ID | STK-038 |
| Name | Martin Hrášek |
| Aliases | — |
| Organization | Dr. Max / BDC infra |
| Role | Higher-tier infrastructure escalation contact — bigger tickets, more authority than day-to-day requests |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-03 |
| Status | Active |
| Notes | Distinct from Vladislav Tvarůžek (STK-016), who is the day-to-day MaxBuddy infra contact — Hrášek is the BDC-level escalation tier, per Jura Brázdil: "everything takes longer" at that level. Source: 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

### STK-039

| Field | Value |
|-------|-------|
| ID | STK-039 |
| Name | "Machata" (surname uncertain) |
| Aliases | — |
| Organization | Dr. Max — DVH (Data Warehouse) team |
| Role | DVH-team contact for database/data-warehouse change requests |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Blocker |
| Sentiment context | Per Jura Brázdil (2026-09-03): extremely inflexible and slow — a trivial one-column database change reportedly takes a week just to file as a ticket and 2-3 months to resolve, unless personally escalated through Luboš Vosmek (STK-011), in which case it's resolved the next day. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Low-confidence entry — single mention, surname uncertain from transcript. Kept per PM instruction to route everything; needs verification. Source: 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

### Inactive

{Inactive external stakeholders}

## Org Chart

-tbd-

---

## Entry Formats

### Internal Team Entry

| Field | Value |
|-------|-------|
| ID | STK-{NNN} |
| Name | {Full name} |
| Aliases | {Other names, nicknames — empty if none} |
| Role | {Project role} |
| Location | {City / country / timezone — `-tbd-` if unknown} |
| Status | Active |
| Joined | {YYYY-MM-DD} |
| Left | — |
| Notes | -tbd- |

### External Stakeholder Entry

| Field | Value |
|-------|-------|
| ID | STK-{NNN} |
| Name | {Full name} |
| Aliases | {Other names, nicknames — empty if none} |
| Organization | {Company or entity} |
| Role | {Project role} |
| Location | {City / country / timezone — `-tbd-` if unknown} |
| Influence | {High / Medium / Low — `-tbd-` if unknown} |
| Sentiment | {Champion / Neutral / Skeptic / Blocker — `-tbd-` if unknown} |
| Sentiment context | {Why this label — `-tbd-` if unknown} |
| Communication preference | {How they prefer to communicate — `-tbd-` if unknown} |
| Expectations | {What they care about — `-tbd-` if unknown} |
| Last interaction | {YYYY-MM-DD — `-tbd-` if unknown} |
| Status | Active |
| Notes | -tbd- |
