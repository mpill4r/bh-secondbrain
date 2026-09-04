---
last_updated: 2026-09-04
last_updated_by: auto — project-lessons (triggered by project-meeting routing, 2026-09-04-ai-platform-standup-xmanager-lexi-demo)
owner: Marek Pillár
---

# Lessons Learned

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
