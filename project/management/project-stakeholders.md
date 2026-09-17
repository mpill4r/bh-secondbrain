---
last_updated: 2026-09-17
last_updated_by: auto — project-meeting routing (2026-09-17-lexie-max-maxie-weekly-sync)
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
| Notes | Owner and sole user of this second brain. Works as a PM at BigHub. Formal role on the Dr. Max account: AI Analyst, working alongside Jindřich Tůma. Formally introduced to the ViaPharma logistics team on 2026-09-03 (previously introduced only to core Dr. Max/vendor contacts, 2026-09-01). On 2026-09-03, received a project handoff from Jura Brázdil (specs, technical docs, session logs) for MaxBuddy/chatbot/OCR — building a personal sub-repo/harness to process this material with Claude, echoing the "umbrella + per-project harnesses" architecture idea from 2026-09-02. Got partial VPN access working (MaxBuddy admin interface reachable; other resources still blocked) — fully resolved 2026-09-04. On 2026-09-04, scope explicitly confirmed as Dr. Max exclusively (at least the first month) — not the broader cross-client AI platform; owns the "Product Scope" X-Manager ticket from Kateřina Kadlecová. On 2026-09-10, offered to run a short usability-testing session with the Dr. Max CC team to observe app usage directly and feed findings into the roadmap with Jura Brázdil — pending scheduling; also asked Mertová whether X-Manager could be reused by other Dr. Max streams (deferred by Jindřich pending Dudaško's DevOps environment project). On 2026-09-16, in an internal DevOps/Kanban status sync, gave a same-day Listing update: sent the spec to Jan Sovka for review (comments received, mostly minor per Marek's own read despite Sovka calling it significantly broken), and held an informal call with Petr Neuman agreeing to reconvene next week to properly kick off the project with domain expert Michaela Vdovicynová. Reiterated that the spec's real value is diagnosing why Listing has stalled since the start, not just documentation. Requested a short KPI-alignment check-in, deferred to a future session. On 2026-09-17, in the recurring Lexie/Max/Maxie weekly sync, reframed the Lexie design-feedback ask for Dr. Max directly ("we need your problem, not your solution") and took ownership of coordinating a follow-up design working session once Dr. Max's pain-point list arrives; also took the action to coordinate directly with "Míša"/Michal Machata (Prague) on X-Manager reuse for other Dr. Max streams. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-16-devops-kanban-rollout-status-sync, 2026-09-17-lexie-max-maxie-weekly-sync |

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
| Notes | Onboarded Marek onto the Dr. Max account. Currently ~10% allocated to the account, aiming to increase involvement now that Marek is on board. Weekly 1:1s with Marek. Proposed a 5-supplier pilot approach for the reklamace supplier-data rollout (~4 hours, unblocks quickly before scaling to ~280 suppliers). Covering the 2026-09-03 logistics test session for Jindřich Tůma (out for a medical appointment) and recording it for later review. On 2026-09-03, ran the recurring BigHub↔ViaPharma logistics status call in Jindřich's/Alana's absence; owes Petr Sláma (STK-034) a concrete two-sided freight-invoicing timeline, and still hasn't closed his carried-forward task to talk to Jan Žižka about DHL overlap. Also attended the order-prediction dashboard live demo (2026-09-03) — proposed a three-layer review order (data accuracy → display/UX → model accuracy) and set phase-1 scope (Šimoník/Ondráček as primary users, a separate logistics contact deferred to a later phase). Present (mostly quiet) at the Max chatbot demo (2026-09-03). Named 2026-09-07 as the intended sign-off reviewer for the consolidated AI portfolio/roadmap once it's finished (Alana Sihelská also flagged as having context from the original specs). On 2026-09-08, gave Marek and Jindřich the full history of BigHub's "AI platform": an ~1.5-year-old vision to sell it as a shared, white-labeled B2B product across clients, which never got internal traction and was formally killed ~4 months ago (~2026-05) in favor of fully custom per-client builds. Personally candid that this has been a "painful point" for him, but treats it as a closed chapter and is glad to see fresh investment. Flagged a sensitivity: the platform's Kooperativa deployment is built heavily around Kooperativa-specific needs, so care is needed that Kooperativa traces aren't visible if the platform is demoed to Dr. Max. Recommended Jindřich/Marek sync with Ján Kabát (STK-005) before further platform conversations with Tomáš Dudaško (STK-010), since Kabát shaped how Dudaško currently frames the ask. On 2026-09-10, reframed the reklamace UAT timeline for Petr Sláma (STK-034) to reduce anxiety — clarifying each timeline row maps to a specific feature scope, not full functionality — and facilitated the Fakturace doprav live demo to Jan Žižka (STK-015). Also active in the same-day Lexie/Max/Maxie weekly sync: clarified that Dr. Max-side Entra ID groups (not BigHub) control test-account permissions, and suggested a practical workaround (own-login browser window + anonymous/incognito window with the test account) for testers needing two roles simultaneously. Was expected to join the 2026-09-15 order-prediction dashboard follow-up ("měl by ještě Honza Sovka") but did not attend. On 2026-09-14, left detailed corrective comments on the Fakturace doprav roadmap board (relayed to Marek via screenshots 2026-09-16): clarified that Axapta — not the platform — owns the actual km comparison and deviation-flagging (platform only supplies data), proposed splitting "Kontrola kilometrů" into two tickets (ZOPV/OCR now, GPS Dozor later), corrected "Potvrzení řidiči" to "Potvrzení přepravci" (confirmation goes to the carrier, not the driver) and merged it with "Generování potvrzení o skenování," and cancelled the "Měsíční uzávěrka" item (routes now sent to Axapta continuously, Axapta decides closure timing) — see [[ASM-082]], [[ASM-083]], [[ASM-084]]. A 2026-09-16 direct codebase read independently confirmed all of these. Also flagged on 3 further cards initially missed and caught by the PM: "Kontrola údajů" is marked Done but only covers km — temperature-datalogger validation isn't built, splitting into 3 parts for Plná verze (ZOPV paper-slip presence check, electronic dataloggers via GPS Dozor, paper dataloggers directly, since ViaPharma can't guarantee a fast electronic transition) (see [[ASM-086]]); flagged that defining "km on the route" will need real experimentation (time vs. location); and flagged kiosk authentication as undecided pending a debate on 2026-09-17, leaning "no authentication" for now but floating the idea of knowing who scanned (driver / foreman covering multiple drivers / ViaPharma staffer / someone else) (see [[ASM-087]]) — Marek replied directly on both of the latter two threads (tracking the km-window question as an open item; scoping kiosk auth as a future extension, not a planned phase). Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-15-order-prediction-dashboard-follow-up, Fakturace doprav roadmap board comments (2026-09-14, relayed 2026-09-16) |

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
| Notes | Holds the single coordination role spanning both BigHub and Dr. Max sides, replacing the previous split PM setup. Splits time ~50/50 between BigHub and Dr. Max. Works alongside Marek on account ownership (~30% Jindřich / ~70% Marek per Jan Sovka's framing). On 2026-09-02, proposed a VBS (work-breakdown-structure) framework for project detail tracking, agreed to simplify the business-facing roadmap sheet to Ideas/Active only, and pushed for specs to carry an explicit business-signed hypothesis + acceptance-criteria section before build starts. Still hasn't scheduled Marek's introduction to Tomáš Dudaško as of that date. Also reiterated the shared Kanban-platform plan (technical + business board, 15-20 min standups, target next week) in a separate 2026-09-02 team sync; out for a medical appointment the morning of 2026-09-03, with Jan Sovka (STK-002) covering the logistics test session in his place. Ran the order-prediction dashboard live demo with Marek Šimoník (2026-09-03), representing Alana/Lukáš Szücs on that workstream; owns sending dashboard access, deciding whether a shared platform can carry Dr. Max's feedback backlog (currently email), and scheduling an in-person follow-up at Dr. Max's site next week. Also ran the Max chatbot demo (2026-09-03) — asked that all X-Manager feature requests for Max/Lexie/Maxie route through Mertová as single point of contact; asked Mertová for lightweight business-case/time-savings metrics per initiative; committed to a weekly Thursday sync starting next week (testing results, tickets, first roadmap showing) and to fixing 3 blocking Lexie bugs by Tue/Wed. On 2026-09-04, finally got X-Manager access after "fighting for 10 days"; ran an internal ticket-triage stand-up (getting the priority-3 Lexie fixes moving same-day, ahead of the Tue/Wed estimate); flagged an urgent AKS node-pool cost issue with BDC; will call Mertová to align MVP/harmonogram terminology and check with Honza Sovka whether he retains cross-client AI-platform ownership vs. Marek owning Dr. Max only. On 2026-09-09, reviewed Marek's plan for presenting the roadmap to Logistika/CC the next day and approved it, but flagged that MD-based phase estimates ("MVP in one man-day") are meaningless to non-technical stakeholders without a real calendar attached — asked for a simple timeline table (item + filled time-axis cells for testing/bugfix/rollout) before the presentations; also asked Marek to quantify business value in concrete numbers per initiative going forward (starting with CC), and will join Marek only for the first MaxBuddy domain-expert 1:1 to introduce a separate topic, leaving subsequent meetings to Marek solo. On 2026-09-10, ran a recurring ViaPharma sync that turned tense during reklamace UAT timeline negotiation with Petr Sláma (STK-034) — de-escalated well by repeatedly clarifying he wasn't pressuring a specific timeline and handing the parallel-vs-sequential testing decision back to the client; landed on an October 15-16 UAT start. Same day, ran the recurring Lexie/Max/Maxie weekly sync with the Dr. Max CC team: confirmed the thumbs-feedback bug fixed, committed to building a cross-project harmonogram (Lexie/Max/Maxie, weekly/workday granularity), committed to finding a Lexie design compromise with Jura pending the platform-wide design decision, and will follow up with Lukáš to clarify the stalled test-account ticket RITM0797678. On 2026-09-15, ran the order-prediction dashboard follow-up with Marek Šimoník/Petr Ondráček — proposed and landed formal "version 1" acceptance with a batched v2/v3 change-request cadence (see [[ASM-069]]); confirmed BigHub's coordination point of contact stays Lukáš Síč; owes Marek Pillár a follow-up on team capacity/prioritization across the e-commerce stream vs. other pipeline projects, not answered on the call. On 2026-09-16, rolled out a new Azure DevOps Kanban board across all projects (Epic=project/Story=requirement/Task=dev breakdown) as a lightweight internal-visibility layer — explicitly not full Scrum, Easy Project stays the time-tracking system of record; discovered an AI agent can interact with the board via Azure CLI. Ran a cross-project status walkthrough (Fakturace doprav, Reklamace, order prediction, Listing); has an open to-do to investigate whether Reklamace's warehouse-WiFi mobile access will work equivalently to today's VPN-based testing, and to send a formal network-access request to Dr. Max; planning an internal review sync with Jan Sovka around 2026-09-28 ahead of the 2026-09-29 Marek Šimoník sync. On 2026-09-17, ran the recurring Lexie/Max/Maxie weekly sync: reviewed the new cross-project timeline (Kadlecová flagged an unresolved MVP-vs-full-product scoping mismatch), triaged a large batch of Max chatbot bug fixes, and negotiated the go-live date with Mertová — held firm that BigHub would target its 3 internal deployment phases by end of September while accepting her end-of-October public-launch target rather than pushing back. Opened a GDPR-consent ticket for the Max chatbot pending Lenka Henichová's (DPO) input, and committed to filing a BDC ticket for 4 separate (non-2FA) Lexie test accounts. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-jindrich-marek-introduction, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync, 2026-09-02-logistics-listing-team-sync, 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-09-logistics-cc-roadmap-presentation-prep, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-15-order-prediction-dashboard-follow-up, 2026-09-16-devops-kanban-rollout-status-sync, 2026-09-17-lexie-max-maxie-weekly-sync |

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
| Notes | Previously carried most of the client-side PM burden on Dr. Max. Transitioning out of day-to-day ownership as Marek and Jindřich take over; handed off context to Marek (call completed). On 2026-09-16, stood in for Jindřich Tůma (out that day) to run a TEO/OCR technical sync with Dr. Max — arranged local recording via Tomáš Burda's account since she couldn't record from her own, and handled scheduling for the next sync. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-16-teo-ocr-technical-sync-pilot-results |

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
| Notes | Primary day-to-day sales contact with Tomáš Dudaško on the client side. Formally introduced Marek to Dr. Max client contacts on 2026-09-01. Originally delivered the "no shared roadmap" message to Dudaško once BigHub's internal shared-platform vision was dropped (~2026-05), which shaped how Dudaško now frames his AI-platform investment ask. Jan Sovka flagged (2026-09-08) that Jindřich/Marek should sync with him before further platform conversations with Dudaško, to avoid conflicting messaging. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-dr-max-business-sync, 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-08-ai-platform-strategy-history-with-jan-sovka |

### STK-006

| Field | Value |
|-------|-------|
| ID | STK-006 |
| Name | Filip Černý |
| Aliases | — |
| Role | Developer — designated dev owner for Reklamace (per PM decision, 2026-09-08); also logistics + listing streams (Dr. Max) |
| Location | -tbd- |
| Status | Active |
| Joined | -tbd- |
| Left | — |
| Notes | Flagged as needing more product-level input, especially on the listing stream, where he's already bringing informal product judgment. On 2026-09-02, led the reklamace end-to-end API test (positive result, one temporary certificate/nodepool workaround in place) and took a firm position that further Listing development is pointless until Dr. Max delivers the category/parameter system ("we'll just burn money for nothing"). On 2026-09-03, delivered a live demo of the reklamace mobile app to ViaPharma — well received; owns adding the "odběratel" (recipient) field to the reklamace API. In the 2026-09-07 portfolio review, described Reklamace dev work as currently split between himself, Jakub Turner (STK-007), and Lukáš Starenko (STK-028); named 2026-09-08 by Marek as the designated single dev owner going forward — see [[ASM-007]]. On 2026-09-10, demoed the Fakturace doprav kiosk portal internally then live to the client (Jan Žižka, STK-015) — got a major architecture correction from Žižka (Axapta owns all route/document state, not the app — see ASM-053), which he said genuinely simplifies his design; several open questions resolved (POPLSOL document type, confirmation-screen scope, kiosk hardware). Also raised his own list of business questions for the client (stamp validation, cross-document-context OCR) — largely resolved by Žižka revealing an independent ViaPharma initiative to standardize the ZOPV form. On 2026-09-16 (transcript originally misattributed to Alana Sihelská, corrected by PM during routing): actively updating the Fakturace doprav Swagger spec (~9 sub-tasks collapsing into one deliverable); defining local document-storage structure ahead of wiring in a container (infra-ready, not yet done); confirmed document-versioning is out of scope on BigHub's side — Axapta owns it, BigHub just forwards new scans with a version flag; access-rights/read-write storage tested and confirmed working with Jan Kopecký (STK-032), carrying over identically to Reklamace; coordinating the Boomy integration (mostly Boomy-side, Filip's piece is the Swagger handoff); touched the Axapta integration lightly with Petr Sláma (notably open to the proposed changes) and Jan Kopecký (fully on board). Also flagged that the Reklamace mobile app's real-world warehouse-WiFi network access (vs. today's VPN-based testing) is genuinely unconfirmed. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-01-dr-max-listing-introduction, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-16-devops-kanban-rollout-status-sync |

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
| Notes | Surname confirmed as Turner (2026-09-02) — resolves the "Kuba Turner" mentioned in the 2026-09-01 listing-intro note, originally misattributed to reklamace; confirmed working on MaxBuddy instead (see ASM-007, Decided 2026-09-02). Update 2026-09-03: PM confirmed Turner is also actively engaged in reklamace-app backend work (OAuth/Entra ID auth design, hardcoded test-login issuance, Axapta write integration) alongside Jura Brázdil's (STK-026) ownership — both are true; see ASM-007 amendment. On 2026-09-10, active in both halves of the ViaPharma sync — pushed back on Petr Sláma's (STK-034) testing-timeline concerns with a clear feature-by-feature testing model, and in the Fakturace doprav demo consistently raised the open-kiosk security/LLM-injection risk (see ASM-052) that document-type validation alone doesn't solve. On 2026-09-16, working on Reklamace OAuth — received OAuth server details from an unnamed external Boomy-side contact, needs to implement and test; agreed with Petr Sláma not to let this block warehouse testing, deploying only once tested on-site. Flagged a still-open question on CERT/email-registration status needed for the Reklamace mailbox app, to raise with infra. Source: 2026-08-25-marek-onboarding-with-jan-sovka; identity confirmed 2026-09-02; role expanded 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-16-devops-kanban-rollout-status-sync |

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
| Notes | Owns the e-commerce predictive model; opportunity to extend into a fuller application. Order-prediction dashboard v1 is done as of 2026-09-02, demoing live to the business 2026-09-03; static React BI-style view with no interactivity, ~30 min data delay. Demo on 2026-09-03 to Marek Šimoník (STK-019) landed very well — a real 8-minute outage correctly showing as a dip validated the model live. Model trained purely on recognized revenue (tested blending order-backlog data, revenue-only performed better); reliable within a 14-day horizon, extrapolated and unguaranteed beyond that. Owns a small feature backlog (order-count toggle, D-7/D-365 historical overlay, split warehouse/method filters, tooltip clarity) and needs to verify model responsiveness to the current Brno order-backlog spike. On 2026-09-15, ran a detailed client feedback session with Marek Šimoník and Petr Ondráček — delivered the previously-backlogged T-7/T-364 historical comparison feature live, took on roughly 10 new feature requests (mobile/non-VPN access, budget/forecast/predikce unified view, warehouse-level reservation breakdown, a "Metrix" redesign for reservations vs. delivery method, Business Overview polish), and agreed the current build stands as formally accepted "version 1" (see [[ASM-069]]). Confirmed the "predikce" naming convention going forward (see [[ASM-070]]). On 2026-09-16 (transcript originally misattributed to Alana Sihelská, corrected by PM during routing): confirmed order-prediction scope is on track, with extra runway since Marek Šimoník is on vacation the following week; the one meaningfully-sized remaining item is Marketplace aggregation (not blocked, just larger). Invited to a same-day 4pm infra sync to raise mobile/non-VPN access questions, though uncertain of the full scope beforehand. Source: 2026-08-25-marek-onboarding-with-jan-sovka; surname resolved via Who's Who reference card, 2026-09-01-dr-max-x-bighub-project-status-sync; dashboard status from 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-15-order-prediction-dashboard-follow-up, 2026-09-16-devops-kanban-rollout-status-sync |

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
| Notes | Confirmed by Marek (2026-09-02) as owning both reklamace and freight invoicing. Resolves a conflict with the 2026-09-01 listing-intro note, which had named "Kuba Turner" as building reklamace — Turner is instead associated with MaxBuddy. See ASM-007 (Decided). On 2026-09-03, demoed the Max chatbot live to strong client praise (order status, pharmacy locator, e-recepty, medication lookup, all LLM-backed with a medical-advice guardrail); also owns MaxBuddy (oldest project — pharmacist upsell tool, originally a dosage-checking product until a medical-device certification requirement froze that feature) and a new early-stage OCR project (pharmacy equipment service-protocol extraction, targeting Dr. Max's November inspection cycle). Taking over the shared AI platform infrastructure from Viliam Gago (STK-027) once the new AKS sandbox is ready, migrating MaxBuddy and Lexie onto it. On 2026-09-04, flagged an urgent AKS node-pool cost issue (idle pools costing money, needs BDC cleanup or a cross-project node-selector redeploy); proposed the AI platform's frontend stay a standardized template by default, customized per client only on explicit request. On 2026-09-08, gave the technical reality check on the platform's current state: in practice it's just one RAG/document-retrieval product, MaxBuddy still isn't in it (blocked on the new AKS since early August), and today's shared setup has a shared DB with no isolation between use cases plus a single shared admin account. Confirmed the existing role-based permission system is Lexie-specific, not platform-wide. Plans to self-migrate MaxBuddy and Max Chatbot into the platform once the new AKS lands and unify its UX around a single "crossroads" landing page; also wants a standard changelog convention for platform pull requests. Confirmed he has some spare capacity for this work and expects it to help rather than purely cost him, since he's migrating his own projects into it anyway. On 2026-09-10, demoed a live (VPN-gated) Max chatbot test environment with mocked sample test scenarios (not yet wired to production data); confirmed he maintains a near-complete internal platform documentation doc (screenshots + descriptions) and will finish and send it out; agreed to open a Lexie design-compromise ticket with Jindřich, explaining the platform-wide design-consolidation plan (centralize all Dr. Max apps under one entry point first, unify per-app design afterward); committed to researching whether a shared, multi-group test account with an in-app role switcher can support concurrent multi-tester use without conflicts. On 2026-09-16, ran a blind validation of the TEO/OCR pipeline against a real, untouched 2025 dataset (140 protocols, 2 pilot vendors) — results a few points above prior benchmarks, though he cautioned some of that may be luck; caught and is investigating 2 new bugs Michaela Albrechtová (STK-042) flagged (duplicated defects-text field, one unflagged genuine error) plus a known missing-address extraction failure and bounding-box crop imprecision. Migrating the platform project to new AKS node pools and self-provisioning Blob storage for a TEST environment — explicitly confirmed this needs no BDC/infra-team involvement to create (see [[ASM-088]]). Open to expanding the autumn pilot to a 3rd vendor if Dr. Max sends samples, given his pipeline is now reusable (~1 day of work per new vendor, see [[ASM-089]]). On 2026-09-17, in the Lexie/Max/Maxie weekly sync, proactively built an in-app "pseudo-ticket" view surfacing every feedback-form submission (addressing a duplicate-testing complaint raised 2026-09-10); walked through fixes for 7 pharmacy-location-search bugs, a Paralen stock-lookup false negative, a false call-transfer claim, and a city/district-recognition issue (upgraded the underlying model GPT-5.1→GPT-5.4, switched to fuzzy/syllable-based matching); confirmed nothing is stored server-side today (conversations live only in-browser). Laid out a 3-phase go-live plan (prod backend connection → BDC security clearance, hidden → public toggle) targeting end of September for BigHub's side, while accepting Mertová's end-of-October public date. Asked Dr. Max to write a first-person "tone brief" for the chatbot's prompt. Dropped off the call before the end (missed the final Lexie bug reports). Source: 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil, 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-16-teo-ocr-technical-sync-pilot-results, 2026-09-17-lexie-max-maxie-weekly-sync |

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
| Notes | Owns the shared LLM platform work — common backend/infra shared across the Dr. Max AI use cases, not itself a use case. Marek was added to the "Dr. Max LLM Platforma" chat during the 2026-09-02 call. Marek reached out to him 2026-09-02 — resolved. Separately, in a 2026-09-02 AKS/Atlantis infra sync, asked whether legacy PTU/model infrastructure was set up manually or via Terraform (relevant to potential redeployment) — nobody present had a confident answer. That meeting's source attendee data tagged him "EXT" (external) despite his BigHub-internal placement here — flagged as an open question, not yet reconciled. Per Jura Brázdil (2026-09-03): built the shared AI platform infrastructure currently hosting the chatbot's document-search use case; still developing the Lexie platform as of 2026-09-03 (X-Manager ticket status unclear even to Jura); upgraded the GPT model 5.1→5.4 on 2026-09-02; handing platform ownership to Jura once the new AKS sandbox is ready. On 2026-09-04, demoed the Lexie admin/RAG interface live; committed to same-day fixes for the thumbs-up/down overlap bug, the status-announcement banner, and the response-links deploy; his future role is loosely defined (possibly ad hoc/cluster-level support later) but not yet transitioning; needs to clean up and hand off platform documentation. On 2026-09-17, in the Lexie/Max/Maxie weekly sync, was asked about a Lexie fallback-message bug (the "second," no-source-found message never seems to trigger for testers) but wasn't certain of the answer live — to file a ticket and investigate. Source: 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-02-aks-atlantis-infra-sync, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-17-lexie-max-maxie-weekly-sync |

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
| Notes | Named Owner/Customer for MaxBuddy and Lexie on the BigHub roadmap sheet (2026-09-02). Confirmed 2026-09-02 as the IT/budget-side owner of Lexie, co-owning alongside Mertová (STK-017), who holds the operational/product side — not a conflict, see ASM-006 (partially resolved). On 2026-09-08, asked (via Jindřich) for visible investment in the AI platform — unified test/prod environments, improved UX/visual polish, and consolidation of all Dr. Max BigHub projects onto it. Sat down with an AI assistant to draft a large requirements Excel, which both Jan Sovka and Marek independently assessed as ~70% governance/compliance-framed and not addressing actual use cases. Near-term interest is dependency visibility, cost visibility, and usage metrics rather than governance minutiae. Source: 2026-08-25-marek-onboarding-with-jan-sovka, roadmap sheet 2026-09-02; resolved 2026-09-02, 2026-09-08-ai-platform-strategy-history-with-jan-sovka |

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
| Sentiment context | MaxBuddy was his idea to push; benefits (or loses) directly based on whether it delivers the promised cross-sell uplift. Leads an "expert group" of senior pharmacists/branch leads, receptive to hands-on prototype testing. Per Jura Brázdil (2026-09-03): warm relationship, positive on the analytics work so far; has enough standing to get the notoriously slow DVH team to resolve requests in a day when he escalates personally. On 2026-09-17, in the first MaxBuddy Business Quantification interview, came across as unusually candid and self-correcting — refused to round up an uncertain revenue figure, proactively vetoed an employee-satisfaction value claim before Marek could propose it, and corrected Marek's own assumption about domain-expert roles unprompted. |
| Communication preference | -tbd- |
| Expectations | Wants a molecule/group coverage-visibility dashboard (red/blue/yellow status) — currently "blind" to which groups are configured and working, surfaced by a ~14-day undetected data-feed outage. Has a broader MaxBuddy scope-expansion wishlist to send separately. |
| Last interaction | 2026-09-17 |
| Status | Active |
| Notes | Business owner of MaxBuddy **without budget** — IT/budget authority sits with Tomáš Dudaško (STK-010). Domain-expert responsibilities on his side split between Lukáš Sýč (functionality/decisions/escalation — bridges BigHub, Farmy, BDC, and Vosmek) and Jiří Trajer (STK-049, data-feed only via Power BI, not involved in feature decisions) — see [[ASM-097]], [[ASM-098]], [[ASM-099]]. Gave a JTBD origin story explaining MaxBuddy's dosage-checking-to-upsell pivot was driven partly by a need to build pharmacy-staff trust before introducing "AI," and stated the current live upsell feature is data/rule-based rather than LLM-driven. Source: 2026-08-25-marek-onboarding-with-jan-sovka, 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-17-business-quantification-maxbuddy-vosmek |

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
| Name | Tereza Foltýnová |
| Aliases | — |
| Organization | ViaPharma CZE (vendor) |
| Role | Handles logistics/claims data consolidation |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral |
| Sentiment context | Proactive, reassuring about not blocking BigHub; working through ~15 rows of supplier-specific data. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-15 |
| Status | Active |
| Notes | Name corrected 2026-09-11 from "Tereza Foltová" to "Tereza Foltýnová" per PM (surfaced via a Jindřich Tůma message referencing an upcoming Monday meeting with her on AI initiatives). Supplier Excel for the reklamace rollout still expected Monday, per her earlier commitment (reconfirmed 2026-09-02). On 2026-09-03: consolidating ~120 suppliers into a single structure, working three-deep on it (including Jana, despite being on vacation); original 2026-09-07 deadline at risk given the manual-verification load — committed to a status update Monday 2026-09-08 (~80% clean estimate). Also coordinating with Dr. Max accounting to add an Axapta reference number and customer-vs-vendor distinction to the same data; staying in Excel for now rather than moving to a database. Confirmed 2026-09-09 as the primary requester behind the 2026-09-10 Logistika roadmap walkthrough — reklamace scope is expected to largely match what she asked for. On 2026-09-10, still consolidating the supplier Excel with Jana Egrmaierová (STK-044, ViaPharma) — data across 3-4 source tables doesn't fully reconcile yet; targeting a demo to Filip Černý (STK-006) next Tuesday, wants a short session with him specifically rather than a broader walkthrough. On 2026-09-15, ran the first live Business Quantification interview with Marek Pillár, covering Reklamace and Fakturace doprav — gave detailed, well-grounded JTBD answers and pushed back on her own initiative's inflated savings estimate rather than accepting it (see [[ASM-072]]); requested naming clarity on the roadmap (domain qualifiers matching the Core/Ecom convention), which incidentally helped resolve part of [[ASM-006]]; only covered 2 of ~11 prepped initiatives before running out of time, unavailable from Friday. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-02-logistics-listing-team-sync, 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-09-logistics-cc-roadmap-presentation-prep, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-15-business-quantification-reklamace-fakturace-doprav |

### STK-014

| Field | Value |
|-------|-------|
| ID | STK-014 |
| Name | Petr Spilka |
| Aliases | — |
| Organization | Dr. Max |
| Role | Head of Logistics CORE — owns Reklamace (claims); reviews Fakturace doprav scope (freight invoicing owned by Jan Žižka, STK-015 — see [[ASM-006]]) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Reviewing the reworked freight-invoicing scope, expected mid-September. Confirmed 2026-09-15 (via Tereza Foltýnová, ViaPharma) as Reklamace's owner and tentative domain expert, pending his own confirmation — Jana Egrmaierová (STK-044) floated as a possible alternative domain expert. Role description narrowed from "owns Reklamace and Fakturace doprav" to "owns Reklamace, reviews Fakturace doprav" given today's call reinforced Jan Žižka as the actual Fakturace doprav owner. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-15-business-quantification-reklamace-fakturace-doprav |

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
| Notes | Agreed the freight-invoicing scope with Lukáš Szücs. Also named 2026-09-07 as the contact for Fakturace od dodavatelů (supplier invoicing) — Filip Černý has never spoken with him directly and is unsure of his seniority/hierarchy; that area is still very early ("in diapers"). Possible overlap/confusion between the two "fakturace" streams (freight vs. supplier invoicing) not yet fully disentangled. On 2026-09-10, first substantive engagement — attended Filip Černý's live Fakturace doprav kiosk demo and gave clear, opinionated, largely positive feedback: confirmed open/no-login kiosk access is fine, rejected an optional driver-notes field, wants specific missing-page numbers in the confirmation table, and delivered a major architecture clarification that Axapta (not the app) owns all route/document state (see ASM-053) — a correction that resolved real confusion on Filip's side and simplified the design. Also revealed an independent ViaPharma initiative (with Petr Sláma, STK-034) to build a new standardized, pre-filled ZOPV form that should eliminate most of the illegible-handwriting problem at the source. Has no personal visibility into kiosk hardware procurement and flagged an internal ownership gap on his side. Reinforced 2026-09-15 (via Tereza Foltýnová, ViaPharma, in the Business Quantification call) as the owner/domain expert for the roadmap's "fakturace od dodavatelů" line — which she described as actually the transport/freight initiative, matching Fakturace doprav rather than a separate supplier-invoicing stream (see [[ASM-006]]); hasn't seen the quantification tracker yet as of that call. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-15-business-quantification-reklamace-fakturace-doprav |

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
| Expectations | Asked (2026-09-03) to be the single point of contact for X-Manager feature requests on Max/Lexie/Maxie; owes lightweight business-case/time-savings metrics per initiative, due early next week. On 2026-09-17, owes an agent/FTE cost rate and Kateřina Kadlecová's domain-expert successor name, both due 2026-09-18. |
| Last interaction | 2026-09-17 |
| Status | Active |
| Notes | Surname spelling resolved 2026-09-02 (Mertová correct, "Martová" was a transcription error) and Lexie co-ownership with Dudaško confirmed as non-conflicting — see ASM-006 (partially resolved). Present at the 2026-09-03 Max chatbot demo (introduced as present; no clearly attributed lines in the transcript — see that meeting's Open Questions). On 2026-09-04, sent a message (via Kateřina Kadlecová, STK-037) that mixed up a harmonogram document from Honza Sovka with a separate MVP-definition ask — Jindřich calling to align terminology directly; will send an invite for a Thursday sync covering all her streams (Max, Maxie, etc.). On 2026-09-10, clearly attributed with substantial speaking lines for the first time (previous transcripts left her mostly unattributed): asked about design quality (Lexie vs. Max), laid out her team's 4-round phased testing plan (CC colleagues now → shadow a live operator → supervisors → wider user base), and drove most of the test-account/role-switching discussion — her team spans 4 CC sub-departments each needing a distinct document-access scope. Still can't locate the original test-account ticket (RITM0797678), which was reassigned away from her. On 2026-09-17, in the first direct Business Quantification interview covering all three CC initiatives, confirmed as business owner of Max chatbot/Maxie/Lexie; gave solid JTBD framing for each and consistently pushed back against framing any of the three as FTE/headcount savings — call volume is fixed regardless of chatbot/voicebot/Lexie adoption, so value is coverage/capacity and reduced agent cognitive load instead. Explicitly resisted turning Lexie's ~30 min/day time-savings estimate into a cost-cutting narrative, worried aloud it could be misused to justify headcount cuts on her team. Revised Maxie's containment-rate target down live on the call from an initial 90% to a 50/50 placeholder after Marek flagged it as unrealistic for a first version. Disclosed that Kateřina Kadlecová (STK-037), her most engaged domain expert across all three initiatives, is departing on maternity leave with no successor yet named — see [[ASM-091]]. Also on 2026-09-17, in the recurring Lexie/Max/Maxie weekly sync (separate from the Business Quantification interview above), held a firm line on the Max chatbot go-live date — wants end of October for public launch, explicitly prioritizing testing thoroughness over speed ("jakmile to nebude dobře udělané, tak jsme si vykopali vlastní hrob"), and wants a quiet/soft launch with no active promotion until the tool is fully mature. Confirmed she tracks call-desk contact-reason volume but expects the chatbot to mostly add throughput capacity rather than reduce total call volume — sees the separate Voicebot project as the bigger lever for genuinely offloading live agents. Accepted BigHub's fallback plan of 4 separate (non-2FA) Lexie test accounts over the in-app role-switcher. Source: 2026-09-01-dr-max-x-bighub-project-status-sync, roadmap sheet 2026-09-02, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-17-business-quantification-cc-max-maxie-lexie, 2026-09-17-lexie-max-maxie-weekly-sync; resolved 2026-09-02 |

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
| Last interaction | 2026-09-15 |
| Status | Active |
| Notes | Confirmed as Owner/Customer of "E-Shop order forecast" (= Řízení poptávky) on the BigHub roadmap sheet (2026-09-02) — clean match, no conflict. Saw the order-prediction dashboard live for the first time 2026-09-03 (moved up from the originally-expected 2026-09-04) — reception very positive; flagged a 2026-08-29 Brno marketing campaign the model doesn't yet account for, and will explore/test the dashboard over 1-2 weeks ahead of an in-person follow-up next week. On 2026-09-15, brought detailed written feedback to a structured follow-up session — data grouping, terminology (predikce vs. budget/forecast, see [[ASM-070]]), mobile access — and formally accepted the current build as "version 1" (see [[ASM-069]]). Explained that pharmacy reservations are a deliberate strategic e-commerce differentiator for Dr. Max, not just another channel (see [[ASM-071]]); flagged a request for a separate session with Marek Pillár to recap business value/KPIs, to be scheduled (likely Friday). Out the week of 2026-09-21 (full week off). Source: 2026-09-01-dr-max-x-bighub-project-status-sync, roadmap sheet 2026-09-02, 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-15-order-prediction-dashboard-follow-up |

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
| Notes | Flagged as "never actioned" — nobody has followed up with him yet on Kontrola beden. **Possible identity match (2026-09-15, unconfirmed)**: the 2026-09-15 order-prediction dashboard follow-up repeatedly references a "Honza/Jan Maroušek" who plans warehouse staffing (Nučice, Brno) based on reservation/pickup volume — plausibly the same person as this record, and/or the same as STK-036 ("Honza," a low-confidence logistics contact from 2026-09-03 with a similar profile). Not explicitly confirmed on either call — flagged for PM verification rather than merged. Source: 2026-09-01-dr-max-x-bighub-project-status-sync (Who's Who reference card), 2026-09-15-order-prediction-dashboard-follow-up |

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
| Sentiment | Champion |
| Sentiment context | Warm and candid on first direct contact with Marek (2026-09-16) — self-critical about the state of the listing process rather than defensive, pushed back constructively rather than accepting an unfounded KPI number, and visibly relieved by being told it's OK not to know every figure off the top of his head. Tone sharpened with genuine urgency describing Magento's instability — "if we'd had this yesterday, I'd be thrilled — and yesterday was already late for me" [translated from Czech]. |
| Communication preference | Prefers first-name terms ("Petr," not the more formal "Neumann/Neuman"). |
| Expectations | Wants the listing team moved entirely out of day-to-day Magento use (batch import ~biweekly instead); values realistic, non-inflated numbers over invented precision — explicitly declined to commit to a KPI figure he couldn't stand behind. |
| Last interaction | 2026-09-16 |
| Status | Active |
| Notes | Previously mentioned only as "pan Neumann" — handles all listings, reports to a bigger boss; positively received a proposed hierarchical listing-minimum structure but the category system itself is still undelivered client-side (main blocker to clean integration). Confirmed as the formal listing owner via the BigHub roadmap sheet (2026-09-02). Per Jindřich Tůma (2026-09-02), there is a second listing business owner alongside him — name not yet known; both are described as approachable and willing to explain things directly. On 2026-09-16, in the first direct Marek↔Neuman call (Business Quantification/Discovery kickoff), gave a well-grounded JTBD origin story: he inherited the listing problem when he joined his role at the start of 2026. Reframed the initiative's primary driver — the original "poor supplier data quality" problem is now secondary to Magento's growing instability at Dr. Max's ~80-100k SKU scale (frequent save failures/timeouts destroying completed work); his core ask is to get the listing team out of Magento entirely for day-to-day work, batch-importing ~biweekly instead. Gave real quarter-over-quarter Fermi data: Q1 2026 ~3,600 items/quarter at ~230 Kč/item → Q2 2026 ~6,000 items/quarter at ~130 Kč/item (achieved despite one fewer headcount). Flagged Q3 2026 will likely be worse (vacations + a new EU environmental-claims regulation affecting ~10,000+ products, ~4,000 critical, against only ~1,000 items/quarter current compliance capacity). Confirmed no formal "head of listing" role exists yet on Dr. Max's side — possibly the same gap as the previously-referenced "second listing business owner" (unconfirmed). Nominated Michaela Vdovicynová (STK-048) as the practical domain-expert/testing contact. Declined to commit to a firm KPI target, floating only a directional "~20% faster, compounding quarter over quarter" placeholder. Source: 2026-09-01-dr-max-listing-introduction, 2026-09-01-dr-max-x-bighub-project-status-sync, roadmap sheet 2026-09-02, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync, 2026-09-16-business-quantification-listing-petr-neuman |

### STK-024

| Field | Value |
|-------|-------|
| ID | STK-024 |
| Name | Rudolf Žůrek |
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
| Notes | Name corrected 2026-09-11 from "Rudolf Zurek" to "Rudolf Žůrek" per PM (surfaced via a Jindřich Tůma message: Tereza Foltýnová's Monday AI-initiatives meeting is specifically interested in every project where the Business Owner is Žůrek or logistics — per that same message, only ~2 of those are currently "in progress," with ~5 more still at "idea" stage). New name, first seen on the 2026-09-02 roadmap sheet. Unresolved overlap with existing records: "Invoicing solution" may be the same initiative as Fakturace doprav (freight invoicing), currently attributed to Jan Žižka (STK-015, scope owner) and Petr Spilka (STK-014, reviewer); "Receiving compliants in stock" may be the same initiative as Reklamace (claims), currently attributed to Marie Hulešová (STK-020). Recorded both per PM instruction — not yet reconciled. See ASM-006. Source: roadmap sheet 2026-09-02 |

### STK-025

| Field | Value |
|-------|-------|
| ID | STK-025 |
| Name | Tomáš Burda |
| Aliases | — |
| Organization | Dr. Max |
| Role | Owner/Customer — "TD revisions"; likely business owner of TEO/OCR (see Notes) — head of the technical department |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | "TD revisions" is a project stream not previously mentioned in any processed meeting — nature of the initiative unknown beyond the name. **Possible identity match (2026-09-15, unconfirmed)**: in the TEO/OCR Business Quantification call, Radim Švarc (STK-041) named Tomáš Burda, head of the technical department, as the actual business owner for TEO/OCR — major directional decisions need his sign-off. "TD revisions" (Technical Department revisions) is a strong name match for TEO/OCR (TEO = Dr. Max's technical department; the initiative processes service/revision protocols), but this hasn't been explicitly confirmed by Burda himself. Marek asked Radim to loop him in for confirmation. On 2026-09-16, personally attended a TEO/OCR technical sync (his first appearance in a working-level meeting for this initiative, not just the business-quantification call) — reviewed BigHub's technical/API documentation and found it in good shape, committed to starting Dr. Max-side build work 2026-09-17 with something concrete targeted for the next sync (~2026-09-23). Privately flagged a resourcing concern to Alana Sihelská afterward: the people on "Radim's side" who handled BigHub's requested antivirus/security-review task are largely done and risk reassignment unless he lines up follow-on work soon — committed to prioritizing this himself. Source: roadmap sheet 2026-09-02, 2026-09-15-business-quantification-teo-ocr, 2026-09-16-teo-ocr-technical-sync-pilot-results |

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
| Notes | Low-confidence entry — name spelling uncertain. Lukáš Starenko (STK-028) was pointed to him by Filip Černý to request access. **Possible identity overlap (2026-09-17, unconfirmed)**: the MaxBuddy Business Quantification call names a "Lukáš Sýč" as Luboš Vosmek's (STK-011) IT liaison bridging BigHub/Farmy/BDC — a similar name in a third context (this record's Reklamace Teams/Swagger access, and separately Jindřich Tůma's 2026-09-15 note naming "Lukáš Síč" as BigHub's own order-prediction coordination contact). Flagged for verification, not merged — could be one person spanning roles or several similarly-named people. Source: 2026-09-02-logistics-listing-team-sync, 2026-09-17-business-quantification-maxbuddy-vosmek |

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
| Notes | New contact, first appearance 2026-09-03. Confirmed 2026-09-07 as the primary "manažer"-type Reklamace contact alongside Jan Kopecký (STK-032). On 2026-09-10, pushed back hard on a proposed short UAT testing window — needs to validate full downstream Axapta financial/logistics effects, not just app UX, citing ~18 process variants and a Finance-team dependency; also personally capacity-constrained in September by two unrelated GoLive projects (a "A-Frame" project and one in Ostrava). Negotiation landed constructively on an October 15-16 UAT start (see ASM-056); he committed to continuous blocker reporting during testing. Also flagged the reklamace-Axapta API documentation lacks enough sequencing detail to start backend dev safely — a dedicated walkthrough was scheduled to resolve it (ASM-057). Source: 2026-09-03-viapharma-logistics-status-reklamace-demo, 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |

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
| Last interaction | 2026-09-15 |
| Status | Active |
| Notes | Joined the 2026-09-03 dashboard demo ~15 min in. Previously supplied a manual promo/campaign CSV (now ~2 months stale) and manually-pulled "created orders" figures before the dashboard existed. Owes a refreshed campaign/promo data file so the model can account for the 2026-08-29 Brno campaign. On 2026-09-15, drove the logistics half of a detailed dashboard feedback session — pushed for pharmacy reservations to be split out from the general order aggregate and broken down per warehouse for staffing planning (see [[ASM-071]]), requested a Metrix-to-Excel export, and flagged a 30-minute vs. hourly granularity need for BDC outage reporting. Source: 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-15-order-prediction-dashboard-follow-up |

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
| Notes | Low-confidence entry — single mention by Jan Sovka, surname and identity not confirmed. Not clearly the same person as Jan Maroušek (STK-021, Kontrola beden) — needs verification before merging. Deliberately placed into a later phase (2/3/4) of the order-prediction dashboard rather than phase 1. **Possible identity match (2026-09-15, unconfirmed)**: the 2026-09-15 dashboard follow-up repeatedly references a "Honza/Jan Maroušek" who plans warehouse staffing (Nučice, Brno) and needs a per-warehouse reservation/pickup breakdown — same first name and the same "logistics planning, month-ahead-style need" profile originally used to describe this entry. Plausibly the same person as this record and/or STK-021, but not explicitly confirmed on either call — flagged for PM verification rather than merged. Source: 2026-09-03-order-prediction-dashboard-live-demo, 2026-09-15-order-prediction-dashboard-follow-up |

### STK-037

| Field | Value |
|-------|-------|
| ID | STK-037 |
| Name | Kateřina "Kačka" Kadlecová |
| Aliases | Kačka; previously recorded as "Karlecová" — corrected 2026-09-10, see Notes |
| Organization | Dr. Max — Call Center |
| Role | CC team member testing Lexie (Lucie); detailed bug reporter, active UX voice on the Max chatbot's feedback-mechanism design |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral (leaning engaged) |
| Sentiment context | Detail-oriented and constructive — well-documented bug reports (video evidence attached to X-Manager tickets), proactive UX opinions grounded in her own prior chatbot data (star/emoji ratings over free text, green→red color order), and explicit concern for her operators' experience (avoiding "panic" from over-broad status visibility). On 2026-09-10, thorough ticket triage (confirmed the thumbs-feedback fix, flagged a new permission-scope error on ticket 150 with a screenshot already attached) and positive, constructive feedback on the X-Manager Kanban view. |
| Communication preference | -tbd- |
| Expectations | Wanted the 3 blocking Lexie bugs fixed before her team resumed testing (1 of 3 resolved as of 2026-09-10); wants feature requests centralized through Mertová rather than scattered; wants the X-Manager Kanban (grouped by scope) to remain the roadmap source of truth rather than a separate Excel export. |
| Last interaction | 2026-09-17 |
| Status | Active — departing on maternity leave (disclosed by Mertová, 2026-09-17); domain-expert successor for Max chatbot/Maxie/Lexie not yet named |
| Notes | **Name correction (2026-09-10)**: this meeting's transcript clearly and repeatedly names her "KADLECOVÁ Kateřina" as a distinct speaker with detailed, consistent bug-report content — matching the behavior previously attributed to "Karlecová" under the ambiguous "CZ-BRN-TIT-CCManager" transcript tag on 2026-09-03/09-04. Treating "Kadlecová" as the correct spelling going forward; "Karlecová" was likely a transcription error. The "CZ-BRN-TIT-CCManager" tag itself spoke a few short, separate lines in this same 2026-09-10 meeting even while Kadlecová was independently and clearly attributed — suggesting the tag is a generic dial-in/room identity, not fixed to one person; not resolved further. On 2026-09-04, created the X-Manager "Product Scope" ticket (MVP/roadmap ask, now owned by Marek) and sent Jindřich a message that mixed up terminology between a harmonogram document and an MVP-definition ask. Per Jindřich (2026-09-09), wanted to scroll through the roadmap herself during the 2026-09-10 CC session. **Update 2026-09-17**: Mertová disclosed (in a separate Business Quantification interview) that Kadlecová — the lead domain expert across all three CC initiatives — is departing on maternity leave; the team needs to internally reassign this before a successor can be named — see [[ASM-091]]. Also on 2026-09-17, in the Lexie/Max/Maxie weekly sync held earlier the same day (before that disclosure), participated actively: reviewed the new cross-project timeline and flagged an unresolved MVP-vs-full-product scoping mismatch, confirmed her team's draft X-Manager Kanban column/status restructure (to be sent to Jindřich for review), and took the action to run a "vibe check" exercise on Lexie's UX to hand concrete pain points to Marek. Source: 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, 2026-09-04-ai-platform-standup-xmanager-lexi-demo, 2026-09-09-logistics-cc-roadmap-presentation-prep, 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-17-business-quantification-cc-max-maxie-lexie, 2026-09-17-lexie-max-maxie-weekly-sync |

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
| Notes | Low-confidence entry — single mention, surname uncertain from transcript. Kept per PM instruction to route everything; needs verification. **Possible identity match (2026-09-17, unconfirmed)**: in the Lexie/Max/Maxie weekly sync, Mertová named "Míša Machata" (Prague) as the new owner of X-Manager — same surname, but a distinct role (tooling ownership vs. DVH/data-warehouse change requests) and no confirmation these are the same person. Marek is coordinating with him directly; flag for reconciliation once confirmed either way. Source: 2026-09-03-maxbuddy-chatbot-ocr-project-handoff, 2026-09-17-lexie-max-maxie-weekly-sync |

### STK-041

| Field | Value |
|-------|-------|
| ID | STK-041 |
| Name | Radim Švarc |
| Aliases | — |
| Organization | Dr. Max — TEO (technical department) |
| Role | TEO/OCR project contact — domain expert / daily working contact (business ownership sits with Tomáš Burda, STK-025 — see below) |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral (leaning engaged) |
| Sentiment context | Came prepared to the 2026-09-15 quantification call with a presentation and a real historical estimate rather than guessing; pushed back constructively on Marek's proposed KPI instead of accepting it passively. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-15 |
| Status | Active |
| Notes | Building his own application/API that will call BigHub's OCR pipeline directly — the two systems' integration boundary (who owns which side) still needs defining. On 2026-09-15, in the Business Quantification interview, clarified he is the domain expert/daily contact rather than the business owner — major directional decisions need Tomáš Burda's (STK-025) sign-off. Gave a well-grounded business-value estimate (~250 handwritten service protocols/week, ~40h/~5MD monthly manual re-keying into ServiceNow, pulled from a note previously sent to Lukáš Síč) and shared a technical presentation confirming these figures and proposing a concrete automated-process architecture (dedicated intake email → PowerAutomate → AI extraction via API → reviewable Excel → ServiceNow import) — see `documents/client/2026-09-15-teo-ocr-technical-process-presentation.md`. Pushed back on Marek's proposed time/FTE-saved KPI in favor of a document-count/correction-rate framing; confirmed he received BigHub's API service spec the day before and is starting to test it. Source: 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-15-business-quantification-teo-ocr |

### STK-042

| Field | Value |
|-------|-------|
| ID | STK-042 |
| Name | Michaela Albrechtová |
| Aliases | — |
| Organization | Dr. Max — TEO (technical department) |
| Role | TEO/OCR project contact — owns the Dr. Max-side ServiceNow-import build |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-16 |
| Status | Active |
| Notes | Named alongside Radim Švarc (STK-041) as a TEO contact; no further detail yet. **Update 2026-09-16** (identity inferred from a conference-room speaker label in the transcript and Burda addressing her as "Míša," confirmed by PM): active, detail-oriented participant in the TEO/OCR technical sync — caught 2 real bugs BigHub hadn't spotted (a duplicated defects-text field, and a protocol with a genuine error that wasn't flagged for review), and reconfirmed the exact-text-match requirement for service-company/vendor names against Dr. Max's supplier master list. Owns the Dr. Max-side ServiceNow-import form/pipeline (built around "Wágner's," STK-047, BDC mechanism) — nearly complete, tested, one cosmetic bug outstanding, expected live this week or early next. Source: 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-16-teo-ocr-technical-sync-pilot-results |

### STK-043

| Field | Value |
|-------|-------|
| ID | STK-043 |
| Name | "Kopčík" / Zábojník (name uncertain) |
| Aliases | — |
| Organization | BDC (possibly not directly Dr. Max) |
| Role | BDC-side technical contact on Reklamace |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-07 |
| Status | Active |
| Notes | Low-confidence entry — name and even employer (BDC vs. Dr. Max directly) uncertain from transcript; Filip Černý himself wasn't sure. Kept per PM instruction to route everything; needs verification. Source: 2026-09-07-ai-portfolio-roadmap-scope-review |

### STK-044

| Field | Value |
|-------|-------|
| ID | STK-044 |
| Name | Jana Egrmaierová |
| Aliases | "Egermajerová" (earlier low-confidence transcription, now corrected) |
| Organization | ViaPharma CZE |
| Role | Reklamace business/end user, working with Tereza Foltýnová (STK-013) on supplier data consolidation |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-10 |
| Status | Active |
| Notes | Name spelling confirmed 2026-09-10 (was low-confidence "Egermajerová" from 2026-09-07) — attended directly, correctly transcribed as "EGRMAIEROVÁ Jana". Actively working with Tereza Foltýnová on consolidating the reklamace supplier Excel (3-4 source tables, not yet fully reconciled); has dedicated time allocated to this work. Floated by Tereza on 2026-09-15 as a possible Reklamace domain-expert alongside/instead of Petr Spilka (STK-014) — unconfirmed, Tereza to check with Spilka directly. Source: 2026-09-07-ai-portfolio-roadmap-scope-review, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, 2026-09-15-business-quantification-reklamace-fakturace-doprav |

### STK-045

| Field | Value |
|-------|-------|
| ID | STK-045 |
| Name | Lucie Fendrichová |
| Aliases | — |
| Organization | Dr. Max CZE |
| Role | CC team member — active UX/product voice on the X-Manager Kanban view and platform documentation |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | Neutral (leaning engaged) |
| Sentiment context | Proactive and detail-oriented — demonstrated a Kanban filtering feature unprompted to help Kadlecová find a "missing" ticket, and flagged a UX-improvement idea (hide-empty-columns toggle) during the roadmap-view review. |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-17 |
| Status | Active |
| Notes | New contact, first appearance 2026-09-10. On 2026-09-17, in the Lexie/Max/Maxie weekly sync, offered to connect BigHub's test environment to Dr. Max's staging/test orders (unblocking phone-number-based order lookup testing for the Max chatbot); flagged a city/district-recognition bug (Brno-Líšeň not recognized as part of Brno) for Jura to investigate; raised a Lexie conversation-title bug (some titles save in English instead of Czech) to be filed as a ticket. Transcript shows her tagged twice in this meeting ("DrMax CZE" and "DrMax CZE1") — treated as the same person, likely a diarization artifact. Source: 2026-09-10-lexie-max-maxie-weekly-sync, 2026-09-17-lexie-max-maxie-weekly-sync |

### STK-046

| Field | Value |
|-------|-------|
| ID | STK-046 |
| Name | "Verča" Strnisková (first name uncertain — transcribed as "Verča," likely short for Veronika) |
| Aliases | Verča |
| Organization | Dr. Max — Call Center |
| Role | CC operator named as an example tester for Lexie's role-based test-account setup |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-10 |
| Status | Active |
| Notes | Low-confidence entry — single mention by Simona Mertová as a concrete example of how a tester would need to run two logins simultaneously (own role + test-account role) once the test account is set up. Kept per PM instruction to route everything; needs verification. Source: 2026-09-10-lexie-max-maxie-weekly-sync |

### STK-047

| Field | Value |
|-------|-------|
| ID | STK-047 |
| Name | "Wágner" (first name uncertain) |
| Aliases | — |
| Organization | BDC |
| Role | Preparing the manual Excel-to-ServiceNow import mechanism for TEO/OCR, as a fallback/interim path alongside a possible fully automated (click-simulation) alternative |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- |
| Status | Active |
| Notes | Low-confidence entry — surname only, mentioned in Dr. Max's own TEO/OCR technical presentation, not yet directly contacted by BigHub. Kept per PM instruction to route everything; needs verification. **Update 2026-09-16**: per Michaela Albrechtová (STK-042), his manual SNOW-import mechanism is functionally near-complete — one cosmetic bug remains (a chart component not rendering/linking correctly), non-blocking. Source: documents/client/2026-09-15-teo-ocr-technical-process-presentation.md, 2026-09-16-teo-ocr-technical-sync-pilot-results |

### STK-048

| Field | Value |
|-------|-------|
| ID | STK-048 |
| Name | Michaela Vdovicynová |
| Aliases | — |
| Organization | Dr. Max — Listing team |
| Role | Practical domain-expert/testing contact for Listing — day-to-day BigHub liaison, distinct from Petr Neuman's (STK-023) business-owner role |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- (not yet contacted directly by Marek) |
| Status | Active |
| Notes | Nominated by Petr Neuman (2026-09-16) as the listing team's practical contact — a pharmacist's-assistant by background who does the listing work herself; will run team testing sessions, collect and relay feedback, and handle operational work Neuman doesn't have time for. There is currently no formal "head of listing" role on Dr. Max's side; she fills a working-level gap rather than that role itself. Neuman has a separate internal Monday sync with her on current data-import/feed status. Marek plans to connect with her directly as part of kicking off Listing's Discovery phase (see [[ASM-011]]). Source: 2026-09-16-business-quantification-listing-petr-neuman |

### STK-049

| Field | Value |
|-------|-------|
| ID | STK-049 |
| Name | Jiří Trajer |
| Aliases | — |
| Organization | Dr. Max — datový sklad / Power BI |
| Role | Feeds MaxBuddy its underlying data (Power BI / data warehouse) — not involved in feature/functionality decisions |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | -tbd- (not yet contacted directly by Marek) |
| Status | Active |
| Notes | Named by Luboš Vosmek (STK-011) as one of two MaxBuddy contacts, alongside Lukáš Sýč (see STK-031, possible identity overlap flagged). Marek initially assumed Trajer would be the fallback contact for roadmap/feature questions; Vosmek corrected this — Trajer only supplies data (reading pharmacy POS/Farmy receipt data via Power BI), and is not involved in any functionality or roadmap decisions. Source: 2026-09-17-business-quantification-maxbuddy-vosmek |

### STK-050

| Field | Value |
|-------|-------|
| ID | STK-050 |
| Name | Šárka Andělová |
| Aliases | — |
| Organization | Dr. Max CZE |
| Role | CC team member — active tester on the Max chatbot, raised the GDPR/consent gap |
| Location | -tbd- |
| Influence | -tbd- |
| Sentiment | -tbd- |
| Sentiment context | -tbd- |
| Communication preference | -tbd- |
| Expectations | -tbd- |
| Last interaction | 2026-09-17 |
| Status | Active |
| Notes | New contact, first appearance 2026-09-17 in the Lexie/Max/Maxie weekly sync. Flagged a GDPR/consent gap in the Max chatbot (no consent checkbox for phone/email collection, no anonymization step) — Jura confirmed this hadn't been planned for; ticket opened, needs DPO (Lenka Henichová) input before copy is drafted. Also asked whether BigHub needs @-mention notifications on new tickets (answer: no, status-column monitoring is sufficient). Source: 2026-09-17-lexie-max-maxie-weekly-sync |

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
