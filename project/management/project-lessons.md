---
last_updated: 2026-09-15
last_updated_by: auto — project-meeting routing
owner: Marek Pillár
---

# Lessons Learned

---

### LL-034

| Field | Value |
|-------|-------|
| ID | LL-034 |
| Created | 2026-09-15 |
| Category | interviewing technique |
| Source | 2026-09-15-business-quantification-teo-ocr |

**Lesson**
In a business-quantification or scoping interview, don't take the interviewee's first "yes, that's me" on the Owner field at face value — explicitly reflect the Owner/Domain-Expert distinction back to them ("so X is the owner and you're my daily contact?") before writing it down. People default to saying yes to the person asking, then self-correct once the actual decision-making implication is spelled out.

**Context**
In the TEO/OCR quantification call, Radim Švarc initially confirmed he was the business owner ("Můžete si to tam napsat"), but immediately qualified it once Marek probed further — major decisions actually need Tomáš Burda's sign-off. Marek caught this by explicitly reflecting the corrected roles back ("takže business owner tohoto byl pan Burda a vy budete ten můj daily contact?"), which Radim then confirmed. Without that reflect-back step, Radim would likely have stayed recorded as owner.

**Cross-reference**
project-stakeholders STK-025, STK-041; product/solution-space/ai-initiatives-okr-framework.md (Pole 1 — Vlastník)

---

### LL-033

| Field | Value |
|-------|-------|
| ID | LL-033 |
| Created | 2026-09-15 |
| Category | workshop planning |
| Source | 2026-09-15-business-quantification-reklamace-fakturace-doprav |

**Lesson**
A per-item interview script's stated time budget (e.g. "~10-15 min per initiative") is a floor for a focused, uninterrupted exchange — real calls with a client stakeholder run longer per item once genuine back-and-forth, self-correction, and tangents happen, so a session prepped to cover many items in one sitting should expect to cover far fewer and plan an explicit follow-up rather than treating partial coverage as a shortfall.

**Context**
The Business Quantification workshop was prepped for 11 initiatives using a 6-field, ~10-15-min-per-item script. The first live execution covered only 2 (Reklamace, Fakturace doprav) in the available time before the client stakeholder had to leave for another call — each item ran meaningfully longer than the script's estimate once real discussion, self-correction on numbers, and tangential clarifications (naming, phasing) were included.

**Cross-reference**
product/solution-space/ai-initiatives-okr-framework.md; meetings/prep/2026-09-14-ai-initiatives-business-quantification-prep.md

---

### LL-032

| Field | Value |
|-------|-------|
| ID | LL-032 |
| Created | 2026-09-15 |
| Category | stakeholder tracking |
| Source | 2026-09-15-order-prediction-dashboard-follow-up |

**Lesson**
When processing a recurring meeting, actively cross-check any newly-named person against existing *low-confidence* stakeholder entries (not just full duplicates) — a name and role profile that loosely matched an old "unclear identity" record is a stronger signal than it looks, and flagging the possible match (without merging) keeps the record honest while surfacing it for PM confirmation.

**Context**
The 2026-09-15 order-prediction dashboard follow-up repeatedly referenced "Honza/Jan Maroušek," a warehouse-staffing planner needing a per-warehouse reservation breakdown. This closely matched two existing low-confidence entries created from earlier, thinner mentions: STK-036 ("Honza," flagged 2026-09-03 as wanting a month-ahead logistics view) and STK-021 (Jan Maroušek, the Kontrola beden contact). Rather than creating a third entry or silently merging, both existing records were annotated with the possible match and left for PM verification.

**Cross-reference**
project-stakeholders STK-021, STK-036; 2026-09-03-order-prediction-dashboard-live-demo

---

### LL-031

| Field | Value |
|-------|-------|
| ID | LL-031 |
| Created | 2026-09-11 |
| Category | working method |
| Source | project-daily-2026-09-11 |

**Lesson**
A workshop-prep artifact's field set and scope (how strict, how many entities, prefilled vs. blank) is a design decision the requester usually only discovers by seeing a first draft — expect at least one full restructure after showing initial work, and treat that as normal iteration rather than a sign the first attempt was wrong.

**Context**
The Žůrek/logistics Business Quantification prep went through three real restructures in one session: scope narrowed from 17 portfolio initiatives to 11, then the field set tightened from a loose OKR/confidence structure to a strict 6-field card with prefill rules, then an interview script was layered on top per field. Each pass was fast because the underlying research (OKR framework, JTBD, Fermi estimation) stayed valid across all three — only the presentation and scope changed.

**Cross-reference**
product/solution-space/ai-initiatives-okr-framework.md

---

### LL-030

| Field | Value |
|-------|-------|
| ID | LL-030 |
| Created | 2026-09-11 |
| Category | working method |
| Source | project-daily-2026-09-11 |

**Lesson**
An existing skill's internal structure can be borrowed for a deliverable that doesn't fit that skill's formal mechanics — apply its rigor (e.g. User Story / Acceptance Criteria discipline) without invoking its file-registration or ID-tracking machinery, when the underlying tracking system (FEAT-NNN, product-scope) doesn't actually apply to the content being produced.

**Context**
Drafting a first-ever Listing project spec, the PM asked to "leverage" the `/product-feature` skill's structure. This harness's `product-scope`/`FEAT-NNN` system is scoped to the Second Brain meta-tool, not Dr. Max's products, so the spec was written using `product-feature`'s section shape and AC rigor directly in `product/solution-space/listing-specifikace.md`, without registering a `feat_id` or linking to a `product-scope` file — kept the quality bar, skipped the mismatched mechanics.

**Cross-reference**
product/solution-space/listing-specifikace.md

---

### LL-029

| Field | Value |
|-------|-------|
| ID | LL-029 |
| Created | 2026-09-11 |
| Category | discovery method |
| Source | 2026-09-11-ai-listing-tool-demo-walkthrough |

**Lesson**
A live product demo/walkthrough can surface built capabilities that status meetings and roadmap trackers never mention — status updates report *progress against a plan*, while a demo reveals *what actually exists*, including features nobody thought to report because they weren't asked about.

**Context**
A structured walkthrough of the AI Listing Tool (presented by Filip Černý) surfaced several capabilities — a per-product catalog health score, version history/rollback, a granular per-field AI prompt configuration system, and a regulatory compliance blacklist for medical claims — none of which appeared anywhere in prior Listing meeting notes or the roadmap Excel, despite the underlying features being marked "Done."

**Cross-reference**
2026-09-11-ai-listing-tool-demo-walkthrough, `project-knowledge` (AI Listing Tool entry)

---

### LL-028

| Field | Value |
|-------|-------|
| ID | LL-028 |
| Created | 2026-09-10 |
| Category | requirements-gathering / access & permissions |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |

**Lesson**
A client request that sounds like a single simple ask (e.g. "we need a test account") can conceal several orthogonal technical requirements that only surface once you ask concretely how it will actually be used — who, how many people at once, and what exactly must and must not be visible to each. Treating the original request's brevity as evidence of simplicity, rather than as a sign the real requirement was never spelled out, wastes a cycle chasing the wrong ticket.

**Context**
A months-old ticket simply said "create a test account for AI," with no group/role detail — which nobody downstream had been able to act on. Only when the client (Mertová) was asked directly how testing would actually happen did it surface that 4 distinct role-scoped identities were needed simultaneously, that a single shared account in every permission group wouldn't actually test real role-restriction behavior, and that concurrent multi-tester use of one account might itself cause conflicts — three separate technical problems hiding inside what had been logged as one generic access request.

**Cross-reference**
2026-09-10-lexie-max-maxie-weekly-sync, ASM-063

---

### LL-027

| Field | Value |
|-------|-------|
| ID | LL-027 |
| Created | 2026-09-10 |
| Category | architecture / client communication |
| Source | 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |

**Lesson**
A confusing implementation detail (e.g. "why doesn't this count match?") can be a visible symptom of a much bigger unstated assumption (e.g. "who actually owns this system's state?") rather than a bug worth patching in isolation. When a data-contract question keeps not quite making sense despite incremental fixes, it's worth asking the client a blunt, higher-level ownership question directly — the answer can retire several smaller confusions at once.

**Context**
Filip Černý built the Fakturace doprav kiosk assuming the app needed to track its own route-completion state (deciding when a route was ready for manual review or invoicing) and had separately convinced himself Axapta returned per-document page counts to validate completeness — a claim that turned out, live in an internal demo, to be a hardcoded/faked value. Both confusions dissolved at once when the client (Jan Žižka) clarified directly, in the very next meeting, that Axapta is the sole owner of route/document state and the app should hold none at all. The page-count question had never been the real problem — it was a downstream symptom of an unstated architecture assumption nobody had asked the client to confirm.

**Cross-reference**
2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, ASM-053

---

### LL-026

| Field | Value |
|-------|-------|
| ID | LL-026 |
| Created | 2026-09-09 |
| Category | stakeholder communication |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |

**Lesson**
Effort estimates alone (e.g. man-days) don't communicate delivery timing to non-technical business stakeholders — a unit like "one man-day" has no fixed meaning in wall-clock time without a calendar attached, and can be misread as "one day away." Pairing any effort-based roadmap with a simple calendar/timeline view (what happens when: testing, fixes, rollout) closes that gap.

**Context**
Reviewing the roadmap board ahead of presenting it to Logistika and CC, Jindřich Tůma pointed out that a phase estimate like "MVP in one man-day" would mean nothing to Tereza Foltová — she needs to see concretely when testing starts, how long it runs, and when rollout lands, not an abstract effort unit. The fix didn't require new data, just a second, simpler view (item + filled time-axis cells) built from the same information already collected.

**Cross-reference**
2026-09-09-logistics-cc-roadmap-presentation-prep, ASM-050

---

### LL-025

| Field | Value |
|-------|-------|
| ID | LL-025 |
| Created | 2026-09-09 |
| Category | harness |
| Source | project-daily-2026-09-09 |

**Lesson**
When a client-facing board/deck is built by distilling a source-of-truth data file, check that per-item annotations (comments, caveats, rationale notes) carried over along with the headline numbers — a derived view can transfer the numeric totals correctly while silently dropping or misplacing the supporting detail attached to individual rows, and that gap isn't visible unless someone spot-checks the rendered artifact against its source.

**Context**
The PM noticed Honza Zelený's effort estimates appeared in the v3 roadmap board without any supporting comments, and initially thought they'd been misattributed to Lexie. Checking the live Excel confirmed the numbers were correctly Maxie's, and Maxie's sheet actually has 6 rich supporting comments (including a reuse note from Jura Brázdil) — none of which had made it into the board. The board's numeric totals were right; the per-box narrative context wasn't carried over during the board build.

**Cross-reference**
project-daily-2026-09-09

---

### LL-024

| Field | Value |
|-------|-------|
| ID | LL-024 |
| Created | 2026-09-09 |
| Category | tooling-collaboration |
| Source | project-daily-2026-09-09 |

**Lesson**
Never script-write to a file the user has open live in Excel/Office with AutoSave on. It's not just a race condition (see LL-023) — Excel's cloud co-authoring session actively breaks: it detects the file changed outside its own sync protocol and cannot reconcile that with its in-memory change history, so it locks all further saves ("Upload Blocked... can't save any new changes"). The fix isn't a longer delay before re-checking — it's confirming the file is closed before writing at all.

**Context**
While routing Filip Černý's estimates into the live roadmap Excel, Marek had the file open with AutoSave and was actively editing (mid-keystroke in a cell) when the script overwrote the file on disk. Excel Online surfaced a hard "Upload Blocked" error and would not save further changes; Marek had to close the file and discard his in-progress edit before a clean re-run of the same script succeeded. This explains an earlier silent-revert incident (LL-023) too — likely the same root cause, just resolved by Excel's autosave overwriting the script's change instead of blocking outright.

**Cross-reference**
LL-023, project-daily-2026-09-09

### LL-023

| Field | Value |
|-------|-------|
| ID | LL-023 |
| Created | 2026-09-08 |
| Category | tooling-collaboration |
| Source | project-daily-2026-09-08 |

**Lesson**
A programmatic write to a live cloud-synced file (OneDrive, Google Drive, etc.) can appear to succeed — and even verify correctly if re-read immediately — but still get silently reverted moments later by a sync conflict, most likely if the file is open elsewhere. Immediate post-write verification is not sufficient proof of persistence for actively-synced files; re-check after a short delay (several seconds) before reporting success, and if a write is found reverted, flag to the user that the file may be open elsewhere and ask them to close it before retrying.

**Context**
A batch of Excel comment/estimate writes to the live `product-roadmap-portfolio-full.xlsx` (OneDrive) verified correctly right after saving, but had reverted to the pre-write state by the next turn. Re-running the same write and checking again after a 10-second delay confirmed it held that time. The file had also spontaneously renamed itself mid-session earlier (dropping a version-number suffix), independently confirming OneDrive was actively manipulating the file outside of direct control.

**Cross-reference**
project-daily-2026-09-08

### LL-022

| Field | Value |
|-------|-------|
| ID | LL-022 |
| Created | 2026-09-08 |
| Category | discovery-methodology |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |

**Lesson**
When scoping new work on top of an existing internal system, a manager's or account owner's strategic/historical account and the actual builder's technical account can diverge significantly even when both are told in good faith — the strategic account explains *why* and *what was intended*, but only the person who currently maintains the code can say *what's actually built*. Get both, in that order, before committing to a delivery plan.

**Context**
Jan Sovka's account of BigHub's AI platform (deployed for ~2 years, role-based permissions live across the client base) was accurate as far as intent and history go, but Jura Brázdil's technical deep-dive the same day revealed a materially different present-day reality: the platform in practice is just one RAG product, MaxBuddy still isn't migrated into it, the permission system Jan described is Lexie-specific rather than platform-wide, and there's a shared database with zero isolation between use cases. Scoping the near-term delivery plan only became reliable once Jura's account was folded in — holding both meetings back-to-back the same day, rather than relying on the manager's account alone, is what surfaced the gap before commitments were made to the client.

**Cross-reference**
2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil, ASM-038, ASM-039

---

### LL-021

| Field | Value |
|-------|-------|
| ID | LL-021 |
| Created | 2026-09-07 |
| Category | tooling-collaboration |
| Source | project-daily-2026-09-07 |

**Lesson**
When a stakeholder is actively hand-editing a shared deliverable in parallel with AI-assisted generation, treat their live edits as the source of truth and layer additions on top rather than regenerating from scratch — a fresh regeneration silently overwrites judgment calls (manual status assignments, row splits, renumbering, owner attributions) that took real thought to make.

**Context**
While building `product-roadmap-portfolio-full.xlsx`, Marek began hand-editing the workbook directly (Status values, Owner names, deliberate row splits distinguishing MVP-done vs. Full-Version-continuation work) between generation passes. Continuing to regenerate the file from the original script would have destroyed that work. Switching to load-and-append edits on his live copy instead preserved everything and let new additions (new rows, Portfolio entries, comments) sit alongside his own changes without conflict.

**Cross-reference**
project-daily-2026-09-07

---

### LL-020

| Field | Value |
|-------|-------|
| ID | LL-020 |
| Created | 2026-09-07 |
| Category | discovery-methodology |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |

**Lesson**
Cross-referencing a shared tracker against every independent source that fed it (exports, specs, meeting transcripts, live stakeholder edits) before treating it as final surfaces real conflicts that no single source alone would reveal — disputed ownership, duplicate/stale entries, and quietly-changed decisions all hide in the gaps between sources.

**Context**
Reconciling the AI portfolio/roadmap workbook against v8.xlsx, the BigHub Notion export, the MVP Scope & Acceptance doc, and the 2026-09-07 review meeting surfaced several real discrepancies that a single-source build would have missed: disputed Reklamace dev ownership (two independent people each named as owner), the Maxie/Voicebot naming collision (same initiative tracked under two names), and a claim in the meeting note (Campaign Recommendation Model "confirmed Full Version") that turned out to overstate what was actually decided once checked against the PM's own live-edited Excel.

**Cross-reference**
2026-09-07-ai-portfolio-roadmap-scope-review, project-daily-2026-09-07

---

### LL-019

| Field | Value |
|-------|-------|
| ID | LL-019 |
| Created | 2026-09-04 |
| Category | discovery-methodology |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

**Lesson**
When onboarding onto a client-facing AI product, explicitly ask whether the underlying platform/infrastructure is dedicated to this client or shared across others. Don't assume a component is client-exclusive just because that's the only context you've seen it deployed in — shared internal platforms are common, and the assumption gets baked into scope, ownership, and design decisions before anyone corrects it.

**Context**
Several days into the Dr. Max account, a routine internal stand-up revealed the AI/chatbot platform (Max, Maxie, Lexie) is actually shared BigHub infrastructure also deployed for other clients (Brněnská komunikace, Kooperativa, Unica) — not built exclusively for Dr. Max. This reframed an open question about who owns the platform's product roadmap (a single client-scoped PM, or someone owning it across all clients) and how design/theming decisions should be made (centralized template vs. per-client customization) — questions that hadn't been asked earlier because the Dr. Max-exclusive framing had gone unchallenged.

**Cross-reference**
2026-09-04-ai-platform-standup-xmanager-lexi-demo, ASM-025, ASM-026

---

### LL-018

| Field | Value |
|-------|-------|
| ID | LL-018 |
| Created | 2026-09-04 |
| Category | client-management |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

**Lesson**
When a client is eager for visual polish but technical validation isn't done yet, offer a zero-engineering-cost placeholder — a single AI-generated image of what the redesign could look like — rather than either building real mockups or ignoring the request. It manages expectations and gives the client something concrete to react to, without pulling engineering time away from the actual priority.

**Context**
Dr. Max's CC team casually mentioned wanting Lexie to look as polished as the newly-demoed Max chatbot. Rather than scoping a real design pass (which would compete with fixing 3 blocking bugs) or dismissing the comment, the BigHub team's plan was to generate a single representative image via an AI tool — no mockup, no frame, no code — just something to show "this is the direction," while keeping actual engineering focused on technical fixes.

**Cross-reference**
2026-09-04-ai-platform-standup-xmanager-lexi-demo, ASM-024

---

### LL-017

| Field | Value |
|-------|-------|
| ID | LL-017 |
| Created | 2026-09-03 |
| Category | harness |
| Source | project-daily-2026-09-03 |

**Lesson**
When generating Office file formatting programmatically (fill colors especially), a structurally valid, error-free file can still render as blank/invisible if a color is written with a transparent alpha channel. Don't stop verification at "did it save without error" or "does the XML parse" — check the actual color/format values themselves (e.g. that an RGB fill starts with `FF` alpha, not `00`) before declaring a formatting change done.

**Context**
Applying conditional-formatting row colors to a client roadmap spreadsheet, a fill color built from a bare 6-character hex string (e.g. `"C8E6C9"`) saved successfully, passed zip/XML integrity checks, and correctly referenced the right cells and formulas — but rendered with 0% opacity because the alpha channel defaulted to `00` instead of `FF`. The PM reported "not working" with a screenshot; the fix was supplying an explicit 8-character ARGB string (`"FFC8E6C9"`). Root cause was only found by reading the raw dxf XML values, not by re-running the generation script and re-checking structural validity.

**Cross-reference**
project-daily-2026-09-03

| Field | Value |
|-------|-------|
| ID | LL-016 |
| Created | 2026-09-03 |
| Category | domain-specific |
| Source | 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

**Lesson**
On a regulated-industry AI feature (healthcare, finance, etc.), get a compliance/regulatory review early — as soon as the feature's data flow is defined — rather than after significant development investment. A feature that looks clearly compliant in early prototyping can turn out to require formal certification once its actual data-handling pattern is examined.

**Context**
MaxBuddy's original core feature — flagging outdated drug dosages against updated SPC guidance — was developed for roughly six months before Dr. Max discovered it made the product a regulated medical device requiring certification: any pipeline where patient data goes in and an LLM-derived recommendation comes out is prohibited without it. The feature is now frozen rather than shipped, and development pivoted to an expert-panel-reviewed upsell/cross-sell recommendation feature instead, which doesn't trigger the same certification requirement.

**Cross-reference**
2026-09-03-maxbuddy-chatbot-ocr-project-handoff, [[project-knowledge]] (MaxBuddy entry)

---

### LL-015

| Field | Value |
|-------|-------|
| ID | LL-015 |
| Created | 2026-09-03 |
| Category | design |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |

**Lesson**
When designing an in-product feedback mechanism, default to a lightweight rating widget (stars, emoji, a color-ordered scale) over a free-text form — and if the client already has UX data from prior deployments about what actually gets used, defer to it rather than re-litigating the design from scratch.

**Context**
Dr. Max's CC team pushed back on a free-text feedback form for the Max chatbot, citing their own prior chatbot data: free-text fields see low completion, and a green→red color-ordered rating scale outperformed the reverse order in their testing. The team adopted stars/emoji-only, no free text. Logged as ASM-017 (Decided).

**Cross-reference**
ASM-017, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync

---

### LL-014

| Field | Value |
|-------|-------|
| ID | LL-014 |
| Created | 2026-09-03 |
| Category | project-management |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |

**Lesson**
Route all client feature/change requests for a given product through a single named point of contact rather than accepting them individually from every user who touches it. Aggregate requests from many individual testers tend to drown out what the actual business owner needs, creating noise and duplicate or conflicting asks.

**Context**
Jindřich Tůma requested this explicitly for Max/Lexie/Maxie X-Manager tickets, routing everything through Simona Mertová, based on prior experience where requests from ten-plus individual users didn't reflect what the business owner actually wanted in the end. Logged as ASM-018 (Decided).

**Cross-reference**
ASM-018, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync

---

### LL-013

| Field | Value |
|-------|-------|
| ID | LL-013 |
| Created | 2026-09-03 |
| Category | stakeholder-management |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |

**Lesson**
When first-demoing a predictive or analytics dashboard to its real business owner, proactively point out a moment where the live data correctly reflects a known real-world event (an outage, a campaign, an anomaly the stakeholder already knows happened). This is a far more persuasive trust-building signal than any amount of explaining the model's methodology, because the stakeholder can verify it themselves against something they already know is true.

**Context**
An 8-minute site outage on 2026-08-24 showed up as a visible dip in the order-prediction dashboard's live chart during the demo. Marek Šimoník (Dr. Max, Head of E-commerce) immediately recognized and confirmed it, unprompted, calling it "an extremely good indicator" — this single moment did more to establish confidence in the tool than the rest of the walkthrough combined.

**Cross-reference**
2026-09-03-order-prediction-dashboard-live-demo

---

### LL-012

| Field | Value |
|-------|-------|
| ID | LL-012 |
| Created | 2026-09-03 |
| Category | delivery-process |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |

**Lesson**
When rolling a predictive/forecasting tool out to a business stakeholder for testing, set an explicit review order upfront: verify the underlying data/numbers are correct first, then gather display/UX feedback, and only then evaluate and tune the model's forecasting accuracy. Skipping this order lets an engaged, technical stakeholder pull the conversation into premature model-accuracy debates before the more basic, more easily verified layers are settled.

**Context**
Jan Sovka set this three-layer order (data accuracy → UX → model accuracy) proactively during the order-prediction dashboard's first live demo, reasoning that today's model accuracy was "good enough" and that arguing over forecasting precision too early would distract from the data/UX issues that are actually blocking the client from trusting the tool. Logged as ASM-014 (Decided).

**Cross-reference**
ASM-014, 2026-09-03-order-prediction-dashboard-live-demo

---

### LL-011

| Field | Value |
|-------|-------|
| ID | LL-011 |
| Created | 2026-09-03 |
| Category | delivery-process |
| Source | 2026-09-03-viapharma-logistics-status-reklamace-demo |

**Lesson**
When rolling out a new feature or app to client testers, don't let a proper production auth system (SSO, OAuth, Entra ID, etc.) block the start of testing — ship the simplest workable stand-in (e.g. hardcoded per-user logins) and build the real auth in parallel. Confirm what the requester actually needs first: sometimes a request that sounds like a security requirement ("I need to see who's logged in") is really about traceability/audit logging, which a much simpler mechanism satisfies.

**Context**
For the Dr. Max reklamace mobile app, Entra ID/OAuth was flagged as a likely integration friction point. Rather than wait for it, the team issued hardcoded per-tester logins so ViaPharma's testers (Tereza Foltová, then Jana) could start immediately, while Entra ID work continued in parallel. The client's stated interest in per-user login was clarified as wanting traceability in Axapta's logs (who performed which action), not concern about credential misuse — confirming a simple mechanism was sufficient. Logged as ASM-012 (Decided).

**Cross-reference**
ASM-012, 2026-09-03-viapharma-logistics-status-reklamace-demo

---

### LL-010

| Field | Value |
|-------|-------|
| ID | LL-010 |
| Created | 2026-09-02 |
| Category | project-management |
| Source | project-daily-2026-09-02 |

**Lesson**
When deriving task priority algorithmically (e.g. from milestone proximity, activity type, or "strategic vs. housekeeping" framing), explicitly weight requests from people with direct reporting-line authority as heavily as external stakeholder asks — and don't let a task's housekeeping surface appearance discount it, since the person requesting it may see it as a real delivery blocker even though it doesn't look that way from the outside.

**Context**
The daily's derived priority ranking treated a tooling migration (moving a tracking artifact into Notion) and setting up an internal sync cadence with the new PM as low-priority process/housekeeping. Both had in fact been directly requested by direct-authority figures (Jindřich Tůma as PM, Honza Sovka as line manager) during today's meetings, and the PM flagged that such requests should outrank the algorithmic ranking.

**Cross-reference**
project-daily-2026-09-02, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync

---

### LL-009

| Field | Value |
|-------|-------|
| ID | LL-009 |
| Created | 2026-09-02 |
| Category | delivery-process |
| Source | 2026-09-02-aks-atlantis-infra-sync |

**Lesson**
Before planning any redeployment, migration, or significant change to an existing system, confirm whether it was provisioned via infrastructure-as-code or set up manually (ad hoc clicking) — manually-configured infrastructure has no reliable reproduction path, and that risk stays invisible until someone actually needs to touch it again.

**Context**
A question about redeploying legacy MaxBuddy infrastructure (PTU/model provisioning) surfaced that it had been configured manually rather than via Terraform, and that the people most familiar with the original setup were no longer easily reachable — nobody in the room could confidently reconstruct how it was built. The team's practical response was to leave it untouched while it keeps working rather than risk a change with no clean rollback path.

**Cross-reference**
2026-09-02-aks-atlantis-infra-sync

---

### LL-008

| Field | Value |
|-------|-------|
| ID | LL-008 |
| Created | 2026-09-02 |
| Category | trust-building |
| Source | 2026-09-02-logistics-listing-team-sync |

**Lesson**
When automating a client-facing communication channel for the first time, default to producing a human-reviewed draft rather than an automatic send — even once the underlying logic is trusted, the send action itself is where an error becomes visible and costly to the client relationship.

**Context**
Designing the reklamace email-automation workflow, Jindřich Tůma set the rule explicitly the moment it was raised: the system pre-fills a draft from the applicable supplier procedure, a human reviews and edits it, then sends — never an automatic send. Logged as ASM-010 (Decided).

**Cross-reference**
ASM-010, 2026-09-02-logistics-listing-team-sync

---

### LL-007

| Field | Value |
|-------|-------|
| ID | LL-007 |
| Created | 2026-09-02 |
| Category | scope-protection |
| Source | 2026-09-02-logistics-listing-team-sync |

**Lesson**
When a project is blocked on an undefined client-side dependency (data model, category system, taxonomy), stop further development rather than continuing to build speculatively against a moving target — the cost of rework outweighs the appearance of progress, and framing the pause as "we need X from you before we continue" protects both budget and the relationship.

**Context**
Filip Černý refused to continue Listing development until Dr. Max delivers a category/parameter system, explicitly reasoning that further coding would "burn money for nothing." Jindřich Tůma validated this rather than pushing for visible progress, and the team agreed to a Discovery-first path instead (ASM-011) — explicitly framed as not a billing play, but as the only productive way forward.

**Cross-reference**
ASM-011, 2026-09-02-logistics-listing-team-sync

---

### LL-006

| Field | Value |
|-------|-------|
| ID | LL-006 |
| Created | 2026-09-02 |
| Category | scope-protection |
| Source | 2026-09-02-roadmap-tracking-and-listing-onboarding-sync |

**Lesson**
Protect delivery against scope creep by requiring every spec to carry an explicit, business-signed hypothesis + acceptance-criteria section before build starts — a short "what we're solving, what we'll build, how we'll know it's done" framing gives both sides a clear reference point when disputes arise later, without needing a heavyweight spec process.

**Context**
Jindřich Tůma introduced this as a direct response to requirement creep observed on the Dr. Max account ("the requests never stop") — the specific failure mode being a business owner claiming after delivery that an unstated expectation wasn't met (his example: "the button should have been pink"). Logged as ASM-009 (Decided).

**Cross-reference**
ASM-009, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync

---

### LL-005

| Field | Value |
|-------|-------|
| ID | LL-005 |
| Created | 2026-09-02 |
| Category | data-quality |
| Source | 2026-09-02-order-prediction-dashboard-walkthrough |

**Lesson**
When two independent team members separately name different individuals as owning the same workstream, treat both attributions as provisional and record both rather than silently picking one — single-source ownership claims on an account with fragmented documentation are a recurring failure mode, not a one-off.

**Context**
Filip Černý (2026-09-01) named "Kuba Turner" as the main builder of the reklamace stream; Juraj Kmec (2026-09-02), speaking independently, instead attributed both reklamace and freight invoicing to "Jura Brázdil." Neither source expressed full confidence. This is the third such conflict surfaced on the account in two days (see also ASM-005, ASM-006), suggesting the underlying documentation/reporting gap Jindřich was hired to fix is still actively producing inconsistent records.

**Update (2026-09-03)**: The "resolved" version of this conflict (ASM-007, Decided 2026-09-02 — Turner=MaxBuddy only, Brázdil=reklamace) turned out to be incomplete rather than either side being wrong: a follow-up meeting showed Turner is *also* active on the reklamace backend. Lesson refined — when reconciling two conflicting ownership claims, don't assume the resolution must be exclusive (one right, one wrong); check whether both can be true at once (shared/overlapping ownership) before closing the conflict as Decided.

**Cross-reference**
ASM-007, ASM-005, ASM-006, 2026-09-02-order-prediction-dashboard-walkthrough

---

### LL-004

| Field | Value |
|-------|-------|
| ID | LL-004 |
| Created | 2026-09-01 |
| Category | delivery-process |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync |

**Lesson**
When a deliverable is blocked by an unrelated internal process the client is running on their own timeline (e.g. a company-wide tender or approval), ship using what's currently available and explicitly plan a follow-up wave once the client-side process resolves — rather than waiting for it and blocking delivery.

**Context**
A chatbot's design/logo was blocked because Dr. Max's Brno headquarters was running its own company-wide tender for design/logo work. Resolved by shipping now with the existing design (following a prior Slovak precedent) and agreeing to apply the new branding in a later wave once the tender concludes — explained directly to the affected stakeholder, who agreed not to block the release on it.

**Cross-reference**
2026-09-01-dr-max-x-bighub-project-status-sync

---

### LL-003

| Field | Value |
|-------|-------|
| ID | LL-003 |
| Created | 2026-09-01 |
| Category | stakeholder-management |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |

**Lesson**
Passive delivery of a finished feature (one announcement email, then silence) rarely drives adoption — sustained, active promotion (workshops, demos, reminders) is usually required even when the feature clearly solves a stated problem.

**Context**
An early call-center automation feature was released for UAT with a single announcement; after 14 days, zero users had engaged with it. By contrast, presenting the listing automation work live on the client's board (with a short demo video and deck, ~6 hours of prep) produced strong visible buy-in.

**Cross-reference**
2026-08-25-marek-onboarding-with-jan-sovka

---

### LL-002

| Field | Value |
|-------|-------|
| ID | LL-002 |
| Created | 2026-09-01 |
| Category | discovery |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |

**Lesson**
When learning an unfamiliar account or process, gather input from both directions before proposing changes: management's stated priorities/KPIs, and separately, the reality reported by the people actually doing the work day to day. The two often diverge, and the gap is where the real risk hides.

**Context**
A warehouse claims-automation project was speced based on the Prague warehouse's process; two months before go-live it emerged that three other warehouses (including Brno) ran a materially different, paper-based process the process owner hadn't accounted for.

**Cross-reference**
2026-08-25-marek-onboarding-with-jan-sovka, [[project-knowledge]] ("old wise man" discovery approach)

---

### LL-001

| Field | Value |
|-------|-------|
| ID | LL-001 |
| Created | 2026-09-01 |
| Category | specification |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |

**Lesson**
Showing business stakeholders a clickable/prototype mockup before or alongside writing a spec surfaces edge cases and gets substantially better engagement than a text brief alone — stakeholders who won't react to a two-paragraph description will spot and raise issues when they can click through a flow.

**Context**
Prototype-first specs became the default approach across the Dr. Max streams (e.g. MaxBuddy, logistics/claims) after repeatedly producing better-informed specs and stronger stakeholder buy-in than text-only briefs.

**Cross-reference**
2026-08-25-marek-onboarding-with-jan-sovka

---

## Entry Format

```markdown
---

### LL-{NNN}

| Field | Value |
|-------|-------|
| ID | LL-{NNN} |
| Created | {YYYY-MM-DD} |
| Category | {open-ended label} |
| Source | {meeting-slug, daily-slug, document-slug, or "PM"} |

**Lesson**
{Generalized insight — 1-3 sentences, understandable without project context}

**Context**
{What specifically happened — project-specific details}

**Cross-reference**
{Links to related artifacts: assumptions, meetings, dailies — when applicable}
```
