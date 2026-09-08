---
last_updated: 2026-09-08
last_updated_by: manual — conversational (client-facing roadmap decision)
owner: Marek Pillár
---

# Project Assumptions & Decisions

## Index

| ID | Status | Created | Description (short) |
|----|--------|---------|---------------------|
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
| ASM-006 | Open (2/4 resolved, 2026-09-02) | 2026-09-02 | BigHub roadmap sheet vs. transcripts — 4 ownership/spelling conflicts recorded; surname spelling and Lexie co-ownership resolved, invoicing/reklamace ownership still open |
| ASM-005 | Decided (2026-09-02) | 2026-09-01 | Who's Who reference card cross-referenced against transcripts for 2026-09-01 status sync — verified by Marek |
| ASM-004 | Decided (2026-09-01) | 2026-09-01 | MaxBuddy changes touching the shared data model require Dr. Max analytics team review before shipping |
| ASM-003 | Decided (2026-08-25) | 2026-09-01 | Alfred stays a BigHub-internal asset, never delivered to clients |
| ASM-002 | Decided (2026-08-25) | 2026-09-01 | Marek's mandate is delivery ownership of the 9 existing Dr. Max streams, not new sales |
| ASM-001 | Decided (2026-08-25) | 2026-09-01 | Dr. Max client-side coordination unified into one role (Jindřich Tůma) |

## Entries

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
| Source | roadmap sheet (PM-provided image, 2026-09-02) |
| By | Marek Pillár (STK-001) |
| Status | Open (2/4 resolved, 2026-09-02) |

**Description**
A BigHub "Initiative → Owner/Customer" roadmap sheet was cross-checked against existing meeting-derived stakeholder records. Two entries matched cleanly (MaxBuddy → Tomáš Dudaško; E-Shop order forecast → Marek Šimoník). Two entries were net-new (Product listing → Petr Neuman; TD revisions → Tomáš Burda). Four points conflicted with existing records and were recorded on both sides rather than resolved:
1. **Invoicing solution → Rudolf Zurek** (STK-024) vs. Fakturace doprav → Jan Žižka (STK-015) / Petr Spilka (STK-014) reviewing — possibly the same initiative under different names, possibly distinct. **Still open** — Marek not yet sure, needs to check directly with Zurek or Žižka.
2. **Receiving compliants in stock → Rudolf Zurek** (STK-024) vs. Reklamace → Marie Hulešová (STK-020) — possibly the same initiative, possibly distinct. **Still open** — same as above.
3. ~~Maxie/Max → Simona Mertova (STK-017) — surname spelling conflict.~~ **Resolved 2026-09-02**: "Mertová" confirmed correct; "Martová" was a transcription error.
4. ~~Lexie → Tomáš Dudaško (STK-010) vs. Martová/Mertová owning Max/Maxie/Lexie together.~~ **Resolved 2026-09-02**: not a real conflict — Dudaško holds IT/budget-side ownership, Mertová holds operational/product ownership; both own it.

**Rationale**
PM explicitly asked to record both sides of each conflict rather than pick one now — "record both and let me decide later." Consistent with the same approach taken for ASM-005. On 2026-09-02, Marek resolved the two naming/ownership-framing conflicts (surname, Lexie co-ownership) but is not yet sure on the two possible-duplicate-initiative conflicts (invoicing solution, reklamace/complaints) — those remain open pending direct follow-up with Zurek, Žižka, or Hulešová.

**Impact**
- **Data quality**: STK-017 and STK-010 updated to reflect resolved co-ownership and correct spelling. STK-014, STK-015, STK-020, STK-024 still carry a note pointing to this assumption — none should be treated as resolved until Marek confirms with the people involved whether "Invoicing solution"/"Receiving complaints in stock" are the same initiatives as Fakturace doprav/Reklamace or genuinely distinct.

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
