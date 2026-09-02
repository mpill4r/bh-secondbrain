---
last_updated: 2026-09-02
last_updated_by: manual — conversational (ASM-006 partial resolution)
owner: Marek Pillár
---

# Project Assumptions & Decisions

## Index

| ID | Status | Created | Description (short) |
|----|--------|---------|---------------------|
| ASM-011 | Decided (2026-09-02) | 2026-09-02 | Listing project gets a formal client-side Discovery phase before further development continues |
| ASM-010 | Decided (2026-09-02) | 2026-09-02 | Reklamace email drafts are never sent automatically — always created for human review first |
| ASM-009 | Decided (2026-09-02) | 2026-09-02 | Specs must include a business-signed hypothesis + acceptance-criteria section before build starts |
| ASM-008 | Decided (2026-09-02) | 2026-09-02 | Business-facing roadmap sheet trimmed to Ideas/Active only; dev detail moves to a VBS breakdown in a separate system |
| ASM-007 | Decided (2026-09-02) | 2026-09-02 | Reklamace/freight-invoicing dev ownership conflict — resolved: Brázdil owns reklamace + freight invoicing, Turner owns MaxBuddy |
| ASM-006 | Open (2/4 resolved, 2026-09-02) | 2026-09-02 | BigHub roadmap sheet vs. transcripts — 4 ownership/spelling conflicts recorded; surname spelling and Lexi co-ownership resolved, invoicing/reklamace ownership still open |
| ASM-005 | Decided (2026-09-02) | 2026-09-01 | Who's Who reference card cross-referenced against transcripts for 2026-09-01 status sync — verified by Marek |
| ASM-004 | Decided (2026-09-01) | 2026-09-01 | MaxBuddy changes touching the shared data model require Dr. Max analytics team review before shipping |
| ASM-003 | Decided (2026-08-25) | 2026-09-01 | Alfred stays a BigHub-internal asset, never delivered to clients |
| ASM-002 | Decided (2026-08-25) | 2026-09-01 | Marek's mandate is delivery ownership of the 9 existing Dr. Max streams, not new sales |
| ASM-001 | Decided (2026-08-25) | 2026-09-01 | Dr. Max client-side coordination unified into one role (Jindřich Tůma) |

## Entries

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
| Source | 2026-09-02-order-prediction-dashboard-walkthrough |
| By | Juraj Kmec (STK-009) |
| Status | Decided (2026-09-02) |

**Description**
Two different sources named two different people as owning reklamace (complaints): Juraj Kmec (2026-09-02) believed **Jura Brázdil** (STK-026) owns both reklamace and freight invoicing under one shared "logistics" umbrella. Filip Černý (2026-09-01, listing intro) had named **"Kuba Turner"** (plus "Flurimo") as the one who mostly built reklamace.

**Rationale**
Resolved by Marek (2026-09-02): **Turner works on MaxBuddy**, not reklamace — Filip's original attribution was incorrect. **Jura Brázdil is confirmed** as owning both reklamace and freight invoicing (fakturace dopravy).

**Impact**
- **Data quality**: STK-026 (Jura Brázdil) updated to confirmed. STK-007 confirmed as the same person as "Kuba Turner" — surname updated to Turner, role updated to include MaxBuddy.

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
4. ~~Lexie → Tomáš Dudaško (STK-010) vs. Martová/Mertová owning Max/Maxi/Lexi together.~~ **Resolved 2026-09-02**: not a real conflict — Dudaško holds IT/budget-side ownership, Mertová holds operational/product ownership; both own it.

**Rationale**
PM explicitly asked to record both sides of each conflict rather than pick one now — "record both and let me decide later." Consistent with the same approach taken for ASM-005. On 2026-09-02, Marek resolved the two naming/ownership-framing conflicts (surname, Lexi co-ownership) but is not yet sure on the two possible-duplicate-initiative conflicts (invoicing solution, reklamace/complaints) — those remain open pending direct follow-up with Zurek, Žižka, or Hulešová.

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
