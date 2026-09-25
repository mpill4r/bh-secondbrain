---
last_updated: 2026-09-24
type: external
attendees: [Tomáš Dudaško, Jindřich Tůma, Marek Pillár, Jura Brázdil]
recording_link:
---

# AI Initiatives: Business Quantification Review & AI Platform Prototype Demo with Tomáš Dudaško

**Date**: 2026-09-24 (14:00)
**Attendees**: Tomáš Dudaško (Dr. Max CZE, AI platform/IT owner), Jindřich Tůma (BigHub), Marek Pillár (BigHub, Business Quantification tracker owner), Jura Brázdil (BigHub, platform/MaxBuddy/chatbot dev; joined ~20 min in, from the Krkonoše over a mobile hotspot)
**Type**: external
**Recording**: N/A (Fireflies transcript)
**Previous session**: [2026-09-21-ai-platform-vision-discovery-dudasko.md](2026-09-21-ai-platform-vision-discovery-dudasko.md)
**Meeting prep**: N/A

> **Transcript note**: Fireflies mixed up the speaker labels. Before Jura joined (~20:12), lines labeled "Jura Brázdil" are Jindřich (Czech, addresses "Máro"/"Tome"), and lines labeled "Jindřich Tůma" in Slovak are Marek. After ~20:12, "Jura Brázdil" is Jura, except one Slovak line at 38:21 (Marek). Czech lines labeled "Jindřich Tůma" after 30:00 are Jindřich ("JUDr." is a transcription of "Juro"). Attribution below uses the corrected speakers.

## TL;DR

Dudaško endorsed the Business Quantification tracker. He said he had always wanted this and never got it from the business, and that the owner-guaranteed, email-confirmed figures finally deliver it. He immediately raised the bar: every KPI now needs a defined measurement method and baseline, and the tracker format becomes the mandatory intake standard for all new AI ideas. The department backlogs are targeted for end of November. Jura then demoed the AI Platform prototype (role-based entry, per-project cost/usage/technical-status views, permissions and audit trail), and Dudaško closed with "po velmi dlouhé době můžu BigHubu říct, dobrá práce" [translated from Czech: "after a very long time I can tell BigHub: good job"]. A first release is estimated at ~3–4 weeks once database access on the new cluster works. There's a conflict here: Dudaško says Tvarůžek reports it's done, while BigHub's latest check says it isn't.

## Continuity from 2026-09-21 (and 2026-09-22/23)

- **3-phase AI Platform sequencing ([[ASM-115]])**: on track. The Phase 1 UX/access prototype was shown and well received. Design polish is still deliberately deferred ([[ASM-147]]), and Marek framed the demo as "UX way, not colors/branding".
- **Send Dudaško the current MaxBuddy reporting (Jindřich)**: resolved in the meeting. The MaxBuddy report inside the prototype is the latest one ("dvě mouchy jednou ranou" [translated from Czech: "two birds with one stone"]).
- **Combined Dudaško session (Reklamace continue-or-close + full portfolio priority review)**: this was it, but only partly. The BQ tracker was reviewed and the prioritization *method* agreed. The Reklamace decision and a line-by-line priority ranking ([[ASM-125]]) were **not** discussed and remain open.
- **Mertová's figures**: still unconfirmed. Dudaško was told Mertová hasn't had time and that Šimoník (on vacation) hasn't signed off either.
- **Cost reporting test vs. prod ([[ASM-148]])**: partly answered. Dudaško wants everything, with a breakdown.
- **Infra/DB access blocker**: still unresolved, and now in conflict (see below).

## Key Discussion Points

### Business Quantification tracker: status

Marek (arrived late from the CC weekly sync) summarized:
- For each initiative, Marek met the owner and domain expert and defined business values (what can be saved or earned, and how it could be measured). He then annualized them, e.g. Reklamace via the fully loaded cost of the affected employee.
- Business owners have approved the values, with two exceptions: Marek Šimoník (order prediction), who is on vacation though the numbers are his, and Simona Mertová, who hasn't had time.
- The annualized columns (M and N, annual savings/revenue) have **not** been shown to the business owners.

Jindřich added that the per-initiative confirmations are kept by email as an audit trail: "i když nám to tady někdo potvrdí a za půl roku řekne: 'Tady ty čísla jsem v životě neviděl,' tak my to máme" [translated from Czech: "even if someone confirms it now and in half a year says 'I've never seen these numbers', we have it"].

### Dudaško: from values to measurement (the "B" and "C")

Dudaško was clearly happy with the tracker ("jsem s tím úplně spokojenej"). He then set the next step: KPIs are defined, but **how each one is measured** is missing. His example is the first row, "25× faster than today": you have to measure today's baseline, implement, then measure the new state. He laid out three layers:
- **Business value**: what the business says the initiative is worth.
- **KPI**: what BigHub thinks the implementation will achieve, agreed jointly with the business.
- **Measurement method**: how the KPI is measured. This should live in the tracker too.

He wants this to become the **status quo for all new ideas**. Anyone proposing something must bring a goal description, a business value and 1–3 KPIs. That goes into the tracker, and prioritization goes after the biggest values ("chceme jít po těch největších špecích" [translated from Czech: "we want to go after the biggest ones"]).

He was openly appreciative. He had always asked the business for this and been told "we've never done it, we won't do it". He let BigHub, as the "new broom", swim in it, and it worked. Jindřich credited the key win as making **owners the guarantors** of the figures, instead of the previous "let's see how it turns out" engagement.

### Listing as the model case, and "PR" stories per initiative

Marek pointed to Petr Neuman (Listing) as already having the "B" in place. He tracks cost per listed item quarter by quarter (before him, since he joined, and expected after deployment) in a simple artifact. Dudaško, drily: "Neumann is an analyst."

Dudaško then asked for a **"PR" narrative per tracker row**. Each would show the assumption (e.g. 230 → 130 Kč per item), an interim state, the current state after deployment, and the trend or learning curve. With ~3,600 items per quarter, the savings are then measurable and can be shown. He asked Jindřich to present this at **next Tuesday's project meeting (2026-09-29)**, at least for initiatives already live or close to live. Jindřich will prepare it; he has a session tomorrow to update the presentation and will preview it with Dudaško. Dudaško noted he "already has 34 million in Listing" (consistent with [[ASM-123]]); if that materializes, "it'll pay your invoices".

Jindřich asked Marek to own this discipline: push business users on specification and measurement, and always get the figures confirmed by email. "Je to rozhodující faktor pro to rozhodování, jestli to bude go nebo nebude" [translated from Czech: "it's the deciding factor for go or no-go"].

### Milestones and measurement column

Marek (product background) asked whether phased initiatives should have milestone checkpoints, e.g. after phase 1 of a 2027 Q1 project, to judge early whether it will succeed. Dudaško: case by case, but every KPI must have a measurement method and a way to show whether it's being met. Marek will add a **measurement column** to the tracker and ask each business owner how their KPI can be measured. He expects most can report it in a basic, MVP-style way (e.g. 3 FTEs across 3 warehouses). He starts tomorrow with Tereza Foltýnová on logistics.

### Department AI-initiative backlogs, targeting end of November

Jindřich relayed that Logistics wants to map further AI initiatives and go through them with Marek. The agreed approach:
- **Part A (now)**: finish the specs for the two running logistics projects, Reklamace and Fakturace doprav.
- **Part B (has time)**: capture new topics into the same tracker format.
- Logistics sets its own priorities. Dudaško decides go/no-go based on annual value.
- Jindřich cautioned Marek not to get pulled into specifying 10 topics at once ("teďka budeš měsíc zavřenej na skladech" [translated from Czech: "you'll be locked in the warehouses for a month"]).

Target: **by end of November**, each department (logistics, marketing, others) has its AI initiatives filled in and prioritized as a ready backlog, so management (Dudaško, possibly pan Žák) can set 2027 goals. Dudaško: end of November is fine; he'd prefer earlier, but it must be achievable. Marek noted the priority remains running projects and unblocking them, and he'll try for November. Jindřich framed November as an ideal plan, "not set in stone". Dudaško has already connected BigHub with **Marek Dvořák (marketing)**. BigHub will keep Dudaško updated on which department is being worked on.

### AI Platform prototype demo

Marek introduced it: the goal was the UX, not colors or branding, focused on Dudaško's asks (the platform concept, overview, and role separation), with several simulated role combinations. If this is OK, design and development planning can follow.

Jura demoed (the prototype is hosted on his private infra, not Azure, with mocked data and a mocked entry gate):
- **Role-based entry**: a CC user with only Lexie access goes straight into Lexie, with no platform screen. A super-admin lands in the full platform.
- **Project overview tiles**: go into each project (chat with Lexie, a MaxBuddy demo since Farmis isn't reachable, the chatbot, etc.). Every project should carry reporting and technical status.
- **Cost report**: per project, showing spent, forecast and budget. Covers OpenAI tokens and Azure consumption, broken down by prod and test. Jura would also include prototyping token spend.
- **Platform reporting**: platform-level usage, including internal-only projects (Listing, TEO/OCR service protocols). Jindřich added that it will reflect the BQ KPIs and track adoption-campaign reach.
- **Technical status**: health checks per project. For MaxBuddy these are API, kiosks, nightly export processing and SPC changes; Jura currently checks this manually each morning from local telemetry. It also shows external dependencies (Dr. Max services, AKS) so a central outage is visible.
- **Permissions**: per-tile access settings for tenants and roles (e.g. platform status for super-admins only, Lexie status for CC/IT admins), plus a **live audit trail** of who did what.
- **Limited-role views**: Lexie + service protocols shows only those two; Lexie admin + Chatbot admin gets both, with "no permission" on the chatbot settings they lack; MaxBuddy reporting-only goes straight to reporting.
- **MaxBuddy admin, "argumenty produktů"**: Dudaško was surprised to learn cross-sell arguments aren't fully automated. An expert writes a rough idea (e.g. Amoxiclav → offer magnesium), the LLM generates ~15 phrasings, and the expert group approves or rejects them. The platform gives this a proper interface instead of a URL passed around. BigHub has also been collecting SPC changes for 2 months (a possible future feature, not discussed further).
- **Roadmap/blockers view** (Jura's own idea): Dudaško said it belongs in the Azure DevOps setup Jindřich is preparing, possibly as an admin view. Jindřich added that release info should surface in the platform.

**Zabbix integration (Dudaško)**: Dudaško wants the platform to be the central aggregation point for telemetry. It should correlate signals ("three small problems make a big mess") and push alerts to Dr. Max's **Zabbix**. Jura agreed and added alerting (email/phone), a full **incident history for auditability** (certifications/legal), and a BigHub developer panel for manual incident notes. He briefly questioned whether Zabbix should connect directly rather than through BigHub, but Dudaško was clear the platform is the central point.

**Cost granularity**: asked whether he wants test and prod separately or combined, Dudaško said "everything, but a breakdown is better". Jura will show test, prod and total.

The prototype link will be shared with Dudaško to click through. It's public but behind a PIN.

**Dudaško's verdict**: "s tímhle začínám být spokojený" [translated from Czech: "I'm starting to be satisfied with this"], and "po velmi dlouhé době můžu BigHubu říct, dobrá práce, máte pěkně spočítaný náklady a máte pěkně udělanej frontend" [translated from Czech: "after a very long time I can tell BigHub: good job, you've got the costs nicely worked out and a nice frontend"].

### First release estimate and the DB-access conflict

Jindřich asked Jura for a rough first-release estimate. Jura's sequence once the database on the new cluster is reachable:
1. Deploy the platform to the new cluster.
2. Migrate MaxBuddy, currently outside the platform.
3. Deploy the Max chatbot there, to enable public access.
4. Fix some existing security concerns.

That's ~14 days to a unified platform with costs and reporting, then wiring in the already-built web frontend. Total ~3 weeks, excluding unknown permission requirements. Jindřich: plan for 4, given BDC turnaround. MaxBuddy stays the top priority.

**Conflict**: Dudaško said Vladislav Tvarůžek told him today that DB access is done ("zvedněte telefon a zavolejte Tvárovi" [translated from Czech: "pick up the phone and call Tvarůžek"]). Jura's last exchange (last Friday or Monday) was handing Vláďa a repro script: it works from the old cluster, not from the new one. Vláďa forwarded it to BDC. Jindřich's last information (yesterday 15:30) was that it still didn't work. Both sides are wary of "it works" claims. Jura will test right after the meeting.

## Decisions Made

- The BQ tracker format (goal, owner-guaranteed business value, 1–3 KPIs, email confirmation) becomes the mandatory intake standard for all new AI initiatives. Prioritization is by annual value, and Dudaško makes go/no-go calls.
- Every KPI must also carry a measurement method and baseline. A measurement column is added to the tracker.
- Initiatives that are live or near-live get a "PR" story (assumption → interim → current → trend), starting with the 2026-09-29 project meeting.
- Department AI-initiative backlogs target end of November: an ideal plan, not a hard deadline. Running projects keep priority.
- Logistics work splits into Part A (finish Reklamace and Fakturace doprav specs) and Part B (capture new topics into the tracker). Logistics prioritizes, Dudaško decides.
- The AI Platform is the central telemetry and alerting point and should integrate with Dr. Max's Zabbix. Incident history is kept for auditability.
- Cost reporting shows the total plus a test/prod breakdown (and prototyping spend).
- The roadmap/blockers view belongs in Azure DevOps, not the platform (at most an admin view).
- The Phase 1 prototype direction is accepted by Dudaško. The first release is planned at ~4 weeks after DB access works.

## Action Items

- [ ] **Jura Brázdil**: Test DB access from the new cluster right after the meeting and report whether Tvarůžek's "done" is accurate — due 2026-09-24 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Jura Brázdil / Jindřich Tůma**: Share the prototype link (with PIN) with Tomáš Dudaško to click through — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Jindřich Tůma**: Prepare a "PR" story per live or near-live initiative for the 2026-09-29 project meeting; preview the updated presentation with Dudaško — due 2026-09-29 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Marek Pillár**: Add a KPI measurement-method column to the BQ tracker and collect how each KPI will be measured from every business owner — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Marek Pillár**: With Tereza Foltýnová (logistics), agree the Part A / Part B split: finish the Reklamace and Fakturace doprav specs first, then capture new logistics AI initiatives in the tracker format — due 2026-09-25 (session) — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Marek Pillár**: Collect and prioritize AI-initiative backlogs from the departments (logistics, marketing via Marek Dvořák, others) in the BQ tracker format — target end of November 2026 — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Marek Pillár**: Get email sign-off on BQ figures from Marek Šimoník (after his vacation) and Simona Mertová — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Jindřich Tůma / Jura Brázdil**: Plan the first platform release internally in detail (new-cluster deploy, MaxBuddy migration, chatbot deploy, security fixes, frontend wiring; ~4 weeks after DB access) — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko
- [ ] **Jindřich Tůma**: Keep Dudaško regularly updated on which department's AI-initiative backlog is being worked on — from 2026-09-24-ai-initiatives-bq-review-platform-prototype-demo-dudasko

## Open Questions

- Is DB access on the new cluster actually working? Tvarůžek says yes; BigHub's last check (2026-09-23 15:30) says no.
- Should business owners see and approve the annualized savings columns (M/N), which they haven't seen yet?
- The Reklamace continue-or-close decision and the portfolio priority ranking ([[ASM-125]]) weren't addressed. Still pending a separate meeting.
- Zabbix integration: is it direct from source systems or via the platform? Dudaško wants the platform as the aggregator; Jura raised the question but didn't pursue it.
- The exact cost-report cadence ("rozpad v týdnu" may mean a weekly breakdown).
- Whether phase-level success milestones should be formalized per initiative. Dudaško: case by case.
- Who at Dr. Max management sets the 2027 goals (Dudaško, pan Žák?).

## Sentiment & Tone

The most positive Dudaško interaction on record. After the guarded tone of 2026-09-21 (where Jindřich read him as wary from past unmet promises), he gave explicit, repeated praise. The BQ tracker delivered something he says he "always wanted and never got", and the prototype drew "after a very long time I can tell BigHub: good job". That's a meaningful trust reset on the account.

His style is demanding and forward-leaning: praise came with an immediate next bar (measurement methods, PR stories, Zabbix integration, backlogs by end of November). This reads as engagement, not dissatisfaction, and it raises expectations on Marek's workload and on the 2026-09-29 presentation.

The DB-access exchange showed a shared skepticism toward infra "it's done" claims, and it aligned both sides rather than creating tension. Jindřich positioned Marek clearly as the owner of the BQ/measurement discipline in front of Dudaško, while protecting him from being swamped by logistics. The meeting ended informally and warmly (a long Fortran/Algol tangent from Dudaško, a theoretical CS PhD), another signal of relaxed rapport.

## Routing Log

- **project-assumptions**: Added ASM-158 (BQ intake standard), ASM-159 (KPI measurement column), ASM-160 (PR value stories), ASM-161 (department backlogs end of November; logistics Part A/B), ASM-162 (central telemetry + Zabbix + incident audit), ASM-163 (roadmap view → Azure DevOps), ASM-164 (first release ~4 weeks after disputed DB access, Open). Annotated ASM-115 (Phase 1 accepted), ASM-147 (design can start), ASM-148 (total + test/prod breakdown wanted).
- **project-knowledge**: Updated "Business Quantification tracker" (intake standard, measurement layer, approval status, M/N columns unseen by owners), "AI platform — current technical state" (demoed Phase 1 feature set, Zabbix, release sequence), "MaxBuddy" (semi-manual cross-sell argument workflow, manual health checks).
- **project-stakeholders**: Updated STK-001, STK-003, STK-010, STK-013, STK-016, STK-017, STK-019, STK-023, STK-026. Added STK-052 (Marek Dvořák, Dr. Max marketing).
- **project-daily**: Added 9 action items; marked "send Dudaško MaxBuddy reporting" and "hold the combined Dudaško meeting" done (Reklamace decision moved to the separate meeting); annotated the AI Platform spec/roadmap item as partial.
- **meeting-index**: Added entry for this meeting.
