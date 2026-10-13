---
last_updated: 2026-10-13
type: external
attendees: [Tomáš Burda, Radim Švarc, Jindřich Tůma, Marek Pillár]
recording_link:
---

# TEO 2027 Initiatives with Tomáš Burda — Power-Outage Notifications, Driving Logbook & "Focus on OCR First"

**Date**: 2026-10-13 (Tuesday)
**Attendees**: Tomáš Burda (STK-025, Dr. Max CZE — head of the technical department, TEO), Radim Švarc (STK-041, TEO — present, silent after the greeting), Jindřich Tůma (STK-003, BigHub), Marek Pillár (STK-001, BigHub)
**Type**: external
**Recording**: N/A (transcript, ~52 min, Czech/Slovak)
**Previous session**: [2026-10-01 TEO/OCR sync](2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors.md) (no Burda) · related: [2027 outreach](../../documents/client/2026-10-06-lexie-new-departments-szucs-brief.md)
**Meeting prep**: [2026-10-13 Burda prep](../prep/2026-10-13-burda-teo-2027-initiatives-meeting-prep.md)

> **Transcript note**: "Beecamp" = BigHub; "EAN iniciativy" = AI iniciativy; "Tomáš Drožek / Dudačko" = Tomáš Dudaško; "DEU, DUO" = Duo ([[ASM-187]]). Lines labelled "Marek Pillár1" at 35:56 and 36:21 are **Jindřich Tůma** (Czech; he mistakenly says "pane Dvořáku"); at 50:12 it is Marek. "Rozumím. Pane Burda, je" (19:47) is Jindřich. In the long 29:18 block, from "Ale to já si zrovna jako myslím…" on, the speaker is **Burda**.

## TL;DR

Marek opened the 2027 initiative collection with TEO. Burda brought one ready-made, already-analysed candidate: **automating power-outage notifications** for pharmacies (~250 so far this year, ~300/yr across ~600 pharmacies), where the value is preparedness and key-person risk rather than time saved. Late in the call he added a second, company-wide idea: a **driving logbook (kniha jízd)** generator (he spends ~3 h/month on it). He was clear that TEO's priority is the **current OCR project, ideally sooner than "next year"**, and that he won't submit 10 initiatives because his team can't co-develop and test them. Next: Marek drafts the BQ rows and Burda comments by e-mail; Marek + Jindřich send an overview of what BigHub automates elsewhere.

**Continuity with 2026-10-01**: Burda's cost concern didn't come up; the OCR work is his top priority. His BQ row for OCR is in the master tracker (Marek confirmed he moved it there right after their e-mails). Burda didn't comment on the spring 2027 proposal.

## Key Discussion Points

### 1. Opening: how the 2027 collection works

**Marek** framed the round: BigHub and Jindřich collect improvement ideas per department for 2027 (AI or data, not only AI). Each gets defined, quantified (BQ: return, effect), then prioritised with Tomáš Dudaško, followed by discovery and development next year.

### 2. Burda's candidate: power-outage notifications

**Burda** shared TEO's Excel of known pharmacy power outages:
- **Sources**: mostly **standardised e-mails from the distributor** (e.g. EGD notices by EAN of the supply point + address); sometimes **free-form landlord e-mails** (e.g. "Kaufland service day"), occasionally with the information in an **attachment**; sometimes a phone call.
- **Today, all manual**: the energy specialist (energetik) identifies the pharmacy / středisko (by address or supply-point EAN), logs it in the Excel (what, when, pharmacy, regional director, technician, recipients in column J, when sent, notes) and forwards the e-mail to the středisko address (e.g. 293), the technician, the regional director, with the facility mailbox in CC (copy-paste).
- **Volume**: ~250 so far this year, so ~300/yr; Dr. Max has ~600 pharmacies, so about half have an outage each year. The Excel has a "vliv na provoz" (impact on operation, i.e. closing) flag.
- **Vision**: read the e-mails (and attachments), identify the pharmacy and recipients, send automatically; first with human validation, later fully automatic once trusted.

**Value** (Burda, after Marek asked whether the time saving justifies BigHub capacity):
- Time saved is small ("nothing dramatic").
- The real value is **preparedness**: otherwise 8 pharmacists turn up with nothing to do for half a day, or IT has to drive out because a server didn't restart. With notice, one person waits for power to return, checks the PCs, and calls the rest in.
- **Key-person risk**: one person does this. If they're off sick for a month or two, ~30 pharmacies would "go dark without warning".
- Possibly just a script, with AI only for the free-form landlord e-mails. Burda's guess: ~3 MD for BigHub given the Reklamace e-mail agent, "put it in May".
- TEO's Excel already documents the process; Burda can send sample e-mails. He considers it "90% described".

**Jindřich**: the effort side matters too. BigHub already has a similar e-mail pipeline in Reklamace, so the effort would be much lower, which can get a modest-benefit item selected.

### 3. Burda's stance: focus, not a long list

**Burda**:
- TEO's priority is the **OCR project**, "and if it could be sooner than over the whole next year, we'd be glad."
- He won't submit 10 initiatives: each needs a client-side partner with time to test and answer questions daily, and running many in parallel "slows us down rather than moves us forward". His experience is that IT projects stall near production and MDs keep growing.
- He hopes selection doesn't work as "submit 10, get 20% picked".
- **TEO team**: of 10–12 people, only two handle regular processing (Michaela Albrechtová; **Kocián** in Prague, who will join the OCR project with his inspections). The other eight are field technicians (building pharmacies, repairs, suppliers, authorities): human-factor work that AI won't solve.
- He doesn't know what AI can do, so he can't spot candidates. He asked BigHub what it automates elsewhere, so TEO can recognise similar processes.

**Jindřich** (reframing after Marek's capacity remark landed badly):
- BigHub doesn't decide priorities; Dr. Max's business does. By end of November (maybe end of year) Tomáš Dudaško and management review all departments' initiatives and pick about ten for next year. Items not picked stay in the register for later.
- The register is cross-country (e.g. a Polish automation could be reused in CZ).
- Departments are owners of their initiatives; BigHub only helps meet the criteria (benefit, KPIs, how it will be measured).
- Many departments want an analyst to map their processes; he will discuss with Dudaško using external analysts (BigHub, Duo) where departments lack time.
- Dr. Max is starting an **AI-adoption programme** (regular newsletter, intranet).
- Expects that in January every department will be pulling BigHub towards itself.

**Marek** apologised that his capacity remark sounded dismissive; he meant only that he'll collect ~30 items from ~10 meetings and management will pick the highest-impact ones. A cluster of cheap initiatives (e.g. preparing for closures and unexpected events) can also score well.

### 4. Next step on the outage row

**Marek** initially proposed a 30-min session to fill the BQ row. **Burda** preferred to start from a draft: BigHub writes keywords from today, sends it, he expands and comments, a few rounds by e-mail. Marek agreed.

**Burda** noted that the master tracker hadn't reflected what they agreed separately for the OCR row; **Marek**: he put it there right after their e-mail exchange.

### 5. Lexie for TEO's manuals

**Jindřich** explained Lexie (knowledge base over a department's documents, rolled out across departments). **Burda**: TEO has ~200 manuals on the intranet. **Marek**: Lexie works like ChatGPT over your own files only, doesn't invent, cites sources. Burda found it appealing; no request made.

### 6. Driving logbook (kniha jízd)

**Burda** asked if BigHub has anything that writes the driving logbook from where he went, where he refuelled, which towns he drove to in the month, and start/end km. He spends **~3 h/month** reconstructing it from fuel receipts. **Jindřich**: not here, but something similar exists elsewhere; probably many employees with company cars do this. **Marek**: a good company-wide candidate (applicable in CZ and beyond); he'll add it as a row and send it to Burda for review, possibly with Burda as owner. Marek's "1,000 drivers × 3 h = 3,000 h/month" was illustrative, not data.

## Decisions Made

1. **TEO's 2027 submissions**: power-outage notifications (Burda's prepared candidate) plus a company-wide driving-logbook idea. No long list.
2. **BQ rows drafted by BigHub, refined by Burda by e-mail** (no extra meeting).
3. **OCR remains TEO's top priority**; Burda would welcome it sooner.
4. **BigHub sends Burda an overview** of what it automates elsewhere ("a taste"), to help TEO spot candidates.

## Action Items

- [ ] **Marek Pillár**: Draft the BQ row for TEO power-outage notifications (sources, volume ~300/yr, preparedness and key-person-risk value, validation-first approach, reuse of the Reklamace e-mail pipeline) and send it to Burda for comments; ask him for sample e-mails (EGD + landlord) — from 2026-10-13-teo-2027-initiatives-burda-power-outages-logbook
- [ ] **Marek Pillár**: Add the driving-logbook (kniha jízd) row (company-wide candidate, Burda ~3 h/month) and send it to Burda for review — from 2026-10-13-teo-2027-initiatives-burda-power-outages-logbook
- [ ] **Marek Pillár / Jindřich Tůma**: Send Burda a short overview of what BigHub automates for Dr. Max elsewhere (Reklamace e-mail agent, Listing, Lexie, OCR …) — from 2026-10-13-teo-2027-initiatives-burda-power-outages-logbook
- [ ] **Tomáš Burda**: Send sample outage e-mails; comment on the drafted rows — from 2026-10-13-teo-2027-initiatives-burda-power-outages-logbook
- [ ] **Jindřich Tůma**: Discuss with Tomáš Dudaško providing analyst capacity (BigHub / Duo) to departments that lack time to map their processes — from 2026-10-13-teo-2027-initiatives-burda-power-outages-logbook

## Open Questions

- How to quantify preparedness value (avoided idle pharmacist hours, IT call-outs, lost sales during unannounced outages)? Which KPI and how to measure it?
- How many outage notices come as free-form e-mails or attachments vs. standard EGD e-mails?
- Is the logbook a real company-wide pain? How many employees keep one, and who would own it on the Dr. Max side?
- Can the OCR project be accelerated, as Burda wants? (Production depends on BDC.)
- Does TEO want Lexie over its ~200 intranet manuals?
- Who is Kocián, and when does he join the OCR project?

## Sentiment & Tone

**Engaged but guarded; a moment of friction, recovered.**

- **Tomáš Burda**: well prepared and proud of it ("served on a silver platter"; "90% described"). Pragmatic and protective of his team's capacity; sceptical of initiative sprawl from past IT experience. He bristled when Marek questioned whether the outage case justified BigHub capacity ("then why are you asking us for more tasks?"). He relaxed once Jindřich reframed the process and Marek apologised. He ended warm, offering the logbook idea himself.
- **Radim Švarc**: silent after the greeting.
- **Jindřich Tůma**: did the heavy lifting on framing (business decides, effort matters, the register is cross-country), firmly respectful of Burda's priorities.
- **Marek Pillár**: clear opener; his value/capacity challenge came too early for a first-round collection meeting.

**Watch-outs**:
- Don't pre-judge an idea's worth in a collection meeting. Collect first, quantify later.
- Burda measures BigHub by OCR progress. Any slip there colours everything else.
- He wants a written draft to react to, not open-ended sessions.

## Routing Log

Confirmed by PM on 2026-10-13 (confirm all).

- **project-assumptions**: added ASM-271 to ASM-276; ASM-168 updated (stays Open)
- **project-stakeholders**: STK-025, STK-041; new STK-068 Kocián
- **project-knowledge**: TEO team structure; pharmacy power-outage notifications; 2027 AI-initiative selection
- **client-overview**: Ways of Working (client-side testing capacity; owners need AI examples)
- **project-daily**: 3 PM-owned items added; Burda 2027 item annotated; Burda BQ-figures item resolved. Burda's and Jindřich's items stay in this note.
- **project-lessons**: LL-91
