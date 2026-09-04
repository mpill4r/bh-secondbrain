---
last_updated: 2026-09-03
type: internal
attendees: [Marek Pillár, Jura Brázdil]
tldv_link:
---

# MaxBuddy/Chatbot/OCR Project Handoff with Jura Brázdil

**Date**: 2026-09-03
**Attendees**: Marek Pillár, Jura Brázdil
**Type**: internal
**Recording**: N/A
**Previous session**: N/A — new thread (ran immediately after 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync, same day)
**Meeting prep**: N/A

## TL;DR

A working-context handoff: Jura walked Marek through all three projects he personally owns — MaxBuddy, the Max chatbot, and a new early-stage OCR project for pharmacy equipment service protocols. Covered MaxBuddy's regulatory history (a frozen dosage-checking feature, now pivoted to expert-approved upsell recommendations), its phased canary-pharmacy rollout strategy, the org/access landscape (Teams channels, X-Manager gap, key people), and got Marek Teams access plus partial VPN access working.

## Key Discussion Points

### Jura's project portfolio

Jura currently owns three Dr. Max AI projects: **MaxBuddy** (oldest, pharmacist-facing upsell/dosage tooling), the **Max chatbot** (demoed earlier today — see 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync), and **OCR** — a new, early-stage project extracting data from pharmacy equipment service-inspection protocols. He has functional specs (Dr. Max-facing) and technical/programmer documentation for MaxBuddy and the chatbot, and will share both plus a zip of raw session logs (conversation-by-conversation records since April) — flagged as messy and large; explicitly advised Marek not to feed the raw zip to an AI tool without knowing its size first.

### MaxBuddy live walkthrough

Jura demoed his own tester environment (what pharmacists see): scan an e-recept or trigger an upsell ("příprodej") flow. On scanning, the system identifies the active ingredient and surfaces upsell suggestions from vendor-defined product groups — group membership is configured by Dr. Max's own DVH team, with BigHub adding supporting "arguments"/comments per group via a dedicated interface (example shown: Amoxiclav). E-recept lookups pull the real packaging from Farmis, swapped in over a placeholder.

### MaxBuddy's regulatory history — dosage-checking feature is frozen

MaxBuddy's original core idea was **dosage-checking**: flagging when a doctor's prescribed dosage was outdated against the latest SPC (package leaflet) guidance — motivated by legislation shifting dosing-error liability onto prescribing doctors. About six months into development, Dr. Max discovered this makes the product a regulated **medical device requiring certification**: any pipeline where patient data goes in and an LLM-derived recommendation comes out is prohibited without it — "no blackbox: patient data in, drug advice out." That feature is **frozen, not removed** — pending a possible future certification push. Development pivoted instead to **upsell/cross-sell recommendations**, which combine pharmacological knowledge but are reviewed and approved by an expert panel rather than generated directly by an LLM for a specific patient — the compliant path. Separately, BigHub is pushing (with SOS support) for anonymized receipt-data access to base upsell recommendations on actual purchase patterns — permitted, since anonymized data with no patient-specific medical inference isn't the same restricted category.

A related, already-running but not-yet-shared system: **SPC-change monitoring**, collecting periodic diffs to drug package leaflets (running ~2 months). Most changes (~99%) are noise (phrasing, formatting, grammar); dosage-paragraph changes are flagged critical. Jura plans to add an AI re-sorting pass before sending anything to Dr. Max, since the signal-to-noise ratio isn't good enough yet.

### MaxBuddy deployment strategy — canary pharmacies

MaxBuddy runs provisionally on 30 of ~600 pharmacies. Dr. Max originally wanted full rollout within 14 days; Jura determined this wasn't safe — best case, MaxBuddy itself would crash under load; worst case, it could take down the pharmacies' payroll/POS system — given no proper 1:1 test environment (the available virtual test environment is limited: single e-recept item only, ~16-second DB response time). This is what triggered the broader AKS infrastructure effort started in July. Rollout plan: the same ~20-30 pilot pharmacies (deliberately chosen for younger, more technically flexible pharmacists comfortable with things changing under them) serve as a permanent **canary environment** for new versions — validated live there first, then rolled to the remaining ~580.

### Platform consolidation

MaxBuddy started as a standalone build. Viliam Gago ("Vil"/"Will") has been building shared platform infrastructure meant to host multiple Dr. Max AI use cases centrally (unified spend tracking, dashboards, etc.) — currently only the chatbot's document-search use case actually runs on it. Once the new AKS sandbox is live, Jura takes over from Viliam and migrates MaxBuddy onto the same platform.

### Org landscape and access

Jura walked through the people and channels around MaxBuddy:
- **Lukáš Szücs** — nominally "PM core" for MaxBuddy, but Jura characterized him candidly as more of a CC'd/copied presence than an actively driving one.
- **Vláďa Tvarůžek** — BigHub's primary infra contact, handles day-to-day infrastructure requests.
- **Martin Hrášek** — higher-tier/BDC infrastructure escalation contact; bigger tickets, more authority, everything takes longer at that level.
- **Luboš Vosmek** — the Dr. Max-side business owner and original motivator behind MaxBuddy; described warmly, is positive on the analytics work so far, and has enough standing that a DVH escalation through him resolves in a day what otherwise takes months.
- **The DVH (Data Warehouse) team**, and specifically a contact Jura named as "Machata" (surname uncertain) — described as extremely inflexible and slow: a trivial one-column database change ticket takes a week just to file and 2-3 months to resolve, unless escalated through Luboš Vosmek directly.
- **Pharmis** — the external vendor building Dr. Max's pharmacy system, written in Delphi (described as archaic/unmaintainable by modern standards); engaged only for integration needs or incidents (e.g. when a pharmacy stops syncing to MaxBuddy).

Teams channels identified: **BigHubInfrastructureChat** (in Dr. Max's Teams — where BigHub developers, including Will, Jura, and a contact named "Duri," coordinate infrastructure; Marek was added, but channel history wasn't visible to him even after joining), and **MaxBuddy.DVH x BigHub** (coordination with the Data Warehouse team specifically).

**X-Manager gap confirmed**: Jura confirmed X-Manager (the formal ticketing tool BigHub was granted access to ~1 month ago) currently has essentially nothing in it for MaxBuddy — it's only being used for the new chatbot/REX platform. MaxBuddy itself still runs via email and Teams, with a weekly Wednesday sync. Historical screenshots of X-Manager tickets have informally been posted in the "LLM Platforma" Teams chat by Jura and Will rather than tracked anywhere central.

**Marek's access**: got added to the BigHub Infrastructure Teams channel (no history visible) and the LLM Platforma chat. VPN access is partially working — could reach the MaxBuddy Admin Interface (with a changelog dating back to April) but other resources (Filip Černý had shared some the day before) still didn't work as of yesterday.

### OCR project — early-stage

New, third project Jura owns: automating extraction from pharmacy equipment **service-inspection protocols** (legally mandatory inspections — automatic doors, air conditioning, etc.) — currently staff manually retype these into Excel, which is the time sink this project targets. Scope narrowed to one category first: automatic doors, two vendors, extracting door type/faults/branch address/follow-up requests from the (often handwritten) protocols via an LLM pipeline (~16 prompts) — Jura candidly called it "a fairly nonsensical system" given how messy the source documents are. Currently in a second feasibility-measurement round (first round handled what could be cleanly extracted; now tackling free-text notes). Target: production-ready in time for Dr. Max's November inspection cycle. Will eventually move onto the same shared platform once the new AKS is available. "OCR" is a working name, not literally OCR-only — mostly an LLM-based extraction pipeline over scanned/photographed documents.

### Practical asks

Jura would like BigHub to provision him proper Teams + (unclear — possibly Outlook, transcript says "na autě"/"on the car," likely a mishearing) app access — estimated at costing him about a minute of friction per day currently.

## Decisions Made

- (No new decisions — this was primarily context transfer. MaxBuddy's regulatory constraint and canary-rollout strategy are established prior decisions being relayed, not made in this call.)

## Action Items

- [ ] **Jura Brázdil**: Send Marek the MaxBuddy and Max chatbot specs (business-facing + technical/programmer docs) — from 2026-09-03-maxbuddy-chatbot-ocr-project-handoff
- [ ] **Jura Brázdil**: Send Marek a zip of session logs (since April) for MaxBuddy/chatbot — from 2026-09-03-maxbuddy-chatbot-ocr-project-handoff
- [ ] **Marek Pillár**: Continue troubleshooting VPN access — MaxBuddy Admin Interface/changelog now reachable, some other resources (shared by Filip Černý) still not working — from 2026-09-03-maxbuddy-chatbot-ocr-project-handoff (relates to the existing open VPN item from 2026-09-02-logistics-listing-team-sync)
- [ ] **Someone at BigHub**: Provision Jura Brázdil proper Teams (and possibly Outlook) app access — from 2026-09-03-maxbuddy-chatbot-ocr-project-handoff

## Open Questions

- Exact surname of the DVH-team contact referred to as "Machata" — low confidence, single mention.
- Who "Duri" is (member of the BigHub Infrastructure Teams channel) — role and full name unknown, single mention.
- What Jura meant by wanting access "na autě" ("on the car") — likely a mishearing/mistranscription of something else (possibly Outlook), not literally a vehicle system.

## Sentiment & Tone

Informal, candid, high-trust working session between two BigHub colleagues rather than a formal status meeting — Jura was unusually frank about organizational friction (Lukáš Szücs's limited engagement, the DVH team's slowness, distaste for Teams as a tool) in a way he wouldn't likely be with the client present. No tension between Marek and Jura; genuine peer-to-peer knowledge transfer, with Jura proactively flagging what's usable vs. not (e.g. warning Marek off blindly feeding raw session logs to an AI tool).

## Routing Log

- **project-stakeholders**: Added STK-040 ("Duri", low-confidence); enriched STK-001, STK-011, STK-012, STK-016, STK-026, STK-027.
- **project-assumptions**: No new entries — context transfer, not new decisions.
- **project-knowledge**: Added the OCR project entry; enriched MaxBuddy (regulatory history, deployment strategy, platform consolidation); added Communication Channels & X-Manager coverage gap entry.
- **project-daily**: Added 4 action items.
