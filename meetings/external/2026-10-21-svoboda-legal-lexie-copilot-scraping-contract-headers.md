---
last_updated: 2026-10-21
type: external
attendees: [Martin Svoboda, Legal department colleagues, Marek Pillár]
recording_link:
---

# Legal Department (Martin Svoboda) — Lexie vs. Copilot, Directive Search, Marketing Compliance & Contract-Header Autofill

**Date**: 2026-10-21 (inferred: prep created the same day; date not in the transcript)
**Attendees**: Martin Svoboda (Dr. Max CZE, Právní oddělení; business owner) with legal colleagues in the room "Praha Florentinum Rosa" (individual speakers not separable), Marek Pillár (BigHub, PM). Jindřich Tůma did not join.
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: N/A (first meeting)
**Meeting prep**: [2026-10-21-svoboda-pravne-oddelenie-lexie-2027-meeting-prep](../prep/2026-10-21-svoboda-pravne-oddelenie-lexie-2027-meeting-prep.md)

> **Transcript note**: all legal-side lines come from one room microphone ("CZ Praha Florentinum Rosa"); they are attributed to Martin Svoboda / the legal team. Míra Švestka is named as the working contact but it's unclear whether he was in the room.

## TL;DR

Legal is deciding between **Lexie and Microsoft Copilot** (which they're starting to roll out) and asked what Lexie adds. They brought three use cases: **(1) smart search over ~70 internal directives** (Dr. Max, ČLH, ViaPharma) — low value, units of hours a month; **(2) checking marketing materials against legislation**, including live public databases (SÚKL, Ministry of Agriculture health claims) — daily, ~50 % of one colleague's time; **(3) auto-filling contract headers from the commercial register / ARES by IČO in Word** — daily. Marek positioned (1) as a quick Lexie extension and (2)+(3) as separate 2027 initiatives needing a business case. **Business owner: Martin Svoboda; working contact: Míra Švestka.**

## Key Discussion Points

### 1. Lexie vs. Copilot

- **Svoboda**: Legal is going deeper into **Copilot** (a premium M365 tier; it sees the SharePoint and shared folders the user can access — exact setup known by IT). Before choosing a path, they want to know Lexie's added value over Copilot. They haven't tested these use cases in Copilot yet.
- **Marek**: Lexie is "ChatGPT searching only over the set we define", **role-based** (Legal sees only its own pool), answers **cite and link the source document**. It runs on the **AI platform owned by Tomáš Dudaško**: access and the data pool are managed centrally and flexibly, unified across Dr. Max, with **one development team** that extends it for them. Rules for current vs. archived documents are defined per department. Track record: live in customer care, extending to finance and others.
- **Svoboda**: Copilot can also share an agent with other people; the deciding factor is what works better for their cases.

### 2. Use case 1 — search over internal directives

- ~**70 directives** (Dr. Max, ČLH, ViaPharma), mostly **PDF** (some presentations); "higher tens" to hundreds of documents. Stored on the **intranet = SharePoint** (drmaxglobal.sharepoint.com); users see only the **current version** and don't need history.
- Example questions: how archiving of document XY is regulated; **which PPE a pharmacist must have** (find the right directive, then the pharmacist part — sanitary staff and warehouse workers are covered too, sometimes across several directives); **what an employee breaches by coming late**; (Care Day bonus — already covered by a benefits chatbot).
- **Not sensitive**: directives are accessible to all employees; fine for BigHub as consultants to see.
- Value: **low — units of hours per month** at most.
- **Petr Macháň** manages the intranet (Legal sends him directive updates) → he knows where and how they're stored.
- **Marek**: a simple Lexie extension, not a big project; needs folders, structure, what to include/exclude, quick testing. No dates promised.

### 3. Use case 2 — marketing-material compliance

- Legal checks marketing materials daily against legislation, internal manuals and sub-statutory rules in **public databases**: SÚKL (SPC/package leaflets, active substances), Ministry of Agriculture (approved health claims, e.g. "does cranberry have an approved health claim?"), others. They can list the exact URLs; some are **web forms** returning results on screen, others downloadable PDFs/Excel; **thousands to tens of thousands** of external documents, updated continuously.
- They don't want to download everything to SharePoint — Lexie should query the sources live.
- Should be **shareable with marketing**, so marketing pre-checks materials before they reach Legal. Example: "an ad for a sunscreen — which legal lines must / must not be there?"
- Value: **~50 % of one colleague's time** goes to reviews, part of it searching. Daily use.
- Svoboda asked whether MaxBuddy gets leaflets via Farmis or SÚKL — Marek to find out. (Harness: SPC is synced every morning from the DVH team's SPC API, which mirrors SÚKL.)
- **Marek**: feasible in principle; must validate whether it's a Lexie feature or a separate AI-platform component.

### 4. Use case 3 — contract-header autofill

- Template contracts need the counterparty header: name, IČO, DIČ, registered seat, signatory, bank account — from **justice.cz (commercial register)** and **ARES** (both public, no API key). Wanted: type the IČO and have it filled in **inside Word** (a plugin).
- Svoboda tried Copilot a few months ago: it couldn't fetch from the web, and even with a downloaded register extract it failed after 30 minutes.
- Daily use. **Marek** sees the most value here (automatic filling) and treats it as a separate workflow / product.

### 5. Prioritisation and 2027

- **Marek**: BigHub's capacity is limited; initiatives are collected for early next year and presented to Tomáš Dudaško by benefit vs. effort ("an hour a month isn't worth three months of work"). Proposed a dedicated session on use cases 2–3 with his framework (value, goal, savings); framed as "repetitive tasks taking good people's time", not "AI".
- Legal will discuss numbers within the team and can supply data for Dudaško.

### 6. TAS

- Legal uses TAS heavily and dislikes it ("a terrible tool"). The vendor has promised **TAS 5 with an AI agent** for document extraction for ~1.5 years; the launch keeps slipping.

## Decisions Made

- **Business owner: Martin Svoboda; primary working contact: Míra Švestka.**
- **Use case 1 = Lexie extension** (directives on SharePoint, current versions, role-based) — to validate with the developer and Petr Macháň.
- **Use cases 2 and 3 = separate 2027 initiatives** (not Lexie by default), to be quantified in a dedicated session.

## Action Items

- [ ] **Marek Pillár**: Send Legal a short recap of the meeting — due 2026-10-22 — from 2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers
- [ ] **Marek Pillár**: Ask Petr Macháň where and how the directives are stored on SharePoint (current-only?) and arrange access — from 2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers
- [ ] **Marek Pillár / Jura Brázdil**: Validate use case 1 as a Lexie extension, and whether live external sources (SÚKL, ministries) fit Lexie or a separate AI-platform component; reply to Legal with an indicative timing — from 2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers
- [ ] **Marek Pillár**: Answer Svoboda's question on MaxBuddy's leaflet source (DVH SPC API mirroring SÚKL) in the recap — due 2026-10-22 — from 2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers
- [ ] **Marek Pillár**: Schedule a dedicated BQ session with Legal on use cases 2 (marketing compliance) and 3 (contract headers); draft the 2027 rows — from 2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers
- [ ] **Martin Svoboda / Míra Švestka**: Estimate time savings for use cases 2–3 and list other repetitive tasks — from 2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers

## Open Questions

- Will Legal go with Lexie or Copilot for directive search? What tips the decision?
- Use case 2: Lexie feature or separate platform component? How to query web forms (SÚKL, ministries) reliably?
- Use case 3: Word add-in feasibility within Dr. Max's IT/security rules?
- Is Míra Švestka the knowledge-base owner for the directives?

## Sentiment & Tone

Open and practical, slightly testing. Legal came prepared with concrete cases and asked a fair competitive question (Lexie vs. Copilot); they've been burned by tools that over-promise (Copilot's failed register test, TAS 5 delays). Svoboda was candid that directive search is low value and the daily pain is elsewhere — the real opportunity for BigHub is use cases 2 and 3, if quantified. Copilot is an emerging internal alternative to Lexie worth watching.

## Routing Log

Confirmed by PM 2026-10-21 ("confirm all"):
- **project-stakeholders**: STK-062 (Svoboda) and STK-069 (Macháň) updated; added STK-085 (Míra Švestka).
- **project-assumptions**: ASM-327 (UC1 = Lexie extension), ASM-328 (UC2+3 = 2027 initiatives), ASM-329 (Copilot as alternative, open).
- **project-knowledge**: Microsoft Copilot at Dr. Max; TAS 5.
- **client-overview**: §9 Copilot as an in-house alternative.
- **project-daily** (2026-10-21): 6 items; 2027-initiatives item annotated.
- **2027 backlog** (OneDrive): 2 rows added (marketing compliance, contract headers).
