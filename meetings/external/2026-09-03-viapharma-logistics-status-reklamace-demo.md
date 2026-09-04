---
last_updated: 2026-09-03
type: external
attendees: [Jan Sovka, Jakub Turner, Filip Černý, Marek Pillár, Tereza Foltová, Petr Sláma, Jan Kopecký, Lukáš Szücs]
tldv_link:
---

# ViaPharma Logistics Status Sync — Reklamace App Demo

**Date**: 2026-09-03
**Attendees**: Jan Sovka (BigHub, running the call), Jakub Turner (BigHub, developer), Filip Černý (BigHub, developer), Marek Pillár (BigHub, silent — formally introduced), Tereza Foltová (ViaPharma CZE), Petr Sláma (ViaPharma CZE), Jan Kopecký (ViaPharma CZE), Lukáš Szücs (Dr. Max CZE)
**Type**: external
**Recording**: N/A
**Previous session**: N/A — no matching prior instance found in the index; treated as a new thread despite clear signs of being an established recurring status call (frequent references to "z minula" / "from last time")
**Meeting prep**: N/A

## TL;DR

Recurring BigHub↔ViaPharma logistics/reklamace status call, run by Jan Sovka in Jindřich's and Alana's absence. Cleared a batch of previously-open small bugs, confirmed OAuth/Entra ID auth is deferred behind hardcoded test logins, agreed a Swagger change-notification process, and closed with a live demo of Filip Černý's reklamace mobile app — well received, targeting tester (Jana) access before she returns from vacation next week. Marek was formally introduced to the ViaPharma team.

## Key Discussion Points

### Supplier-data consolidation (Tereza Foltová)

Tereza is consolidating ~120 suppliers into a single simplified structure before handling supplier-specific exceptions individually. The original 2026-09-07 deadline is at risk — described as "a lot of manual work" and complicated by the fact that Jana (who normally owns this) is on vacation but still contributing; the team is currently three people deep on it. Tereza committed to a status update Monday, expecting roughly 80% of the table clean with ~20% still needing manual address/detail verification. Separately, she's coordinating with Dr. Max's accounting team to add an Axapta reference number and a customer-vs-vendor distinction to the same knowledge base — the base will grow but stays in Excel for now rather than moving to a proper system. Jan Sovka offered Filip Černý's support if the manual pass proves too slow, while acknowledging the activity is necessary given messy legacy data with no remaining owner to consult.

### Housekeeping close-outs

A batch of previously-tracked small issues were confirmed resolved and cleared from the working notes: an invalid-certificate test issue (was a VUMI-side bug, not BigHub's), an inventory-potency fix (Filip Černý confirmed shipped), a minor date-format bug (fixed last week), and the reklamace-headliner-with-supplier issue (resolved outside this call). The Hartmann invalid-contract issue turned out not to be a legal matter — Dr. Max's business department will simply have the contract re-signed (Lukáš Szücs).

### Freight invoicing (fakturace dopravy) timeline alignment

Petr Sláma firmed up his review commitment to next week (previously "mid-September"). Jan Kopecký confirmed Dr. Max's side has built to the latest MOC-level spec and will deploy to UAT soon, though the internal analysis of implementation days hasn't happened yet. Petr Sláma pushed for a concrete two-sided timeline (when BigHub will be done vs. when Dr. Max's dev needs to start) so both teams can align sprints rather than block on each other — **Jan Sovka does not have this and deferred to Jindřich/Alana**, committing to chase it down. Jakub Turner noted BigHub's side is developed but integration timing depends on "Boomy" [name/system unclear from transcript, needs verification] more than on BigHub.

### Swagger / API change coordination

An older open item — whether "Boomy" had incorporated the previous freight-invoicing Swagger update — remains unresolved; Lukáš Szücs recalled Kopecký commenting in a thread that it would go through with the developer, but nobody confirmed directly on the call. Separately, the team agreed a lightweight change-notification process going forward: whenever a Swagger endpoint changes, post the link and a summary of the change to the shared group so everyone stays in sync. Jakub Turner committed to posting the current freight-invoicing Swagger by end of this week (confirming nothing in fakturace dopravy changed today).

### Jump Server access (stalled ~1 month)

Jan Kopecký reopened a month-old, silent topic: the plan for BigHub to get direct (jump-server) access to Dr. Max's logs — which also reaches their Mongo archive — instead of routing every check through Dr. Max's team. Jakub Turner wasn't across the topic ("Honza" had apparently owned it on BigHub's side); Lukáš Szücs confirmed on the spot that it "definitely hasn't moved." No new owner was assigned on the call.

### Reklamace mobile app demo (Filip Černý)

Filip walked through the app live: scan a shipping label → Accepta lookup returns product info → operator confirms/adjusts quantity → photos any damage → optional note → submit → returns a reklamace number. Also demoed the second flow, "receipt with reservation," which writes into Axapta and returns a case number. Reception was positive — Petr Sláma and Tereza Foltová both called it clean and simple, with the only issue being an English-language error message on an invalid label (a known, already-queued localization fix, not urgent). Petr Sláma asked to have the invalid-label screenshot sent to Teams so he could investigate the specific data mismatch.

**Auth approach**: for the testing phase, Jakub Turner will issue hardcoded per-user logins (starting with Tereza) rather than wait for Entra ID/OAuth — Jan Kopecký flagged Entra ID integration as a likely friction point to resolve in parallel, not a blocker. Petr Sláma clarified his interest in per-user logins is about traceability in Axapta's logs (who did what), not access security. Target network for testers: Dr. Max's internal network, VPN, or in-warehouse WiFi — Petr Sláma believes it'll be their local network in practice. Jan Sovka's team agreed to note in the minutes that per-tester access should be live before next week so Jana can start testing the moment she's back from vacation.

**API gap flagged**: Jan Kopecký asked whether the reklamace API returns the "odběratel" (recipient/customer) field yet — it doesn't currently. Filip Černý and Jakub Turner agreed to add it, targeting the same day, so Dr. Max's side (referred to as "Boomy") sees it too.

### Marek's introduction to ViaPharma

Jan Sovka formally introduced Marek Pillár to the ViaPharma team as the new BigHub team member taking ownership of the Dr. Max account, with a product/business-analyst background. This is Marek's first introduction specifically to the ViaPharma-side contacts (he was introduced to core Dr. Max/vendor stakeholders on 2026-09-01).

## Decisions Made

- OAuth for the reklamace mobile app stays out of scope until after the Phase 1 demo — deferring it was agreed upfront and reconfirmed; Dr. Max/ViaPharma raised no objection.
- Testing-phase authentication will use hardcoded per-user logins issued by Jakub Turner; Entra ID/OAuth integration proceeds in parallel without blocking test rollout.
- Going forward, any Swagger endpoint change gets proactively posted (link + change summary) to the shared group rather than discovered passively.
- The reklamace app is cleared to move into ViaPharma-side testing — target before next week, so Jana can start immediately on her return from vacation.
- The "odběratel" (recipient) field will be added to the reklamace API, targeted same-day.

## Action Items

- [ ] **Jan Sovka**: Get a concrete two-sided freight-invoicing timeline (BigHub completion vs. Dr. Max dev start) from Jindřich/Alana and relay to Petr Sláma — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Jakub Turner**: Post the current freight-invoicing Swagger spec to the shared group — due end of this week (~2026-09-04/05) — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Jakub Turner**: Issue hardcoded test logins for the reklamace app, starting with Tereza Foltová, then Jana before she returns from vacation — due before next week — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Filip Černý / Jakub Turner**: Add the "odběratel" (recipient) field to the reklamace API — due 2026-09-03 (same day) — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Jan Sovka**: Follow up with Jan (Honza) Žižka on the DHL parallel-project overlap — carried from a previous session, still not done — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Lukáš Szücs**: Confirm status of the older freight-invoicing Swagger update with "Boomy"/the developer — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] `blocker` **Unassigned**: Push forward the stalled (~1 month) Jump Server access request for BigHub (also unlocks Mongo archive access) — no clear owner assigned on this call — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Tereza Foltová**: Deliver a status update on the 120-supplier consolidation table (~80% clean estimate) — due Monday (2026-09-08) — from 2026-09-03-viapharma-logistics-status-reklamace-demo
- [ ] **Petr Sláma**: Review the freight-invoicing scope and confirm dev sprint alignment — due next week (week of 2026-09-08) — from 2026-09-03-viapharma-logistics-status-reklamace-demo

## Open Questions

- What/who is "Boomy" — referenced repeatedly as the Dr. Max-side system or team that freight-invoicing/reklamace integration timing depends on. Needs clarification before it can be tracked properly.
- Is the "Lukáš" Filip asked to have added to the "CZE AXE BOOM AI" Teams group (via Lukáš Szücs) the same person as Lukáš Starenko (STK-028), whose Teams/Swagger-group access is already an open item from 2026-09-02? If so, this may be the resolution path for that item.
- Jakub Turner appears actively engaged in reklamace-app backend work (OAuth, login design, Axapta integration) in this meeting — this sits awkwardly next to ASM-007 (Decided, 2026-09-02), which concluded Turner works only on MaxBuddy and Jura Brázdil solely owns reklamace. Needs PM reconciliation — see Routing Log.

## Sentiment & Tone

Positive and collegial throughout — practical problem-solving tone with visible trust between the two teams (multiple items resolved with "no objection" / "makes sense" rather than friction). The reklamace app demo landed well: both Petr Sláma and Tereza Foltová volunteered unprompted praise ("looks nice, simple"). Jan Sovka's framing of the supplier-consolidation grind as necessary-but-painful was met with agreement rather than pushback, suggesting the relationship tolerates acknowledging slow, unglamorous work without it reading as a delivery risk. Marek's introduction landed as a routine, warm handoff, consistent with the account's broader "team-building" narrative from earlier in the week.

## Routing Log

- **project-stakeholders**: Added STK-034 (Petr Sláma, new); enriched STK-001 (Marek Pillár), STK-002 (Jan Sovka), STK-006 (Filip Černý), STK-007 (Jakub Turner — role expanded), STK-012 (Lukáš Szücs), STK-013 (Tereza Foltová), STK-028 (Lukáš Starenko), STK-032 (Kopecký — full name/org resolved: Jan Kopecký, ViaPharma CZE).
- **project-assumptions**: Added ASM-012 (Decided) — reklamace-app test auth approach; ASM-013 (Decided) — Swagger change-notification process. Amended ASM-007 — Turner confirmed also active on reklamace backend, alongside Brázdil (PM confirmation: both attributions true).
- **project-knowledge**: Enriched Axapta entry with reklamace mobile-app flow and Jump Server context; amended Dr. Max/ČLH dev-side ownership map re: Turner.
- **project-daily**: Added 9 action items (Jan Sovka ×2, Jakub Turner ×2, Filip Černý/Jakub Turner ×1, Lukáš Szücs ×1, Tereza Foltová ×1, Petr Sláma ×1, unassigned blocker ×1 — Jump Server).
