---
last_updated: 2026-09-02
last_updated_by: auto — project-lessons (triggered by project-meeting routing, 2026-09-02-aks-atlantis-infra-sync)
owner: Marek Pillár
---

# Lessons Learned

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
