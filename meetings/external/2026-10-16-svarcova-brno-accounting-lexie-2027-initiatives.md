---
last_updated: 2026-10-16
type: external
attendees: [Renata Švarcová, Simona Vaxmonská, Jindřich Tůma, Marek Pillár]
recording_link:
---

# Brno Accounting (Švarcová) — Lexie over Accounting Directives, File-Transfer Monitoring Idea & Lexie for Pharmacies

**Date**: 2026-10-16
**Attendees**: Renata Švarcová (Dr. Max CZE, Brno accounting, STK-063), a colleague Simona Vaxmonská ("Simča", Brno accounting; name confirmed by PM 2026-10-22), Jindřich Tůma (BigHub / Dr. Max), Marek Pillár (BigHub, PM)
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: N/A (first meeting)
**Meeting prep**: [2026-10-13-svarcova-brno-uctarna-lexie-2027-meeting-prep](../prep/2026-10-13-svarcova-brno-uctarna-lexie-2027-meeting-prep.md) (prepared for 10-13; the meeting took place on 10-16)

> **Transcript note**: The date comes from Švarcová saying "15. 10., that's yesterday". The transcript is heavily garbled (mixed Slovak/Czech). Uncertain names are marked: the TAS owner at BDC (heard as "simona Ilík", referred to as "he"), the TAS vendor (heard as "Nate Group"), and the tool replacing GoAnywhere (heard as "TABID"). Some lines under Švarcová's label are her colleague talking.

## TL;DR

First meeting with the Brno accounting team. They want **Lexie over their accounting directives and procedures**. It must be accurate, cite the source document and its date, and flag archived (no longer valid) documents. Sources are SharePoint (the intranet) and her own folders on the shared drive. Jindřich said **TAS integration isn't possible yet**, but SharePoint and local files are fine. Marek gave no date, since BigHub's capacity is limited. For 2027, Švarcová says a new cloud accounting system arrives next year, so most accounting automation should wait. She named one solid candidate: **daily monitoring of the pharmacy → accounting file transfers**. She also suggested **Lexie for pharmacies**: staff ask accounting basic how-to questions. Jindřich will raise that with Vosmek. Follow-up: **Thu 2026-10-22, 14:00**.

## Key Discussion Points

### Lexie for accounting: what they want

- **Problem**: there are many central directives, internal accounting directives and procedures, so finding the right one is hard. Accountants ask Švarcová instead. The goal is: ask Lexie first, and come to her only if the answer is wrong.
- **Accuracy rules (Švarcová)**: Lexie must not invent anything and must answer only from the directives. Every answer shows a **link to the source** and the **document's date**.
- **Folder structure** she showed, on the shared drive, folder "Směrnice účetní":
  - Root: the ~10 directives currently valid for accounting.
  - Archive of older directive versions. Lexie may look there, but must **say explicitly** that the information is archived and no longer valid.
  - "Formuláře a pokyny": procedures (what to do, when, why), with its own archive.
  - "ISO standardní postupy": **must not be used** here. Lexie should instead use the current company-wide directives on the intranet ("Zaměstnanecké info"), always the current version.
- **Sources**: the company-wide directives are on the intranet, which is SharePoint (Jindřich clarified that). Some are also in **TAS**, but probably not all; Švarcová will check with the TAS colleague. Her own documents sit on the S: drive. She doesn't like SharePoint ("it's messy" `[translated from Czech]`) but would move everything there so BigHub takes it from one place.
- **Jindřich**: SharePoint and local data both work. **TAS doesn't work for now.** Several departments ask for it, and BigHub will look into it. Švarcová: TAS moves to a new version next year, and the vendor promises AI cooperation.
- She also wants to add links to CC manuals and guides on SharePoint, which are sometimes useful for accounting too.
- **Marek**: send the SharePoint links (or a list of all documents). BigHub then validates internally and estimates when it fits the roadmap. BigHub serves all of Dr. Max with limited capacity, so it won't be next week. He wouldn't guess at end of year vs. early 2027. Marek has no access to the internal share from his external laptop and will find out how BigHub can reach it.
- **How users reach Lexie (Jindřich)**: through the AI Platform website. You log in and see the apps assigned to you; for accounting, only Lexie for now.

### TAS

- TAS is an external document system used across the Dr. Max group. A person at BDC owns it across all entities (name unclear), and an external vendor sold and runs it. It holds contracts, directives (not all of them), and invoices and orders.
- **Contract expiry**: Jindřich mentioned another department wanting an overview of expiring contracts. Švarcová showed that TAS already supports custom views and filters (validity from/to). Anyone can ask the helpdesk for an "expired contracts" view. TAS can also set **reminders before a contract ends** (e.g. for lease options), but someone has to enter them; legal does that today. So this is **a training issue, not an AI case** ("the people who handle the contracts maybe don't know" `[translated from Czech]`).
- **Lease contracts**: "very sensitive, nobody will want to put them into any AI" `[translated from Czech]`. Accounting is building a lease-contract app in its accounting software ("Benefit" as heard) so it can book payments and share data with acquisitions.
- **Invoice-flow ideas (half-formed)**: check that an invoice went through the whole process (Eva does this by hand today); remind people about unapproved invoices; flag an invoice that arrives against an expired order. Duplicate invoices sent to the accounting mailbox should be caught **inside TAS**, because TAS reads the incoming mail.

### 2027 initiatives

- Jindřich explained the collection: one Excel row per idea, with the benefit quantified (time, money, people). It's the 4th week of collecting across all departments. Results go up to management and decide what gets done in 2027.
- **Švarcová**: not prepared, and no list yet. Accounting moves to a **new cloud version of its accounting software next year**, so building on the current system makes little sense.
- **Candidate: pharmacy file-transfer monitoring.** Pharmacies' Farmis systems send large numbers of files to accounting every day, landing in folders on the shared drive: issued invoices (PDF) and supplier invoices (PDF) daily, **~5 DBF files per active pharmacy** daily, and some files on the 1st and 5th of the month. Accountants only notice a missing file when they need it, and finding out why takes long, with ~20 people potentially chasing it. Idea: every morning, take the current list of open pharmacies, check what should have arrived, and **report what's missing**, ideally raising the IT ticket automatically. Closed pharmacies are fine (e.g. pharmacy 581, last file 2024). On 10-15 everything arrived. A request to IT for automatic monitoring went in when Romana left, but in practice accounting watches and files the tickets. **Caveat**: GoAnywhere, the current transfer tool, is being replaced from **2027-01-01** (new tool name unclear), which may bring better overviews.
- **AI skepticism (Švarcová)**: AI is being pushed everywhere, while some things only need hard-coded programming. Earlier simplification requests got no capacity, and AI may be needlessly expensive. **Jindřich**: management (Žák, Hoffman) is reasonable about it. If an idea turns out to be automation or digitalization, it's still pursued; it doesn't have to be AI.
- **Deloitte** is currently reviewing accounting processes, also with an AI focus. Jindřich: BigHub will work with Deloitte, "it goes hand in hand" `[translated from Czech]`.
- Švarcová asked what other companies' accounting teams use AI for. **Jindřich** will put together a list of typical use cases from other clients.
- **Marek**: think of 3–4 cases, then we'll quantify them together (added value, how to measure, hours saved or money brought in). Ideas are needed by **end of November** and prioritized with Dudaško.

### Lexie for pharmacies (new idea)

- Švarcová asked if pharmacies will get Lexie. Pharmacy staff ask accounting basic questions: how to make a credit note in Farmis, how to print Dr. Max vouchers. They often skip the long directives.
- Pharmacies have a **normal PC with Farmis**, so they could open Lexie on the AI Platform website.
- A pharmacy knowledge base could use in-house directives, ISO procedures, manuals, and **Mertová's e-shop order manuals**. That could also cut calls to the CC (which uses Lexie internally today).
- **Jindřich**: never considered, "it makes sense". He will discuss it with **Luboš Vosmek**.

### Next meeting

- **Thu 2026-10-22, 14:00**, Marek sends the invite. It covers both remaining Lexie questions and the initiatives. Švarcová's colleague leaves on Friday and has another holiday at the end of the month.

## Decisions Made

- **Lexie for accounting goes ahead on SharePoint + local files**, not TAS for now (Jindřich).
- **Lexie answer rules for accounting**: answer only from the documents, cite the source and its date, flag archived content as no longer valid; the "ISO standardní postupy" folder is excluded and the current intranet directives are used instead.
- **No delivery date promised**: BigHub validates and estimates after it gets the links.
- **Contract-expiry overview is not an AI case**: TAS views and reminders already cover it, via helpdesk and legal.
- **Follow-up meeting Thu 2026-10-22, 14:00.**

## Action Items

- [ ] **Renata Švarcová**: E-mail the SharePoint / intranet links for Lexie (accounting directives, procedures, manuals, relevant CC guides), or a list of all documents — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Renata Švarcová**: Decide whether to move her S: drive directives to SharePoint; check with the TAS colleague whether all directives are in TAS — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Renata Švarcová**: Think through 3–4 initiative candidates for 2027 before the follow-up — due 2026-10-22 — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Marek Pillár**: Send the invite for Thu 2026-10-22, 14:00 (Lexie + initiatives) — due 2026-10-16 — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Marek Pillár**: Find out how BigHub can reach the internal share / intranet documents from an external laptop — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Marek Pillár / Jindřich Tůma**: Once links arrive, validate Lexie for accounting internally and estimate where it fits the roadmap — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Marek Pillár**: Draft the "pharmacy file-transfer monitoring" row in the 2027 tracker (volumes, people, time spent), to quantify with Švarcová on 10-22 — due 2026-10-22 — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Jindřich Tůma**: Put together a list of typical accounting AI/automation use cases from other clients and send it to Švarcová — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives
- [ ] **Jindřich Tůma**: Discuss Lexie for pharmacies with Luboš Vosmek — from 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives

## Open Questions

- **Lease contracts and AI**: Švarcová says lease contracts are too sensitive for any AI. That cuts against Šišo's use case 1 (compare / extract lease contracts from TAS). Who decides?
- **Initiatives deadline**: Marek told Švarcová "end of November". The outreach e-mails gave departments **23 October**, with the full backlog due end of November. Which one holds for accounting?
- **TAS owner and vendor**: exact names (heard as "simona Ilík" at BDC and "Nate Group").
- **GoAnywhere replacement** (from 2027-01-01): which tool, and will its own monitoring make the file-transfer initiative redundant?
- **New accounting software** (cloud, 2027): which system and when? It gates other accounting initiatives.
- ~~**Who is "Simona"** in Švarcová's team?~~ Answered 2026-10-22: Simona Vaxmonská (role -tbd-).
- **Pharmacy Lexie**: who owns it (Vosmek? Mertová?), and which documents go in?

## Sentiment & Tone

Cordial, practical and somewhat guarded. Švarcová came with a clear, well-structured Lexie need: concrete folders, strict accuracy rules, citations and dates. That shows a detail-oriented owner who will judge Lexie on correctness. On initiatives she was **openly skeptical**: not prepared, the system change makes work now pointless, and "AI is pushed everywhere" when plain programming would often do and earlier requests got no capacity. Jindřich handled this well by reframing the effort as automation in general, backed by management. She warmed up after that: she asked for examples from other companies, offered the file-transfer idea with real detail, and came up with Lexie for pharmacies herself. The Deloitte review running in parallel makes BigHub one of two voices in this department. Jindřich did most of the talking; Marek framed the purpose and set expectations on capacity.

**Signals**
- She keeps her best ideas grounded in pain she sees (missing files, repeated pharmacy questions). Concrete follow-ups will work better than generic AI talk.
- Lexie quality is the trust test here. A wrong or uncited answer would confirm her skepticism.
- Capacity is tight on her side too: colleague away, month-end, and the Deloitte review.

## Routing Log

- **project-assumptions**: Added ASM-298 (Lexie for accounting), ASM-299 (no TAS for now; contract expiry not AI; lease-contract sensitivity), ASM-300 (file-transfer monitoring candidate), ASM-301 (Lexie for pharmacies).
- **project-stakeholders**: Updated STK-063 (Švarcová), STK-003 (Jindřich); added STK-076 Simona (low confidence).
- **project-knowledge**: Added TAS, GoAnywhere (pharmacy → accounting file transfer), Směrnice účetní; Deloitte updated.
- **client-overview**: §7 accounting systems change in 2027; §9 AI skepticism in accounting.
- **product-requirements**: Added REQ-004, REQ-005.
- **project-daily** (2026-10-16): 9 items (6 BigHub, 3 waiting); 2027-initiatives item annotated.
- **Conflicts left open (PM confirm all)**: lease contracts vs. Šišo use case 1; initiatives deadline (end of November vs. 23 Oct).
