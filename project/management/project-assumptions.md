---
last_updated: 2026-09-25
last_updated_by: auto — project-meeting routing (2026-09-25-reklamace-supplier-data-source-options)
owner: Marek Pillár
---

# Project Assumptions & Decisions

## Index

| ID | Status | Created | Description (short) |
|----|--------|---------|---------------------|
| ASM-176 | Open (2026-09-25) | 2026-09-25 | Reklamace Kontakty, Poznámky, Typ odvozu have no agreed home; Axapta manual address entry unowned |
| ASM-175 | Open (2026-09-25) | 2026-09-25 | Reklamace claims worker loses the one-sheet-per-supplier view; display option to be chosen by client |
| ASM-174 | Open (2026-09-25) | 2026-09-25 | Rozvozový list Axapta fields (reklamace no., RD no., issue date) missing from API contract |
| ASM-173 | Decided (2026-09-25) | 2026-09-25 | Filip builds ~1 MD Reklamace email-agent demo for the 2026-10-01 logistics meeting |
| ASM-172 | Decided (2026-09-25) | 2026-09-25 | Reklamace per-case communication timeline dashboard killed — out of scope, weeks of work |
| ASM-171 | Decided (2026-09-25) | 2026-09-25 | Reklamace main-contact concept kept; <5 category-conditional supplier exceptions handled in spec |
| ASM-170 | Decided (2026-09-25) | 2026-09-25 | Non-Axapta Reklamace supplier store extends Axapta via supplier-account key; no duplicated fields |
| ASM-169 | Decided (2026-09-25) | 2026-09-25 | Reklamace supplier data: Excel on SharePoint not recommended; client chooses between Excel, SharePoint Lists, Confluence with risks listed |
| ASM-168 | Open (2026-09-25) | 2026-09-25 | TEO/OCR never had process discovery; wider process and follow-on use cases unknown, per-cycle effort unknown |
| ASM-167 | Open (2026-09-25) | 2026-09-25 | BigHub Dr. Max capacity is a flexible ~3 FTE (~60 MD/month) annual pool with accumulated unused budget since May |
| ASM-166 | Decided (2026-09-25) | 2026-09-25 | TEO/OCR direction goes through Radim Švarc first (informal vibe check) as the entry point to Tomáš Burda |
| ASM-165 | Decided (2026-09-25) | 2026-09-25 | TEO/OCR stays on Excel for the autumn 2026 cycle; non-Excel review solution targeted before spring 2027 |
| ASM-164 | Open (2026-09-24) | 2026-09-24 | First AI Platform release ~3–4 weeks after DB access on the new cluster works, and that access is disputed |
| ASM-163 | Decided (2026-09-24) | 2026-09-24 | Roadmap/blockers view belongs in Azure DevOps, not the AI Platform (at most an admin view) |
| ASM-162 | Decided (2026-09-24) | 2026-09-24 | AI Platform is the central telemetry/alerting point, integrated with Dr. Max's Zabbix, with an auditable incident history |
| ASM-161 | Decided (2026-09-24) | 2026-09-24 | Department AI-initiative backlogs targeted for end of November (ideal, not hard); running projects keep priority |
| ASM-160 | Decided (2026-09-24) | 2026-09-24 | Live or near-live initiatives get a "PR" value story (assumption → interim → current → trend), starting 2026-09-29 |
| ASM-159 | Decided (2026-09-24) | 2026-09-24 | Every KPI in the BQ tracker must carry a measurement method and baseline (new measurement column) |
| ASM-158 | Decided (2026-09-24) | 2026-09-24 | BQ tracker format is the mandatory intake standard for all new AI initiatives; Dudaško decides go/no-go by annual value |
| ASM-157 | Decided (2026-09-24) | 2026-09-24 | Max quick-reply bubbles kept, chat-style layout; profile-based personalization deferred to on-site integration |
| ASM-156 | Decided (2026-09-24) | 2026-09-24 | Lexie visual polish folded into platform-wide redesign; minor padding/border requests are low priority |
| ASM-155 | Open (2026-09-24) | 2026-09-24 | Who pays for ElevenLabs licences and custom/extended voices (BigHub project vs. Dr. Max) is unclear |
| ASM-154 | Decided (2026-09-24) | 2026-09-24 | Maxie must replicate Dr. Max's existing Atlantis IVR "Maxí" solution exactly, split per IVR topic branch |
| ASM-153 | Decided (2026-09-24) | 2026-09-24 | Dr. Max public methodologies served to Max via AI-platform RAG, with self-service document management |
| ASM-152 | Decided (2026-09-24) | 2026-09-24 | Free-text feedback on Max's end-conversation screen is test-only; removed for public launch |
| ASM-151 | Decided (2026-09-24) | 2026-09-24 | Max opening message stays hardcoded; Dr. Max supplies exact wording incl. AI Act disclosure |
| ASM-150 | Decided (2026-09-24) | 2026-09-24 | Client tone-prompt input for Max limited to short keywords, replacing the 09-17 first-person tone-brief approach |
| ASM-149 | Open (2026-09-24) | 2026-09-24 | Max chatbot runs on GPT-5 mini and has hit its instruction ceiling (~10–12 instructions); model upgrade pending cost projection |
| ASM-148 | Open (2026-09-23) | 2026-09-23 | AI Platform test/prod cost-reporting mechanism undecided (endpoint-pull vs. periodic dump vs. global env switcher) |
| ASM-147 | Decided (2026-09-23) | 2026-09-23 | AI Platform prototype design work deliberately deferred until navigation/interaction validated with Dudaško |
| ASM-146 | Open (2026-09-23) | 2026-09-23 | Cross-platform RAG "ask anything" agent concept kept in reserve, not built — offer only if Dudaško asks for more |
| ASM-145 | Open (2026-09-23) | 2026-09-23 | Security gap: MCP server registration leaks secret/header values to any agent reading server descriptions |
| ASM-144 | Decided (2026-09-23) | 2026-09-23 | "Platform" and "Lexie" now treated as explicitly separate concepts — conflation was a source of Dudaško's frustration |
| ASM-143 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav: rozvozový list needs warehouse-worker free-text input with no defined data source |
| ASM-142 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav API-contract renegotiation with Petr Sláma stuck — no counter-proposal, slow replies |
| ASM-141 | Decided (2026-09-23) | 2026-09-23 | Logistics delivery timelines now explicitly factor in client-side response delays, not just BigHub-side ones |
| ASM-140 | Decided (2026-09-25) | 2026-09-23 | MaxBuddy annual value: 81M Kč/yr per BQ tracker (source of truth); ~130M figure superseded |
| ASM-139 | Open (2026-09-23) | 2026-09-23 | Dudaško plans to retire Axapta within ~6 months; willing to pay more now for a Reklamace solution portable to its replacement |
| ASM-138 | Open (2026-09-23) | 2026-09-23 | Second post-closing carrier confirmation from June 2026 Fakturace doprav draft not carried into current scope — status unclear |
| ASM-137 | Decided (2026-09-23) | 2026-09-23 | Fakturace doprav carrier confirmation: one consolidated email per scan session decided; sending code not yet built |
| ASM-136 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav business value re-quantified via Aug 2026 workshop — 787,500 Kč/yr + 4 KPI targets, supersedes 09-15 Fermi estimate |
| ASM-135 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav: multi-vehicle routes silently overwritten in code — second ZOPV treated as correction, not separate document |
| ASM-134 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav: temperature-log document type modeled downstream but not reachable via OCR classification — scans rejected |
| ASM-133 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav: AR pairing key for ZOPV/OPIATY already implemented in code, contradicting "still missing" claim from P. Sláma |
| ASM-132 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav: document versioning is local/full in code, contradicting 2026-09-16 "Axapta owns all versioning" understanding |
| ASM-131 | Open (2026-09-23) | 2026-09-23 | Fakturace doprav: kiosk scan flow requires Entra ID auth in code, contradicting "open access" communicated to client |
| ASM-130 | Open (2026-09-23) | 2026-09-23 | PM flags the fully-manual, Excel-based TEO/OCR review workflow (no AI assistance downstream of extraction) as worth revisiting |
| ASM-129 | Open (2026-09-22) | 2026-09-22 | Conflict: Blob storage/deployment described as still depending on Dr. Max infra/BDC, contradicting ASM-088 |
| ASM-128 | Open (2026-09-22) | 2026-09-22 | Conflict: TEO rejected sending multiple disambiguation candidates to reviewers, apparently reversing ASM-119 |
| ASM-127 | Decided (2026-09-22) | 2026-09-22 | SPEDOS confirmed as a real vendor, actively onboarded as TEO/OCR's 3rd autumn-2026 pilot vendor — resolves ASM-089 |
| ASM-126 | Open (2026-09-22) | 2026-09-22 | Honza Kabát's Microsoft/Azure backlog-costing request deprioritized until Dudaško's Friday priority sign-off |
| ASM-125 | Open (2026-09-22) | 2026-09-22 | Portfolio priority-ranking tension: dollar-value ranking (MaxBuddy>Listing>Max/Maxie) vs. PM/stakeholder view that Listing should be top priority |
| ASM-124 | Decided (2026-09-22) | 2026-09-22 | Max chatbot/Maxie/Lexie business value: Mertová's FTE-avoidance figures stay illustrative-only; measured request-volume KPI added |
| ASM-123 | Decided (2026-09-22) | 2026-09-22 | Petr Neuman's Listing KPI figures now committed and concrete (~34M Kč/year) — supersedes ASM-075 placeholder |
| ASM-122 | Open (2026-09-22) | 2026-09-22 | Reklamace reframed as digitization/data-consolidation, not AI — continue-or-close decision pending Dudaško + logistics-head alignment |
| ASM-118 | Open (2026-09-21) | 2026-09-21 | No regular, reliable MaxBuddy reporting exists despite months of Dudaško raising it |
| ASM-117 | Decided (2026-09-21) | 2026-09-21 | AI adoption campaign scope split: BigHub owns awareness/comms, Dr. Max's training center + expert groups own rollout/training |
| ASM-116 | Open (2026-09-21) | 2026-09-21 | Agentic workflow/orchestrator builder — deferred to a future (~November) conversation |
| ASM-115 | Decided (2026-09-21) | 2026-09-21 | AI Platform 3-phase delivery sequencing agreed with Dudaško (UX/access → FinOps → capability matrix) |
| ASM-114 | Decided (2026-09-21) | 2026-09-21 | Per-department Lexie instances collapse into one unified, role-gated Lexie + public-doc tier |
| ASM-121 | Decided (2026-09-21) | 2026-09-21 | BigHub will not build the ServiceNow export for TEO/OCR — hands Radim's team clean data via API, his team owns export |
| ASM-120 | Decided (2026-09-21) | 2026-09-21 | TEO/OCR reviewer corrections must flow back to BigHub via API to measure/improve accuracy over time |
| ASM-119 | Decided (2026-09-21) | 2026-09-21 | TEO/OCR disambiguation shifts to classify-against-known-branch-list + ranked candidate alternatives, not forced verbatim transcription |
| ASM-113 | Decided (2026-09-21, updated 2026-09-21) | 2026-09-21 | AI Platform home screen becomes a unified, role-based directory to every AI tool — external tools open inline, not via deep link |
| ASM-112 | Decided (2026-09-21) | 2026-09-21 | AI Platform must behave as platform-as-a-service — all AI-consuming tools route through it for FinOps visibility |
| ASM-111 | Open (2026-09-18) | 2026-09-18 | Logistics shift-planning dashboard extension (~90% ready per M. Šimoník) — open, outside his ownership |
| ASM-110 | Decided (2026-09-18) | 2026-09-18 | Order-prediction dashboard: no new feature backlog — next roadmap conversation deferred to Q4/year-end |
| ASM-109 | Decided (2026-09-18) | 2026-09-18 | Order-prediction dashboard reaction/outage-prevention value quantified at ~100–200k Kč/month (conservative) |
| ASM-108 | Decided (2026-09-18) | 2026-09-18 | Order-prediction dashboard KPI: catch ≥1 serious issue (web or logistics) per month |
| ASM-107 | Decided (2026-09-18) | 2026-09-18 | Order-prediction dashboard KPI: analyst control-time reduced from ~5h/week to 2h/week (long-term target) |
| ASM-106 | Decided (2026-09-18) | 2026-09-18 | Order-prediction dashboard business ownership confirmed — Marek Šimoník sole owner, Petr Ondráček domain expert |
| ASM-105 | Decided (2026-09-17) | 2026-09-17 | False call-transfer claims and unauthorized medical advice explicitly disallowed in Max chatbot's prompt |
| ASM-104 | Open (2026-09-17) | 2026-09-17 | Some shared timeline items are mis-scoped as MVP when they belong to the full product — not yet itemized |
| ASM-103 | Decided (2026-09-17) | 2026-09-17 | Lexie test-account approach: 4 separate accounts without 2FA, not the in-app role-switcher |
| ASM-102 | Open (2026-09-17) | 2026-09-17 | Max chatbot GDPR consent/anonymization copy blocked pending DPO (Lenka Henichová) input |
| ASM-101 | Decided (2026-09-17) | 2026-09-17 | Max chatbot public launch will be a quiet/soft launch — no active promotion until fully mature |
| ASM-100 | Decided (2026-09-17) | 2026-09-17 | Max chatbot go-live: public launch end of October; BigHub's 3 internal deployment phases targeted for end of September |
| ASM-099 | Open (2026-09-17) | 2026-09-17 | All three MaxBuddy KPI targets (single-item dispensing, molecule/group volume, conversion-by-benefit) pending quantification from Luboš Vosmek |
| ASM-098 | Open (2026-09-17) | 2026-09-17 | MaxBuddy revenue-uplift (~1-1.2%) and dispensing-coverage (~40%) figures provisional pending exact numbers from Luboš Vosmek |
| ASM-097 | Open (2026-09-17) | 2026-09-17 | MaxBuddy's live upsell feature is data/rule-based, not LLM/AI-driven — open question for AI-portfolio classification |
| ASM-096 | Open (2026-09-17) | 2026-09-17 | Simona Mertová owes a blended agent (FTE) cost rate needed to convert Max chatbot/Maxie/Lexie time estimates into Kč |
| ASM-095 | Open (2026-09-17) | 2026-09-17 | Lexie business-value quantification and KPI unresolved — two candidate directions proposed, neither finalized |
| ASM-094 | Open (2026-09-17) | 2026-09-17 | Maxie containment-rate KPI walked back from 90% to a 50/50 placeholder, explicitly non-final |
| ASM-093 | Open (2026-09-17) | 2026-09-17 | Max chatbot conversation-resolution KPI set directionally at ~50% initial / ~80% aspirational, not committed |
| ASM-092 | Decided (2026-09-17) | 2026-09-17 | Max chatbot and Maxie business value framed as capacity/coverage increase and reduced agent cognitive load, not FTE savings |
| ASM-091 | Open (2026-09-17) | 2026-09-17 | Kateřina Kadlecová's domain-expert role for Max chatbot/Maxie/Lexie vacant pending reassignment (maternity leave) |
| ASM-090 | Open (2026-09-16) | 2026-09-16 | Whether to add the code-confirmed driver PDF confirmation feature to the Fakturace doprav roadmap Excel/Artifact (currently only in the rebuilt spec doc) |
| ASM-089 | Resolved by ASM-127 (2026-09-22) | 2026-09-16 | Whether to expand TEO/OCR's autumn 2026 pilot scope to a 3rd, larger vendor ("PEDOS," name uncertain) not yet decided |
| ASM-088 | Decided (2026-09-16) | 2026-09-16 | TEO/OCR TEST-environment Blob storage will be self-provisioned by BigHub on the existing platform — no BDC/infra-team dependency to create it |
| ASM-087 | Open (2026-09-17) | 2026-09-14 | Fakturace doprav kiosk authentication — undecided, pending a debate on 2026-09-17; leaning "no authentication" for now |
| ASM-086 | Decided (2026-09-14) | 2026-09-14 | Fakturace doprav "Kontrola údajů" (marked Done) actually only covers km — temperature-datalogger validation is not built, split into 3 Plná verze sub-parts |
| ASM-085 | Decided (2026-09-16) | 2026-09-16 | 2. Fakturace doprav.docx and spec-template.docx had leaked, unrelated Listing review comments in their comments.xml (from template cloning) — stripped out |
| ASM-084 | Decided (2026-09-14) | 2026-09-14 | Fakturace doprav "Měsíční uzávěrka" (monthly-closing cron job) cancelled — routes now sent to Axapta continuously, Axapta decides closure timing itself |
| ASM-083 | Decided (2026-09-14) | 2026-09-14 | Fakturace doprav "Potvrzení řidiči" renamed "Potvrzení přepravci" and merged with "Generování potvrzení o skenování" — confirmation goes to the carrier, not the driver |
| ASM-082 | Decided (2026-09-14) | 2026-09-14 | Fakturace doprav km comparison and deviation-flagging is entirely Axapta's responsibility; platform only supplies data (ZOPV/OCR now, optional GPS Dozor later), split into two tickets |
| ASM-081 | Open (2026-09-16) | 2026-09-16 | Vendorský portál (supplier self-service listing submission) flagged by PM as medium priority, possible future AI initiative — tracked here only, Listing spec document left unmodified per PM instruction |
| ASM-080 | Open (2026-09-16) | 2026-09-16 | Likely runtime bug in claims_api's generate_delivery_note (undefined `key` field) — flagged for dev team, not yet fixed |
| ASM-079 | Decided (2026-09-16) | 2026-09-16 | Fakturace doprav's Axapta integration confirmed built and live in code — corrects prior spec/roadmap claim that it was not yet built |
| ASM-078 | Open (2026-09-16) | 2026-09-16 | BigHub-internal recommendation: roll out TEO/OCR starting with the 3-4 highest-volume document categories |
| ASM-077 | Open (2026-09-16) | 2026-09-16 | Which of 4 proposed TEO/OCR solution variants (API/Hybrid/Aplikace + add-ons) to formally pursue with Dr. Max not yet decided |
| ASM-076 | Decided (2026-09-16) | 2026-09-16 | TEO/OCR internal architecture agreed: blob storage → batch AI processing (dual GPT-5/GPT-5-mini) → API |
| ASM-075 | Superseded by ASM-123 (2026-09-22) | 2026-09-16 | Listing KPI target not yet committed — only a directional "~20% faster, compounding quarter over quarter" placeholder floated by Petr Neuman |
| ASM-074 | Decided (2026-09-16) | 2026-09-16 | Michaela Vdovicynová confirmed as Listing's practical domain-expert/testing contact, distinct from Petr Neuman's business-owner role |
| ASM-073 | Decided (2026-09-16) | 2026-09-16 | Listing's primary near-term driver reframed: eliminating day-to-day Magento use for the listing team (batch import ~biweekly) now outranks the original supplier-data-quality problem |
| ASM-072 | Decided (2026-09-15) | 2026-09-15 | Business-quantification KPI decisions for Reklamace/Fakturace doprav: error rate excluded as a KPI for both, driver time/cost excluded from Fakturace doprav's FTE calc, Reklamace's ~1 FTE saving contingent on all 5 phases shipping |
| ASM-071 | Decided (2026-09-15) | 2026-09-15 | Pharmacy reservations confirmed as a strategic e-commerce differentiator for Dr. Max — to be broken out as their own top-line dashboard category, split per warehouse for logistics staffing |
| ASM-070 | Decided (2026-09-15) | 2026-09-15 | Order-prediction dashboard's model output stays named "predikce," kept terminologically distinct from Dr. Max's own "budget"/"forecast" planning figures |
| ASM-069 | Decided (2026-09-15) | 2026-09-15 | Order-prediction dashboard's current build formally accepted as "version 1"; future requests batch into v2/v3 on a roughly quarterly cadence instead of continuous ad hoc releases |
| ASM-068 | Decided (2026-09-15) | 2026-09-15 | Listing category hierarchy/inheritance ("vrstvené/složené listovací standardy") split out of Nice to Have into Plná verze scope, separate from raw category-count scaling |
| ASM-067 | Decided (2026-09-15) | 2026-09-15 | Listing "produkční nasazení" finish-line criterion defined: listingový tým can self-import, edit, and return a product to Magento without manual ctrl-c/ctrl-v |
| ASM-066 | Decided (2026-09-15) | 2026-09-15 | Listing's "Tvorba popisů pro nové produkty" reclassified from Backlog to Hotovo — new products always enter the tool as existing products since Magento entry happens first |
| ASM-065 | Decided (2026-09-14) | 2026-09-14 | Listing must be connected to Magento before production — current phase is import-only by design, full Magento connection is a confirmed must-have for launch |
| ASM-064 | Open (2026-09-14) | 2026-09-14 | Listing blacklist enforcement stays advisory (warning) for now — whether it should become a blocking pre-publish check is an open business/compliance decision |
| ASM-063 | Open (2026-09-10) | 2026-09-10 | Lexie test-account approach: shared account + in-app role switcher preferred over 4 separate accounts, pending feasibility confirmation |
| ASM-062 | Decided (2026-09-10) | 2026-09-10 | X-Manager not extended to other Dr. Max streams yet — waiting on Tomáš Dudaško's promised DevOps environment project |
| ASM-061 | Decided (2026-09-10) | 2026-09-10 | Cross-project harmonogram (Lexie + Max + Maxie) will be built at weekly/workday granularity including testing windows — orientational, not fixed |
| ASM-060 | Decided (2026-09-10) | 2026-09-10 | Lexie design/UX polish stays at a compromise-ticket level; full redesign deferred until AI-platform-wide design consolidation lands |
| ASM-059 | Open (2026-09-10) | 2026-09-10 | X-Manager Kanban grouped by scope confirmed as the roadmap-visibility solution — no separate Excel deliverable planned, pending Mertová's business-side sign-off |
| ASM-058 | Decided (2026-09-10) | 2026-09-10 | Lexie's thumbs-up/down feedback blocker is resolved; testing has formally resumed |
| ASM-057 | Open (2026-09-10) | 2026-09-10 | Reklamace-Axapta API sequencing needs a dedicated walkthrough with Petr Sláma before further backend dev — current docs insufficiently detailed |
| ASM-056 | Decided (2026-09-10) | 2026-09-10 | Reklamace full-functionality UAT: starts Oct 15-16, target completion Oct 2 — landed after tense negotiation with Petr Sláma over testing scope/capacity |
| ASM-055 | Decided (2026-09-10) | 2026-09-10 | Fakturace doprav kiosk hardware (scanner + PC) stays ViaPharma's procurement responsibility |
| ASM-054 | Decided (2026-09-10) | 2026-09-10 | Fakturace doprav confirmation-screen scope confirmed with client: keep table with specific missing page numbers, drop driver-notes field, touchscreen-only UI |
| ASM-053 | Decided (2026-09-10) | 2026-09-10 | Axapta is the sole source of truth for Fakturace doprav route/document state — the BigHub app holds no state, just forwards scans as they arrive |
| ASM-052 | Open (risk, 2026-09-10) | 2026-09-10 | Fakturace doprav kiosk has no authentication — open access confirmed acceptable to client, but LLM-injection/security-surface risk remains technically unaddressed |
| ASM-051 | Decided (2026-09-10) | 2026-09-10 | Fakturace doprav OCR confidence-flagging + AR-number/barcode fallback design confirmed working via demo, accepted by client without objection |
| ASM-050 | Decided (2026-09-09) | 2026-09-09 | A calendar/timeline view (item + filled time-axis cells) is needed alongside the MD-estimate roadmap board — raw man-days aren't meaningful to non-technical stakeholders |
| ASM-049 | Decided (2026-09-09) | 2026-09-09 | Roadmap presentations to Logistika and CC split by audience — Logistika morning, CC mostly for testing-feedback review with only ~15 min on roadmap |
| ASM-048 | Decided (2026-09-09) | 2026-09-09 | Domain-expert engagement model — Jindřich joins only the first MaxBuddy 1:1; Marek runs the rest solo, keeping Jindřich informed of scheduling |
| ASM-047 | Decided (2026-09-09) | 2026-09-09 | Business value per initiative must be quantified in concrete numbers, not vague qualitative claims — starting with CC |
| ASM-046 | Decided (2026-09-09) | 2026-09-09 | MVP-phase exit criteria: client testing, feedback via an established channel, change-request/new-feature triage — before a Discovery session opens the next phase |
| ASM-045 | Decided (2026-09-08) | 2026-09-08 | AI platform UX scoped lean for the first prototype — 4 screens only (catalog, usage reports, kill switch, simulation), access via flexible admin-defined user groups, kill switch on two axes (per-product + per-model) |
| ASM-044 | Decided (2026-09-08) | 2026-09-08 | Roadmap board and Excel are client-facing deliverables — internal meeting dates and named attributions must be scrubbed from all notes/comments |
| ASM-043 | Open (2026-09-08) | 2026-09-08 | AI-platform project should be framed internally as feeding validated learnings back into BigHub's own platform, not a purely bespoke Dr. Max build |
| ASM-042 | Decided (2026-09-08) | 2026-09-08 | Jura Brázdil has spare capacity for AI-platform work and expects it to help rather than purely cost him, since he's migrating his own projects into it |
| ASM-041 | Decided (2026-09-08) | 2026-09-08 | AI platform treated as a formal project with Tomáš Dudaško as owner/sponsor, run via a standard prioritization/Discovery session |
| ASM-040 | Decided (2026-09-08) | 2026-09-08 | Dudaško's AI-platform requirements Excel gets distilled into a small realistic ticket set, not answered line-by-line |
| ASM-039 | Decided (2026-09-08) | 2026-09-08 | AI-platform near-term delivery scoped as 3 phases: UX rework, migrate existing projects to test+prod, build backlog into admin/reporting |
| ASM-038 | Decided (2026-09-08) | 2026-09-08 | BigHub's platform strategy is fully custom-per-client going forward; the shared-roadmap B2B-product vision is retired |
| ASM-037 | Open (2026-09-08) | 2026-09-08 | Reklamace has no DNS ingress yet — testing via port forwarding only; no clickable test URL for either logistics app currently |
| ASM-036 | Open (2026-09-08) | 2026-09-08 | Fakturace doprav not yet deployed to any environment; targeting end of this week / start of next |
| ASM-035 | Open (2026-09-07) | 2026-09-07 | TEO and Fakturace doprav share the same mixed-format document-extraction problem — worth comparing approaches |
| ASM-034 | Decided (2026-09-07) | 2026-09-07 | TEO OCR pilot deliberately scoped to 2 suppliers first, before considering expansion |
| ASM-033 | Open (risk, 2026-09-07) | 2026-09-07 | Listing's external-source scraping (e.g. Notino) paused pending legal review — may need an official API instead |
| ASM-032 | Decided (tentative, 2026-09-07) | 2026-09-07 | Listing category rollout starts with a small non-pharma set, not a large/complex one |
| ASM-031 | Decided (2026-09-07) | 2026-09-07 | Listing category/structure recommendation confirmed out of agreed scope — future feature request, not a tracked gap |
| ASM-030 | Open (2026-09-07) | 2026-09-07 | Řízení poptávky campaign recommendation/generation — no firm phase decision, stays Nice to Have/Backlog pending real scoping |
| ASM-029 | Open (risk, 2026-09-07) | 2026-09-07 | Max Chatbot/Maxie run on an unofficial scraped Dr. Max API in production — risk before full public launch |
| ASM-028 | Open (2026-09-07) | 2026-09-07 | MaxBuddy dosage-calc features stay blocked pending Dr. Max's medical-device certification decision |
| ASM-027 | Open (2026-09-07) | 2026-09-07 | MaxBuddy full 600-pharmacy rollout blocked on new AKS access; ~1 month pessimistic estimate post-grant |
| ASM-026 | Decided (2026-09-04) | 2026-09-04 | Marek's scope is Dr. Max exclusively, at least for the first month — not the broader cross-client AI platform |
| ASM-025 | Open (tentative, 2026-09-04) | 2026-09-04 | AI platform frontend defaults to one standardized template across clients, customized only on explicit request |
| ASM-024 | Decided (2026-09-04) | 2026-09-04 | Lexie redesign work stays deprioritized behind technical fixes; a rough visual is an acceptable low-cost placeholder |
| ASM-023 | Open (intent, 2026-09-04) | 2026-09-04 | X-Manager becomes the single tracking tool for all Dr. Max project tickets, not just Lexie/chatbot |
| ASM-022 | Decided (2026-09-03) | 2026-09-03 | Maxie (voicebot) scope starts at order-status only, expands incrementally as Dr. Max's IVR is updated |
| ASM-021 | Decided (2026-09-03) | 2026-09-03 | Lexie testing and design work paused entirely until 3 blocking bugs are fixed |
| ASM-020 | Decided (2026-09-03) | 2026-09-03 | Medical/dosage questions in the Max chatbot redirect to the official SPC leaflet, never answered directly |
| ASM-019 | Decided (2026-09-03) | 2026-09-03 | Max chatbot production-readiness bar: functional correctness against agreed scope now, polish deferred to a later release |
| ASM-018 | Decided (2026-09-03) | 2026-09-03 | X-Manager feature/change requests for Max/Lexie/Maxie route through one point of contact (Mertová) |
| ASM-017 | Decided (2026-09-03) | 2026-09-03 | Max chatbot in-chat feedback mechanism: star/emoji rating only, no free text, green→red color order |
| ASM-016 | Decided (2026-09-03) | 2026-09-03 | Order-prediction revenue model stays trained on recognized revenue only, not blended with order-backlog signals |
| ASM-015 | Decided (2026-09-03) | 2026-09-03 | Order-prediction dashboard phase-1 users are Šimoník/Ondráček; other logistics contact deferred to a later phase |
| ASM-014 | Decided (2026-09-03) | 2026-09-03 | Dashboard review order: verify data accuracy first, then display/UX changes, then model-accuracy tuning last |
| ASM-013 | Decided (2026-09-03) | 2026-09-03 | Swagger endpoint changes get proactively posted (link + summary) to the shared group |
| ASM-012 | Decided (2026-09-03) | 2026-09-03 | Reklamace-app auth: hardcoded per-user test logins first, Entra ID/OAuth built in parallel without blocking testing |
| ASM-011 | Decided (2026-09-02) | 2026-09-02 | Listing project gets a formal client-side Discovery phase before further development continues |
| ASM-010 | Decided (2026-09-02) | 2026-09-02 | Reklamace email drafts are never sent automatically — always created for human review first |
| ASM-009 | Decided (2026-09-02) | 2026-09-02 | Specs must include a business-signed hypothesis + acceptance-criteria section before build starts |
| ASM-008 | Decided (2026-09-02) | 2026-09-02 | Business-facing roadmap sheet trimmed to Ideas/Active only; dev detail moves to a VBS breakdown in a separate system |
| ASM-007 | Decided (2026-09-08) | 2026-09-02 | Reklamace dev ownership — Filip Černý designated single dev owner (2026-09-08), after Brázdil/Turner/Černý/Starenko multi-attribution history |
| ASM-006 | Open (2.5/4 resolved, 2026-09-15) | 2026-09-02 | BigHub roadmap sheet vs. transcripts — 4 ownership/spelling conflicts recorded; surname spelling and Lexie co-ownership resolved, invoicing/fakturace doprav conflict now leaning resolved (same initiative), reklamace ownership still open |
| ASM-005 | Decided (2026-09-02) | 2026-09-01 | Who's Who reference card cross-referenced against transcripts for 2026-09-01 status sync — verified by Marek |
| ASM-004 | Decided (2026-09-01) | 2026-09-01 | MaxBuddy changes touching the shared data model require Dr. Max analytics team review before shipping |
| ASM-003 | Decided (2026-08-25) | 2026-09-01 | Alfred stays a BigHub-internal asset, never delivered to clients |
| ASM-002 | Decided (2026-08-25) | 2026-09-01 | Marek's mandate is delivery ownership of the 9 existing Dr. Max streams, not new sales |
| ASM-001 | Decided (2026-08-25) | 2026-09-01 | Dr. Max client-side coordination unified into one role (Jindřich Tůma) |

## Entries

---

### ASM-169

| Field | Value |
|-------|-------|
| ID | ASM-169 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Jindřich Tůma (STK-003), Filip Černý (STK-006) |
| Status | Decided (2026-09-25) |

**Description**
Reklamace supplier data that doesn't live in Axapta is presented to logistics as an options table with risks and a BigHub-preferred option marked: Excel on SharePoint (possible, not recommended — no synchronization, no change audit trail, weak authorization, plus unknowns incl. whether BigHub can read it automatically via SharePoint API), SharePoint Lists, or Confluence. The original Axapta preference is withdrawn as unrealistic. The client picks and owns the risk; if they accept Excel's risks, BigHub delivers it as asked.

**Rationale**
Logistics keeps treating "Excel was agreed" as settled, though it was never presented that way — their real driver is having no other tool and refusing Axapta because it is being retired ([[ASM-139]]), not UX. BigHub's job is to surface risks, not to make the call for them.

**Impact**
- **Delivery**: Filip researches SharePoint Lists, Jindřich researches Confluence; the options table goes to the 2026-10-01 logistics meeting.
- **Relationship**: Moves the decision (and accountability) to the client, de-escalating the "BigHub doesn't want to deliver" narrative ([[ASM-122]]).
- **Tech**: Whatever store is chosen must be a secured table with easy automated reads, authorization and ideally an audit trail — ~2 editors per warehouse, viewers = all claims workers (count -tbd-).

---

### ASM-170

| Field | Value |
|-------|-------|
| ID | ASM-170 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Filip Černý (STK-006), Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-25) |

**Description**
Any non-Axapta store for Reklamace supplier data is an extension of Axapta, keyed by supplier account (účet dodavatele). No field is held in both systems.

**Rationale**
A separate BigHub database or table creates Axapta-sync problems and stale snapshots as supplier accounts change or suppliers leave. Filip: "we definitely don't want the same information in two places."

**Impact**
- **Data**: Supplier account, address and main contact stay in Axapta (committed); only fields Axapta won't hold go to the external store.
- **Tech**: The external store needs the supplier account as the join key.

---

### ASM-171

| Field | Value |
|-------|-------|
| ID | ASM-171 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Filip Černý (STK-006), Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-25) |

**Description**
The Reklamace "main contact" (hlavní kontakt, one email per supplier driving the email draft) concept is kept. It covers ~95–97% of suppliers; the <5 suppliers whose contact depends on goods category (e.g. food vs. drugs) are handled as exceptions in the spec.

**Rationale**
Agreed with Jana Egrmaierová and Tereza Foltýnová ~2–3 weeks earlier; the category-conditional exceptions surfaced later but are too few to abandon the simple model.

**Impact**
- **Scope**: The spec needs a defined exception mechanism (conditional contacts), not a redesign.

---

### ASM-172

| Field | Value |
|-------|-------|
| ID | ASM-172 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-25) |

**Description**
The per-case communication timeline/dashboard idea for Reklamace (web interface showing drafts sent, replies received, whose turn it is) is killed.

**Rationale**
Filip attributed the idea to Jan Sovka — one sentence in the spec, with no client response — and estimated it at weeks of work ("a new project"). Also answers the open "local case-status dashboard" question on the Reklamace brief.

**Impact**
- **Scope**: Removed from Reklamace scope; email threading in Outlook is the substitute for case history.

---

### ASM-173

| Field | Value |
|-------|-------|
| ID | ASM-173 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Filip Černý (STK-006), Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-25) |

**Description**
Filip builds a ~1 MD demo of the Reklamace email agent (text files, not wired to Outlook): a supplier reply triggers an LLM that extracts structured info (e.g. which of a multi-warehouse supplier's warehouses to ship to), prints it on the rozvozový list and drafts the next reply. Shown at the 2026-10-01 logistics meeting.

**Rationale**
Framed as a goodwill gesture ("the bone we throw them") after the Reklamace fallout — partly-built capability BigHub can offer. Full integration is considerably larger than the demo.

**Impact**
- **Timeline**: Demo due before 2026-10-01; production integration still blocked on the Microsoft Graph API from infra.
- **Relationship**: Aims to calm logistics before the Reklamace management meeting (pushed to the following week, Dudaško unavailable).

---

### ASM-174

| Field | Value |
|-------|-------|
| ID | ASM-174 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-25) |

**Description**
Rozvozový list fields sourced from Axapta — reklamace number, document number (RD) and issue date — are not in the Axapta API contract. Warehouse address/contact at the bottom could instead come from a location lookup (Brno / Praha / Pavlov, e.g. via machine IP).

**Rationale**
Missed when Lukáš worked on the contract while still new; Filip flagged it ~1 week earlier, Petr Sláma didn't respond (only Jana Egrmaierová did). Jindřich wants one complete Axapta requirements package so nothing more surfaces later; Filip will present it openly as BigHub's own debt. Related to the operator free-text gap in [[ASM-143]].

**Impact**
- **Delivery**: The rozvozový list can't be complete without these fields.
- **Relationship**: Another ask to Sláma, who is resisting Axapta development ([[ASM-139]]).

---

### ASM-175

| Field | Value |
|-------|-------|
| ID | ASM-175 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-25) |

**Description**
The Reklamace claims worker (zaměstnanec reklamací — a different person from the receiving foreman who uses BigHub's app) loses the old one-sheet-per-supplier Excel view that showed the rozvozový list with the supplier notes around it. Options: the flat table directly, a small web app (~1–2 MD: process info, rozvozový list preview, inputs like crate count), or the email agent alone.

**Rationale**
Filip surfaced the gap; Jindřich decided BigHub raises it to the client as an open question rather than solving it unilaterally. Filip prefers the worker still sees the notes the agent works from, but dislikes creating a new system to maintain.

**Impact**
- **Scope**: A web app would be outside the current spec.
- **UX**: Searching a ~300-row table per claim is a real usability regression vs. the old workflow.

---

### ASM-176

| Field | Value |
|-------|-------|
| ID | ASM-176 |
| Created | 2026-09-25 |
| Source | 2026-09-25-reklamace-supplier-data-source-options |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-25) |

**Description**
Kontakty (unstructured free-text contacts, typically 0–2 per supplier), Poznámky (notes) and Typ odvozu (own-pickup flag, ~70–75 suppliers) have no agreed storage location — Axapta has not committed to them. Separately, Axapta needs ~2 hours of manual data entry to replace supplier HQ addresses with real warehouse return addresses; agreed in principle, not done, no owner.

**Rationale**
Petr Sláma's team won't develop further on Axapta given its planned retirement ([[ASM-139]]); only supplier account, address and main contact are committed.

**Impact**
- **Data**: These fields are the main content of the external store under [[ASM-169]].
- **Delivery**: Typ odvozu is printed on the rozvozový list (warehouses sort own-pickup vs. standard shipments), so it must be sourced somewhere.

---

### ASM-168

| Field | Value |
|-------|-------|
| ID | ASM-168 |
| Created | 2026-09-25 |
| Source | 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics |
| By | Alana Sihelská (STK-004), Marek Pillár (STK-001) |
| Status | Open (2026-09-25) |

**Description**
TEO/OCR started from a cold call: Radim Švarc phoned Alana, described a twice-yearly service with a large volume of manually processed documents, and suggested automation. Unlike the other streams, where Jan Sovka interviewed people and shaped the use cases himself, nobody at BigHub has done discovery on the full TEO process or what else happens in it. Possible follow-on work includes tracking when the next service is due. The per-cycle manual effort is also unknown (Alana doesn't know if it's, say, a month of work), which reopens Jan Sovka's recurring question of whether a task done once or twice a year justifies investment.

**Rationale**
Alana expects the stream to be a success and Dr. Max to want more, "but we don't know in which direction" [translated from Slovak]. A fast, visible win brings positive feedback for free, unlike the voicebot and other streams that drag on for a year.

**Impact**
- **Scope**: Follow-on TEO work, on this stream or a new one with the same team, is undefined until discovery happens.
- **Business value**: Per-cycle effort is needed to judge ROI. See the volume conflict in the TEO/OCR project-knowledge entry (steady ~250 docs/week vs. two batches a year).
- **Relationship**: Discovery doubles as relationship building with Radim, the route to Burda ([[ASM-166]]).

---

### ASM-167

| Field | Value |
|-------|-------|
| ID | ASM-167 |
| Created | 2026-09-25 |
| Source | 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics |
| By | Alana Sihelská (STK-004) |
| Status | Open (2026-09-25) |

**Description**
BigHub's Dr. Max engagement is budgeted as roughly 3 FTE for a full year starting about May 2026, which is ~3 × 20 = ~60 MD/month. Capacity is a shared pool: the team can direct it at any stream, and going somewhat over in a given month is acceptable. Little work happened in the first months, so unused budget has accumulated. The only constraint Alana named: if "Tomáš" says no work on TEO, the capacity goes elsewhere. **Unconfirmed**: (1) which Tomáš is meant, assumed to be Tomáš Dudaško (STK-010, budget holder), not Tomáš Burda; (2) how much budget has accumulated (Jindřich to find out); (3) whether Jindřich Tůma is inside the 3 FTE or on top of it (a 4-FTE pool). Alana was counted in the 3 FTE while on the account and suspects Jindřich is extra; he keeps a September capacity table.

**Rationale**
Marek asked because Filip Černý and others propose extra work, and he didn't know whether saying yes would overspend or take capacity from another stream.

**Impact**
- **Delivery**: Marek can approve reasonable dev initiatives inside the pool without per-item sign-off.
- **Budget**: The actual headroom stays unknown until Jindřich confirms the accumulated amount and his own inclusion.

---

### ASM-166

| Field | Value |
|-------|-------|
| ID | ASM-166 |
| Created | 2026-09-25 |
| Source | 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics |
| By | Marek Pillár (STK-001), Alana Sihelská (STK-004) |
| Status | Decided (2026-09-25) |

**Description**
Before proposing any TEO/OCR direction beyond Excel, Marek consolidates Jura Brázdil's comments and holds an informal, non-committal call with Radim Švarc to gauge his openness to further build or innovation. Radim is treated as the entry point; Tomáš Burda holds the decision on where TEO goes next.

**Rationale**
Alana: Radim is young and capable but has no decision-making say; Burda is older and "pricklier". Marek: Radim is the foot in the door, since he'd never get to Burda directly.

**Impact**
- **Relationship**: Protects the proposal from landing cold with Burda.
- **Timeline**: The Phase 2 proposal ([[ASM-165]]) waits on the Radim call.

---

### ASM-165

| Field | Value |
|-------|-------|
| ID | ASM-165 |
| Created | 2026-09-25 |
| Source | 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics |
| By | Marek Pillár (STK-001), Alana Sihelská (STK-004) |
| Status | Decided (2026-09-25) |

**Description**
TEO/OCR service protocols arrive only twice a year, in spring and autumn. The autumn 2026 cycle is already running, so the review step stays on Excel for this cycle. A non-Excel review solution becomes the Phase 2 target, ready before the spring 2027 cycle, with a longer-term vision after that. This updates the 2026-09-24 one-pager for Alana (`documents/internal/2026-09-24-teo-ocr-excel-vystup-ai-framing-odporucania-radim.md`), which recommended building a standalone review app now.

**Rationale**
Changing the process mid-cycle has no payoff. The spring 2027 cycle gives enough runway, and for BigHub a frontend is no longer an expensive or long piece of work for Jura. Alana questions why Dr. Max would want Excel at all.

**Impact**
- **Scope**: Resolution path for [[ASM-130]] (Excel-only, unassisted review step).
- **Timeline**: Phase 2 due before spring 2027. The earlier "November inspection cycle" target for the pilot is in question.
- **Relationship**: Depends on Radim's appetite ([[ASM-166]]).

---

### ASM-164

| Field | Value |
|-------|-------|
| ID | ASM-164 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Jura Brázdil (STK-026), Jindřich Tůma (STK-003) |
| Status | Open (2026-09-24) |

**Description**
Release sequence once the DB on the new cluster is reachable: deploy the platform to the new cluster, migrate MaxBuddy (currently outside the platform), deploy the Max chatbot (for public access), fix some security concerns (~14 days total), then wire in the already-built web frontend. Jura estimates ~3 weeks; Jindřich plans 4 given BDC turnaround. MaxBuddy stays top priority. The trigger is disputed: Dudaško says Vladislav Tvarůžek reported DB access done on 2026-09-24, while BigHub's last check (2026-09-23 15:30) said it still failed. Jura had handed Vláďa a repro script (old cluster works, new doesn't) and will retest right after the meeting.

**Rationale**
The whole platform, MaxBuddy rollout and chatbot go-live chain depends on this one access item.

**Impact**
- **Timeline**: Directly gates [[ASM-100]] and the MaxBuddy rollout.
- **Relationship**: Both sides are wary of infra "it's done" claims.

---

### ASM-163

| Field | Value |
|-------|-------|
| ID | ASM-163 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Tomáš Dudaško (STK-010) |
| Status | Decided (2026-09-24) |

**Description**
Jura's idea of a per-project roadmap/blockers view in the platform (what waits on BigHub vs. Dr. Max) should live in the Azure DevOps setup Jindřich is preparing. The platform may at most carry an admin view, plus release information.

**Rationale**
Avoids duplicating the work-tracking tool.

**Impact**
- **Scope**: Removes a feature from the platform Phase 1 scope.

---

### ASM-162

| Field | Value |
|-------|-------|
| ID | ASM-162 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Tomáš Dudaško (STK-010), Jura Brázdil (STK-026) |
| Status | Decided (2026-09-24) |

**Description**
The platform aggregates technical-status telemetry across projects (e.g. for MaxBuddy: Azure logs, services, DB, pods), correlates signals (several small problems → one big alert), and pushes alerts to Dr. Max's Zabbix. It also keeps a full incident history for auditability (certifications/legal) and a BigHub developer panel for manual incident notes.

**Rationale**
Dudaško: "this is the central point". Jura briefly questioned routing Zabbix via BigHub vs. directly, but didn't pursue it.

**Impact**
- **Scope**: Adds Zabbix integration and incident audit to the platform roadmap (see [[ASM-115]]).
- **Compliance**: Supports audit requirements.

---

### ASM-161

| Field | Value |
|-------|-------|
| ID | ASM-161 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Tomáš Dudaško (STK-010), Jindřich Tůma (STK-003), Marek Pillár (STK-001) |
| Status | Decided (2026-09-24) |

**Description**
Each Dr. Max department (logistics, marketing via Marek Dvořák, others) should have its AI initiatives captured in the tracker format and prioritized as a ready backlog by end of November 2026, so management can set 2027 goals. Logistics is split: Part A finishes the specs of the two running projects (Reklamace, Fakturace doprav); Part B captures new topics. Logistics sets its own priorities, and Dudaško decides go/no-go. November is Jindřich's ideal plan, not set in stone; Dudaško accepts it but would prefer earlier.

**Rationale**
Logistics proactively wants to map more AI initiatives with Marek. Jindřich explicitly guarded Marek from being pulled into specifying many topics at once.

**Impact**
- **Workload**: A significant new stream for Marek on top of running projects.
- **Timeline**: The end-of-November target is at risk if running projects need more attention.

---

### ASM-160

| Field | Value |
|-------|-------|
| ID | ASM-160 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Tomáš Dudaško (STK-010), Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-24) |

**Description**
For each tracker row that is live or close to live, BigHub prepares a narrative showing the original assumption (e.g. 230 → 130 Kč per item), interim state, current post-deployment state, and trend or learning curve, making the realized saving visible (e.g. × ~3,600 items/quarter). Jindřich presents the first set at the 2026-09-29 project meeting and previews it with Dudaško beforehand.

**Rationale**
Dudaško wants realized value demonstrable to management, not just modeled.

**Impact**
- **Relationship**: A high-visibility deliverable to management next week.
- **Data**: Requires actual post-deployment metrics per initiative.

---

### ASM-159

| Field | Value |
|-------|-------|
| ID | ASM-159 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Tomáš Dudaško (STK-010), Jindřich Tůma (STK-003), Marek Pillár (STK-001) |
| Status | Decided (2026-09-24) |

**Description**
Beyond business value and KPIs, each initiative must define how each KPI will be measured, including the current-state baseline measured before implementation (e.g. "25× faster" needs today's speed measured first). Marek will add a measurement column and collect methods from each business owner, starting with logistics (Tereza Foltýnová). Phase-level success milestones are case by case.

**Rationale**
Dudaško's "B/C": without a measurement plan you can't prove the value is delivered. Petr Neuman's quarterly cost-per-item tracking (Listing) is the model case.

**Impact**
- **Delivery**: Adds baseline-measurement work before or alongside implementation.
- **Reporting**: Feeds the AI Platform's KPI reporting (see [[ASM-162]]).

---

### ASM-158

| Field | Value |
|-------|-------|
| ID | ASM-158 |
| Created | 2026-09-24 |
| Source | 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko |
| By | Tomáš Dudaško (STK-010), Jindřich Tůma (STK-003), Marek Pillár (STK-001) |
| Status | Decided (2026-09-24) |

**Description**
Every new AI initiative proposed by any Dr. Max department must bring a goal description, an owner-guaranteed business value, 1–3 KPIs, and email confirmation from the business owner, captured in the Business Quantification tracker format. Initiatives are prioritized by modeled annual value ("going after the biggest ones"), and Dudaško (or management) decides go/no-go.

**Rationale**
Dudaško had always asked the business for this and been refused ("we've never done it, we won't do it"). BigHub, as the "new broom", got it done. Making owners the guarantors of their figures, with email confirmation as an audit trail, fixes the earlier pattern of loose "let's see how it goes" engagement.

**Impact**
- **Prioritization**: Gives a single comparable basis for the portfolio (see [[ASM-125]]).
- **Workload**: Marek owns enforcing this discipline with business users.
- **Relationship**: A major trust win with Dudaško.

---

### ASM-157

| Field | Value |
|-------|-------|
| ID | ASM-157 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Kateřina Kadlecová (STK-037), Šárka Andělová (STK-050), Jura Brázdil (STK-026) |
| Status | Decided (2026-09-24) |

**Description**
The quick-reply bubbles stay. The intro text moves down to sit directly above them, so the chat behaves like a normal chat (newest at the bottom, history scrolling up). Separately, using logged-in doktormax.cz profile data (e.g. gender for salutation) is deferred until the widget is integrated on the site: it needs technical plumbing to the one-line embed and probably consent.

**Rationale**
Dr. Max's experience is that customers don't read help text, but they want a clear menu. Jura's URL-contextual bubbles (built the previous week) complement this. Profile data would help with the gender-neutral address problem but can't be done before integration.

**Impact**
- **UX**: A small layout change, ticketed by Kadlecová.
- **Compliance**: Profile use will need consent handling (see [[ASM-102]]).

---

### ASM-156

| Field | Value |
|-------|-------|
| ID | ASM-156 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Marek Pillár (STK-001) |
| Status | Decided (2026-09-24) |

**Description**
Lexie's redesign will be part of the eventual AI-platform-wide redesign rather than a separate effort. Minor visual tweaks (padding, borders) are low priority and can be logged in X-Manager so they aren't lost. Focus now is on the technical side.

**Rationale**
Design authority sits at the platform level ([[ASM-060]]) and platform design is deliberately deferred until navigation is validated with Dudaško ([[ASM-147]]).

**Impact**
- **Delivery**: Avoids rework on Lexie-specific design.
- **Relationship**: Sets expectations with the CC team on cosmetic requests.

---

### ASM-155

| Field | Value |
|-------|-------|
| ID | ASM-155 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Simona Mertová (STK-017) |
| Status | Open (2026-09-24) |

**Description**
Dr. Max wasn't satisfied with the sample voices, which were ElevenLabs marketing samples. The full product offers many more voices, character tuning, voice cloning and a voice designer, likely behind payment (Jura's rough guess: thousands of Kč). Mertová asked whether licences are covered within the project or she must find budget herself. Jindřich doesn't know and will find out, possibly via an ElevenLabs Q&A meeting.

**Rationale**
Nobody on the call could answer. Jindřich joined the project mid-stream.

**Impact**
- **Commercial**: Unassigned cost line.
- **Delivery**: Voice selection for Maxie is stalled until this is resolved.

---

### ASM-154

| Field | Value |
|-------|-------|
| ID | ASM-154 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Simona Mertová (STK-017), Kateřina Kadlecová (STK-037), Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-24) |

**Description**
Dr. Max already runs a "Maxí" in its Atlantis-hosted IVR, built ~2–3 years ago with another vendor; Tecl (Atlantis, STK-033) knows the setup, and the PBX is rented from Atlantis. The BigHub voicebot must copy that integration and flow exactly, not a new design. Maxie is split by IVR topic branch (order tracking, prescriptions, etc.), not one assistant answering everything. The SIP trunk still has to be configured; Atlantis is 2nd of 5 infra requests queued at BDC.

**Rationale**
Mertová was not invited to BigHub's Atlantis meeting ~3 weeks ago, and colleagues were unaware of the existing solution, although she had told Lukáš this when he owned it. Dr. Max has already done IVR prep work (recording structure, voice tree) assuming the same design. Jindřich confirmed reuse is the direction and will convene a joint meeting (Mertová, Honza Zelený, Tecl).

**Impact**
- **Relationship**: A trust dent from lost continuity during the ownership handover; quick follow-through matters.
- **Delivery**: Reusing a proven design lowers technical risk; the SIP trunk and BDC access remain blockers (see [[ASM-022]]).

---

### ASM-153

| Field | Value |
|-------|-------|
| ID | ASM-153 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Jura Brázdil (STK-026), Kateřina Kadlecová (STK-037), Simona Mertová (STK-017) |
| Status | Decided (2026-09-24) |

**Description**
Dr. Max's customer-safe "public methodologies" (derived from internal CC playbooks, ~2–20 pages each, PDF) will be used for follow-up questions (e.g. reservation holding periods). Too large for the prompt, so Max will connect to the AI platform's existing RAG/search. The platform rewrite will give Dr. Max one place with usage reporting, an instant kill switch to pull the chatbot off the site, and self-service document settings (choosing which sources Max draws from). The order-tracking/reservation methodology is essentially done and goes first.

**Rationale**
Jura: "pošlete PDFko, formát je mi šuma fuk" [translated from Czech: "send the PDF, format doesn't matter"]. RAG already exists on the neighboring platform project, so reusing it avoids a separate build. Timing is open: it's a bigger piece of work.

**Impact**
- **Delivery**: New dependency between Max and the AI platform workstream.
- **Scope**: Adds a document-management capability to the platform roadmap (see [[ASM-115]]).

---

### ASM-152

| Field | Value |
|-------|-------|
| ID | ASM-152 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Simona Mertová (STK-017) |
| Status | Decided (2026-09-24) |

**Description**
The new end-conversation flow (header button, or detected "děkuju"/goodbye) currently shows a free-text feedback box. Mertová confirmed free text is fine during testing but must not reach the public; Jura agreed to remove it.

**Rationale**
Consistent with the earlier decision that public in-chat feedback is a star/emoji rating with no free text ([[ASM-017]]).

**Impact**
- **Delivery**: Small change before phase 3 (public toggle).

---

### ASM-151

| Field | Value |
|-------|-------|
| ID | ASM-151 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Jura Brázdil (STK-026), Kateřina Kadlecová (STK-037) |
| Status | Decided (2026-09-24) |

**Description**
Max's first message is predefined and not affected by the prompt. Dr. Max will send the exact sentence, which must include an AI Act disclosure ("Dobrý den, jsem Max, AI virtuální asistent"), a requirement from Dr. Max Legal. Dr. Max also wants to stop the opener listing every capability, since that won't scale to 10+ topics.

**Rationale**
A fixed opener gives Legal control over the disclosure wording and keeps it consistent. Wider GDPR requirements are still being defined by Dr. Max Legal (see [[ASM-102]]).

**Impact**
- **Compliance**: Closes the one confirmed legal requirement so far.
- **Delivery**: Blocked on Dr. Max sending the wording.

---

### ASM-150

| Field | Value |
|-------|-------|
| ID | ASM-150 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-24) |

**Description**
Dr. Max's tone input to the Max system prompt should be a short, comma-separated list of keywords (e.g. "buď zdvořilý, vykej"), not the ~2-paragraph first-person brief agreed on 2026-09-17. Core rules (vykání, no medical advice, tool usage) are already covered by BigHub's own prompt.

**Rationale**
The brief Dr. Max sent was about as long as the main prompt and risked overloading GPT-5 mini (see [[ASM-149]]). Kadlecová noted the first-person format itself inflated the text. Shorter input has a bigger effect on a small model.

**Impact**
- **Quality**: Reduces the risk of instruction conflicts and dropped rules.
- **Process**: Supersedes the 2026-09-17 tone-brief guidance recorded in project-knowledge.

---

### ASM-149

| Field | Value |
|-------|-------|
| ID | ASM-149 |
| Created | 2026-09-24 |
| Source | 2026-09-24-lexie-max-maxie-weekly-sync |
| By | Jura Brázdil (STK-026) |
| Status | Open (2026-09-24) |

**Description**
The Max chatbot runs on GPT-5 mini, which Jura estimates can reliably hold roughly 10–12 instructions before some start dropping at random. With BigHub's own ~1,200-character system prompt plus a growing list of edge-case rules, Max is at that ceiling: early hallucination creep is showing, and tone issues Dr. Max raised ("přátelská připomínka", repeated apologies to abusive users, gender-neutral Czech address) can't be fixed reliably with prompting alone. Upgrading (e.g. to full GPT-5.4) is the fix on the table; Jura will bring a cost projection across models and a model switcher on the test page. Monthly spend can be capped, with the widget auto-hiding once the cap is reached.

**Rationale**
Starting on the cheapest model was deliberate for development. Quality now depends on a cost decision, which Dr. Max needs to own with numbers in hand. Corrects project-knowledge, which recorded a GPT-5.1→5.4 upgrade for Max on 2026-09-17.

**Impact**
- **Quality**: Several open tone/behavior complaints are blocked on this decision, not on BigHub effort.
- **Cost**: Recurring run cost rises with a bigger model; mitigated by a monthly cap.
- **Relationship**: Reframes quality complaints as a joint cost/quality trade-off rather than a delivery gap.

---

### ASM-148

| Field | Value |
|-------|-------|
| ID | ASM-148 |
| Created | 2026-09-23 |
| Source | 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting |
| By | Jura Brázdil (STK-026), Marek Pillár (STK-001) |
| Status | Open (2026-09-23) |

**Description**
How the AI Platform will report combined AOAI/token costs across test and prod environments is undecided. Options discussed: prod pulling directly from a narrow test-side reporting endpoint, test periodically pushing stats to an intermediary store prod reads, or a global test/prod environment switcher in the UI (Marek's suggestion, which Jura pushed back on).

**Rationale**
Dudaško has previously indicated he wants combined cost visibility across both environments, at one point suggesting test projects could appear grayed-out within the prod view. A full network bridge between test and prod clusters raises security concerns Jura wants to avoid; a global environment switcher risks implying "everything I see now is test-only," which conflicts with the combined-view want. Not blocking the Friday demo — flagged as a discrete follow-up.

**Impact**
- **Delivery**: Needs resolving before real cost-reporting is built, but doesn't block navigation/UX validation with Dudaško.
- **Security**: Whatever mechanism is chosen must avoid a genuine network bridge between test and prod.

**Update (2026-09-24)**: Partly answered. Asked directly, Dudaško wants everything, with a breakdown ("mě zajímá všechno, ale když to bude mít rozpad, tak je to lepší" [translated from Czech: "I'm interested in everything, but a breakdown is better"]). Jura will show test, prod and total, and also prototyping token spend. The technical mechanism is still open. Source: 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko

---

### ASM-147

| Field | Value |
|-------|-------|
| ID | ASM-147 |
| Created | 2026-09-23 |
| Source | 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting |
| By | Jura Brázdil (STK-026), Marek Pillár (STK-001) |
| Status | Decided (2026-09-23) |

**Description**
The current AI Platform prototype deliberately excludes any visual/color/design-language work. The goal at this stage is only to validate with Dudaško whether the navigation and interaction structure feels right — design iteration comes after that's confirmed.

**Rationale**
Aligned between Jura and Marek the day before this session. Reinforces the existing lean-MVP framing (see [[ASM-045]]) — sequencing infrastructure fundamentals (cost/FinOps reporting, per-project status) ahead of visual polish avoids wasted design work if the navigation structure itself needs to change after Dudaško's feedback.

**Impact**
- **Delivery**: The Friday demo to Dudaško will present navigation/structure only; any design feedback gets deferred to a later pass.
- **Relationship**: Jura has a prepared framing ("we hit 9/10 of your requirements fast, categorization/colors come next") if Dudaško raises design prematurely.

**Update (2026-09-24)**: Navigation/interaction was validated with Dudaško, so the condition for starting design work is met. Source: 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko

---

### ASM-146

| Field | Value |
|-------|-------|
| ID | ASM-146 |
| Created | 2026-09-23 |
| Source | 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting |
| By | Jura Brázdil (STK-026) |
| Status | Open (2026-09-23) |

**Description**
A cross-platform RAG "ask anything" agent — with access to everything a given user can already click into (reporting, docs, roadmap) so they could just ask a question instead of navigating — is a concept both Jura and Marek see as valuable long-term, but deliberately not being built now given how few projects are currently active on the platform.

**Rationale**
Echoes an idea from Marek's earlier Databricks-styled benchmark artifact, independently proposed by Jura without having seen that artifact. Building it now would be premature relative to platform maturity (only ~3 active projects) — kept in reserve to offer only if Dudaško specifically asks for more than the navigation-based approach, consistent with a "show less now, layer on later" client-management principle.

**Impact**
- **Delivery**: No work planned on this now; revisit once project count grows or Dudaško asks for it directly.
- **Relationship**: Held back deliberately rather than offered proactively, to avoid inviting premature scope demands.

---

### ASM-145

| Field | Value |
|-------|-------|
| ID | ASM-145 |
| Created | 2026-09-23 |
| Source | 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting |
| By | Jura Brázdil (STK-026) |
| Status | Open (2026-09-23) |

**Description**
A real security gap was found during platform build-out: MCP server registration currently leaks secret/header values to any agent that reads MCP server descriptions.

**Rationale**
Discovered by Jura while working on the platform's internal architecture — flagged as something that needs sealing before further build-out, ahead of migrating MaxBuddy and Chatbot Max directly under the platform.

**Impact**
- **Security**: Real exposure risk if left unaddressed before more projects/agents are wired into the platform.
- **Delivery**: Part of Jura's pre-database-access prep work, alongside other platform hardening.

---

### ASM-144

| Field | Value |
|-------|-------|
| ID | ASM-144 |
| Created | 2026-09-23 |
| Source | 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-23) |

**Description**
"Platform" and "Lexie" will now be treated as explicitly separate concepts. The team had previously been calling Lexie itself "the platform" — Jura believes this conflation explains part of Dudaško's frustration, since he wants an actual platform and what existed under that name was really just Lexie wearing the label.

**Rationale**
Surfaced while discussing multi-department Lexie knowledge-base navigation — platform-level features (navigation, cross-project reporting, adoption metrics) are a different layer of concern than Lexie-level features (its own internal KB/UX behavior, e.g. a possible future single cross-department knowledge base).

**Impact**
- **Communication**: Going forward, conversations with Dudaško should distinguish platform asks from Lexie-specific asks explicitly, rather than let them blend together as they have been.
- **Scope**: Lexie-level feature requests (like a unified cross-department KB) route as Lexie decisions, not platform decisions.

---

### ASM-143

| Field | Value |
|-------|-------|
| ID | ASM-143 |
| Created | 2026-09-23 |
| Source | 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-23) |

**Description**
A previously-unaddressed gap in Reklamace: the "rozvozový list" (delivery/dispatch list) needs free-text input from warehouse workers themselves (e.g. a complaint/reklamace number), but now that BigHub generates this document, there's no defined source for that operator-entered text — in the old Excel-based process workers could type anything directly.

**Rationale**
Nobody had accounted for this gap before; it surfaced only once the address-field flow (via PUME) was already working and tested. To be raised at the next logistics status meeting.

**Impact**
- **Delivery**: Needs a defined data-source/input mechanism before the rozvozový list can be considered complete, even though the address portion already works.
- **Scope**: A new, previously invisible requirement — worth tracking separately from the address-sourcing work already done.

**Update (2026-09-25)**: A related gap surfaced — Axapta-sourced rozvozový list fields (reklamace number, RD number, issue date) are also missing from the API contract; see [[ASM-174]]. Source: 2026-09-25-reklamace-supplier-data-source-options.

---

### ASM-142

| Field | Value |
|-------|-------|
| ID | ASM-142 |
| Created | 2026-09-23 |
| Source | 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-23) |

**Description**
Fakturace doprav's API-contract renegotiation with Petr Sláma (STK-034) is stuck. Filip's original proposal (backed by Jan Sovka) was rejected outright with no counter-proposal; a further simplified version sent the next day got only a "no time, will look next week" reply.

**Rationale**
The original API contract doesn't provide enough information to validate certain checks, making the current spec undeliverable as-is. Filip is frustrated by the lack of technical reasoning behind Sláma's refusals — without a counter-argument, there's nothing to iterate against. Jindřich plans to push directly with Sláma, with Filip briefing him on the technical specifics first.

**Impact**
- **Delivery**: Fakturace doprav's backlog is ~95% done but genuinely blocked on this contract approval — no further work possible until resolved.
- **Timeline**: See [[ASM-141]] — this delay now explicitly counts against the schedule.

---

### ASM-141

| Field | Value |
|-------|-------|
| ID | ASM-141 |
| Created | 2026-09-23 |
| Source | 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-23) |

**Description**
Logistics delivery timelines will now explicitly factor in client-side response delays (e.g. waiting a week-plus on a decision from Dr. Max's side), not just delays attributable to BigHub.

**Rationale**
Prompted directly by the stuck Fakturace doprav API-contract renegotiation ([[ASM-142]]) — Jindřich's reasoning: if Dr. Max's side can point to things they're waiting on from BigHub, BigHub should equally be able to point to things it's waiting on from them, and have that reflected in the schedule rather than absorbed silently.

**Impact**
- **Expectation management**: Timeline communications going forward should name specific client-side waits as schedule inputs, not just internal BigHub effort.
- **Relationship**: To be communicated "elegantly," not as a confrontational stance.

---

### ASM-140

| Field | Value |
|-------|-------|
| ID | ASM-140 |
| Created | 2026-09-23 |
| Source | 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-25) |

**Description**
Jindřich cited MaxBuddy's annual business value as ~130M Kč in this session, previewing the near-final Business Quantification tracker. This differs from the ~81M Kč figure discussed directly with Marek on 2026-09-22 (see [[ASM-098]], [[ASM-099]]).

**Rationale**
Not assumed to be an update superseding the earlier figure — flagged as an open discrepancy needing reconciliation before the tracker is presented at a future status, since the tracker is meant to have each business owner's sign-off on validated numbers.

**Impact**
- **Data quality**: The Business Quantification tracker should not be treated as finalized until this is resolved.
- **Prioritization**: Whichever figure is correct feeds directly into the portfolio priority-ranking discussion (see [[ASM-125]]).


**Resolution (2026-09-25)**: The BQ tracker (sheet `new_Přehled`), confirmed by the PM as the source of truth for business quantification, sets MaxBuddy at **81,000,000 Kč/yr revenue uplift** (60M dispensing cases × 75% coverage × 1.2% conversion × 150 Kč). The ~130M figure is superseded.
---

### ASM-139

| Field | Value |
|-------|-------|
| ID | ASM-139 |
| Created | 2026-09-23 |
| Source | 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers |
| By | Tomáš Dudaško (STK-010), relayed by Jindřich Tůma (STK-003) |
| Status | Open (2026-09-23) |

**Description**
Dudaško plans to retire Axapta within roughly the next 6 months, calling it too expensive to keep developing against. He's willing to accept higher near-term development cost on Reklamace now for a solution that can be cleanly reapplied on whatever system replaces it.

**Rationale**
Directly shapes the pending Reklamace continue-or-close decision ([[ASM-122]]) — a decision meeting (Jindřich, Dudaško, Rudolf Žůrek, Petr Spilka, Jan Žižka) is needed to align on what "portable to the replacement system" actually requires from BigHub's side.

**Impact**
- **Scope**: Reklamace's technical design may need to prioritize system-agnostic patterns over Axapta-specific optimizations, even at higher near-term cost.
- **Timeline**: The ~6-month Axapta retirement window is a soft constraint worth tracking, though Jindřich has no further detail on it yet.

**Update (2026-09-25)**: Petr Sláma cites the planned retirement as his reason for doing no further Axapta-side development, which is why several Reklamace supplier fields have no home ([[ASM-176]]). Source: 2026-09-25-reklamace-supplier-data-source-options.

---

### ASM-138

| Field | Value |
|-------|-------|
| ID | ASM-138 |
| Created | 2026-09-23 |
| Source | Redline review of Fakturace doprav spec (comparison against `Logistika - 2026-06 Fakturace_doprav_specifikace_3.docx`), this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-23) |

**Description**
The May/June 2026 spec draft described two carrier confirmations: an immediate post-scan receipt confirmation, and a second, separate post-billing-period notice on whether documents/km were approved and payment would follow. The current (September) spec and every reviewed 2026-09 meeting note only describe the first (single post-scan) confirmation — the second never appears anywhere in the newer material.

**Rationale**
Found comparing the June 2026 draft line-by-line against the current spec and all available Fakturace doprav meeting notes. No meeting explicitly discusses removing the second notice — it's unclear whether this was a deliberate scope cut or simply dropped during the spec rebuild.

**Impact**
- **Delivery**: if ViaPharma actually expects a post-billing approval/payment notice, this is a silent scope gap, not a confirmed decision.
- **Relationship**: needs a direct yes/no from Jan Žižka rather than being assumed dropped.

---

### ASM-137

| Field | Value |
|-------|-------|
| ID | ASM-137 |
| Created | 2026-09-23 |
| Source | 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo + code audit (cz-ai-logistics), this session |
| By | Jan Žižka, Jakub Turner |
| Status | Decided (2026-09-23) |

**Description**
On the 2026-09-10 client demo, Jan Žižka raised mailbox-overload risk (20+ emails/day with attachments) if every scan session emails the carrier individually. Jakub Turner confirmed images are already compressed client-side (kilobyte-range) and proposed one consolidated email per scan session rather than a storage-link approach, which Žižka rejected outright (carriers shouldn't get storage access). This resolves the mechanism. A full code audit (2026-09-23) found no email-sending code anywhere in `transport_invoicing_api` or `transport_invoicing_web` — the feature is entirely unbuilt, not merely unlocated.

**Rationale**
Meeting note capture plus direct code search (smtp/sendgrid/mailgun/mail/notify/graph.microsoft) across both apps and Helm values, this session.

**Impact**
- **Delivery**: this decision isn't yet reflected against roadmap item #6 ("Potvrzení přepravci") — needs to be added, along with a note that the email-sending feature itself still needs to be built from scratch, not just triggered.

---

### ASM-136

| Field | Value |
|-------|-------|
| ID | ASM-136 |
| Created | 2026-09-23 |
| Source | Business Quantification workshop screenshots (owner Jan Žižka, record dated 2026-08-01), provided by PM this session |
| By | Jan Žižka |
| Status | Open (2026-09-23) |

**Description**
A more detailed Business Quantification workshop breakdown (status "K doplnění" — not yet formally approved) quantifies Fakturace doprav's saving as 10.5 h/day across 3 warehouses — Expedice Ostrava 1.5 h/den (1 pracovník), Xdock Brno 1 h/den (1 pracovník), Doprava Pavlov 4+2+2 h/den (3 pracovníci) — at a 50,000 Kč/month rate, ≈ 787,500 Kč/year, covering Fáze 1 and 2 combined (Fáze 2 doesn't add a separately-counted saving). Four concrete KPI targets were captured for the first time: Fáze 1 ≥40% of cases processed fully without manual intervention; Fáze 2 ≥40% of shipments with auto-verified km; overall administrative time-fund reduced ~40%; ≥60% of temperature records auto-checked without manual reading.

**Rationale**
Both this figure and the earlier ~16 h/day / ~1.5M Kč/year Fermi estimate (captured 2026-09-15 from Tereza Foltýnová, who herself flagged it as possibly too large and pending verification with Jan Žižka) trace back to the same underlying Ableneo ~90h/month source figure — but this workshop number is a direct per-warehouse breakdown from the initiative owner himself, and is likely the more reliable of the two.

**Impact**
- **Data**: recommend project-knowledge and any client-facing materials adopt 787,500 Kč/year, superseding the 2026-09-15 estimate — pending formal confirmation, since status is still "K doplnění."
- **Delivery**: the four KPI targets should replace the generic candidate metrics currently in the spec's KPI section, once formally approved.

---

### ASM-135

| Field | Value |
|-------|-------|
| ID | ASM-135 |
| Created | 2026-09-23 |
| Source | Code audit (cz-ai-logistics, `scan_session_projection.py`), this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-23) |

**Description**
ZOPV is modeled as single-instance per AR in code (`_SINGLE_INSTANCE_TYPES`, `_group_key`). A second vehicle's ZOPV scanned for the same route is treated as a new "generation" (correction) of the first document and supersedes it, rather than being filed as a separate document. This is undocumented, unintended behavior — not a deliberate design choice — for the "trasy rozdělené na více vozidel" case the spec currently treats as a pure open design question.

**Rationale**
Found during code audit; the spec text discusses this scenario as something still to be designed with J. Žižka, without knowing the code already has concrete (risky) behavior in this case today.

**Impact**
- **Delivery**: real risk of silent data loss if a multi-vehicle route is scanned before a deliberate solution is designed. Should be prioritized ahead of being treated as a purely future design conversation.

---

### ASM-134

| Field | Value |
|-------|-------|
| ID | ASM-134 |
| Created | 2026-09-23 |
| Source | Code audit (cz-ai-logistics, `page_prompt.py`, `page_extraction.py`), this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-23) |

**Description**
TEMPERATURE_LOG exists as a document type in the Axapta data contract, the PDF confirmation renderer, and test fixtures — but the OCR classification prompt and extraction schema have no variant for it. A driver scanning a temperature log today gets classified UNRECOGNIZED and the document is rejected.

**Rationale**
Found during code audit; directly contradicts the current spec's claim "potvrzeno v kódu (6 typů, ne 5)" for document-type coverage.

**Impact**
- **Delivery**: MVP claims 6 recognized document types; only 5 are actually reachable from a scan today. Needs a decision — build classification now, or defer to Fáze 2 alongside the rest of temperature handling.

---

### ASM-133

| Field | Value |
|-------|-------|
| ID | ASM-133 |
| Created | 2026-09-23 |
| Source | Code audit (cz-ai-logistics, `page_extraction.py`), this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-23) |

**Description**
Code shows the AR pairing field already exists and is functional on both the ZOPV and OPIATY (narcotics-confirmation) document types, with barcode-priority-over-printed-AR resolution logic already implemented. The current spec text (sourced from P. Sláma) says this pairing key is still missing on both types and "bude doplněno."

**Rationale**
Found during code audit — a direct contradiction between what's communicated as an outstanding dependency and what the deployed code actually does.

**Impact**
- **Delivery**: the corresponding open dependency ("rozšíření párovacího klíče AR na ZOPV a OPL") may already be resolved — needs verification with P. Sláma before continuing to track it as outstanding work.

---

### ASM-132

| Field | Value |
|-------|-------|
| ID | ASM-132 |
| Created | 2026-09-23 |
| Source | Code audit (cz-ai-logistics, `scan_session_projection.py`), this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-23) |

**Description**
Code shows the app retains a full local version history per document — no row is ever deleted, each re-scan gets its own versioned blob path, and a version number is computed locally and also sent to Axapta. This contradicts the 2026-09-16 project-knowledge entry stating multi-scan/historical version storage is explicitly out of scope for BigHub and that Axapta owns all document versioning.

**Rationale**
Found during code audit. Notably, the May/June 2026 spec draft actually matches what the code does today (local versioning) — suggesting the "Axapta owns it" framing from 2026-09-16 may describe an intended future simplification rather than the current reality.

**Impact**
- **Data**: which version is the target architecture matters for the spec's accuracy and for any storage/retention conversation with the client.
- **Delivery**: needs reconciling before the spec is finalized — currently the spec, the 09-16 project-knowledge note, and the code all disagree.

---

### ASM-131

| Field | Value |
|-------|-------|
| ID | ASM-131 |
| Created | 2026-09-23 |
| Source | Code audit (cz-ai-logistics, `main.py`, `test_scans.py`), this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-23) |

**Description**
The entire `/scans` router (session creation, page upload/OCR, route submission to Axapta, confirmation) is gated behind `Depends(auth.require_user)` — Entra ID login is required for the whole scan flow. This directly contradicts the current spec's claim that the kiosk is "plně anonymní," the framing of [[ASM-087]] (kiosk authentication debate scheduled 2026-09-17, which assumes no authentication exists today), and what was communicated to Jan Žižka in the 2026-09-10 client demo (open access confirmed as acceptable to the client).

**Rationale**
Found during code audit — a genuine code-vs-communicated-state mismatch, not a PM interpretation. Test `test_requires_auth` directly proves a tokenless scan request returns 401.

**Impact**
- **Delivery**: the [[ASM-087]] debate should be reframed — the question isn't "add auth or not," it's "is the existing auth intentional, and does it match what's been told to the client?"
- **Relationship**: Jan Žižka was told the kiosk is open-access; if auth is actually required, this needs correcting with the client before it causes confusion at rollout.

---

### ASM-130

| Field | Value |
|-------|-------|
| ID | ASM-130 |
| Created | 2026-09-23 |
| Source | 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal |
| By | Marek Pillár (STK-001) |
| Status | Open (2026-09-23) |

**Description**
The TEO/OCR review/correction step is entirely manual, Excel-based work — Radim Švarc's own process design has Michaela Albrechtová manually checking and correcting rows in a spreadsheet, with no AI assistance in that part of the loop, even though BigHub's own extraction upstream is AI-driven. Marek flags this as a real gap worth revisiting, not just a format preference.

**Rationale**
BigHub's pipeline already does the hard extraction work with AI; letting the entire human-review layer downstream stay a raw, unassisted spreadsheet exercise leaves an obvious opportunity on the table (e.g. inline confidence flags, a lighter review UI, or AI-assisted correction suggestions) that the current Excel-centric design doesn't capture. Not yet raised with Jura Brázdil or Radim Švarc — Marek's own observation after reviewing Radim's process notes.

**Impact**
- **Delivery**: If pursued, this could mean augmenting or replacing the raw-Excel handoff step in Radim's process (see the TEO/OCR project-knowledge entry) with something more AI-assisted — scope and effort not yet assessed.
- **Relationship**: Should be raised carefully, since Radim has already built real working automation around the current Excel-based design (mailbox, Power Automate flows, folder structure) — any change here has migration cost on his side too.


**Update 2026-09-25**: Resolution path agreed with Alana Sihelská: phased, with Excel kept for the autumn 2026 cycle and a non-Excel review solution before spring 2027 ([[ASM-165]]), proposed via Radim first ([[ASM-166]]). Source: 2026-09-25-alana-1on1-teo-phasing-capacity-pool-team-dynamics
---

### ASM-129

| Field | Value |
|-------|-------|
| ID | ASM-129 |
| Created | 2026-09-22 |
| Source | 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal |
| By | Alana Sihelská (STK-004) |
| Status | Open (2026-09-22) |

**Description**
Alana's notes from this session state Blob storage and deployment "still stand on Dr. Max infra, resp. BDC" — i.e. still blocked pending Dr. Max-side infrastructure/BDC action. This directly contradicts [[ASM-088]] (decided 2026-09-16: Blob storage for the TEST environment would be self-provisioned by BigHub, with no BDC/infra-team dependency to create it).

**Rationale**
Rather than silently overwrite ASM-088 on a single secondhand note, this is recorded as an open conflict pending direct confirmation with Jura Brázdil — the blocker may have genuinely shifted to a different piece of infrastructure than what ASM-088 covered, or this may be a note-taking imprecision from a condensed bullet-point summary rather than a full transcript.

**Impact**
- **Delivery**: If the blocker is real, the TEST-environment deployment timeline depends on Dr. Max infra/BDC action that isn't yet scheduled — worth surfacing to Jura immediately given the autumn service season is already underway.
- **Data quality**: ASM-088 should not be marked resolved/closed until this is reconciled one way or the other.

---

### ASM-128

| Field | Value |
|-------|-------|
| ID | ASM-128 |
| Created | 2026-09-22 |
| Source | 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal |
| By | Alana Sihelská (STK-004) |
| Status | Open (2026-09-22) |

**Description**
Alana's notes record that "sending multiple possible candidate variants (cities and dates) to reviewers" was rejected in this session — a simple flag for manual review in cases of uncertainty is considered sufficient instead. This appears to directly reverse [[ASM-119]] (decided just one day earlier, 2026-09-21: "TEO/OCR disambiguation shifts to classify-against-known-branch-list + ranked candidate alternatives, not forced verbatim transcription").

**Rationale**
It isn't clear from the condensed notes available whether this rejection covers the same mechanism ASM-119 describes, or a narrower point — e.g. how candidates are *presented* to reviewers (a UI/UX choice) vs. the underlying classify-and-rank *logic* itself (which could still run internally even if reviewers only ever see a flag, not the ranked list). Recorded as an open conflict rather than assumed to fully reverse ASM-119.

**Impact**
- **Delivery**: Jura needs to confirm which reading is correct before this changes any actual pipeline behavior — ASM-119 was decided and potentially already being implemented as of 2026-09-21.
- **Data quality**: ASM-119 should not be marked reversed/closed until this is reconciled directly with Jura.

---

### ASM-127

| Field | Value |
|-------|-------|
| ID | ASM-127 |
| Created | 2026-09-22 |
| Source | 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal |
| By | Alana Sihelská (STK-004), Jura Brázdil (STK-026) |
| Status | Decided (2026-09-22) |

**Description**
SPEDOS is confirmed as a real vendor, now being actively onboarded as TEO/OCR's 3rd autumn-2026 pilot vendor. This resolves [[ASM-089]] (open since 2026-09-16: whether to expand pilot scope to a 3rd, larger vendor referenced only as "PEDOS," name uncertain) — "PEDOS" was evidently a mishearing/mis-transcription of "SPEDOS." BigHub committed to giving SPEDOS additional pipeline attention and sending an export by end of this week (2026-09-25).

**Rationale**
ASM-089 flagged genuine uncertainty about whether "PEDOS" was even a real vendor name. This session confirms it is, under the correct spelling, and BigHub is already acting on it rather than still deliberating — moving this from an open question to a decided, in-progress item.

**Impact**
- **Delivery**: SPEDOS onboarding proceeds this week alongside the existing 2-vendor autumn scope (Racun, Thermetal).
- **Data quality**: ASM-089 marked resolved/superseded by this entry.

---

### ASM-126

| Field | Value |
|-------|-------|
| ID | ASM-126 |
| Created | 2026-09-22 |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |
| By | Jindřich Tůma (STK-003) |
| Status | Open (2026-09-22) |

**Description**
Ján "Honza" Kabát (STK-005) asked Marek directly for a full list of everything in the backlog/pipeline — including effort and expected Azure spend — for Microsoft partnership costing purposes. Jindřich considers this premature and is deprioritizing it until the current confirmed initiatives are locked in with Dudaško's priority sign-off (targeted for this Friday).

**Rationale**
Jindřich's read: BigHub isn't pushing the wider backlog to Dr. Max yet, so costing it out for Microsoft now is "trošku overkill" — that work is "part B," to happen once the confirmed initiatives (and their priority order) are settled with Dudaško. Marek had already shown Kabát the rough backlog but flagged it isn't cost-planned.

**Impact**
- **Sequencing**: No backlog-costing work happens before Friday's Dudaško priority alignment. Jindřich will coordinate directly with Kabát on next steps afterward.
- **Stakeholder management**: STK-005 (Kabát) updated with this ask; STK-003 (Jindřich) updated with the coordination commitment.

---

### ASM-125

| Field | Value |
|-------|-------|
| ID | ASM-125 |
| Created | 2026-09-22 |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |
| By | Jindřich Tůma (STK-003), Marek Pillár (STK-001) |
| Status | Open (2026-09-22) |

**Description**
A portfolio-wide priority-ranking tension surfaced while reviewing the consolidated Business Quantification tracker. Filtering to initiatives above 1M Kč/year in modeled annual value, Jindřich ranked MaxBuddy's full 600-pharmacy rollout as the clear must-have top priority (~81M Kč/year, by far the largest figure), followed by Max chatbot/Maxie (~13-14M), then Listing (~34M) third. Marek pushed back that Listing should stay top priority regardless, consistent with the repeated view from Honza (Sovka), Alana (Sihelská), and Petr Neuman himself.

**Rationale**
Marek's argument: at Dr. Max's ~10,000-SKU, multi-billion-Kč revenue scale, even a 1% optimization on any single item compounds into very large money that this quarter's modeled dollar figure doesn't fully capture — the ranking-by-modeled-value approach may understate Listing's real strategic weight. The disagreement was raised but explicitly not argued out in this meeting.

**Impact**
- **Prioritization**: This tension is likely to resurface at Friday's combined Dudaško session, where the full priority ranking will be presented. Whoever's read wins shapes near-term resourcing across MaxBuddy, Max/Maxie, and Listing.
- **Stakeholder alignment**: Worth explicitly surfacing to Dudaško rather than presenting one ranking as settled fact, given the live internal disagreement.


**Update (2026-09-25)**: Authoritative tracker values give the value-based ranking MaxBuddy 81M > Listing 34.1M > Max/Maxie 13.9M (illustrative, shared scenario) > order prediction 1.9M > Lexie 1.2M (illustrative) > Fakturace doprav 0.79M > Reklamace 0.43M (phase 1 only) > TEO/OCR 0.27M. The tracker's own Priority (1–5) column gives Listing 5, OCR 4, Lexie 2, the rest 3 (scale direction unconfirmed). The ranking tension itself remains open.
---

### ASM-124

| Field | Value |
|-------|-------|
| ID | ASM-124 |
| Created | 2026-09-22 |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-22) |

**Description**
For Max chatbot, Maxie (voicebot), and Lexie, the business-value methodology now has two distinct parts: (1) Simona Mertová's (STK-017) illustrative FTE-avoidance figures (~13-14M Kč/year for Max/Maxie combined from 20 avoided 24/7 agents; ~1.2M for Lexie from 30 min/day saved) stay explicitly illustrative-only, never to be presented as an accepted business case; (2) a second, harder KPI is added — actual measured request-handling volume per month × 12, targeting a 50% reduction/offload figure.

**Rationale**
Mertová has repeatedly and explicitly refused to let her FTE-avoidance numbers be treated as a real business case, worried it could be used to justify cutting her operator headcount — Jindřich accepts that constraint rather than pushing past it. But he wants a second, measurable KPI that doesn't depend on her cooperation with the FTE framing: how many requests the chatbot/voicebot/Lexie actually handle, with a concrete -50% reduction target against that measured baseline.

**Impact**
- **KPI design**: The Max/Maxie/Lexie OKR cards in the Business Quantification tracker should carry both figures side by side, clearly labeled — Mertová's illustrative estimate, and the new measured-volume target.
- **Data dependency**: The measured-volume KPI depends on Mertová supplying the average monthly request-volume figure she has so far declined to give beyond the "more than half an hour a day" framing — see the open action item and [[ASM-096]].

---

### ASM-123

| Field | Value |
|-------|-------|
| ID | ASM-123 |
| Created | 2026-09-22 |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |
| By | Petr Neuman (STK-023) |
| Status | Decided (2026-09-22) |

**Description**
Petr Neuman has now committed to concrete Listing KPI figures, superseding [[ASM-075]] (where he explicitly declined to commit to a number): +1 percentage point conversion per optimized listing (better SEO/discoverability/filtering), quarterly throughput rising from 6,000 to 8,000–10,000 processed items, and cost-per-item dropping from 200 Kč to 100 Kč as automation lets one worker process roughly 2 items/hour instead of ~1.3. Combined, these total approximately 34M Kč/year in modeled business value.

**Rationale**
ASM-075 recorded Neuman's earlier reluctance to fix a number before seeing the tool's real performance. This session shows he now has a live report backing these figures directly, rather than a directional placeholder — a meaningful upgrade in data quality for the Listing business case.

**Impact**
- **Reporting**: The corporate KPI Excel (`businessQuantificationWorskop.xlsx`, E-commerce BQ sheet) should be updated to replace ASM-075's placeholder with these committed figures.
- **Prioritization**: This ~34M Kč/year figure directly feeds the portfolio priority-ranking discussion — see [[ASM-125]].


**Correction (2026-09-25, BQ tracker = source of truth)**: The figures above are partly wrong. Per the tracker: conversion uplift is **+0.1 pp (5% → 5.1%)**, not +1 pp, worth ≈ 31M Kč/yr (orientational/extrapolated; Neuman approved the method as the primary KPI). Cost per item was **230 → 130 Kč** actual (Q1 → Q2 2026, ≈ 2.4M Kč/yr), with a further target of **130 → 100 Kč** (≈ 0.72M Kč/yr). Throughput ≥6,000 → 8–10k items/quarter. Total **34,120,000 Kč/yr**.
---

### ASM-122

| Field | Value |
|-------|-------|
| ID | ASM-122 |
| Created | 2026-09-22 |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |
| By | Jindřich Tůma (STK-003), Tomáš Dudaško (STK-010) |
| Status | Open (2026-09-22) |

**Description**
Reklamace's real efficiency driver has been reframed — internally and directly to Dudaško — as digitization and data consolidation rather than AI. The underlying knowledge base isn't robust enough to support meaningful AI features beyond minor add-ons (e.g. historical email-status summarization); this holds for the current phase and all four planned future phases, since they'd reuse the same digitization flow across different complaint types. Whether the project continues as digitization-only or is closed outright is not yet decided — pending a Dudaško + head-of-logistics alignment meeting (with Jan Sovka brought in for historical context).

**Rationale**
This surfaced last Thursday's status call and was reinforced when Jindřich told Dudaško directly. Dudaško is pushing back somewhat on the framing and wants to align with the head of logistics before deciding next steps, since the future AI-labeled phases don't actually contain much AI either.

**Impact**
- **Scope**: Phase 1.1 is the only Reklamace phase currently confirmed in motion; the 4 further phases behind it now have an uncertain future pending this alignment meeting.
- **Stakeholder management**: STK-010 (Dudaško) updated with this sentiment; Marek to be looped into all future reklamace-thread meetings as a fresh context-builder.

**Update (2026-09-25, Reklamace supplier data)**: Supplier data won't fully consolidate into Axapta. Only supplier account, address and main contact are committed; contacts, notes and pickup type need another store, offered to logistics as options with risks — see [[ASM-169]], [[ASM-176]]. Source: 2026-09-25-reklamace-supplier-data-source-options.

---

### ASM-118

| Field | Value |
|-------|-------|
| ID | ASM-118 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |
| By | Tomáš Dudaško (STK-010) |
| Status | Open (2026-09-21) |

**Description**
No regular, reliable reporting exists for MaxBuddy to evaluate it against — Dudaško says he's raised this for months. One report was generated via Claude at some unknown past point, with no known owner or cadence since.

**Rationale**
Dudaško: "to já to už opakuju několik měsíců... já nevím, kde to jako hnije." Jindřich says he saw current reporting last week and will send it over, and separately wants every AI initiative to end with defined KPIs/reporting — ties into the Business Quantification/OKR effort already running (`ai-initiatives-okr-framework.md`).

**Impact**
- **Relationship**: A standing, repeated complaint from the budget-holder — direct contributor to his "frosty" sentiment (STK-010); resolving it has outsized relationship value beyond its own scope.
- **Delivery**: No owner or cadence currently assigned — needs one before this can close.

---

### ASM-117

| Field | Value |
|-------|-------|
| ID | ASM-117 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |
| By | Jindřich Tůma (STK-003), Tomáš Dudaško (STK-010) |
| Status | Decided (2026-09-21) |

**Description**
The AI adoption campaign splits into two parts: Part A (BigHub-owned) is internal communications/awareness — intranet content, PR, and guides/FAQ/knowledge-base content hosted directly on the AI Platform so people have a standing reason to visit it. Part B (Dr. Max-owned) is end-to-end operational rollout — pharmacist training and hypercare — which stays entirely with Dr. Max's own training center and "expertní skupiny" (expert groups); BigHub's only touchpoint for post-rollout evaluation is the relevant expert-group lead ("osmec"), not the training center directly.

**Rationale**
Jindřich raised a concrete worry (a MaxBuddy pilot pharmacist who didn't know whether/how to use the tool) to test whether BigHub needed broader ownership. Dudaško's answer was unambiguous: training is handled identically to any other Armis feature rollout, entirely by "provoz" (operations) — not BigHub's job. This is distinct in scope from ASM-101 (Max chatbot's public *customer*-facing launch staying quiet) — this entry covers *internal employee-facing* platform awareness, a different audience.

**Impact**
- **Scope**: Caps BigHub's adoption-campaign ownership at awareness/comms — prevents scope creep into training delivery BigHub isn't resourced for.
- **Relationship**: Gives Jindřich a concrete next contact (expert-group lead) instead of an ambiguous "check in on adoption" ask.
- **Process**: Reinforces the org concept captured in `project-knowledge` (expertní skupiny, osmec, tréninkové centrum).

---

### ASM-116

| Field | Value |
|-------|-------|
| ID | ASM-116 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |
| By | Tomáš Dudaško (STK-010) |
| Status | Open (2026-09-21) |

**Description**
Dudaško wants a longer-term agentic-workflow/orchestrator builder — drag-and-drop agent flows with configurable models/prompts per step — referencing an unnamed external tool (MCP servers, agent builder, agent registry) purely as inspiration. Both Marek and Jindřich deferred this to a future (tentatively November) conversation, not near-term scope.

**Rationale**
Partly motivated by frustration that this capability was part of BigHub's original pitch before the shared-platform product vision was retired (see the 2026-05 platform-strategy history). Marek's own untested view is that a custom build is likely the wrong call given commercial alternatives (e.g. Make, Gumloop) already do this cheaply — not yet shared with Dudaško.

**Impact**
- **Scope**: Kept explicitly out of the current 3-phase plan (ASM-115) to protect near-term delivery focus.
- **Cost**: If Dudaško insists on a custom build despite cheaper commercial alternatives, this would be a large, expensive project — flagged early rather than silently built later.

---

### ASM-115

| Field | Value |
|-------|-------|
| ID | ASM-115 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |
| By | Marek Pillár (STK-001), Tomáš Dudaško (STK-010) |
| Status | Decided (2026-09-21) |

**Description**
Delivery sequencing agreed with Dudaško: Phase 1 — unify the UX into one entry point with role-based access and basic cost/usage metrics (the design-brief work already in flight). Phase 2 — deeper backend/token FinOps integration. Phase 3 — work through Dudaško's capability-matrix Excel together, jointly prioritized, likely a separate dedicated session (~November).

**Rationale**
Dudaško was explicit that platform-behavior work (Phase 1/2) is the precondition for the rest, not a parallel track: "Prvně se to musí chovat jako platforma... a v tom okamžiku si můžeme říkat, jak to ještě vylepšíme u dalších capability."

**Impact**
- **Delivery**: Gives the existing UX-mockup work (already scoped per ASM-041/ASM-045) explicit client sign-off on sequencing, reducing risk of scope pressure from the capability-matrix Excel derailing Phase 1.
- **Timeline**: Sets a soft expectation (Dudaško) of visible progress within weeks, not months, given his "frosty" sentiment.

**Update (2026-09-24)**: The Phase 1 UX/access prototype was demoed to Dudaško and accepted ("s tímhle začínám být spokojený" [translated from Czech: "I'm starting to be satisfied with this"]). Design and development planning can proceed. See [[ASM-164]] for the release estimate. Source: 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko

---

### ASM-114

| Field | Value |
|-------|-------|
| ID | ASM-114 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |
| By | Tomáš Dudaško (STK-010) |
| Status | Decided (2026-09-21) |

**Description**
Per-department Lexie instances (IT, "kasťák"/POS, an upcoming Legal instance) collapse into one unified, role-gated Lexie chat, plus a public-document tier visible to everyone regardless of role. Access is modeled on Dr. Max's existing SharePoint permissions rather than a new parallel access model.

**Rationale**
Dudaško: "já bych chtěl mít jednu Lexi, jeden chat, do kterýho podle role a toho, co můžu vidět, dostanu odpovědi." Reusing SharePoint permissions avoids building and maintaining a second access-control system.

**Impact**
- **Tech**: Requires the platform's RAG/indexing layer to respect per-document SharePoint ACLs at query time, not just at index time — a meaningfully bigger lift than today's per-instance Lexie setup.
- **UX**: Removes the current fragmentation (multiple Lexies) that was a named source of Dudaško's UX complaint.

---

### ASM-113

| Field | Value |
|-------|-------|
| ID | ASM-113 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko, 2026-09-21-ocr-progress-ai-platform-prototype-sync |
| By | Tomáš Dudaško (STK-010) |
| Status | Decided (2026-09-21, updated 2026-09-21) |

**Description**
The AI Platform's home screen becomes a unified, role-based directory ("rozcestník") linking to every AI tool Dr. Max has — including tools with their own separate frontend (e.g. the e-commerce forecast dashboard, the listing/copywriting tool). **Updated same day**: these open **inline**, within the platform's own single-URL interface, not via a deep link out to a separate site.

**Rationale**
Dudaško: today, not knowing a tool's exact URL means he can't reach it at all — there's no anchor point anywhere for tools outside the chat pattern. The original entry (written right after the Dudaško call) captured "deep link out, no embedding" — a same-day follow-up working session with Jura Brázdil surfaced that Marek's actual read of Dudaško's ask is inline, matching Jura's own already-built prototype, which assumes single-URL in-page navigation for any browser-accessible tool. PM confirmed inline is correct during that session's routing review.

**Impact**
- **UX**: Directly addresses the "roztrieštené"/fragmented experience diagnosed as the platform's core UX complaint — inline navigation reinforces the "one product" feel more strongly than deep-linking out.
- **Scope**: Confirms Phase 1 UX work must account for external-frontend tools rendering inline, not just chat-pattern tools — relevant for the Jura Brázdil design brief, which has been updated to match. One exception: MaxBuddy has no standalone web service (Farmis-integrated only), so it stays a demo view regardless.

---

### ASM-121

| Field | Value |
|-------|-------|
| ID | ASM-121 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ocr-progress-ai-platform-prototype-sync |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-21) |

**Description**
BigHub will not commit to building the ServiceNow export for TEO/OCR. It hands Radim Švarc's team complete structured data per document via API (values, confidence flags, alternate candidates, bounding boxes); Radim's team owns the review UI and the final export into ServiceNow.

**Rationale**
Jura: promising an export now risks BigHub being on the hook for a ServiceNow-side build whose actual shape isn't known yet (e.g. whether ServiceNow can even host image crops). Radim's team already intends to build their own review interface — better to let them own the full review→export step and hand them everything BigHub knows via API.

**Impact**
- **Scope**: Keeps BigHub's TEO/OCR delivery bounded to data extraction + API, not client-side tooling.
- **Delivery**: If Radim's team later asks BigHub to build the export once their clean-data format is confirmed, that's a new, separate ask — not committed now.

---

### ASM-120

| Field | Value |
|-------|-------|
| ID | ASM-120 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ocr-progress-ai-platform-prototype-sync |
| By | Alana Sihelská (STK-004) |
| Status | Decided (2026-09-21) |

**Description**
Whatever corrections Radim Švarc's team makes in their own TEO/OCR review interface must be captured and sent back to BigHub via API, so accuracy can be measured over time and fed back into improving the pipeline.

**Rationale**
Alana: without this feedback loop, BigHub has no way to know which of its own flagged/ambiguous fields were actually right or wrong in practice. Jura confirmed this isn't a technical blocker — the existing per-field data model (flags, bounding box, alternates) already supports adding a correction field — but it needs to be explicitly requested of Radim's team, since it won't happen by default.

**Impact**
- **Data**: Enables an ongoing accuracy-measurement loop rather than a one-time pilot validation.
- **Delivery**: Requires an explicit ask to Radim's team as they build their review interface — tracked as an action item.

**Update (2026-09-22)**: Radim confirmed his team will send the "correct" excel/json back to BigHub, with the exact format to be agreed directly with Jura — not yet a formal API contract, but the concrete mechanism this assumption called for is now in motion. Radim's own process design (see the TEO/OCR project-knowledge entry) has this happening after Míša's manual review step, before the file moves to SNOW-import prep.

---

### ASM-119

| Field | Value |
|-------|-------|
| ID | ASM-119 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ocr-progress-ai-platform-prototype-sync |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-21) |

**Description**
TEO/OCR disambiguation shifts from forcing all reader models to transcribe an address or date character-for-character to classifying against a known branch/candidate list, surfacing 2-3 ranked candidate values to the human reviewer (e.g. via a dropdown) when the model ensemble disagrees, instead of a blind re-transcription flag.

**Rationale**
Jura: some source documents give only a city with no street/stamp/center number, or contain handwriting (e.g. crossed digit 7) that international OCR models systematically misread — neither is fixable by better prompting alone. Presenting real candidates (validated against the known branch directory) is more reliable than asking a model or human to re-guess from scratch.

**Impact**
- **Quality**: Back-tested improvement — spring batch clean/no-review rows rose from 74→114 of 188 (~54%), autumn batch from 47→61 of 140.
- **UX**: Requires the review interface (built by Radim's team) to support a candidate-selection control, not just accept/reject/retype — worth flagging to them.

---

### ASM-112

| Field | Value |
|-------|-------|
| ID | ASM-112 |
| Created | 2026-09-21 |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |
| By | Tomáš Dudaško (STK-010) |
| Status | Decided (2026-09-21) |

**Description**
The AI Platform must behave as a platform-as-a-service: every AI-consuming tool — chat or programmatic — routes through it so usage/cost (FinOps) is visible and controllable, not just host chat products. Eventually includes an "AI gateway" layer with GDPR controls.

**Rationale**
Dudaško's standing example: MaxBuddy's token cost is invisible to him today because it doesn't route through the platform at all — "nevím to proto, protože prostě nepálí tokeny přes tu platformu." He was explicit the platform's current value is limited if it's just another chat product rather than a backend serving other AI agents/tools.

**Impact**
- **FinOps**: This is the architectural precondition for any usage/cost dashboard work (Phase 2, ASM-115) — without routing enforcement, cost visibility can't be built.
- **Tech**: Implies MaxBuddy (and any future tool) needs to be migrated onto the shared platform's LLM access path, not call models directly — a real integration lift, not just a UI change.

---

### ASM-111

| Field | Value |
|-------|-------|
| ID | ASM-111 |
| Created | 2026-09-18 |
| Source | 2026-09-18-business-quantification-order-prediction-simonik |
| By | Marek Šimoník (STK-019) |
| Status | Open (2026-09-18) |

**Description**
A related dashboard extension for the logistics team — using the same order-forecast data to plan warehouse shifts (staff up or send people home based on forecasted volume) — is already ~90% built, per Šimoník's own estimate.

**Rationale**
Šimoník mentioned it as a side topic during his Business Quantification interview for the order-prediction dashboard, but was explicit that he doesn't manage or speak for the logistics team — it sits under the Director of Logistics, a separate department. No name or confirmed status is available from his side.

**Impact**
- **Delivery**: If real, this is a near-complete parallel deliverable BigHub may not have full visibility into — worth a direct check with Logistics leadership.
- **Value**: Materially multiplies the order-prediction dashboard's business case if confirmed, since it reuses the same underlying data for a second use case.

---

### ASM-110

| Field | Value |
|-------|-------|
| ID | ASM-110 |
| Created | 2026-09-18 |
| Source | 2026-09-18-business-quantification-order-prediction-simonik |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-18) |

**Description**
Šimoník has no additional feature backlog for the order-prediction dashboard beyond what was already fed back in the 2026-09-15 follow-up session.

**Rationale**
He wants the currently-agreed scope delivered in the next 2–3 weeks and stress-tested through the Q4 seasonal peak before discussing any further development; the explicit next check-in point is Q4/year-end.

**Impact**
- **Delivery**: No new scope pressure on this stream in the near term — frees capacity.
- **Planning**: Marek should proactively schedule the Q4/year-end follow-up rather than wait to be asked.

---

### ASM-109

| Field | Value |
|-------|-------|
| ID | ASM-109 |
| Created | 2026-09-18 |
| Source | 2026-09-18-business-quantification-order-prediction-simonik |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-18) |

**Description**
The order-prediction dashboard's reaction/outage-prevention business value is quantified at ~100,000–200,000 Kč/month, explicitly framed as a conservative estimate by Šimoník.

**Rationale**
Based on an estimated ~100–200 orders/month "saved" from issues that would otherwise go undetected, at ~1,000 Kč average order value. Šimoník explicitly resisted inflating this figure ("nechci kreslit vzdušné zámky"). He separately floated a looser, unverified upside of "millions of Kč/year" on a broader annual/company-wide basis, kept explicitly distinct from the conservative monthly figure.

**Impact**
- **Business case**: Gives Tomáš Dudaško's OKR Excel a real, defensible number for this initiative rather than a qualitative claim.

---

### ASM-108

| Field | Value |
|-------|-------|
| ID | ASM-108 |
| Created | 2026-09-18 |
| Source | 2026-09-18-business-quantification-order-prediction-simonik |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-18) |

**Description**
KPI committed — the order-prediction dashboard should help catch at least 1 "serious issue" (web-side or logistics-related, not necessarily a critical bug) per month.

**Rationale**
Marek initially proposed a conservative 1-per-6-months stretch goal; Šimoník pushed for a more ambitious monthly cadence.

**Impact**
- **Product**: Sets a measurable bar for the dashboard's "reaction value" business case (see [[ASM-109]]) once live.

---

### ASM-107

| Field | Value |
|-------|-------|
| ID | ASM-107 |
| Created | 2026-09-18 |
| Source | 2026-09-18-business-quantification-order-prediction-simonik |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-18) |

**Description**
KPI committed — reduce the analyst's control/verification time on the order-prediction dashboard from ~5 hours/week to 2 hours/week.

**Rationale**
Explicitly a long-term target, not a near-term milestone — Šimoník wants the analyst (Petr Ondráček) to keep doing this work in parallel for now as a trust-building double-check on the new dashboard.

**Impact**
- **Business case**: One of two concrete, numeric KPIs from this BQ interview (see [[ASM-108]]) — feeds directly into `BQ_Final.xlsx`'s Year Expenses/Savings calculation (~112,500–150,000 Kč/year, using Šimoník's own 6–8k Kč/day MD rate).

---

### ASM-106

| Field | Value |
|-------|-------|
| ID | ASM-106 |
| Created | 2026-09-18 |
| Source | 2026-09-18-business-quantification-order-prediction-simonik |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-18) |

**Description**
Business ownership of the order-prediction dashboard (Řízení poptávky) confirmed as Marek Šimoník alone; Petr Ondráček confirmed as domain expert, not co-owner.

**Rationale**
Marek offered to let Ondráček — who builds the manual reports today and knows the underlying data sources best — take business ownership instead, since Šimoník's calendar could be a bottleneck. Šimoník declined, explicitly noting Ondráček lacks the strategic view the role needs.

**Impact**
- **Stakeholder map**: Confirms STK-019's ownership and corrects STK-035's role description (previously logged as "logistics-side contact," actually Šimoník's own e-commerce-team analyst).

---

### ASM-105

| Field | Value |
|-------|-------|
| ID | ASM-105 |
| Created | 2026-09-17 |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |
| By | Team |
| Status | Decided (2026-09-17) |

**Description**
False call-transfer claims (Max claiming it can transfer a user to a pharmacist by phone) and unauthorized medical advice are both explicitly disallowed in the Max chatbot's system prompt.

**Rationale**
Both behaviors were observed in live testing — Max cannot actually transfer calls, and the medical-advice guardrail needed confirmation it holds under direct questioning. The call-transfer claim was explicitly prompted against; the medical-advice guardrail was already working correctly when tested by Kadlecová.

**Impact**
- **Trust**: Prevents the chatbot from making false promises to users, which would damage trust faster than a slower/more limited feature set.
- **Compliance**: Keeps the chatbot within its intended scope (informational, not clinical) ahead of the DPO/GDPR review already underway (see [[ASM-102]]).

---

### ASM-104

| Field | Value |
|-------|-------|
| ID | ASM-104 |
| Created | 2026-09-17 |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |
| By | Team |
| Status | Open (2026-09-17) |

**Description**
Some timeline items Jindřich shared as MVP scope actually belong to the full product, per Kateřina Kadlecová's read of the roadmap — specific items were not identified or resolved during the meeting.

**Rationale**
Kadlecová flagged the mismatch live; Jindřich acknowledged Marek might have visibility into it but the discussion moved on without itemizing which entries are affected.

**Impact**
- **Scope clarity**: Risk of Dr. Max testing or expecting features that aren't actually in the current MVP commitment, or BigHub under-scoping what's actually needed for MVP sign-off.
- **Timeline**: Needs resolving before the go-live testing window closes, since it affects what "MVP done" actually means.

---

### ASM-103

| Field | Value |
|-------|-------|
| ID | ASM-103 |
| Created | 2026-09-17 |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |
| By | Team |
| Status | Decided (2026-09-17) |

**Description**
Lexie's multi-role test-account approach is 4 separate accounts (one per CC sub-department), without 2FA — not the in-app role-switcher explored since 2026-09-10.

**Rationale**
Jura assessed the in-app role-switcher as too risky/complex given how strict BDC is about user-permission configuration, and wasn't confident it could be delivered without significant delay. Mertová accepted the simpler 4-account approach as workable for now; the role-switcher isn't ruled out long-term but is no longer the committed near-term path.

**Impact**
- **Delivery speed**: Unblocks Lexie role-based testing immediately via a BDC ticket, rather than waiting on new in-app development.
- **Test fidelity**: 4 separate accounts more accurately mirror how a real operator experiences exactly one role/permission scope at a time — Jura's own caveat from 2026-09-10 about the role-switcher not testing real restriction behavior no longer applies.

---

### ASM-102

| Field | Value |
|-------|-------|
| ID | ASM-102 |
| Created | 2026-09-17 |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |
| By | Šárka Andělová (STK-050) |
| Status | Open (2026-09-17) |

**Description**
GDPR consent/anonymization for the Max chatbot (phone/email collection) is unresolved — needs input from Lenka Henichová (DPO) before any consent copy is drafted.

**Rationale**
Andělová flagged that no consent checkbox or anonymization step currently exists; Jura confirmed BigHub hadn't planned for it. Jindřich judged this needs DPO sign-off rather than an ad hoc BigHub/Dr. Max text, given Dr. Max's existing "ochrana osobních údajů" page already covers adjacent products (Maxí voicebot). Jura clarified the current architecture reduces but doesn't eliminate the exposure: nothing is stored server-side today (conversations live only in the user's browser); future analytics will store only aggregate statistics. The one genuinely new sensitive-data type is e-recepty (e-prescription) content, not previously consented for this use.

**Impact**
- **Compliance**: Blocks any public go-live copy/UX around data collection until DPO input arrives — should be prioritized given the end-of-September internal deployment target (see [[ASM-100]]).
- **Timeline**: Sits on the critical path to phase 2/3 of the go-live plan (public visibility on doktormax.cz).

---

### ASM-101

| Field | Value |
|-------|-------|
| ID | ASM-101 |
| Created | 2026-09-17 |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |
| By | Simona Mertová (STK-017) |
| Status | Decided (2026-09-17) |

**Description**
The Max chatbot's public launch will be a quiet/soft launch — no active promotion (intranet, newsletter, etc.) until the tool is fully mature, deferring the adoption-campaign work Jindřich has otherwise been preparing.

**Rationale**
Mertová: customers are expected to discover the chatbot organically; only promote once satisfaction is validated and ideally once the current chat-bubble UI is refined or removed. She wants to avoid over-promising given the chatbot currently covers only 4 capabilities.

**Impact**
- **Marketing/comms**: Jindřich's adoption-campaign channel planning is paused pending Mertová's go-ahead — not cancelled, just gated.
- **Risk**: Reduces exposure if early bugs surface post-launch, at the cost of slower adoption measurement.

---

### ASM-100

| Field | Value |
|-------|-------|
| ID | ASM-100 |
| Created | 2026-09-17 |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |
| By | Simona Mertová (STK-017), Jura Brázdil (STK-026) |
| Status | Decided (2026-09-17) |

**Description**
Max chatbot go-live: public launch target is end of October (Mertová's ask); BigHub targets completing its 3 internal deployment phases (prod backend connection → BDC-cleared but hidden on doktormax.cz → public visibility toggle) by end of September.

**Rationale**
Jura pushed for an end-of-September public date; Mertová held firm on needing more testing time against real production data (only 4 sample e-recepty tested so far) and judged end-of-September too tight given infra dependencies, explicitly prioritizing trust ("jakmile to nebude dobře udělané, tak jsme si vykopali vlastní hrob") over speed. Jindřich accepted this rather than pushing back, framing BigHub's job as earning an earlier date through demonstrated quality, not forcing one.

**Impact**
- **Timeline**: Gives BigHub a concrete internal deadline (end of September) distinct from the public commitment (end of October), with a month of buffer for hands-on Dr. Max testing against real data in between.
- **Relationship**: Demonstrates BigHub deferring to the client's risk tolerance on a launch date rather than pushing its own schedule — reinforces trust on a project where a bad launch would be highly visible (public website).

**Update (2026-09-24)**: The end-of-September internal-phase target is **at risk**. Production infra/database access has been blocked more than 6 weeks (escalated to Dudaško; MaxBuddy's AKS request is ahead in the BDC queue), and Jura says "nám na tom stojí úplně všechno" [translated from Czech: "everything hinges on it"]. The public end-of-October date is not yet affected. Source: 2026-09-24-lexie-max-maxie-weekly-sync

---

### ASM-099

| Field | Value |
|-------|-------|
| ID | ASM-099 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-maxbuddy-vosmek |
| By | Luboš Vosmek (STK-011) |
| Status | Open (2026-09-17) |

**Description**
All three of MaxBuddy's KPI targets — single-item dispensing rate, molecule/group volume growth, and conversion-by-benefit rate — require target values from Luboš Vosmek; none are finalized as of 2026-09-17.

**Rationale**
The primary KPI (single-item dispensing, tracked by Dr. Max's corporate Holding) has an approximate ~50% baseline but no confirmed target on paper; the two secondary KPIs were deliberately left open for Vosmek to set his own expectation during Excel review rather than have Marek propose numbers.

**Impact**
- **Timeline**: Same 2026-09-18 deadline as [[ASM-098]] — all three should be confirmed together in Vosmek's Excel review pass ahead of the Tomáš Dudaško deliverable.

---

### ASM-098

| Field | Value |
|-------|-------|
| ID | ASM-098 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-maxbuddy-vosmek |
| By | Luboš Vosmek (STK-011) |
| Status | Open (2026-09-17) |

**Description**
MaxBuddy's revenue-uplift (~1–1.2%) and dispensing-coverage (~40%) figures are provisional estimates pending exact numbers from Luboš Vosmek, due 2026-09-18.

**Rationale**
Vosmek was upfront he doesn't have the exact case-count denominator behind the revenue figure on hand and committed to recalculating and sending it, along with the current molecule-coverage count (last confirmed at 26 molecules, expanded again the prior week).

**Impact**
- **Timeline**: The Tomáš Dudaško deliverable will carry provisional figures until Vosmek's follow-up lands tomorrow morning.

---

### ASM-097

| Field | Value |
|-------|-------|
| ID | ASM-097 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-maxbuddy-vosmek |
| By | Luboš Vosmek (STK-011) |
| Status | Open (2026-09-17) |

**Description**
MaxBuddy's current live upsell/cross-sell feature is data/rule-based, not actually LLM/AI-driven, per Luboš Vosmek's own characterization.

**Rationale**
Vosmek was explicit ("it's all tied together with data... it isn't AI") when explaining that legislative blockage of the original dosage-checking feature forced a pivot straight to the current upsell logic, which runs on rules rather than a language model.

**Impact**
- **Portfolio classification**: Worth confirming with Jura Brázdil/the technical team how this affects MaxBuddy's classification and reporting within an "AI initiatives" portfolio tracker — it may not belong in the same bucket as LLM-based initiatives like Max chatbot or Lexie.

---

### ASM-096

| Field | Value |
|-------|-------|
| ID | ASM-096 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |
| By | Simona Mertová (STK-017) |
| Status | Open (2026-09-17) |

**Description**
Simona Mertová owes a blended/average agent (FTE) cost rate at the corporate level, needed to convert the chatbot's "20 extra agents for 24/7" hypothetical and Lexie's ~30 min/day estimate into Kč figures.

**Rationale**
Neither Mertová nor Marek had this rate on hand during the call; without it, the KPI Excel's revenue/cost figures for these initiatives remain qualitative only.

**Impact**
- **Timeline**: Blocks finalizing Kč-based business value for Max chatbot and Lexie in the Tomáš Dudaško deliverable until received.

---

### ASM-095

| Field | Value |
|-------|-------|
| ID | ASM-095 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |
| By | Simona Mertová (STK-017) |
| Status | Open (2026-09-17) |

**Description**
Lexie's business-value quantification and KPI remain unresolved — an estimated ~30 min/day time savings could not be translated into Kč, and two candidate KPI directions (call-handle-time reduction vs. new-agent ramp-time reduction) were proposed but neither finalized.

**Rationale**
Mertová explicitly resisted framing Lexie's value as headcount-reducible ("these are soft skills that can't be converted into money"), worried it could be misread as grounds for cutting staff; the new-agent ramp-time angle (~1–1.5 months → ~14 days faster) is the most concrete lever raised so far.

**Impact**
- **Business case framing**: Of the three CC initiatives, Lexie's is the weakest quantified business case — flag as the one most likely to need a follow-up session once Kadlecová's successor (see [[ASM-091]]) is named.

---

### ASM-094

| Field | Value |
|-------|-------|
| ID | ASM-094 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |
| By | Simona Mertová (STK-017) |
| Status | Open (2026-09-17) |

**Description**
Maxie's forward-looking containment-rate target (% resolved without transfer to a live agent) was walked back live on the call from an initial 90% to a 50/50 placeholder.

**Rationale**
Marek flagged that promising only 10% escalation for an untested first version risks looking bad if real performance lands closer to 30%; Mertová revised down and explicitly called it a soft, non-final placeholder ("let it land where it lands").

**Impact**
- **KPI reporting**: Present 50/50 as a conservative placeholder in the Dudaško deliverable, not a committed target — measurement methodology (transfer due to Maxie failure vs. a mid-call topic change) is also still unresolved.

---

### ASM-093

| Field | Value |
|-------|-------|
| ID | ASM-093 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |
| By | Simona Mertová (STK-017) |
| Status | Open (2026-09-17) |

**Description**
Max chatbot's conversation-resolution-rate KPI target is set directionally at ~50% initially, ~80% aspirational — not a committed number.

**Rationale**
No chatbot is yet in production, so there's no baseline; Mertová deliberately set expectations low for a first version, aiming toward 80% once the chatbot moves beyond its current fixed-menu structure to a fuller LLM model.

**Impact**
- **KPI reporting**: Treat 50%/80% as directional targets in the Dudaško deliverable, not hard commitments — revisit once real production data exists.

---

### ASM-092

| Field | Value |
|-------|-------|
| ID | ASM-092 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |
| By | Simona Mertová (STK-017) |
| Status | Decided (2026-09-17) |

**Description**
Business value for Max chatbot and Maxie is framed as capacity/coverage increase and reduced agent cognitive load, not FTE/headcount cost savings.

**Rationale**
Both Mertová and Marek agreed the call center's total call/email volume is fixed regardless of chatbot/voicebot adoption (pharmacy-network volume drives it, not channel availability), so savings can't credibly be expressed as fewer agents needed.

**Impact**
- **Business case framing**: The KPI Excel for Tomáš Dudaško presents these two initiatives as service-quality/brand-value levers, not cost-reduction levers, to avoid an inflated or misleading ROI narrative.

---

### ASM-091

| Field | Value |
|-------|-------|
| ID | ASM-091 |
| Created | 2026-09-17 |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |
| By | Simona Mertová (STK-017) |
| Status | Open (2026-09-17) |

**Description**
Kateřina Kadlecová (STK-037), the domain expert across Max chatbot, Maxie, and Lexie, is departing on maternity leave with no successor yet named.

**Rationale**
Mertová disclosed this mid-call while confirming domain-expert contacts for the Business Quantification interview; her team needs to internally reassign the responsibility before a replacement can be named.

**Impact**
- **Continuity**: All three CC-owned AI initiatives lose their most engaged domain-expert contact simultaneously — testing, ticket triage, and roadmap input may stall until a successor is named.
- **Timeline**: Could delay finalizing KPI targets and business-value figures still owed for the Tomáš Dudaško deliverable if a successor isn't named quickly.

---

### ASM-090

| Field | Value |
|-------|-------|
| ID | ASM-090 |
| Created | 2026-09-16 |
| Source | Direct file inspection (cz-ai-logistics codebase) + roadmap comparison, this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Open (2026-09-16) |

**Description**
While rebuilding `2. Fakturace doprav.docx` from scratch and cross-checking its MVP/Plná verze/Nice to Have tables 1:1 against the roadmap Excel (`product-roadmap-portfolio-full.xlsx`, "Fakturace doprav" sheet), found that the roadmap tables were missing 3 Plná verze items (Deployment na TEST, Dokončení UI, Napojení na Axaptu a e2e testování) and 5 of 6 Nice to Have items from the rebuilt doc — now fixed in the doc. Separately, confirmed in code (`confirmation_pdf.py`, `routers/scans.py`) that a driver-facing PDF confirmation (issued at the kiosk after scanning, distinct from the carrier-facing electronic confirmation) is fully built and live — but has no corresponding line item anywhere on the roadmap Excel or Artifact. Added it to the doc's MVP table as a flagged "NOVÉ" row with its code source cited.

**Rationale**
The doc's phase tables had drifted into an abstracted "capability summary" (built from the spec's own narrative sections) rather than a literal mirror of the roadmap's ticket-level list, which is what produced the visible mismatch the PM caught by comparing the two side by side.

**Impact**
- **Data**: `2. Fakturace doprav.docx` now mirrors the roadmap Excel exactly (same IDs, names, statuses) across all 6 phase tables, plus a Zdroj (source) column.
- **Open**: the roadmap Excel/Artifact were not modified — only the doc was. The driver-PDF-confirmation item exists only in the doc for now.

---

### ASM-089

| Field | Value |
|-------|-------|
| ID | ASM-089 |
| Created | 2026-09-16 |
| Source | 2026-09-16-teo-ocr-technical-sync-pilot-results; resolved via 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal |
| By | Tomáš Burda (STK-025) |
| Status | Resolved by [[ASM-127]] (2026-09-22) |

**Description**
Whether to expand TEO/OCR's committed autumn 2026 pilot scope beyond the current 2 vendors to include a 3rd, larger vendor (referenced only as "PEDOS" — name uncertain, possibly a mis-transcription) is undecided.

**Rationale**
Burda floated this because inspections continue into October and smaller vendors represent modest volume (10-20 documents) compared to the current two (50-70 each). Jura Brázdil is open to it — his extraction pipeline is now reusable, making a new vendor roughly a day's work — but nothing was committed, and Dr. Max hasn't yet sent sample documents for it.

**Resolved (2026-09-22)**: "PEDOS" was a mishearing of **SPEDOS**, a real vendor now being actively onboarded — see [[ASM-127]].

**Impact**
- **Delivery**: Low marginal engineering cost if pursued, given the reusable pipeline — but adds scope to a season that's already in motion.
- **Data**: Depends on Dr. Max confirming the vendor's real name/spelling and sending representative sample documents.

---

### ASM-088

| Field | Value |
|-------|-------|
| ID | ASM-088 |
| Created | 2026-09-16 |
| Source | 2026-09-16-teo-ocr-technical-sync-pilot-results |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-16) |

**Description**
TEO/OCR's TEST-environment Blob storage will be self-provisioned by BigHub directly on the existing shared AI platform — free, self-service — with no dependency on Vladislav Tvarůžek (STK-016) or the BDC infra team to create it.

**Rationale**
The platform already supports on-demand Blob provisioning as part of the node-pool migration Jura is running. The only possible infra-team touchpoint is a single, simple external network-access grant if Radim Švarc needs programmatic access from outside — not required to create the storage itself.

**Impact**
- **Delivery**: Removes a cross-team dependency that has historically taken days-to-weeks elsewhere in this project (see the accuracy-validation document's provisioning timeline estimates) — TEST-environment readiness is now gated only on BigHub's own node-pool migration.
- **Risk**: If Radim does end up needing external access, that step still depends on Vladislav/BDC turnaround time.

---

### ASM-087

| Field | Value |
|-------|-------|
| ID | ASM-087 |
| Created | 2026-09-14 |
| Source | Figma roadmap board comments (Honza Sovka / Marek Pillár), relayed to this session via screenshots on 2026-09-16 |
| By | Jan "Honza" Sovka (STK-002), Marek Pillár (STK-001) |
| Status | Open (2026-09-17) |

**Description**
Whether and how to authenticate/identify the person scanning documents at the Fakturace doprav kiosk is undecided. Honza Sovka currently leans toward "no authentication" but floated an idea worth keeping in mind: knowing who scanned matters, since it could be the driver, a foreman covering multiple drivers, a ViaPharma staffer, or someone else entirely. A debate is scheduled for **2026-09-17** to resolve this.

**Rationale**
Comment thread on the roadmap's "Autentizace uživatele" card. Marek Pillár's own reply scoped this as a possible future extension rather than a planned phase, regardless of the 17.9 outcome — consistent with the existing spec design (kiosk is anonymous by default per ASM/edge-case D2).

**Impact**
- **Scope**: Added to `2. Fakturace doprav.docx` (§1.4 edge cases, Nice to Have section, Otevřené otázky) and `product-roadmap-portfolio-full.xlsx` (Fakturace doprav sheet, "Autentizace uživatele" row) as an explicit open item pending the 9/17 debate.
- **Timeline**: This debate is scheduled for tomorrow relative to when this was routed (2026-09-16) — flagged as an action item in today's daily so it doesn't get lost.

---

### ASM-086

| Field | Value |
|-------|-------|
| ID | ASM-086 |
| Created | 2026-09-14 |
| Source | Figma roadmap board comments (Honza Sovka), relayed to this session via screenshots on 2026-09-16 |
| By | Jan "Honza" Sovka (STK-002) |
| Status | Decided (2026-09-14) |

**Description**
Fakturace doprav's "Kontrola údajů" roadmap card is marked "Done," but this is only true for the kilometer part. Temperature-datalogger validation is not built at all. It splits into three separate pieces, all planned for Plná verze: (a) check whether a paper datalogger slip was attached to the ZOPV document, (b) read/validate electronic dataloggers via GPS Dozor, (c) read/validate temperature compliance from paper datalogger printouts directly — needed because ViaPharma cannot guarantee a fast transition to fully electronic dataloggers, so both paths must be supported.

**Rationale**
Honza Sovka's comment on the "Kontrola údajů" card: "teplotní údaje z dataloggerů zatím neumíme, je to plán do plné verze," with the three-part breakdown given directly, and the reasoning tied to Žižka's earlier point that ViaPharma can't guarantee fast electronic transition.

**Impact**
- **Scope**: `product-roadmap-portfolio-full.xlsx` (Fakturace doprav sheet) — "Kontrola údajů" (#4) rescoped to km-only, status changed to "Hotovo (jen km) — teplota viz #10"; "Správnost teplotních údajů z dataloggeru" (#10) expanded with the full a/b/c breakdown. Same changes applied to `2. Fakturace doprav.docx` (§1.1, §1.4, §2.1, Plná verze table).
- **Delivery**: Corrects an inflated completion percentage — one MVP item previously counted as fully "Done" is actually only half-done.

---

### ASM-085

| Field | Value |
|-------|-------|
| ID | ASM-085 |
| Created | 2026-09-16 |
| Source | Direct file inspection, this session |
| By | Marek Pillár (STK-001), via Claude |
| Status | Decided (2026-09-16) |

**Description**
`2. Fakturace doprav.docx` and `spec-template.docx` (both in "1. Feature Specs") were found to carry a leaked `word/comments.xml` part containing 39 unrelated, active Listing review comments (Filip Černý ↔ Marek Pillár, dated 2026-09-15/16, discussing Listing's §1.2 scraping content) — not the real Fakturace doprav comments. Both files have been stripped of all comment infrastructure (comments.xml, commentsExtended.xml, commentsIds.xml, commentsExtensible.xml, and in-document comment anchors).

**Rationale**
Root cause: the reusable generic spec template was originally cloned from `1. Listing.docx` by clearing its paragraphs/tables, but its `word/comments.xml` part was never stripped — so Listing's live comment thread rode along silently into every file built from that template lineage. `1. Listing.docx` itself was verified untouched (51 real comments intact). The PM separately renamed the enriched Fakturace doprav spec to replace the original `2. Fakturace doprav.docx` (intentional — the original's 20 comments had already been read and incorporated into the enriched version earlier this session), which is why the leaked comments ended up under that filename.

**Impact**
- **Process**: Any future template-cloning approach must explicitly strip `comments.xml` and related parts, not just body content.
- **Data**: No content was lost — the original `2. Fakturace doprav.docx`'s 20 comments were already fully read and incorporated into the spec earlier this session; only the (irrelevant, leaked) Listing comments were removed from these two files.

---

### ASM-084

| Field | Value |
|-------|-------|
| ID | ASM-084 |
| Created | 2026-09-14 |
| Source | Figma roadmap board comments (Honza Sovka), relayed to this session via screenshots on 2026-09-16 |
| By | Jan "Honza" Sovka (STK-002) |
| Status | Decided (2026-09-14) |

**Description**
Fakturace doprav's "Měsíční uzávěrka" (monthly-closing cron job — sends all unfinished routes to Axapta at month-end) is cancelled from scope. Routes will instead be sent to Axapta continuously/incrementally, and Axapta itself decides when to close a billing period out.

**Rationale**
Honza Sovka's comment on the roadmap card: "Novinka: nebude součástí — trasy budeme posílat do Axapta průběžně a ta si sama vyhodnotí, kdy to uzavře." A direct codebase read on 2026-09-16 independently supports this: `page_filing.py`'s `period_closed` flag is hardcoded `False` with no real trigger wired up — there was never a working period-close mechanism to begin with, so nothing is lost by dropping the ticket.

**Impact**
- **Scope**: Removed as a standalone MVP/Plná verze item everywhere it was tracked — `product-roadmap-portfolio-full.xlsx` (Fakturace doprav sheet, its slot repurposed for the new GPS-Dozor split ticket, see ASM-082), the live "AI Initiative Roadmaps v6" artifact, and `2a. spec-template.docx`.
- **Delivery**: One fewer MD-estimated backlog item; no dev work needed on a batch-closing job.

---

### ASM-083

| Field | Value |
|-------|-------|
| ID | ASM-083 |
| Created | 2026-09-14 |
| Source | Figma roadmap board comments (Honza Sovka), relayed to this session via screenshots on 2026-09-16 |
| By | Jan "Honza" Sovka (STK-002) |
| Status | Decided (2026-09-14) |

**Description**
Fakturace doprav's roadmap card "Potvrzení řidiči" is renamed "Potvrzení přepravci" — the electronic post-processing confirmation of received documents/confirmed km goes to the carrier (přepravce), not the driver; one carrier covers many drivers. It is merged with the separate "Generování potvrzení o skenování" card, since both describe the same underlying feature (auto-generate + email a confirmation from scan results) under different names.

**Rationale**
Honza Sovka's comments: "potvrzení přepravci, nikoliv řidiči (přepravce = X řidičů)" on the "Potvrzení řidiči" card, and "sloučil bych s 'potvrzení řidiči'" on the "Generování potvrzení o skenování" card. A 2026-09-16 codebase read confirmed there is a genuinely separate, already-built feature this should not be confused with: an in-kiosk driver-facing receipt PDF (auth-gated, shown/printed right after scanning) — that one stays a distinct fact to capture in the spec, not part of this merge.

**Impact**
- **Scope**: Card renamed and merged in `product-roadmap-portfolio-full.xlsx` (Fakturace doprav sheet), the live "AI Initiative Roadmaps v6" artifact, and `2a. spec-template.docx` §1.1.
- **Delivery**: One fewer separately-tracked Plná verze item; its estimate folded into "Potvrzení přepravci."

---

### ASM-082

| Field | Value |
|-------|-------|
| ID | ASM-082 |
| Created | 2026-09-14 |
| Source | Figma roadmap board comments (Honza Sovka), relayed to this session via screenshots on 2026-09-16 |
| By | Jan "Honza" Sovka (STK-002) |
| Status | Decided (2026-09-14) |

**Description**
For Fakturace doprav, the actual km-tolerance comparison and deviation flagging ("Identifikace odchylek") are entirely Axapta's responsibility, performed in Axapta's own UI — not a platform feature. The platform's job is limited to supplying input data: declared km from ZOPV via OCR (already done, MVP) and, optionally, km from GPS Dozor (Plná verze). Split into two separate tickets rather than one combined "km control" feature.

**Rationale**
Honza Sovka's comments: on "Kontrola kilometrů" — "samotné porovnání bude dělat Axapta, my jen zajišťujeme data - buď z ZOPV pomocí OCR - a volitelně ve fázi 1.1 i z GPS dozoru. Tzn. asi bych rozdělil na dva tickety"; on "Identifikace odchylek" — "to si bude dělat sama axapta ve svém UI." A direct codebase read on 2026-09-16 confirms this exactly: the `ZopvData` and `TransportRouteSubmissionCreate` docstrings in `libs/axapta_client` state the platform passes `distance_km` and Axapta's own km-tolerance check is authoritative; local verdict logic (`status_verdict.py`) never touches km at all. The data contract already has a `gps_distance_km` field (currently always null) — only the GPS Dozor client itself needs building, not new contract work.

**Impact**
- **Scope**: `product-roadmap-portfolio-full.xlsx` (Fakturace doprav sheet) — "Kontrola kilometrů" split into a ZOPV/OCR ticket (Done) and a new GPS-Dozor ticket (Backlog, replacing the cancelled "Měsíční uzávěrka" slot, see ASM-084); "Identifikace odchylek" status changed to "Mimo scope (Axapta)." Same changes applied to the live "AI Initiative Roadmaps v6" artifact and `2a. spec-template.docx` (§1.4, §2.1, Otevřené otázky).
- **Delivery**: Removes a previously-miscounted "Done" item (Identifikace odchylek was never actually a BigHub deliverable) from the completion percentage.

---

### ASM-081

| Field | Value |
|-------|-------|
| ID | ASM-081 |
| Created | 2026-09-16 |
| Source | PM instruction (conversational) |
| By | Marek Pillár (STK-001) |
| Status | Open (2026-09-16) |

**Description**
Vendorský portál — a separate, client-side initiative (not owned by BigHub) that would let suppliers submit listings directly in a unified format, previously noted in `listing-specifikace.md`'s "Další fáze" section with vazba na tento projekt `-tbd-`. PM flagged it as medium priority and a possible future AI initiative worth tracking.

**Rationale**
PM's own judgment call while reviewing the Listing spec. Explicit instruction: do not write this marking into `listing-specifikace.md` itself — track it only as a todo/assumption, keeping the spec file unmodified.

**Impact**
- **Roadmap**: Worth resurfacing if/when BigHub and Dr. Max scope future AI initiatives together — not currently actionable, no owner or client-side commitment exists yet (see the existing open question in `listing-specifikace.md` on who owns/relates this to the Listing project).
- **Scope**: No change to Listing's current delivery scope; `listing-specifikace.md` deliberately left untouched.

---

### ASM-080

| Field | Value |
|-------|-------|
| ID | ASM-080 |
| Created | 2026-09-16 |
| Source | cz-ai-logistics codebase read (claims_api) |
| By | Marek Pillár (STK-001), via direct code read |
| Status | Open (2026-09-16) |

**Description**
`apps/claims_api/.../claim_cases.py:88` — `generate_delivery_note` returns `GeneratedDeliveryNote(key=key)`, but `key` is never defined anywhere in that function, and `GeneratedDeliveryNote` only has a `document_link` field. This looks like it would raise a `NameError` at runtime whenever the endpoint that generates the reklamace delivery-note PDF is actually called.

**Rationale**
Found during a direct, from-scratch technical read of the Reklamace codebase (no existing business spec was on file to cross-check against). Flagged as a likely real defect rather than a documentation gap — worth a direct heads-up to the dev team rather than describing the feature as working in the new Reklamace brief.

**Impact**
- **Delivery**: `POST /claim-cases/{ref}/generate-doc` (and the Axapta-triggered `POST /claim-cases/{ref}/process` webhook, which calls the same code path on case closure) should be treated as unverified/likely broken until a developer confirms and fixes this.
- **Scope**: `product/solution-space/` — captured in the new `3. Reklamace.docx` brief (§1.3, Otevřené otázky) as a known issue, not a working feature.

---

### ASM-079

| Field | Value |
|-------|-------|
| ID | ASM-079 |
| Created | 2026-09-16 |
| Source | cz-ai-logistics codebase read (transport_invoicing_api) |
| By | Marek Pillár (STK-001), via direct code read |
| Status | Decided (2026-09-16) |

**Description**
Fakturace doprav's Axapta integration is confirmed built and live in code: full read (`GET /transport-routes/{ar}`) and write (`POST /transport-routes/{ar}/documents`) endpoints exist, with idempotency-key support, retry/backoff on 5xx, and typed error mapping (400/401/404/409/5xx). This corrects the spec/roadmap's prior claim that this integration was not yet built and pending business-spec approval.

**Rationale**
Found during a direct codebase read of `apps/transport_invoicing_api` and the shared `libs/axapta_client` OpenAPI contract (which carries its own versioned changelog through v0.9.9), triggered by Jan Sovka's roadmap-comment corrections needing verification against real code. The contract also already defines a `gps_distance_km` field (currently always null) — only the GPS Dozor client itself remains to be built, not new contract work — and a `Carrier` model sourced from Axapta, though Axapta's own data doesn't populate it yet (per Petr Sláma).

**Impact**
- **Scope**: `2a. spec-template.docx` (Fakturace doprav) updated — MVP table item "Integrace na Axaptu" moved from Backlog to Hotovo, Technická příloha now carries the real endpoint table, Závislosti section rewritten to drop this as an open dependency.
- **Roadmap**: `product-roadmap-portfolio-full.xlsx` (Fakturace doprav sheet) and the live "AI Initiative Roadmaps v6" artifact were not further changed by this specific finding (they already tracked the Axapta ticket separately) — noted here for traceability.
- **Related**: Confirms Honza Sovka's km-comparison correction (ASM-073-adjacent, same session) at the code level — `ZopvData` docstring states verbatim that the platform supplies `distance_km` and Axapta runs the km-tolerance check.

---

### ASM-078

| Field | Value |
|-------|-------|
| ID | ASM-078 |
| Created | 2026-09-16 |
| Source | 2026-09-16-teo-ocr-solution-proposal-variants |
| By | Team (BigHub-internal recommendation) |
| Status | Open (2026-09-16) |

**Description**
BigHub's internal (not yet client-shared) recommendation is to roll out TEO/OCR starting with the 3-4 highest-volume document categories, then expand to lower-frequency categories once accuracy is validated in production.

**Rationale**
The highest-volume categories represent the largest share of manual-effort savings, so starting there front-loads ROI. It also lets BigHub validate real-world accuracy and tune the pipeline before extending scope, since high template/format diversity across categories increases extraction complexity and can hurt model accuracy.

**Impact**
- **Delivery**: Sequencing choice affects which document categories get prioritized first if a build variant is approved — see [[ASM-077]].
- **Risk**: Not yet confirmed with Dr. Max (Tomáš Burda / Radim Švarc) — a purely internal BigHub proposal at this stage.

---

### ASM-077

| Field | Value |
|-------|-------|
| ID | ASM-077 |
| Created | 2026-09-16 |
| Source | 2026-09-16-teo-ocr-solution-proposal-variants |
| By | Team |
| Status | Open (2026-09-16) |

**Description**
Which of BigHub's 4 proposed TEO/OCR solution variants to formally propose to and pursue with Dr. Max is undecided: Variant API (12 MD, +6 MD prompt-editing add-on), Variant HYBRID (18 MD), or Variant APLIKACE — a full validation web app (25-35 MD, +2 further TBD-effort ServiceNow add-ons).

**Rationale**
No variant has been formally proposed to the client yet — this is still an internal BigHub draft (July 2026). The choice depends on Dr. Max's appetite for build cost/timeline vs. how much manual validation/control the technical department wants, and on Tomáš Burda's sign-off and the per-MD/hour rate he still owes (open action item).

**Impact**
- **Delivery**: MD estimates range 12-35+ MD depending on variant chosen — materially different timeline/cost commitments.
- **Relationship**: Formal proposal to Dr. Max should likely wait for Tomáš Burda's ownership confirmation and rate, and for the KPI definition to land, so the pitch can be framed against a concrete business case.

---

### ASM-076

| Field | Value |
|-------|-------|
| ID | ASM-076 |
| Created | 2026-09-16 |
| Source | 2026-09-16-teo-ocr-production-spec-v1-1, 2026-09-16-teo-ocr-accuracy-validation-cost-analysis |
| By | Team |
| Status | Decided (2026-09-16) |

**Description**
TEO/OCR's internal (BigHub-side) production architecture is agreed as blob storage intake → batch AI processing → API read-out (v1.1, dated 2026-08-07), using dual independent AI readings (GPT-5 + GPT-5-mini via Microsoft Azure AI Foundry) merged per page, with Azure AI Document Intelligence added for deterministic checkbox detection on checklist-style forms. This reuses BigHub's existing shared AI platform — no new paid Azure resources required.

**Rationale**
Validated against 292-370 real pages / 281 protocols across all 7 tuned document categories: 91% accuracy on handwritten content, 94% on structural content, 0 fabricated values found across 500+ pages tested. This is an internal engineering decision, not yet formally proposed to or agreed with Dr. Max — see [[ASM-077]] for the still-open question of which client-facing variant/scope this architecture gets packaged into.

**Impact**
- **Cost**: Negligible run cost (~8,500-17,000 Kč/year at an assumed 30,000 pages/year) since it reuses already-deployed shared-platform models and infrastructure.
- **Delivery**: Mailbox intake and ServiceNow write-back are explicitly deferred to a later phase, addable without re-architecting — current scope is API-readable structured protocol records only.
- **Risk**: This architecture is independent of, and not confirmed to be the same artifact as, the separate "API service specification" Radim Švarc reported receiving and beginning to test around 2026-09-14 — worth clarifying with Radim before assuming client-side awareness of this specific pipeline.

---

### ASM-075

| Field | Value |
|-------|-------|
| ID | ASM-075 |
| Created | 2026-09-16 |
| Source | 2026-09-16-business-quantification-listing-petr-neuman; superseded by 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |
| By | Petr Neuman (STK-023) |
| Status | Superseded by [[ASM-123]] (2026-09-22) |

**Description**
Listing's KPI has no committed target. Petr Neuman explicitly declined to state a precise figure, floating only a directional placeholder: roughly "~20% faster / ~20% more throughput" in the tool's first live quarter, expected to compound quarter over quarter as the process matures.

**Rationale**
Neuman said fixing a number this early "feels like making it up" — he wants to see the tool's real performance before committing to a benchmark. Today's per-item time varies enormously by task (a full new listing ~30 min vs. a small compliance text fix ~2 min), which makes a single baseline number unreliable without live data.

**Superseded (2026-09-22)**: Neuman now has a live report backing concrete figures — see [[ASM-123]] for the committed ~34M Kč/year value. This entry is kept for the historical record of his initial reluctance.

**Impact**
- **Reporting**: The corporate KPI Excel (`businessQuantificationWorskop.xlsx`, E-commerce BQ sheet) currently carries this placeholder — flagged in its Notes field as orientational, not committed. Replace with ASM-123's figures.
- **Delivery**: A real benchmark should be captured as soon as the tool is live and processing real listing volume, then used to replace this placeholder.
- **Relationship**: Resisting an invented number is consistent with the pattern seen across this week's other Business Quantification interviews (Tereza Foltýnová, Radim Švarc) — treated as a positive trust signal, not stalling.

---

### ASM-074

| Field | Value |
|-------|-------|
| ID | ASM-074 |
| Created | 2026-09-16 |
| Source | 2026-09-16-business-quantification-listing-petr-neuman |
| By | Petr Neuman (STK-023) |
| Status | Decided (2026-09-16) |

**Description**
Michaela Vdovicynová (STK-048) is confirmed as Listing's practical domain-expert/testing contact — the day-to-day working-level liaison for BigHub — distinct from Petr Neuman's business-owner role.

**Rationale**
No formal "head of listing" role exists yet on Dr. Max's side; Neuman is filling that gap at the direction-setting level but doesn't have time for practical/operational work (team testing, feedback collection). He nominated Vdovicynová, a listing-team member who does the work herself, as the person BigHub should work with day-to-day.

**Impact**
- **Delivery**: Marek's planned Discovery kickoff should route through Vdovicynová for testing sessions and feedback, not Neuman directly.
- **Relationship**: Leaves open whether Vdovicynová is the same "second listing business owner" previously referenced (2026-09-02, name unknown) — not confirmed either way; see Open Questions in the source meeting note.

---

### ASM-073

| Field | Value |
|-------|-------|
| ID | ASM-073 |
| Created | 2026-09-16 |
| Source | 2026-09-16-business-quantification-listing-petr-neuman |
| By | Petr Neuman (STK-023) |
| Status | Decided (2026-09-16) |

**Description**
Listing's primary near-term driver is reframed: eliminating the listing team's day-to-day use of Magento (completing products entirely inside BigHub's tool, batch-exporting to Magento roughly once every two weeks) now outranks the project's original framing — poor supplier data quality — as the most urgent problem to solve.

**Rationale**
Petr Neuman was explicit that Magento's growing instability at Dr. Max's ~80,000-100,000 SKU scale (frequent multi-second save failures that discard completed work) is now his primary motivation, more than the original missing-parameter data-quality problem that started the project. An upcoming Magento change (removal of parametric grouping, surfacing all ~100 parameters per category instead of the relevant ~10-15) will make this worse.

**Impact**
- **Scope**: `product/solution-space/listing-specifikace.md`'s "Byznys hodnota" framing and MVP status ("Propis do Magento" currently Backlog) should be reviewed against this reframed priority.
- **Delivery**: The export/import format Magento expects for batch import still needs to be defined with Dr. Max's own import/export technical contact (not yet named) — a follow-up session is expected.
- **Timeline**: Reinforces urgency on the Magento-integration work relative to further data-quality/enrichment features.

---

### ASM-072

| Field | Value |
|-------|-------|
| ID | ASM-072 |
| Created | 2026-09-15 |
| Source | 2026-09-15-business-quantification-reklamace-fakturace-doprav |
| By | Marek Pillár, Tereza Foltýnová (STK-013) |
| Status | Decided (2026-09-15) |

**Description**
Three related KPI-design decisions surfaced while quantifying Reklamace and Fakturace doprav in the Business Quantification interview: (1) document/claim error rate is excluded as a KPI for both initiatives — attribution to the tool vs. driver/staff behavior is too unclear to be a clean metric; (2) driver time and cost are excluded from Fakturace doprav's business-value calculation entirely, since drivers are not ViaPharma/Dr. Max employees — only office/administrative time counts; (3) Reklamace's full projected ~1 FTE saving is contingent on all 5 delivery phases shipping, not any single phase, and the documentation should make phase-by-phase scope explicit rather than implying the saving lands immediately.

**Rationale**
Marek raised error rate as a candidate KPI for both initiatives but both agreed it would require driver/staff education to fix rather than measuring the tool's own effect, and blame attribution would stay murky — dropped rather than force a weak metric into the OKR card. The driver-scope exclusion follows directly from headcount: no driver time is on ViaPharma/Dr. Max's own payroll, so it can't factor into an FTE-savings figure. The phasing note came from Tereza flagging that people already confuse which Reklamace phase/claim-type is being discussed.

**Impact**
- **KPI design**: Both initiatives' OKR cards in the Business Quantification tracker reflect these exclusions/dependencies rather than carrying speculative metrics.
- **Expectation management**: Prevents the ~1 FTE Reklamace saving being read as available before all 5 phases ship.

---

### ASM-071

| Field | Value |
|-------|-------|
| ID | ASM-071 |
| Created | 2026-09-15 |
| Source | 2026-09-15-order-prediction-dashboard-follow-up |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-15) |

**Description**
Pharmacy reservations ("rezervace v lékárnách") are confirmed as a deliberate strategic differentiator for Dr. Max's e-commerce, not just another order channel — leveraging ~600 physical pharmacies as pickup points is dramatically cheaper fulfillment than warehouse-based click & collect (a pharmacist holds a product on a shelf vs. Dr. Max carrying full fulfillment/return cost). A new in-app "reserve at pharmacy" button (alongside add-to-cart) is being actively pushed. On the dashboard, reservations will be broken out as their own top-line category (separate from e-com/marketplace) and further split per warehouse (Nučice, Brno) specifically to support logistics staffing planning.

**Rationale**
Petr Ondráček flagged that reservations were folded into the general new-orders aggregate today, hiding both the reporting distinction Dr. Max cares about and the warehouse-level detail logistics needs to plan staffing. Šimoník's business context made clear this isn't a minor reporting nicety — it's core to how Dr. Max wants to grow the channel.

**Impact**
- **Dashboard scope**: Drives several concrete build items — a top-line rezervace/e-com/marketplace split, and a warehouse × reservation-type breakdown feeding into the existing "Metrix" view (which needs redesign since reservations don't map cleanly onto its warehouse/delivery-method axes today).
- **Business relevance**: Confirms this dashboard workstream has direct visibility into a stated Dr. Max growth strategy, not just operational reporting.

---

### ASM-070

| Field | Value |
|-------|-------|
| ID | ASM-070 |
| Created | 2026-09-15 |
| Source | 2026-09-15-order-prediction-dashboard-follow-up |
| By | Marek Šimoník (STK-019) |
| Status | Decided (2026-09-15) |

**Description**
As budget, forecast, and the model's own predicted-revenue figure all start appearing together on the same dashboard views, the model's output will consistently be called "predikce" — kept terminologically distinct from Dr. Max's own "budget" (set annually each August) and "forecast" (Dr. Max's internal re-budgeting exercise, redone after months 3, 5, and 7 against year-end expectations).

**Rationale**
Šimoník was explicit that mixing up "forecast" (a Dr. Max planning term) with the model's prediction would confuse other managers who see this dashboard — he wants the naming kept clean specifically because more people will use it beyond himself and Petr Ondráček going forward.

**Impact**
- **Dashboard UI**: All future views combining these three figures (e.g. the "new orders" and Business Overview pages) must use this naming consistently.
- **Data pipeline**: Confirms budget/forecast are externally supplied by Dr. Max (a "2026 forecast" Excel column, already sent by Alana) rather than computed by the model — the model only ever produces "predikce."

---

### ASM-069

| Field | Value |
|-------|-------|
| ID | ASM-069 |
| Created | 2026-09-15 |
| Source | 2026-09-15-order-prediction-dashboard-follow-up |
| By | Jindřich Tůma (STK-003), agreed by Marek Šimoník (STK-019) |
| Status | Decided (2026-09-15) |

**Description**
The order-prediction dashboard's currently delivered build is formally accepted by the client as "version 1." Today's feedback (and any further requests) becomes the batched scope for "version 2"; once v2 ships, subsequent requests batch into "version 3" on a roughly quarterly cadence, rather than continuous ad hoc releases.

**Rationale**
Jindřich proposed this partly to meet BigHub-internal reporting pressure to show formally delivered value on a defined cadence, and partly to give the workstream a sustainable release rhythm instead of endless small pushes. Šimoník agreed immediately and warmly, confirming the delivered build already reflects the intended non-final UX direction.

**Impact**
- **Delivery cadence**: Establishes a precedent — v1 accepted now, v2 to bundle today's ~10 feature requests, v3 to bundle whatever surfaces after that, roughly quarterly.
- **Client relationship**: Signals enough trust to move from continuous iteration to a more formal cadence without it reading as BigHub reducing engagement.

---

### ASM-068

| Field | Value |
|-------|-------|
| ID | ASM-068 |
| Created | 2026-09-15 |
| Source | product/solution-space/listing-specifikace.md review (Jan S. comment thread on FigJam board, relayed by Marek Pillár) |
| By | Jan S. |
| Status | Decided (2026-09-15) |

**Description**
"Multi-kategoriální podpora" (Nice to Have) actually bundled two separate questions: (1) how many/which categories to eventually cover (pure scope, orientačně 500–2 000+), and (2) how listovací minima should inherit across a category hierarchy (e.g. Pro sportovce → Sportovní výživa a diety → Proteiny → Hovězí proteiny — a superkategorie sets general minima, subkategorie add specifics). Jan S. proposed carving out (2) into Plná verze since it needs to be specified regardless of when/how far the raw category count scales; Marek confirmed. (1) stays in Nice to Have as a pure scope question.

**Rationale**
Today's model is flat — 1 listovací minimum per category, no matter how deep in the hierarchy — so there's no defined logic for inheritance/nesting. That's an architecture question independent of category count, and blocks designing the category-standards editor properly even before the count is decided.

**Impact**
- **Scope**: `product/solution-space/listing-specifikace.md` section 2.4 now carries this as a Plná verze item (ID 15); section 3.1 (Nice to Have) is narrowed to just the category-count question.
- **Open question carried forward**: exact inheritance/override rules between superkategorie and subkategorie still need to be specified with Petr Neuman.

---

### ASM-067

| Field | Value |
|-------|-------|
| ID | ASM-067 |
| Created | 2026-09-15 |
| Source | product/solution-space/listing-specifikace.md review (Jan S. comment thread on FigJam board, relayed by Marek Pillár) |
| By | Jan S. |
| Status | Decided (2026-09-15) |

**Description**
"Produkční nasazení" (production deployment) previously had no defined completion criterion. Jan S. proposed, and Marek confirmed, the bar: the listingový tým can, by themselves, import a product, edit it in the tool, and get the result back into Magento — even if the first version is "na tupáka" (e.g. copying through an Excel sheet) — as long as nobody has to manually ctrl-c/ctrl-v content between systems. Jan S. framed this explicitly as the *starting line* for reasonable usability in the current version, not the target fully-automated integration.

**Rationale**
Without a defined finish line, "produkční nasazení" was an ambiguous status label. This gives a concrete, testable minimum bar that doesn't require the full Magento integration (see [[ASM-065]]) to be complete first.

**Impact**
- **Scope**: `product/solution-space/listing-specifikace.md` section 1.4 now documents this criterion directly.
- **Sequencing**: Clarifies that "produkční nasazení" can be reached via a manual/semi-manual transfer method before the fully automated Magento integration ([[ASM-065]]) is built.

---

### ASM-066

| Field | Value |
|-------|-------|
| ID | ASM-066 |
| Created | 2026-09-15 |
| Source | product/solution-space/listing-specifikace.md review (Jan S. comment thread on FigJam board, relayed by Marek Pillár) |
| By | Jan S. |
| Status | Decided (2026-09-15) |

**Description**
"Tvorba popisů pro nové produkty" was tracked as a separate Backlog item in Plná verze. Jan S. clarified the actual process: new products must always be created in Magento first (by Dr. Max or dodavatelé) before they can enter this tool — so by the time a product reaches Listing, it always looks like an "existing product," never a genuinely new one from the tool's point of view. The existing generation flow (section 1.2) therefore already covers new products without any additional feature work. Reclassified from Backlog to Hotovo.

**Rationale**
Marek initially proposed moving the item to backlog/a later phase pending clarification; once Jan S. explained the Magento-first process constraint, both agreed the item was already satisfied by existing MVP functionality. The manual effort that does happen before a product reaches Magento is real but sits with Dr. Max/dodavatelé, outside this e-commerce tool's scope — to be addressed (if at all) in the broader E2E listing process, not here.

**Impact**
- **Scope**: `product/solution-space/listing-specifikace.md` section 2.2 rewritten; item status flips from Backlog to Hotovo in both the Management summary and the Plná verze "Co je součástí" table.
- **Scope boundary**: Confirms pre-Magento manual product-creation effort is out of this tool's scope, consistent with [[ASM-031]] (category/structure recommendation also out of scope for the same reason — depends on Dr. Max's own upstream process).

---

### ASM-065

| Field | Value |
|-------|-------|
| ID | ASM-065 |
| Created | 2026-09-14 |
| Source | product/solution-space/listing-specifikace.md enrichment session (codebase read of `cz-ai-listing`) |
| By | Marek Pillár (PM decision) |
| Status | Decided (2026-09-14) |

**Description**
A direct read of the `cz-ai-listing` codebase confirmed there is no Magento integration of any kind today (no API client, no export, no file-based sync) — the tool is a closed loop against its own Postgres database, with product/category identity seeded once from a legacy export as a stand-in. PM confirmed this is expected: the current phase is deliberately import-only. Full Magento connection (the tool working live against Magento, not a stand-in projection) is a confirmed must-have before the tool can go to production — not an open question, a committed requirement for launch.

**Rationale**
Building against a stand-in projection is fine for iterating on generation/validation/standards in the current phase, but production usage requires the tool's data to actually reflect and write back to Magento — otherwise listings approved in the tool never reach the live storefront.

**Impact**
- **Scope**: Magento integration (exact mechanism — file upload vs. direct write vs. API — still `-tbd-`) is a hard dependency for the Produkční nasazení item in the MVP phase, not a nice-to-have.
- **Timeline**: Production go-live cannot be scheduled until this integration is scoped and built.

---

### ASM-064

| Field | Value |
|-------|-------|
| ID | ASM-064 |
| Created | 2026-09-14 |
| Source | product/solution-space/listing-specifikace.md enrichment session (codebase read of `cz-ai-listing`) |
| By | Marek Pillár (PM decision) |
| Status | Open (2026-09-14) |

**Description**
Code confirmed the blacklist of non-compliant medical-claim phrases only produces a warning-severity validation issue — it does not block saving or publishing a listing that contains a banned phrase. This corrected an earlier (incorrect) assumption in the Listing spec that the blacklist was a hard block. PM's call for now: keep it as a warning, not a blocker. Whether it should be tightened into a blocking pre-publish check remains an open business/compliance decision.

**Rationale**
The validation code itself notes forbidden-phrase matching is a simple substring check with real false-positive risk ("context matters") — making it fully blocking today could wrongly prevent legitimate content from being saved. Leaving it as a warning keeps a human in the loop without over-blocking on an imperfect check.

**Impact**
- **Scope**: No code change needed now. If this is later decided to become blocking, it's a validation-logic change plus a client-facing conversation about false-positive tolerance.
- **Risk**: Regulatory/compliance exposure is reduced, not eliminated, while enforcement stays advisory-only.

---

### ASM-063

| Field | Value |
|-------|-------|
| ID | ASM-063 |
| Created | 2026-09-10 |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |
| By | Jura Brázdil, Simona Mertová |
| Status | Open (2026-09-10) |

**Description**
For Lexie role-based testing across 4 CC sub-departments (call centre agent, back office agent, testing, and a fourth), two technical options were identified: (A) four fully separate accounts requiring logout/login to switch, or (B) one account placed in all relevant Entra groups with an in-app role switcher BigHub would build. Dr. Max prefers option B.

**Rationale**
Testers need to run two roles side-by-side on one screen for testing to be practical, and full re-authentication per role switch is disruptive. However, Jura flagged that a single account in all groups simultaneously doesn't actually test the role-restriction behavior a real operator experiences, and Mertová separately raised whether four concurrent testers sharing one account would conflict — neither concern is resolved yet.

**Impact**
- **Scope**: Option B requires new BigHub-side work (an in-app role switcher) not otherwise planned.
- **Timeline**: Blocks meaningful Lexie role-based testing until Jura confirms feasibility.

---

### ASM-062

| Field | Value |
|-------|-------|
| ID | ASM-062 |
| Created | 2026-09-10 |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |
| By | Jindřich Tůma |
| Status | Decided (2026-09-10) |

**Description**
X-Manager will not be extended to other Dr. Max departments/streams for now, even though Marek raised the idea and Jindřich's original instinct was favorable. Jindřich is waiting on Tomáš Dudaško's separately-mentioned future DevOps environment project to be created before deciding whether to extend X-Manager or move CC onto that new environment instead.

**Rationale**
Committing to extend X-Manager now risks being redone once the DevOps environment exists; CC's current X-Manager usage is working well, so there's no urgency to decide ahead of that dependency.

**Impact**
- **Scope**: Keeps X-Manager's footprint limited to Lexie/Max/Maxie for now; any cross-stream tooling decision is deferred.

---

### ASM-061

| Field | Value |
|-------|-------|
| ID | ASM-061 |
| Created | 2026-09-10 |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |
| By | Jindřich Tůma |
| Status | Decided (2026-09-10) |

**Description**
Jindřich will build a cross-project harmonogram (timeline) covering Lexie, Max, and Maxie together, broken down by week and then by individual workday, including testing windows — so Dr. Max can plan CC capacity around expected testing days.

**Rationale**
Kadlecová and Mertová both asked for roadmap visibility beyond ticket-level tracking, specifically to plan their own team's capacity since CC works multiple initiatives in parallel, not just this one.

**Impact**
- **Timeline**: Explicitly framed as orientational, not a fixed commitment, given dependencies on Dr. Max's own side (echoes the same framing used for the existing product-scope roadmap board).

---

### ASM-060

| Field | Value |
|-------|-------|
| ID | ASM-060 |
| Created | 2026-09-10 |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |
| By | Jindřich Tůma, Jura Brázdil |
| Status | Decided (2026-09-10) |

**Description**
Lexie's visual/UX polish (colors, field sizing) stays at a "find a compromise" level — Jindřich and Jura will open a dedicated ticket for incremental improvement, but a full redesign is deliberately deferred until the AI-platform-wide design consolidation (owned by Tomáš Dudaško) is decided, since per-app design can't diverge from the eventual unified platform design without risking rework.

**Rationale**
Mertová raised that Lexie looks noticeably less polished than the newer Max chatbot. BigHub is actively working on consolidating all Dr. Max apps under one central platform entry point first; per-app design should cascade down from that decision once made, not precede it. This extends the earlier deprioritization decision in [[ASM-024]].

**Impact**
- **Scope**: Limits near-term Lexie design work to a bounded compromise ticket rather than an open-ended redesign.
- **Client relationship**: Mertová accepted the framing, asking only that user-facing polish land before end users (not just CC) get access.

---

### ASM-059

| Field | Value |
|-------|-------|
| ID | ASM-059 |
| Created | 2026-09-10 |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |
| By | Jindřich Tůma, Kateřina Kadlecová |
| Status | Open (2026-09-10) |

**Description**
The X-Manager Kanban view, grouped by scope (MVP / Full Version / Nice to Have, with a hide-empty-columns option), is confirmed to satisfy Kadlecová's standing roadmap-visibility ask. No separate Excel roadmap deliverable is planned — the live system is intended as the source of truth going forward, pending Mertová's business-side confirmation that it also works for non-technical stakeholders.

**Rationale**
Jindřich's stated preference is that the system itself should always reflect current state on demand, rather than producing periodic static exports; the scope-grouping reproduces the structure of Kadlecová's own Excel tracker.

**Impact**
- **Client relationship**: Resolves a standing, repeatedly-raised client ask (previously logged at the 2026-09-03 sync) — pending final sign-off from Mertová.

---

### ASM-058

| Field | Value |
|-------|-------|
| ID | ASM-058 |
| Created | 2026-09-10 |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |
| By | Kateřina Kadlecová |
| Status | Decided (2026-09-10) |

**Description**
Lexie's thumbs-up/down feedback bug (one of the 3 original blockers from 2026-09-03) is resolved — Kadlecová confirmed she can now retroactively evaluate conversations she'd previously been unable to rate, and Lexie testing has formally resumed.

**Rationale**
Direct client confirmation after retesting.

**Impact**
- **Timeline**: Unblocks the CC team's Lexie testing, which had been fully paused since 2026-09-03 (see [[ASM-021]]).

---

### ASM-057

| Field | Value |
|-------|-------|
| ID | ASM-057 |
| Created | 2026-09-10 |
| Source | 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Petr Sláma |
| Status | Open (2026-09-10) |

**Description**
Petr Sláma flagged that current documentation doesn't cover API sequencing/behavior between the reklamace app and Axapta in enough operational detail (what gets sent when, what response to expect) to safely start backend development against it. A dedicated walkthrough session with Jindřich/Jakub is needed before backend work proceeds further.

**Rationale**
Sláma needs to validate the full flow before committing dev time on his side; a prior round of written feedback was acknowledged but not actually incorporated into the doc, causing confusion about whether it had been addressed.

**Impact**
- **Timeline**: Blocks further reklamace backend development on ViaPharma's side until the walkthrough happens (targeted for next week).

---

### ASM-056

| Field | Value |
|-------|-------|
| ID | ASM-056 |
| Created | 2026-09-10 |
| Source | 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Petr Sláma / Jindřich Tůma |
| Status | Decided (2026-09-10) |

**Description**
Full-functionality reklamace UAT (through email generation) starts October 15-16, targeting completion by October 2 — sequential-vs-parallel testing (relative to the narrower scan-only UAT already scheduled) was explicitly left to Petr Sláma's judgment.

**Rationale**
Landed after a tense negotiation: Sláma initially rejected a 2-day testing-window draft as unrealistic, citing ~18 process variants, a need to validate downstream Axapta financial/logistics effects (not just app UX), a Finance-team dependency, and his own September capacity constraints from two unrelated GoLive projects. Jindřich de-escalated by clarifying the timeline was an adjustable draft and handing the parallel-vs-sequential decision back to the client.

**Impact**
- **Delivery timeline**: This is now the committal date for full reklamace functionality being client-validated — plan around it.
- **Process**: Sláma committed to reporting blockers continuously during UAT rather than batching them.

---

### ASM-055

| Field | Value |
|-------|-------|
| ID | ASM-055 |
| Created | 2026-09-10 |
| Source | 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Jan Sovka / Jan Žižka |
| Status | Decided (2026-09-10) |

**Description**
Fakturace doprav kiosk hardware (scanner + PC) stays ViaPharma's procurement responsibility, not BigHub's — a position BigHub pushed for internally and which the client (Jan Žižka) confirmed, while flagging his own team currently lacks a clear internal owner for it.

**Rationale**
Consistent with keeping BigHub's scope to the software/AI layer; Žižka will loop in ViaPharma's own IT and Petr Sláma to resolve the ownership gap on their side. Filip is sending a same-day minimum-spec recommendation to help them act.

**Impact**
- **Timeline risk**: Testing with real hardware can't start until ViaPharma sources it — interim testing will use manual file upload instead of live scanning.

---

### ASM-054

| Field | Value |
|-------|-------|
| ID | ASM-054 |
| Created | 2026-09-10 |
| Source | 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Jan Žižka |
| Status | Decided (2026-09-10) |

**Description**
Fakturace doprav confirmation-screen scope confirmed directly with the client: keep the end-of-session confirmation table, but show specific missing page numbers (not just fractional counts like "2 of 7"); drop the optional driver-notes field entirely; kiosk UI is touchscreen-only, no keyboard.

**Rationale**
Žižka wants a dispatcher facing a driver dispute to see exactly which pages are missing, not just a fraction. He rejected the notes field outright — drivers would use it inconsistently, creating manual-review noise with no clear payoff; a driver with a real problem should call directly instead.

**Impact**
- **UI scope**: Removes ambiguity from the internal-demo open question about whether the richer confirmation screen exceeded the original Žižka spec — it's now explicitly client-confirmed as wanted, with two concrete refinements.

---

### ASM-053

| Field | Value |
|-------|-------|
| ID | ASM-053 |
| Created | 2026-09-10 |
| Source | 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Jan Žižka |
| Status | Decided (2026-09-10) |

**Description**
Axapta — not the BigHub Fakturace doprav app — is the sole source of truth for route/document state. The app holds no state of its own; it simply forwards scanned documents as they arrive, whenever they arrive. Axapta needs a row to appear the moment the *first* document for a route lands (so ViaPharma has reaction time to chase a slow carrier before month-end close), and Axapta itself reconciles documents arriving across multiple separate scan sessions for the same route.

**Rationale**
Resolves a real architecture misunderstanding: Filip had built against an assumption that the app needed to track its own completion state and push a manual-review/ready-for-invoicing status to Axapta. Jan Žižka clarified live during the demo that this is backwards. This also **retires the page-count-vs-document-count concern** raised earlier the same day in the internal kiosk demo review (see `2026-09-10-fakturace-doprav-kiosk-portal-demo`) — that confusion was a symptom of this same bigger misunderstanding, not a separate problem needing its own fix.

**Impact**
- **App simplification**: Per Filip, this genuinely simplifies the app's design — no internal state to hold or synchronize.
- **Spec/Swagger update needed**: The Fakturace doprav spec and Swagger need to be corrected to reflect this division of responsibility.
- **New dependency**: A driver-facing "what's been scanned so far" view (requested by Žižka, see ASM below) now requires querying Axapta on demand, since the app holds nothing itself — needs validation against what Axapta's API can actually return.

---

### ASM-052

| Field | Value |
|-------|-------|
| ID | ASM-052 |
| Created | 2026-09-10 |
| Source | 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Jakub Turner / Jan Žižka |
| Status | Open (risk, 2026-09-10) |

**Description**
The Fakturace doprav kiosk has no authentication — anyone can walk up and upload documents directly to the app, which feeds them straight to the LLM with no injection/security review. The client (Jan Žižka) confirmed this open-access model is intentional and acceptable to them, but the underlying security-surface risk Jakub Turner raised (adversarial content embedded in an uploaded document, aimed at the LLM) remains technically unaddressed — document-type validation only catches "not a real document," not injection attempts.

**Rationale**
Mirrors the physical process today (anyone can hand over paper documents); the client is comfortable with this model and takes responsibility for what gets uploaded at the kiosk. A minimal driver identifier (e.g. license plate) per scan session was suggested as a lightweight post-incident traceability measure, not yet committed to.

**Impact**
- **Security**: A real security review of the LLM-facing upload surface is still needed; BigHub has flagged responsibility for what's uploaded sits with the client given the open-access design.
- **Follow-up**: Žižka is taking the driver-identifier suggestion internally, not yet decided.

---

### ASM-051

| Field | Value |
|-------|-------|
| ID | ASM-051 |
| Created | 2026-09-10 |
| Source | 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |
| By | Filip Černý / Jan Žižka |
| Status | Decided (2026-09-10) |

**Description**
Fakturace doprav's OCR confidence-flagging philosophy (read a field correctly, or explicitly flag it as uncertain for human review — never silently guess) and AR-number fallback design (barcode when present, otherwise a computer-printed AR number; handwritten-only AR numbers unacceptable) are confirmed working via live demo and were shown to and accepted by the client without objection.

**Rationale**
This design was first validated internally, then demonstrated live to Jan Žižka the same day with no pushback — a rare same-day internal-to-client validation loop.

**Impact**
- **Confidence**: No further validation needed on this specific design point before proceeding.

---

### ASM-050

| Field | Value |
|-------|-------|
| ID | ASM-050 |
| Created | 2026-09-09 |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |
| By | Jindřich Tůma |
| Status | Decided (2026-09-09) |

**Description**
Alongside the existing MD-estimate roadmap board, a calendar/timeline-style view is needed: item names on the left, a monthly time axis on the right, with filled-in cells marking when testing happens, when bugs get fixed, and when rollout lands.

**Rationale**
Jindřich flagged that a phase estimate like "MVP in one man-day" is meaningless to a non-technical business stakeholder (e.g. Tereza Foltová) without a real calendar attached — a "mandate" could mean a week or much longer in wall-clock time. Doesn't need to be elaborate, just visually clear enough to show concrete testing/fix/rollout windows.

**Impact**
- **Deliverable scope**: Marek needs to build this before 2026-09-10's Logistika/CC presentations, using dev input gathered at the 2026-09-09 3pm internal meeting.
- **Reusability**: Once built for Logistika/CC, the same format likely applies to future roadmap presentations across other streams.

---

### ASM-049

| Field | Value |
|-------|-------|
| ID | ASM-049 |
| Created | 2026-09-09 |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |
| By | Marek Pillár |
| Status | Decided (2026-09-09) |

**Description**
Tomorrow's roadmap presentations are split by audience from the same underlying roadmap board rather than built as separate decks: Logistika in the morning (reklamace, fakturace doprav), CC later (~1 hour, focused mainly on reviewing chatbot/Lexie testing feedback with Kateřina Karlecová, with only the last ~15 minutes on the roadmap itself).

**Rationale**
Tereza Foltová was the primary requester for the Logistika content, which is largely ready. The CC session's real purpose is moving chatbot/Lexie toward a production decision based on testing feedback — Jindřich didn't want the roadmap walkthrough to crowd out that discussion.

**Impact**
- **Meeting prep**: Marek prepares one filtered view per audience rather than two separate presentations.

---

### ASM-048

| Field | Value |
|-------|-------|
| ID | ASM-048 |
| Created | 2026-09-09 |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |
| By | Jindřich Tůma |
| Status | Decided (2026-09-09) |

**Description**
Jindřich will join Marek only for the first MaxBuddy-related domain-expert 1:1, to introduce a separate topic he needs to kick off personally. All other domain-expert meetings across the portfolio run solo by Marek, who keeps Jindřich informed whenever one gets scheduled so he can feed in relevant input beforehand.

**Rationale**
Jindřich has a specific topic he wants raised at the first MaxBuddy meeting; beyond that, Marek's 1:1s with domain experts are part of his own onboarding and don't need Jindřich present.

**Impact**
- **Scheduling**: Marek must notify Jindřich ahead of every domain-expert meeting he books, not just the MaxBuddy one.

---

### ASM-047

| Field | Value |
|-------|-------|
| ID | ASM-047 |
| Created | 2026-09-09 |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |
| By | Jindřich Tůma |
| Status | Decided (2026-09-09) |

**Description**
Business value for each initiative must be captured in concrete, measurable numbers — not vague qualitative statements — so results can be measured against it once delivered. Marek will start with CC initiatives since those deliver within two weeks, and will track this in a new Value/KPI ("Strategy") tab on the roadmap Excel.

**Rationale**
Jindřich wants any business case to be understandable and verifiable by a non-technical, "economically competent" reader (e.g. "3 minutes saved per case" translated into an actual cost figure via average wage rate), and measurable after the fact — not just directional framing like "customers will complain less."

**Impact**
- **1:1 prep**: Every domain-expert meeting from next week onward needs to produce at least a rough numeric value estimate, not just qualitative rationale.
- **Roadmap Excel**: Requires Marek to build out the "Strategy" tab (Value + KPI columns) across all 9 initiatives.

---

### ASM-046

| Field | Value |
|-------|-------|
| ID | ASM-046 |
| Created | 2026-09-09 |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |
| By | Marek Pillár |
| Status | Decided (2026-09-09) |

**Description**
Closing the current MVP phase and opening the next one requires, in order: testing with the client, collecting feedback via an established feedback channel, and triaging what's a change request (in/out of original scope) versus a genuinely new feature. Only after that does a Discovery session with a client-side domain expert start the next phase.

**Rationale**
Marek wants a consistent, repeatable process for phase transitions across all 9 initiatives rather than an ad hoc close-out each time — starting with reklamace and fakturace doprav, where this is discussed as immediately applicable.

**Impact**
- **Process**: Applies first to reklamace/fakturace doprav (Discovery targeted for next week, pending a named domain expert from Logistika) and is the intended template for other streams as they reach MVP completion.

---

### ASM-045

| Field | Value |
|-------|-------|
| ID | ASM-045 |
| Created | 2026-09-08 |
| Source | PM input, 2026-09-08 (scoping Q&A ahead of the Claude Design brief) |
| By | Marek Pillár |
| Status | Decided (2026-09-08) |

**Description**
The first Dr. Max AI Platform prototype is scoped to exactly 4 screens: Home/app catalog, Usage Reports (cost + usage + adoption), Kill Switch, and Simulation mode. The other 44 items in Dudaško's 48-item governance/compliance capability register (identity management, audit trails, policy-as-code, HITL approval queues, agent registry, etc.) stay backend/architecture — not designed as UI this pass. Access is governed by flexible, admin-defined user groups (not a fixed department list) with individual-level overrides on top, which drove adding a new "Skupiny uživatelů" admin screen. The Kill Switch has two independent control axes: per product/agent, and per underlying LLM model — the latter's exact mechanics are provisional pending a technical conversation with Jura Brázdil.

**Rationale**
Matches the near-term pragmatism Jindřich Tůma set at the 2026-09-08 planning meeting ("keep it simple, don't overbuild") and the stated goal of impressing Dudaško with something concrete rather than exhaustively covering his governance checklist. Full brief: `product/solution-space/ai-platform-claude-design-brief.md`.

**Impact**
- **Delivery timeline**: Keeps the prototype buildable by Marek in Claude Design on a next-day timeline rather than requiring a much larger design effort.
- **Follow-up needed**: Per-model kill switch mechanics need validation with Jura Brázdil before being presented as final; real user-group definitions need a conversation with Dr. Max, since none exist yet.

---

### ASM-044

| Field | Value |
|-------|-------|
| ID | ASM-044 |
| Created | 2026-09-08 |
| Source | PM input, 2026-09-08 |
| By | Marek Pillár |
| Status | Decided (2026-09-08) |

**Description**
The 9-product roadmap board and its underlying Excel file are treated as client-facing deliverables, not internal working documents. All internal meeting-date references (e.g. "2026-09-07 portfolio review") and named individual attributions must be scrubbed from every note/comment before the roadmap is shown to Dr. Max.

**Rationale**
The roadmap is now finished and heading toward a client presentation; internal process references and specific team-member names aren't appropriate for that audience and don't add value to a client reading the board.

**Impact**
- **Content standard going forward**: Any new comment or block-reason added to the roadmap or Excel must follow this convention from creation — no more retroactive cleanup passes needed if this is respected upfront.

---

### ASM-043

| Field | Value |
|-------|-------|
| ID | ASM-043 |
| Created | 2026-09-08 |
| Source | 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |
| By | Marek Pillár |
| Status | Open (2026-09-08) |

**Description**
The AI-platform work being done in front of Tomáš Dudaško should be explicitly framed internally as: "we're doing this now for business reasons with Dr. Max, but anything we validate or learn here also feeds back into BigHub's own platform" — not treated as a fully bespoke, isolated build for one client.

**Rationale**
Marek raised this to avoid the work looking like pure custom labor for Dr. Max with no benefit to BigHub's own platform investment, especially given the shared-platform vision (ASM-038) was only recently retired. Not yet resolved with the wider team.

**Impact**
- **Internal positioning**: Affects how this work gets described in BigHub-internal contexts (capacity planning, cost justification) — worth resolving before the work is too far along.

---

### ASM-042

| Field | Value |
|-------|-------|
| ID | ASM-042 |
| Created | 2026-09-08 |
| Source | 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-08) |

**Description**
Jura Brázdil confirmed he has some spare capacity for AI-platform work, and expects the effort to help rather than purely cost him — since he'll be self-migrating MaxBuddy and Max Chatbot into the platform anyway once the new AKS lands.

**Rationale**
Resolves the capacity/cost-impact risk flagged earlier the same day (2026-09-08-ai-platform-strategy-history-with-jan-sovka), where Jindřich worried platform work might require moving Jura from ~0.25 FTE to full FTE with a billed-hours impact to explain to Dudaško. Jura's own answer meaningfully de-risks this, though the exact allocation/FTE question wasn't formally re-quantified.

**Impact**
- **Delivery timeline**: Platform work can proceed without an immediate resourcing blocker, though "spare capacity" is not a hard commitment — worth revisiting if the 3-phase plan (ASM-039) slips.

---

### ASM-041

| Field | Value |
|-------|-------|
| ID | ASM-041 |
| Created | 2026-09-08 |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka |
| By | Marek Pillár |
| Status | Decided (2026-09-08) |

**Description**
The AI platform is treated as a formal project with Tomáš Dudaško (STK-010) as owner/sponsor, run via a standard prioritization/Discovery session — rather than BigHub reactively answering his requirements Excel.

**Rationale**
Marek's proposal, agreed by Jindřich in both 2026-09-08 sessions — puts the engagement on the same footing as other Dr. Max product streams rather than an ad-hoc IT request.

**Impact**
- **Process**: A Discovery session with Dudaško should be scheduled once the mockup (ASM-039) is ready to show him.

---

### ASM-040

| Field | Value |
|-------|-------|
| ID | ASM-040 |
| Created | 2026-09-08 |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka |
| By | Jindřich Tůma (STK-003) / Marek Pillár |
| Status | Decided (2026-09-08) |

**Description**
Rather than answering Tomáš Dudaško's large requirements Excel line-by-line, Jindřich and Marek will distill it into a small, realistic ticket set (Jindřich estimated ~3-5 tickets as a starting slice), validate feasibility/timing with Jura Brázdil, then bring a shaped proposal back to Dudaško.

**Rationale**
Both Jan Sovka and Marek independently assessed the Excel as ~70% governance/compliance-framed (written from an IT-leadership perspective) and not addressing which actual use cases should run on the platform — considered the critical missing piece for scoping a real platform.

**Impact**
- **Scope control**: Prevents BigHub from committing to a large, compliance-driven build without validated use-case need.

---

### ASM-039

| Field | Value |
|-------|-------|
| ID | ASM-039 |
| Created | 2026-09-08 |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-08) |

**Description**
Near-term AI-platform delivery is scoped as three phases: (1) UX rework into one consolidated landing page, (2) migrate existing Dr. Max BigHub projects onto the platform on both test and production, (3) build Tomáš Dudaško's backlog (from his requirements Excel) into an admin/reporting layer.

**Rationale**
Agreed as the pragmatic, achievable near-term path — favoring a simple first pass that can visibly impress Dudaško at a presentation, over an elaborate upfront build. Marek is building the phase-1 mockup in Claude Design, targeting ready-by-lunch 2026-09-09.

**Impact**
- **Delivery timeline**: Phase 1 (mockup) due 2026-09-09; phases 2-3 timing not yet estimated, pending Jura Brázdil's feasibility validation and the new AKS environment landing.

---

### ASM-038

| Field | Value |
|-------|-------|
| ID | ASM-038 |
| Created | 2026-09-08 |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |
| By | Jan Sovka (STK-002) / Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-08) |

**Description**
BigHub's platform strategy going forward is fully custom-per-client. The earlier vision of one shared, white-labeled AI platform sold as a common B2B product across clients is retired — killed internally ~4 months ago (~2026-05).

**Rationale**
The shared-product vision never got internal traction or resourcing; an internal management evaluation ~2026-05 concluded to build custom per client instead, optionally inspired by shared code but with no shared roadmap.

**Impact**
- **AI-platform scoping**: Confirms the "AI platforma" initiative (see `project-knowledge`) is a Dr. Max-specific custom build, not a multi-client product — directly informs ASM-039's phased plan and ASM-041's ownership framing.

---

### ASM-037

| Field | Value |
|-------|-------|
| ID | ASM-037 |
| Created | 2026-09-08 |
| Source | PM input, 2026-09-08 |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-08) |

**Description**
Reklamace has no DNS ingress enabled yet — currently testing via port forwarding only. Goal is to get this finished as soon as possible. As a result, neither Reklamace nor Fakturace doprav has a clickable test/demo URL right now.

**Rationale**
Straightforward infra gap on Reklamace specifically; Filip will notify Marek once ingress is live and a URL exists.

**Impact**
- **Roadmap communication**: Both logistics app entries on `product-roadmap-portfolio-full.xlsx`/the roadmap HTML stay marked "no URL yet" until Filip confirms readiness — do not fabricate a placeholder link.

---

### ASM-036

| Field | Value |
|-------|-------|
| ID | ASM-036 |
| Created | 2026-09-08 |
| Source | PM input, 2026-09-08 |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-08) |

**Description**
Fakturace doprav is not yet deployed to any environment. Targeting end of this week or start of next week (2026-09-08 week / 2026-09-15 week).

**Rationale**
Matches the broader picture from the 2026-09-07 portfolio review — Fakturace doprav was already flagged as early-stage ("chybí toho jako milion").

**Impact**
- **Timeline**: No demo or test URL possible until deployment lands — informs the "Coordinate with Filip on a live demo" action item already on today's daily.

---

### ASM-035

| Field | Value |
|-------|-------|
| ID | ASM-035 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Filip Černý (STK-006) |
| Status | Open (2026-09-07) |

**Description**
TEO's OCR-of-technical-department-protocols problem (mixed printed/handwritten/checkbox documents) closely resembles Fakturace doprav's document-extraction problem. Filip Černý and Jura Brázdil agreed to hold a short knowledge-sharing session comparing what's worked and what hasn't.

**Rationale**
Surfaced live in the meeting when Filip heard Jura describe TEO's extraction challenges and recognized the same pattern from his own Fakturace doprav work.

**Impact**
- **Delivery efficiency**: Comparing notes could shortcut both projects' handwritten-text extraction approaches rather than solving the same problem twice independently.

---

### ASM-034

| Field | Value |
|-------|-------|
| ID | ASM-034 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Jura Brázdil (STK-026) |
| Status | Decided (2026-09-07) |

**Description**
The TEO OCR project is deliberately piloted on just 2 suppliers/document formats first, for more uniform inputs, before considering expansion to more.

**Rationale**
Still a local feasibility prototype on Jura's machine — narrowing the input variety first makes it tractable to get a working extraction pipeline before tackling the full diversity of documents Dr. Max's technical department handles.

**Impact**
- **Scope**: Full-supplier coverage is explicitly out of the current pilot; expansion timing is undetermined and depends on pilot results.

---

### ASM-033

| Field | Value |
|-------|-------|
| ID | ASM-033 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Filip Černý (STK-006) |
| Status | Open (risk, 2026-09-07) |

**Description**
Listing's external-source data enrichment (scraping sites like Notino to fill in missing product data) is built and mostly working, but paused before broader test rollout over legal uncertainty around scraping third-party sites.

**Rationale**
Filip flagged real doubt about whether scraping sites like Notino for enrichment is legally sound; the team doesn't want to roll this out broadly until that's resolved, possibly requiring an official API or a middleman service instead.

**Impact**
- **Legal/compliance**: Needs a legal read before wider rollout — could require re-architecting the enrichment source entirely.
- **Delivery timeline**: This portion of Listing stays gated regardless of technical readiness.

---

### ASM-032

| Field | Value |
|-------|-------|
| ID | ASM-032 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Petr Neuman (STK-023, relayed via Filip Černý) |
| Status | Decided (tentative, 2026-09-07) |

**Description**
Listing's multi-category rollout will start with a deliberately small, non-pharma category set (foods, supplements, sporting goods) rather than jumping straight to a large or complex category set.

**Rationale**
Petr Neuman's suggestion: early categories involving medication carry far more parameter complexity, which could skew or destabilize early AI output. Starting with simpler product types builds confidence in the approach first.

**Impact**
- **Scope/sequencing**: Sets the de facto order for category rollout once multi-category support is built — non-pharma first.
- **Risk**: Reduces risk of early AI-quality problems being blamed on the approach rather than category complexity.

---

### ASM-031

| Field | Value |
|-------|-------|
| ID | ASM-031 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Filip Černý (STK-006) |
| Status | Decided (2026-09-07) |

**Description**
Listing's category/structure recommendation feature is confirmed out of agreed scope — it depends on Dr. Max's own messy, unspecific category system, which isn't BigHub's to fix. Any future ask here is treated as a feature/change request, not a tracked gap.

**Rationale**
Filip assessed this was likely never actually agreed as in-scope in the first place; building around Dr. Max's undefined category system isn't a reasonable ask of BigHub.

**Impact**
- **Scope clarity**: Removes an item that was ambiguously tracked as "missing" from the roadmap — it isn't missing, it was never in scope.

---

### ASM-030

| Field | Value |
|-------|-------|
| ID | ASM-030 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Juraj Kmec (STK-009) |
| Status | Open (2026-09-07) |

**Description**
Řízení poptávky's campaign recommendation model and automated campaign generation were discussed as possibly Full Version, but no firm phase call was made. Both stay Nice to Have/Backlog until a dedicated scoping conversation happens.

**Rationale**
Juraj was explicit these are genuinely hard analytics problems in their own right — "automated campaign generation" as the client described it (fully autonomous campaign creation) isn't realistic as scoped; more likely an optimizer/recommender than true automation.

**Impact**
- **Estimation**: Can't be estimated meaningfully until scoped properly — premature to promise a phase or timeline.
- **Expectations**: Client's mental model ("AI just builds the whole campaign") likely needs recalibrating once scoping happens.

---

### ASM-029

| Field | Value |
|-------|-------|
| ID | ASM-029 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Jura Brázdil (STK-026) |
| Status | Open (risk, 2026-09-07) |

**Description**
Max Chatbot and Maxie's production integration currently runs on Dr. Max's public website API, scraped rather than officially provided. Jura recommends switching to an official integration before a full public launch.

**Rationale**
Jura: "já jsem prostě tak trochu na černo napíchnutý na API, kde vlastně nikdo neví o tom, že to používáme" [translated from Czech: "I'm basically unofficially tapped into an API that nobody even knows we're using"] — no guarantee it won't silently drift or break, and nobody at Dr. Max is aware it's relied upon.

**Impact**
- **Risk**: Production dependency on an integration Dr. Max doesn't know exists and could change without notice.
- **Delivery**: Should be resolved before scaling beyond the current pilot/test footprint — tracked as a new backlog item ("Integrace priamo na 'valid' dáta") on the Max Chatbot roadmap sheet.

---

### ASM-028

| Field | Value |
|-------|-------|
| ID | ASM-028 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Jura Brázdil (STK-026) |
| Status | Open (2026-09-07) |

**Description**
MaxBuddy's dosage-calculation features (verification, traffic-light display, textual justification, etc.) stay formally blocked on the roadmap pending Dr. Max's own decision on whether to pursue medical-device certification.

**Rationale**
Confirms and extends the existing regulatory finding in `project-knowledge.md` (MaxBuddy entry) — Jura additionally flagged that if/when Dr. Max does pursue certification, BigHub will likely also need to prepare the codebase for an audit (logging, auditability), not just re-enable the features.

**Impact**
- **Scope**: These rows stay Full Version/Blocked on the roadmap indefinitely until Dr. Max moves.
- **Future work**: Certification, if pursued, would trigger a codebase-audit-readiness workstream, not just a feature re-enable.

---

### ASM-027

| Field | Value |
|-------|-------|
| ID | ASM-027 |
| Created | 2026-09-07 |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |
| By | Jura Brázdil (STK-026) |
| Status | Open (2026-09-07) |

**Description**
MaxBuddy's full rollout to all ~600 Dr. Max pharmacies is blocked on the new AKS environment. Jura's pessimistic estimate is ~1 month of work after Vláďa Tvarůžek (STK-016) grants access, likely faster.

**Rationale**
Canary rollout plan (20 pilot pharmacies first, already live and matching confirmed MVP scope) is ready to scale as soon as infra access unblocks; the remaining work is environment setup, not feature development.

**Impact**
- **Timeline**: Full-rollout timeline is entirely gated on AKS access, outside BigHub's control.
- **Planning**: Safe to plan the ~1-month rollout work starting whenever AKS access lands, not before.

---

### ASM-026

| Field | Value |
|-------|-------|
| ID | ASM-026 |
| Created | 2026-09-04 |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |
| By | Marek Pillár, Jura Brázdil |
| Status | Decided (2026-09-04) |

**Description**
Marek's scope is Dr. Max exclusively, at least for the first month on the account — not the broader, cross-client AI platform (which also serves Brněnská komunikace, Kooperativa, and Unica).

**Rationale**
Marek's own stated mandate; Jura's practical read is that Dr. Max onboarding alone is already more than enough for the near term, independent of who formally owns the cross-client platform.

**Impact**
- **Scope**: Whether Honza Sovka retains product ownership of the platform across all clients is a separate, still-open question — see the meeting's Open Questions.

---

### ASM-025

| Field | Value |
|-------|-------|
| ID | ASM-025 |
| Created | 2026-09-04 |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |
| By | Jura Brázdil |
| Status | Open (tentative direction, not a finalized company decision) |

**Description**
The shared AI platform's frontend defaults to one standardized template ("muster") reused across all clients; per-client customization only happens if a client explicitly requests it (and is willing to have it built as a "wipe" on top of the standard).

**Rationale**
Keeps the platform maintainable as genuinely reusable "Lego blocks" (separating visual from function) rather than fragmenting into bespoke per-client builds. Jindřich explicitly noted this is really a company-strategy question, not something to settle in a working stand-up.

**Impact**
- **Product**: Affects how Lexie's eventual redesign gets scoped — likely inherits the shared template rather than a Dr. Max-specific visual identity.

---

### ASM-024

| Field | Value |
|-------|-------|
| ID | ASM-024 |
| Created | 2026-09-04 |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |
| By | Jindřich Tůma |
| Status | Decided (2026-09-04) |

**Description**
Lexie's redesign/UI-polish work stays deprioritized behind the 3 blocking technical fixes. A rough, no-engineering-time visual (e.g. AI-generated image, not a real mockup) is an acceptable placeholder to manage the CC team's expectations in the meantime.

**Rationale**
The CC team's redesign comment was minor/in-passing (liked the Max chatbot's look, casually wished Lexie looked similar) — not a hard requirement. Technical validation (thumbs, tickets) remains the actual priority.

**Impact**
- **Delivery**: Protects engineering time from being pulled into premature design work.

---

### ASM-023

| Field | Value |
|-------|-------|
| ID | ASM-023 |
| Created | 2026-09-04 |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |
| By | Jindřich Tůma |
| Status | Open (stated intent, not yet confirmed feasible) |

**Description**
X-Manager becomes the single tracking tool for all Dr. Max project tickets going forward, not just Lexie/chatbot.

**Rationale**
Jindřich wants one central place for everything BigHub sends to test/production for Dr. Max, rather than tracking scattered across email/Teams. Not yet confirmed the tool actually supports the priority/category structure needed — its label/category UI proved confusing during this session.

**Impact**
- **Process**: Depends on resolving X-Manager's own UI limitations (custom labels/priority categories didn't behave as expected when tested live).

---

### ASM-022

| Field | Value |
|-------|-------|
| ID | ASM-022 |
| Created | 2026-09-03 |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |
| By | Jindřich Tůma, Jura Brázdil, Dr. Max CC team |
| Status | Decided (2026-09-03) |

**Description**
Maxie (the voicebot) launches supporting exactly one topic — order status, via a fixed IVR branch ("press 1") — and expands to additional topics only as Dr. Max updates their own IVR tree and phrasing to accommodate them.

**Rationale**
Dr. Max flagged that giving Maxie multiple simultaneous topics would require reworking their existing IVR structure — non-trivial on their side. BigHub confirmed it can flexibly restrict or expand which topics Maxie is allowed to answer, so scope can grow incrementally rather than needing to be right on day one.

**Impact**
- **Scope**: Keeps the voicebot launch simple and lets Dr. Max's IVR rework happen at their own pace.

---

### ASM-021

| Field | Value |
|-------|-------|
| ID | ASM-021 |
| Created | 2026-09-03 |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |
| By | Jindřich Tůma, Dr. Max CC team |
| Status | Decided (2026-09-03) |

**Description**
All Lexie (Lucie) testing and design work is paused until 3 specific bugs are fixed: the feedback button breaking on long/large responses, the autocomplete/suggestion popup ("našeptávač") needing full removal, and configurable fixed/canned status messages (e.g. for outages) needing to exist outside the prompt. The team refocuses fully on the Max chatbot in the meantime.

**Rationale**
The feedback-button bug in particular is confirmed reproducible and blocks meaningful continued testing; the CC team explicitly stated they won't resume testing until these are addressed.

**Impact**
- **Delivery**: Jindřich committed to fixing all 3 by Tuesday/Wednesday, after which testing resumes and focus alternates back to Lexie.

---

### ASM-020

| Field | Value |
|-------|-------|
| ID | ASM-020 |
| Created | 2026-09-03 |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |
| By | Dr. Max CC team, Jura Brázdil |
| Status | Decided (2026-09-03) |

**Description**
When a user asks the Max chatbot something like correct medication dosing, the bot never answers directly — it redirects to the official SPC package leaflet, displayed (and optionally auto-scrolled to the relevant section) via the same SPC API already built for MaxBuddy.

**Rationale**
Same legal/regulatory guardrail that reshaped MaxBuddy — the CC team explicitly drew the parallel ("you know from MaxBuddy that AI can't provide [medical] information at all"). Displaying official leaflet content is safe; generating medical advice via an LLM is not.

**Impact**
- **Compliance**: Reuses an existing, already-cleared pattern rather than opening new regulatory risk. See also the MaxBuddy dosage-checking history in [[project-knowledge]].

---

### ASM-019

| Field | Value |
|-------|-------|
| ID | ASM-019 |
| Created | 2026-09-03 |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |
| By | Jindřich Tůma, Dr. Max CC team |
| Status | Decided (2026-09-03) |

**Description**
For the current phase, the Max chatbot's production-readiness bar is functional correctness against the agreed scope — not full polish. Non-blocking refinement requests get queued for a later release rather than delaying production.

**Rationale**
Dr. Max has an unspecified upcoming "competition" (soutěž) creating real urgency to go live soon; both sides explicitly agreed not to let polish requests become de facto blockers.

**Impact**
- **Delivery**: Protects the production timeline; Dr. Max may still ad hoc reprioritize one scenario ahead of others if the competition timing requires it.

---

### ASM-018

| Field | Value |
|-------|-------|
| ID | ASM-018 |
| Created | 2026-09-03 |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |
| By | Jindřich Tůma |
| Status | Decided (2026-09-03) |

**Description**
All X-Manager feature/change requests for Max, Lexie, and Maxie route through one point of contact on Dr. Max's side — Simona Mertová (STK-017) — rather than arriving individually from every tester.

**Rationale**
Jindřich's explicit ask, based on past experience: when requests arrive from many individual users, the aggregate volume ends up not reflecting what the actual business owner wants, creating noise and duplicate/conflicting asks.

**Impact**
- **Process**: Mertová now owes Marek/Jindřich business-case metrics per initiative in addition to gatekeeping requests — see her action item.

---

### ASM-017

| Field | Value |
|-------|-------|
| ID | ASM-017 |
| Created | 2026-09-03 |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |
| By | Kateřina Karlecová (STK-037), Jura Brázdil |
| Status | Decided (2026-09-03) |

**Description**
The Max chatbot's in-chat feedback mechanism is a lightweight star/emoji rating only — no free-text field — presented unobtrusively at the end of a conversation flow, using a green-to-red color order.

**Rationale**
Grounded in Dr. Max's own prior chatbot UX data: free-text feedback forms see low completion, and a green→red click order tested better than the reverse in their existing deployments. Jura will also design against re-prompting the same user repeatedly.

**Impact**
- **Product**: Sets the design direction before any feedback UI is built — avoids building a free-text form Dr. Max already knows underperforms.

---

### ASM-016

| Field | Value |
|-------|-------|
| ID | ASM-016 |
| Created | 2026-09-03 |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |
| By | Juraj Kmec (STK-009) |
| Status | Decided (2026-09-03) |

**Description**
The order-prediction revenue forecast model stays trained purely on recognized/invoiced revenue, rather than blending in order-backlog (created-but-not-yet-invoiced) signals.

**Rationale**
Juraj tested a blended approach early on; the revenue-only model empirically performed better. Marek Šimoník asked directly whether the model accounts for a current warehouse backlog — confirmed it doesn't directly, but the model self-corrects within a few days via nightly recalibration.

**Impact**
- **Product**: Open follow-up — Juraj to verify exactly how the model responds to the current live backlog spike (Brno under-prediction) before treating this as fully settled.

---

### ASM-015

| Field | Value |
|-------|-------|
| ID | ASM-015 |
| Created | 2026-09-03 |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |
| By | Jan Sovka (STK-002) |
| Status | Decided (2026-09-03) |

**Description**
For the order-prediction dashboard's current phase, Marek Šimoník and Petr Ondráček are the primary users. A separate logistics contact ("Honza" — identity unconfirmed, STK-036) raised different needs (month-ahead view rather than day/14-day) and is deliberately placed into a later phase (2/3/4).

**Rationale**
Keeps the current rollout focused on the users/use case it was actually built for, rather than expanding scope mid-rollout to cover a materially different need (monthly logistics planning vs. daily/2-week e-commerce forecasting).

**Impact**
- **Scope**: Prevents premature scope creep on a dashboard still in its first live-feedback cycle.

---

### ASM-014

| Field | Value |
|-------|-------|
| ID | ASM-014 |
| Created | 2026-09-03 |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |
| By | Jan Sovka (STK-002) |
| Status | Decided (2026-09-03) |

**Description**
For the order-prediction dashboard's acceptance process, the review order is: **(1)** verify the underlying numbers/filters are correct against Dr. Max's own source data, **(2)** request display/UX changes, **(3)** only then assess and tune model accuracy.

**Rationale**
Explicit guardrail against the group getting stuck relitigating forecast precision before the more basic, client-verifiable layers (data correctness, display needs) are settled. Today's model accuracy is considered good enough to build on.

**Impact**
- **Process**: Gives both sides a shared framework for sequencing feedback during the dashboard's testing phase.

---

### ASM-013

| Field | Value |
|-------|-------|
| ID | ASM-013 |
| Created | 2026-09-03 |
| Source | 2026-09-03-viapharma-logistics-status-reklamace-demo |
| By | BigHub/ViaPharma logistics team (call led by Jan Sovka, STK-002) |
| Status | Decided (2026-09-03) |

**Description**
Whenever a Swagger endpoint changes, the change is proactively posted (link + summary of what changed) to the shared group — rather than relying on the other side to notice or ask.

**Rationale**
Followed a case where an older freight-invoicing Swagger update's status was unclear to both sides weeks later, with nobody confident whether it had been incorporated.

**Impact**
- **Process**: Adds a lightweight coordination habit for the reklamace/freight-invoicing workstreams. Jakub Turner (STK-007) committed to posting the current freight-invoicing Swagger by end of week 2026-09-04/05 as the first application of this.

---

### ASM-012

| Field | Value |
|-------|-------|
| ID | ASM-012 |
| Created | 2026-09-03 |
| Source | 2026-09-03-viapharma-logistics-status-reklamace-demo |
| By | Jakub Turner (STK-007), Jan Kopecký (STK-032) |
| Status | Decided (2026-09-03) |

**Description**
For the reklamace mobile app's testing phase, authentication uses hardcoded per-user logins issued directly by Jakub Turner (starting with Tereza Foltová, then Jana). Entra ID/OAuth integration proceeds in parallel but does not block the start of testing.

**Rationale**
Jan Kopecký flagged that wiring up Entra ID may hit permission/infra friction on Dr. Max's side that shouldn't hold up ViaPharma's ability to start testing now. Petr Sláma's interest in per-user logins was clarified as being about Axapta-log traceability (who did what), not access security — so a simple hardcoded login satisfies the actual need for the test phase.

**Impact**
- **Delivery**: Unblocks ViaPharma testing (target: Jana testing immediately on her return from vacation) without waiting on the harder Entra ID integration.
- **Update (2026-09-16, direct codebase read of `cz-ai-logistics/apps/claims_api`)**: This interim state is superseded. Production auth is now full Entra ID (Azure AD via MSAL), required on every business endpoint; the only non-Entra path is a single shared dev-bypass account gated by an env var for local development, not per-user hardcoded logins. No per-user hardcoded-login mechanism remains in the code.

---

### ASM-011

| Field | Value |
|-------|-------|
| ID | ASM-011 |
| Created | 2026-09-02 |
| Source | 2026-09-02-logistics-listing-team-sync |
| By | Marek Pillár (STK-001), Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-02) |

**Description**
The Listing project will not receive further development until a formal client-side Discovery is run with the business stakeholder (implicitly Petr Neuman, STK-023) to produce and validate a proper specification — treating this as the first end-to-end project done "the right way," as a template for other under-specified streams.

**Rationale**
Filip Černý assessed that Listing is blocked purely by Dr. Max's undefined category/parameter system, not by code — continuing to build now would "burn money for nothing." Marek proposed Discovery as the path forward given Listing is otherwise a reasonably scoped, self-contained stream. Jindřich agreed it's a priority and the main blocker to further meaningful work, expects several meetings (not one or two) to resolve it, and wants to attend for context without running the sessions himself. Explicitly not framed as a billing play — the goal is finding a productive path forward, not extracting more paid work from the client.

**Impact**
- **Delivery process**: No further Listing development work until Discovery produces a validated spec; Marek owns leading the Discovery.
- **Team structure**: Establishes Discovery-first as the intended pattern for other brownfield/under-specified streams going forward.

---

### ASM-010

| Field | Value |
|-------|-------|
| ID | ASM-010 |
| Created | 2026-09-02 |
| Source | 2026-09-02-logistics-listing-team-sync |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-02) |

**Description**
The reklamace (complaints) email-automation workflow will always generate a pre-filled draft for human review and editing — it will never send an email automatically.

**Rationale**
Lukáš Starenko raised the question directly during the reklamace document-generation walkthrough; Jindřich confirmed drafts only, reviewed/edited by a human before sending, as the intended high-level flow (extract the applicable supplier procedure → pre-fill draft → human reviews/edits → sends). The exact mechanism (e.g. Microsoft Graph API draft-creation endpoint) is not yet fully specified.

**Impact**
- **Delivery process**: Sets a review gate into the reklamace automation build — no path to a fully unattended send exists in the current design.
- **Update (2026-09-16, direct codebase read of `cz-ai-logistics/apps/claims_api`)**: The email-drafting feature this rule governs does not exist in the code yet at all — no email generation of any kind was found. The human-review-before-send principle remains the right design constraint for whenever this gets built, but it should not be described as an active safeguard today since there is nothing yet to safeguard.

---

### ASM-009

| Field | Value |
|-------|-------|
| ID | ASM-009 |
| Created | 2026-09-02 |
| Source | 2026-09-02-roadmap-tracking-and-listing-onboarding-sync |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-02) |

**Description**
Spec documents (Spec 1 → Spec 2, per the 2026-09-01 structure) must include an explicit hypothesis + acceptance-criteria section — problem description, solution description, and a lightweight acceptance framing — that the business owner signs off on before build starts.

**Rationale**
Without a written, business-signed description of exactly what will be built, requirement creep is inevitable and disputes have no clear reference point ("the button should have been pink"). This protects delivery timelines and gives BigHub a clean basis to say "delivered as agreed" before moving into a backlog of further requests.

**Impact**
- **Delivery process**: Adds a sign-off gate before build on every spec going forward; ties into the existing Spec 1/Spec 2 structure agreed 2026-09-01.

---

### ASM-008

| Field | Value |
|-------|-------|
| ID | ASM-008 |
| Created | 2026-09-02 |
| Source | 2026-09-02-roadmap-tracking-and-listing-onboarding-sync |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-02) |

**Description**
The business-facing roadmap sheet drops the Task/TaskGant/Gantt columns entirely — those move to a dev-facing system (Easy Project or equivalent) using a VBS (work-breakdown-structure) framework. The business-facing sheet keeps only Ideas (full initiative backlog) and Active (currently worked projects) tabs, simplified to: project name, business owner, description, cost estimate, status.

**Rationale**
Business only needs to know what phase a project is in, not internal delivery/ticket-level detail. The previous Stage and Priority-score fields were judged not business-meaningful in their current form and were dropped too. Marek owns the Ideas/Active content going forward as a backlog, surfaced when there's a business conversation opportunity with Tomáš Dudaško rather than actively maintained as a constantly-live artifact.

**Impact**
- **Reporting**: Cleaner, simpler artifact for Dudaško-facing conversations; detailed delivery tracking still needs a home (pending Jindřich's check on whether Easy Project already covers it).

---

### ASM-007

| Field | Value |
|-------|-------|
| ID | ASM-007 |
| Created | 2026-09-02 |
| Source | 2026-09-02-order-prediction-dashboard-walkthrough, 2026-09-03-viapharma-logistics-status-reklamace-demo |
| By | Juraj Kmec (STK-009); amended by Marek Pillár (STK-001) |
| Status | Decided (2026-09-08); amended 2026-09-03, 2026-09-08 |

**Description**
Two different sources named two different people as owning reklamace (complaints): Juraj Kmec (2026-09-02) believed **Jura Brázdil** (STK-026) owns both reklamace and freight invoicing under one shared "logistics" umbrella. Filip Černý (2026-09-01, listing intro) had named **"Kuba Turner"** (plus "Flurimo") as the one who mostly built reklamace.

**Rationale**
Resolved by Marek (2026-09-02): **Turner works on MaxBuddy**, not reklamace — Filip's original attribution was incorrect. **Jura Brázdil is confirmed** as owning both reklamace and freight invoicing (fakturace dopravy).

**Amendment (2026-09-03)**: The 2026-09-03 ViaPharma logistics status call showed Jakub Turner (STK-007) deeply engaged in reklamace-app backend work — OAuth/Entra ID auth design, hardcoded test-login issuance, Axapta write integration. PM confirmed both attributions are simultaneously true: Turner is not limited to MaxBuddy after all — he's also active on the reklamace backend, alongside Brázdil's ownership. The original "MaxBuddy-only" resolution was incomplete rather than wrong.

**Amendment (2026-09-08)**: In the 2026-09-07 portfolio review, Filip Černý (STK-006) described Reklamace dev work as currently split three ways — himself, Jakub Turner (STK-007), and Lukáš Starenko (STK-028) — and ran point answering for the whole stream in that meeting. On 2026-09-08, Marek designated **Filip Černý as the single dev owner** for Reklamace going forward, resolving the multi-attribution ambiguity this assumption has tracked since 2026-09-02.

**Impact**
- **Data quality**: STK-026 (Jura Brázdil) updated to confirmed (2026-09-02). STK-007 confirmed as the same person as "Kuba Turner" — surname updated to Turner, role updated to include MaxBuddy and (as of 2026-09-03) reklamace-app backend/auth work. STK-006 (Filip Černý) now marked as the designated Reklamace dev owner (2026-09-08). See also LL-005 (single-source ownership attributions on this account are recurringly incomplete, not just wrong).
- **Accountability**: Status updates and blockers on Reklamace should now route through Filip Černý as the single point of contact, even though Turner and Starenko remain actively contributing pieces of the build.

---

### ASM-006

| Field | Value |
|-------|-------|
| ID | ASM-006 |
| Created | 2026-09-02 |
| Source | roadmap sheet (PM-provided image, 2026-09-02); updated 2026-09-15-business-quantification-reklamace-fakturace-doprav |
| By | Marek Pillár (STK-001) |
| Status | Open (2.5/4 resolved, 2026-09-15) |

**Description**
A BigHub "Initiative → Owner/Customer" roadmap sheet was cross-checked against existing meeting-derived stakeholder records. Two entries matched cleanly (MaxBuddy → Tomáš Dudaško; E-Shop order forecast → Marek Šimoník). Two entries were net-new (Product listing → Petr Neuman; TD revisions → Tomáš Burda). Four points conflicted with existing records and were recorded on both sides rather than resolved:
1. **Invoicing solution / "fakturace od dodavatelů" → Rudolf Zurek** (STK-024) vs. Fakturace doprav → Jan Žižka (STK-015) / Petr Spilka (STK-014) reviewing — possibly the same initiative under different names, possibly distinct. **Leaning resolved (2026-09-15)**: in the Business Quantification call, Tereza Foltýnová (ViaPharma) discussed the roadmap's "fakturace od dodavatelů" line as the freight/transport initiative ("je to ta doprava"), with Jan Žižka named as its owner — matching Fakturace doprav, not a separate supplier-invoicing stream. Not yet a formal, explicit confirmation (Rudolf Žůrek's own framing wasn't directly addressed), so kept as "leaning resolved" rather than closed. **Further corroboration (2026-09-22)**: Marek reiterated to Jindřich that this is the same initiative Tereza Foltýnová had insisted on unifying under one name ("fakturace doprava"), owned by Jan Žižka — consistent with the 2026-09-15 read, but still Marek's own restatement rather than a fresh independent client confirmation, so kept "leaning resolved" rather than closed.
2. **Receiving compliants in stock → Rudolf Zurek** (STK-024) vs. Reklamace → Marie Hulešová (STK-020) — possibly the same initiative, possibly distinct. **Still open** — the 2026-09-15 call reinforced Petr Spilka (not Hulešová) as Reklamace's owner from the ViaPharma side, but didn't address Žůrek's framing directly — needs its own follow-up.
3. ~~Maxie/Max → Simona Mertova (STK-017) — surname spelling conflict.~~ **Resolved 2026-09-02**: "Mertová" confirmed correct; "Martová" was a transcription error.
4. ~~Lexie → Tomáš Dudaško (STK-010) vs. Martová/Mertová owning Max/Maxie/Lexie together.~~ **Resolved 2026-09-02**: not a real conflict — Dudaško holds IT/budget-side ownership, Mertová holds operational/product ownership; both own it.

**Rationale**
PM explicitly asked to record both sides of each conflict rather than pick one now — "record both and let me decide later." Consistent with the same approach taken for ASM-005. On 2026-09-02, Marek resolved the two naming/ownership-framing conflicts (surname, Lexie co-ownership) but was not yet sure on the two possible-duplicate-initiative conflicts (invoicing solution, reklamace/complaints). On 2026-09-15, the invoicing-solution/Fakturace-doprav conflict moved from fully open to leaning resolved based on Tereza Foltýnová's own framing during live business-quantification — a client-side data point, not just an internal guess.

**Impact**
- **Data quality**: STK-017 and STK-010 updated to reflect resolved co-ownership and correct spelling. STK-014, STK-015, STK-020, STK-024 still carry a note pointing to this assumption. Point 1 (invoicing solution/Fakturace doprav) can likely be treated as resolved with one more explicit confirmation from Žižka or Žůrek; point 2 (Reklamace/complaints) remains genuinely open.

---

### ASM-005

| Field | Value |
|-------|-------|
| ID | ASM-005 |
| Created | 2026-09-01 |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync |
| By | Marek Pillár (STK-001) |
| Status | Decided (2026-09-02) |

**Description**
A PM-provided "Who's Who" reference card was used to correct several mis-transcribed names from the 2026-09-01 status sync audio/PDF (e.g. Petr Spilka, not "Petr Sláma"; Jan Žižka, not "Honza Hříška"; Marek Šimoník, not "Šumoník") and to add several stakeholders and role/title details not present in the transcript itself (Marie Hulešová, Jan Maroušek, Sony Vu Hong, Juraj Kmec's surname, and refined titles for Jan Sovka, Jindřich, Alana, and Jan Kabát). These have been written into project-stakeholders and project-knowledge as best-available information.

**Rationale**
The reference card looks authoritative but its details haven't been independently reconciled against Dr. Max's actual org chart or the live account by Marek. Rather than block routing of the whole meeting, the corrections/additions were applied now and flagged here for a later confirmation pass.

Marek confirmed the reference card details on 2026-09-02 — no corrections needed.

**Impact**
- **Data quality**: Stakeholder entries sourced from the reference card (STK-014 through STK-021, STK-022, and the STK-002/003/004/005/009 refinements) should be treated as provisional until Marek reconciles them.

---

### ASM-004

| Field | Value |
|-------|-------|
| ID | ASM-004 |
| Created | 2026-09-01 |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync |
| By | Jindřich Tůma (STK-003) |
| Status | Decided (2026-09-01) |

**Description**
Any MaxBuddy change that touches the shared data model (e.g. adding a column) must be reviewed by Dr. Max's analytics team before shipping.

**Rationale**
A meeting with pan Machát (Dr. Max analytics) surfaced that such changes risk breaking Dr. Max's company-wide analytics. Agreed process: analytics gets looped in once a batch of backlog items is prioritized for the next release, to review/approve affected data fields before deployment.

**Impact**
- **Delivery process**: Adds an analytics sign-off step to the MaxBuddy release cycle whenever a data-model change is involved.

---

### ASM-003

| Field | Value |
|-------|-------|
| ID | ASM-003 |
| Created | 2026-09-01 |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| By | Jan Sovka (STK-002) |
| Status | Decided (2026-08-25) |

**Description**
BigHub's internal client-knowledge tool concept ("Alfred") remains a BigHub-owned internal asset — it is never handed to clients, even as an account matures and expands.

**Rationale**
Alfred (methodology + eventual tooling for capturing client interactions/specs/agreements) is BigHub's own accumulated expertise and competitive advantage; giving it away would erode the value BigHub sells. This was stated explicitly when Marek asked whether "implementing Alfred at the client" was the long-term goal — Jan corrected that the goal is exporting the *methodology* to new markets, not the tool itself.

**Impact**
- **Account expansion strategy**: The "golden ticket" ambition (exporting BigHub's approach to other Dr. Max country markets) is about replicating proven process, not deploying shared internal tooling to the client.

---

### ASM-002

| Field | Value |
|-------|-------|
| ID | ASM-002 |
| Created | 2026-09-01 |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| By | Jan Sovka (STK-002) |
| Status | Decided (2026-08-25) |

**Description**
Marek's primary mandate on the Dr. Max account is delivery ownership of the 9 existing project streams — not new sales or pipeline generation. Sales/account relationship stays with Ján "Honza" Kabát.

**Rationale**
Jan Sovka framed Marek's role explicitly as the product lens driving existing work to production and expansion, distinct from the sales function. Success in month one is defined as full visibility and active ownership of the existing streams, not new business development.

**Impact**
- **Scope of work**: Marek should prioritize the 9 active streams and their expansion over prospecting new engagements at Dr. Max.

---

### ASM-001

| Field | Value |
|-------|-------|
| ID | ASM-001 |
| Created | 2026-09-01 |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |
| By | Jan Sovka (STK-002) |
| Status | Decided (2026-08-25) |

**Description**
Client-side and BigHub-side project coordination on the Dr. Max account is unified into a single role, now held by Jindřich Tůma, replacing the previous split arrangement (a weak client-side PM plus BigHub's Alana Sihelská absorbing most of the coordination burden).

**Rationale**
The prior split setup left the client-side PM role under-driven, pushing most coordination work onto BigHub. Agreed with Tomáš Dudaško (client IT lead) to consolidate into one person spanning both sides. Jindřich started 2026-08-18 (approx.), one week ahead of Marek.

**Impact**
- **Team structure**: Marek and Jindřich now jointly own the account (~70% Marek / ~30% Jindřich per Jan's framing), replacing Alana's prior coordination role.

---

## Entry Format

```markdown
---

### ASM-{NNN}

| Field | Value |
|-------|-------|
| ID | ASM-{NNN} |
| Created | {YYYY-MM-DD} |
| Source | {meeting-slug, document-slug, or "PM session"} |
| By | {Stakeholder name (STK-ID) or "Team"} |
| Status | {Open / Decided / Retired} ({YYYY-MM-DD}) |

**Description**
{What the assumption is — plain language, 1-3 sentences}

**Rationale**
{Why this assumption was made or proposed. Appended on status changes. 2-4 sentences.}

**Impact**
- **{Dimension}**: {Trade-off analysis — specific to this assumption, referencing project context}
```
