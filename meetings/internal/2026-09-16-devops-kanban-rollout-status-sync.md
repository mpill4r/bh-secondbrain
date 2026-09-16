---
last_updated: 2026-09-16
type: internal
attendees: [Jindřich Tůma, Filip Černý, Jakub Turner, Marek Pillár, Juraj Kmec]
tldv_link:
---

# Azure DevOps Kanban Rollout & Cross-Project Status Sync

**Date**: 2026-09-16
**Attendees**: Jindřich Tůma (BigHub — PM/coordination lead, STK-003), Filip Černý (BigHub — dev, Fakturace doprav/Reklamace/Listing, STK-006), Jakub Turner (BigHub — dev, MaxBuddy/reklamace backend, STK-007), Marek Pillár (BigHub — PM, STK-001), Juraj Kmec (BigHub — data scientist, order prediction, STK-009). **Alana Sihelská's actual presence is unconfirmed** — see Open Questions.
**Type**: internal
**Recording**: N/A — transcript only, no tldv link provided
**Previous session**: No directly equivalent prior "Kanban status sync" exists in the harness; thematically continues the VBS/Kanban framework first discussed 2026-09-02 (see `project-knowledge.md`, "VBS (work-breakdown-structure) framework")
**Meeting prep**: N/A

## TL;DR

Jindřich rolled out a new Azure DevOps Kanban board (Epic = project, Story = business requirement, Task = dev breakdown) as a lightweight internal-visibility layer — not a full Scrum process, and not replacing EasyProject as the system of record for time-tracking — then walked through live status on Fakturace doprav, Reklamace, order prediction, and Listing. No major blockers surfaced; the most consequential open item is whether the Reklamace mobile app will actually work over the warehouse's internal WiFi the way it works over VPN today, which is unconfirmed and infra-dependent.

**Attribution note**: this transcript's speaker diarization mislabeled most of the meeting's substantive content as "Alana Sihelská." Per PM confirmation during routing: the Fakturace doprav/Reklamace technical work is actually **Filip Černý**, the order-prediction reply is actually **Juraj Kmec**, and the Listing update is actually **Marek Pillár**. Attributions below reflect the corrected speakers.

## Key Discussion Points

### Azure DevOps Kanban rollout

Jindřich introduced the new board structure: one Epic per project (Fakturace doprav, Reklamace, order prediction, etc.), Stories underneath defining business requirements ("as a user I click X and it does ABC"), and Tasks as the dev-level breakdown. Explicitly **not** a full Scrum adoption — no fixed sprint cadence or time-boxing, no formal story-point estimation shown in this session. Actual time/billing tracking stays in Easy Project unchanged; the DevOps board exists purely for shared visibility so status meetings can reference "what task is in what state and when it'll ship." Jindřich acknowledged the current story-to-task granularity is inconsistent (some stories are broken into very small tasks) and said this will get smoothed out over time rather than fixed upfront. He also noted he's discovered an AI agent can interact with the board programmatically via Azure CLI.

### Fakturace doprav status (Filip Černý)

Application workflow: 3 items closed/done; 2 remaining items stay in "New" rather than "Active" for now, since Filip isn't picking them up yet.

**API contract / Swagger**: Filip is actively updating the Swagger spec — roughly 9 sub-tasks collapse into this one deliverable (document re-versioning approach folds into the same work). Once done, he'll first route it internally (mentioned sending to "Honza" for review) before sending it to the shared group that includes the Boomy and Axapta teams.

**Document storage**: Provisioning a dedicated storage container is trivial infra-wise (ready to go) but not done yet — Filip is currently focused on defining the local structure first (naming, identifiers, folder structure) before wiring it in. Multiple-scans/historical-versions-per-document was explicitly scoped **out** — Axapta owns document versioning; BigHub just sends new scans with a "new version" flag and doesn't maintain local history. Access-rights and read/write verification (tested with Jan Kopecký, STK-032) are both confirmed done, and this pattern carries over identically to Reklamace since both sit on the same Axapta-backed access model.

**Boomy integration**: mostly on Boomy's side; Filip's own remaining piece is finishing and sending the Swagger update. Ongoing coordination will run over email/Teams as issues come up. Jindřich raised an open question — who at BigHub will actually be assigning/coordinating work to the Boomy-side people now that Lukáš (surname unclear from context) may be on leave — Filip didn't have a firm answer and suggested checking with someone referred to as "Kupčík."

**Axapta integration**: touched lightly in a Monday conversation with Petr Sláma (STK-034), who came across as notably open to the proposed changes; Jan Kopecký is fully on board. Filip plans to route the Swagger to the shared team once ready and expects incremental feedback from there — no further live testing until that "hidden rebuild" work lands.

### Reklamace status (mixed speakers)

**Email agent (Phase 1.1)**: not yet started as its own task — dependent on a prerequisite email/Graph-API infrastructure piece being finished first (registering the mailbox app, retiring the previous app). Filip flagged this as the actual first dependency in the chain — email infra unblocks both the email agent and later automation.

**OAuth (Jakub Turner)**: needs to be implemented on BigHub's side. Jakub received OAuth server details from an external Boomy-side contact (name not retained in the transcript). Plan: implement and test, but explicitly agreed with Petr Sláma not to let this block warehouse testing — Jakub will finish/deploy only once tested at the warehouse itself, timing this week or after the weekend depending on which prerequisite (infra vs. email setup) comes back first.

**Warehouse mobile / internal-network access (raised by Filip, discussed with Jakub the day before)**: today's Reklamace app testing happens over VPN from a computer; in production, warehouse staff will use it on mobile over the warehouse's own local WiFi — and it's genuinely unclear whether that will grant the same effective access as VPN does today. Jindřich has an open to-do on this but hasn't investigated the networking side yet; Entra auth itself is believed to already be in place ("shouldn't be too bad"), but the network path from the Kubernetes-hosted app to the warehouse's local network is the real unknown. Jakub's read: Dr. Max will need to open a specific network path ("prostup") from the app to their warehouse network — a phone simply being on warehouse WiFi won't automatically reach a Kubernetes-hosted service. Two parallel next steps discussed: (1) an informal quick test — ask a warehouse-based contact (Filip floated "paní Eggermayerová," likely Jana Egrmaierová, STK-044) to click the live app link while connected to warehouse WiFi, purely as a fast sanity check; (2) a proper, official request to Dr. Max clarifying exactly what network access is needed — Jindřich prefers leading with this rather than relying on an informal test alone, so the real ask doesn't get missed or attributed to the wrong cause later.

**Onboarding/testing kickoff**: scheduled for tomorrow (2026-09-17) — Filip may be alone for parts of it; Jindřich clarified the process itself doesn't require him personally present, just needs walking through.

**Document storage question (recalled from a previous conversation)**: confirmed resolved — tested successfully with Jan Kopecký the day before, no issue found.

**CERT / email registration (Jakub Turner)**: flagged as a question to raise with infra — status of the CERT/email registration needed for the mailbox app — not yet asked as of this meeting.

### Order prediction / Řízení poptávky status (Juraj Kmec)

Jindřich is leaving this largely as-is for now, since Marek Šimoník (STK-019) is going on a full week's vacation starting next week, giving extra runway. Juraj confirmed the one meaningfully-sized remaining item is Marketplace aggregation — not blocked, just a bigger unit of work than everything else on the board. Mobile/non-VPN dashboard access is theoretically possible but depends on infra — Jindřich will look into it quickly and loop in Vladislav Tvarůžek (STK-016) or another infra contact; invited Juraj to a 4pm infra sync the same day to raise questions directly, though Juraj wasn't fully sure yet what the ask would even cover and said he'd look closer beforehand. Jindřich also flagged (to himself) a reminder to add a ticket Petr Ondráček (STK-035) had sent, which hadn't yet been added to the board. Separately, Jindřich is planning an internal review sync with Jan Sovka (STK-002) — targeting Monday 2026-09-28, ahead of the previously-scheduled 2026-09-29 Tuesday sync with Marek Šimoník — to walk through recent changes together first.

### Listing status (Marek Pillár)

Marek sent the Listing spec to Jan Sovka (STK-002) for review earlier the same day; Sovka left comments and described the spec as, in his own words, significantly broken — but per Marek's own assessment, the actual issues are mostly minor polish items, not structural problems. This is the same spec being prepared as the handoff document for Filip Černý. Marek plans to work through Sovka's comments today and tomorrow. Separately, he had a call with Petr Neuman (STK-023) the same day — an informal (not yet fully official) agreement to meet again next week and try to properly kick off the project: build out the backlog together with Neuman's nominated domain expert Michaela Vdovicynová (STK-048, referred to in this call as "Michaela Dovicinová" — same known spelling-variance pattern already flagged elsewhere in the harness) and validate what actually needs building.

Confirmed via today's call: the deliverable is a tool that produces an export, subsequently imported into Magento — because Magento itself can't keep up with fast/bulk writes at Dr. Max's current catalog scale (consistent with [[ASM-073]]'s Magento-instability reframing from earlier today). On SKUs specifically: **Dr. Max provides/owns SKU identifiers — BigHub does not generate them.** Dr. Max sometimes uses "SKU" loosely as a synonym for "product," but it's literally just the product's identifier. The overall flow: build/edit happens in the new app first, then gets imported into Magento — matching what's already reflected in the spec.

Jindřich flagged that the Listing spec, as currently scoped, should simplify its framing: rather than trying to account for every adjacent system Dr. Max mentions (Farmis, "Quant," "paní Lucy," and others), the spec's core claim is simpler — BigHub takes over exactly what already exists in Magento today, since new products are treated the same as existing ones once a baseline listing exists. He recalled attending one earlier Dr. Max meeting where even their own team wasn't sure how data would flow between Farmis and Magento — read as confirmation that this is still being actively spec'd out on the client side, not yet a settled architecture.

Jindřich asked whether Petr Neuman has actually reviewed/agreed the spec yet — not yet; Marek plans to send it the next morning after incorporating Sovka's comments, though Neuman may be unreachable until Friday. Jindřich clarified nothing is technically blocked on Listing right now — it's blocked on the spec/client engagement cycle, not on missing engineering work. Marek added that the spec's real value isn't just documentation — writing it surfaced precisely why Listing has been stuck on the same issues since the start, which was the actual motivation for producing it.

### KPI check-in (brief, cut off)

Marek asked for a short (~3-5 minute) sync on KPIs before the call ended, mentioning he needed to track down where a specific figure had come from. The call ended before this was substantively discussed.

## Decisions Made

- Azure DevOps Kanban board adopted across all projects as an internal-visibility layer (Epic=project / Story=requirement / Task=dev breakdown); explicitly not a Scrum process, no fixed sprints; Easy Project remains the system of record for time-tracking.
- Multi-scan/document-version history is explicitly out of scope for both Fakturace doprav and Reklamace — Axapta owns document versioning; BigHub only forwards new scans with a version flag.
- Reklamace OAuth work will not block warehouse testing — implementation/deployment happens after warehouse testing, by agreement with Petr Sláma.
- SKU identifiers are owned/provided by Dr. Max for Listing — BigHub does not generate them.
- Next internal Listing/roadmap-adjacent review sync targeted for Monday 2026-09-28, ahead of the 2026-09-29 order-prediction sync with Marek Šimoník.

## Action Items

- [ ] **Jindřich Tůma**: Investigate whether Reklamace's warehouse-WiFi mobile access will grant equivalent network reach to today's VPN-based testing — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Jindřich Tůma**: Send a formal request to Dr. Max clarifying the network access/provisioning needed for the Reklamace app to reach the warehouse's internal network — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Filip Černý / Jakub Turner**: Run an informal quick test — ask a warehouse-based Dr. Max contact (possibly Jana Egrmaierová) to open the live Reklamace app link while on warehouse WiFi — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Jindřich Tůma**: Determine who at BigHub will coordinate/assign work to the Boomy-side team going forward (check with "Kupčík") — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Jakub Turner**: Follow up with infra on CERT/email-registration status needed for the Reklamace mailbox app — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Jakub Turner**: Implement and test Reklamace OAuth against the Boomy-provided OAuth server, timing dependent on infra/email prerequisites — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Filip Černý**: Finish and send the updated Fakturace doprav Swagger spec — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Jindřich Tůma**: Add the ticket Petr Ondráček sent to the order-prediction board — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Jindřich Tůma**: Schedule an internal review sync with Jan Sovka around 2026-09-28, ahead of the 2026-09-29 Marek Šimoník sync — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Marek Pillár**: Incorporate Jan Sovka's spec comments and send the Listing spec to Petr Neuman (may be unavailable until Friday) — from 2026-09-16-devops-kanban-rollout-status-sync
- [ ] **Marek Pillár**: Hold a short KPI-alignment check-in (deferred at the end of this call) — from 2026-09-16-devops-kanban-rollout-status-sync

## Open Questions

- **Alana Sihelská's actual presence/role in this meeting is unconfirmed.** The transcript's diarization attributed nearly all substantive content to her, but PM confirmation during routing reassigned the Fakturace doprav/Reklamace technical work to Filip Černý, the order-prediction reply to Juraj Kmec, and the Listing update to Marek Pillár. It's unclear whether Alana was present at all (the opening off-topic banter about movies may genuinely be hers) or whether this is a broader diarization failure — possibly several attendees sharing one conference-room microphone/channel that got labeled with her name by default.
- Who specifically at BigHub will coordinate Boomy-side work assignments going forward — not resolved in this call.
- Whether "Kupčík" is a BigHub or Boomy-side contact — unclear from context.
- The external Boomy contact who gave Jakub Turner the OAuth server details is unnamed.
- Whether the KPI check-in Marek requested at the end relates to Listing's still-open KPI question ([[ASM-075]]) — not stated explicitly, inferred from adjacency.

## Sentiment & Tone

Low-key, efficient internal working sync — casual and familiar at the open (movie banter, informal Czech/Slovak mix throughout), businesslike once the status walkthrough started. No friction or disagreement surfaced on any topic; Jindřich's board rollout was received without pushback, including the acknowledgment that story/task granularity is still rough. The Reklamace network-access uncertainty was treated as a genuine open risk rather than downplayed — both Jindřich and Jakub independently flagged that an informal test alone wouldn't be enough without a proper request to Dr. Max.

## Routing Log

- **project-knowledge**: Updated "VBS (work-breakdown-structure) framework" with the Azure DevOps implementation; "AI Listing Tool" with SKU ownership/data-flow facts; Fakturace doprav document-types entry with document-versioning-out-of-scope confirmation.
- **project-stakeholders**: Enriched STK-001 (Marek Pillár), STK-003 (Jindřich Tůma), STK-006 (Filip Černý — corrected from mislabeled transcript), STK-007 (Jakub Turner), STK-009 (Juraj Kmec — corrected from mislabeled transcript).
- **project-daily**: 11 action items added to 2026-09-16.
- **meeting-index**: Entry added.
- **project-lessons**: LL-039 captured on the diarization/speaker-misattribution issue.
