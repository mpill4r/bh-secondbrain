---
last_updated: 2026-10-02
type: external
attendees: [Marek Pillár, Jindřich Tůma, Tereza Foltýnová, Petr Spilka]
recording_link:
---

# Logistics AI Initiatives: Green-Field Tracker Reset & Pricing-Clerk (Cenařky) Process Analysis

**Date**: 2026-10-02
**Attendees**: Marek Pillár (BigHub, PM Dr. Max account), Jindřich Tůma (BigHub/Dr. Max coordination), Tereza Foltýnová (ViaPharma CZE, logistics), Petr Spilka (ViaPharma CZE, warehouses, business owner of Reklamace)
**Type**: external
**Recording**: N/A (Teams transcript, ~37 min, Czech/Slovak)
**Previous session**: [2026-09-25 Logistics Part A/B split with Tereza Foltýnová](2026-09-25-tereza-foltynova-reklamace-focus-logistics-initiatives-table.md). This is the "2026-10-02 internal validation debate" agreed there.
**Meeting prep**: N/A

## TL;DR

Marek told logistics that the shared AI-initiative tracker rows from row 13 down are historical and carry no weight. Logistics treats the tracker as a green field: they replace those rows with their own prioritized list, with briefly stated benefits, in their SharePoint copy, and Marek moves the agreed rows into the master. Petr Spilka pushed the pricing clerks ("cenařky") as the biggest logistics opportunity. About 5–6 people per warehouse manually price and confirm supplier deliveries in Axapta, and he claims savings of hundreds of hours a month. What he needs first is a proper on-site process analysis, which no consultancy has done. Everyone agreed: if cenařky comes out top-priority with quantified benefits, BigHub (Marek) does the analysis whether the result is AI or plain automation. Realistic start is January, and Spilka's preferred observation windows are November–December or March.

## Continuity

- **From 2026-09-25 (Part B)**: Tereza's logistics list in the SharePoint copy is still "very rough" by her own words. It wasn't validated before this session; Spilka joined late and spent the session on cenařky. The validation-debate format effectively turned into a reset of how the list is built, not a review of its contents.
- **Cross-department tracker sharing ([[ASM-179]])**: Tereza referred to "the tracker you opened for everyone, the one nobody may write into" [translated from Czech]. The master is now visible (read-only) to departments, which appears to answer the open question.
- **Department backlogs by end of November** (Dudaško, 2026-09-24): Marek said the October–November round through all departments was kicked off with Tomáš Dudaško and Jindřich. Logistics is the first department to run it.
- **Reklamace value**: Spilka called the ~8 h/day Reklamace saving "a promise not backed by data", still with a question mark. That is the basis of the tracker's 425,000 Kč phase-1 value.

## Key Discussion Points

### The shared tracker is a green field

Tereza wanted to reconcile the logistics initiatives she drafted (copied from the tracker into the logistics SharePoint so they can write into it) with the master tracker. The master has extra rows with no department assigned. Marek explained:
- The shared tracker below row 13 is "old data that may not be fully true… I don't know what those rows are", a batch of historical data nobody works with, Dudaško included. It "has no weight" [translated from Slovak].
- Logistics can delete everything from row 13 down and fill it in again.
- For October–November Marek will go through every department the way he did the two top rows with logistics (Reklamace, Fakturace doprav): define a business owner, target, value and KPIs.

Jindřich added that the Word overview Tereza works from and the tracker must match. More importantly, logistics must decide which initiatives matter now, because they know what is small and what is big. Tereza agreed: "make a green field, throw all the points out and say: here are our 10 points we'll start solving together" [translated from Czech]. Her split of topics (e.g. e-commerce vs. core warehouse as separate items) may make the list grow.

**Tracker scope**: Tereza asked whether initiatives they run with "DOOM"/"Duo" belong in the tracker. Answer: no. The tracker is AI + BigHub only; Duo initiatives are kept separately. Tereza later called Duo "our AI initiative, but not BigHub's". *This is likely Deloitte's LLM platform ("Duvo"/"Duvio", [[ASM-187]]), so Duo is already being used for logistics topics. Unconfirmed.*

### Cenařky (pricing clerks): Spilka's case

Petr Spilka described the work:
- A group of ~5–6 people mechanically take information from Axapta, email and a shared drive. Using a "tangle of rules", they identify and confirm prices in Axapta. "The work is about nothing else" [translated from Czech].
- ~230 suppliers, each with its own inputs, outputs, rules and exceptions; the exceptions rarely change. Price lists are involved. Data comes from several sources, and the receiving price can differ from the final price because prices change in the meantime.
- Savings estimate: 2–3 people at the **Pavlov** warehouse. **Ostrava** has the same volume spread across ~6 people who aren't allocated to it, so it doesn't show up in FTEs. "We're talking hundreds of hours a month", vs. ~8 h/day for Reklamace.
- The earlier consultancy analysis (the March "Dr. Max initiative / project overview" Word document Tereza shared) covered only invoice entry/identification, roughly 5–10% of the work, and rated the benefit as low. Consultants (name heard as "Ablena", unclear) sent questionnaires, spent three hours on site and wrote two A4 pages.
- His view: with a proper process map, "80% of the work" could be automated via Power Automate, possibly by Dr. Max themselves. Licence is ~50,000 Kč/year, also usable for Reklamace. Someone on his side reportedly knows Power Automate (name unclear in the transcript), but he can't free them for one to two months and doubts the quality without experience. One supervisor would remain for errors and new suppliers.
- He sketched an end state: scan delivery documents at an OCR station, extract the data, identify and pre-price automatically, and run downstream steps once the warehouse lead confirms receipt. Roughly "80% automation, 20% AI, 1% human input".
- He doesn't care if the automated process is inefficient: "let it do it badly, but let it do it by itself… my feet won't hurt" [translated from Czech]. Jindřich pushed back: a single data source still matters, because multiple sources mean risk, as on Reklamace.

**AI vs. automation**: Spilka asked whether this belongs with BigHub at all, since it may be "just Power Automate". Jindřich: no problem if it ends up top of logistics' list with the biggest benefit. Whether it's AI or automation will come out of the analysis. Logistics owns the output and can hand it to their own Power Automate person or to BigHub. Jindřich can't decide whether Dudaško's budget covers non-AI automation and will raise it with Dudaško today. Spilka: "technically, automation always comes before AI."

**Marek's offer**: if logistics only needs the mapping, it's PM/analyst work. Marek can cover it himself without developers: a few workshops, user journeys and a process description. If the value is there, "I see no reason why we shouldn't do it" [translated from Slovak]. He stressed capacity is limited and initiatives will be about six times as many once all of Max is in, so added value decides. He also promised the analysis won't be wrapped up in a single day.

**Timing**: Spilka asked to pick a week when there's real traffic ("you go to the forest when mushrooms grow" [translated from Czech]):
- November–December is peak (last purchases).
- After New Year is a slow ("cucumber") season.
- March is the next good window.

Tereza thinks January is the realistic earliest start, given how many initiatives are running, "but don't let cenařky be forgotten".

### Process going forward

- Logistics (Tereza with Spilka) finishes the list with brief benefits (goal, business value, hours), the way Reklamace was done with Marek. Cenařky is top of mind. Tereza asks Marek when unsure.
- Jindřich: benefits decide priority, e.g. whether 1M Kč/year is a lot. Once the list exists, he says when BigHub can start, based on capacity.
- Wednesday logistics sessions stay; the list gets reviewed there if ready. Meanwhile Marek cleans the master so irrelevant rows "don't haunt it".
- Hourly rates: Tereza supplies hours; Spilka emails the hourly rate when needed.

## Decisions Made

- **Master tracker rows from row 13 down are historical and non-binding.** Logistics treats the tracker as a green field and replaces them with its own prioritized list. Rationale: nobody, including Dudaško, has worked with those rows; they are a data batch of unknown origin.
- **Logistics' SharePoint copy is the working list; Marek copies agreed rows into the master** (reconfirms [[ASM-178]]). Tereza: no other table, "there was terrible confusion".
- **The AI-initiative tracker is AI + BigHub only.** Initiatives run with "Duo" (likely Deloitte's platform) stay out of it.
- **Cenařky enters the logistics list like any other initiative.** If it ranks top with quantified benefits, BigHub (Marek) does the on-site process analysis regardless of the AI vs. automation outcome. Logistics owns the output and may implement it themselves (Power Automate) or with BigHub.
- **Priority across initiatives is driven by stated benefits.** Jindřich commits timing based on capacity once the list exists.
- **Cenařky analysis needs a high-traffic window:** November–December or March. Realistic start January at the earliest.

## Action Items

- [ ] **Tereza Foltýnová / Petr Spilka**: Finish the logistics initiatives list (green field) in the SharePoint copy, with brief benefits per item (goal, business value, hours), cenařky included and prioritized; ask Marek when unsure — next Wednesday session if ready — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Petr Spilka**: Email the hourly rate for the cenařky savings calculation — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Marek Pillár**: Clean the master AI-initiative tracker (rows from 13 down) so stale rows don't confuse departments — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Jindřich Tůma**: Ask Tomáš Dudaško whether non-AI automation (e.g. cenařky via Power Automate) can be funded from the AI-initiative budget — due 2026-10-02 — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Jindřich Tůma**: Once the logistics list is agreed, say when BigHub can start each item, based on capacity — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis
- [ ] **Marek Pillár**: If cenařky is prioritized, plan the on-site analysis for a high-traffic window (Nov–Dec or March) with Spilka — from 2026-10-02-logistics-initiatives-green-field-cenarky-analysis

## Open Questions

- Does Dr. Max's AI-initiative budget cover pure automation, or only work that contains AI? Jindřich to ask Dudaško.
- Is "DOOM"/"Duo" the same as Deloitte's LLM platform ([[ASM-187]])? If so, Deloitte is already active in logistics.
- Who is the consultancy behind the March analysis ("Ablena" in the transcript) and who is Spilka's Power Automate person ("OKT")? Names unclear.
- Cenařky analysis window: November–December (peak, now) or March? This competes with Reklamace and Fakturace doprav for Marek's time.

## Sentiment & Tone

Cooperative and pragmatic, with Spilka dominating the second half. He was energetic and frank, sometimes self-deprecating ("I took a lot of time with my short question"). He's openly sceptical of consultants who "broke their teeth" on cenařky with questionnaires, which is an opening for BigHub to show depth. He also put Reklamace's value in perspective ("a small saving to me"), which matters given Reklamace's already low tracker value (0.43M Kč phase 1). If cenařky delivers what he claims, it could become logistics' flagship and shift his attention away from Reklamace.

Tereza was apologetic about her "very rough" list and relieved by the green-field framing. She explicitly owned the next step ("it's on our side now"). Jindřich steered firmly toward benefits-driven prioritization and kept the AI-vs-automation question open rather than refusing. Marek managed expectations on capacity (six times as many initiatives coming) while signalling clear interest in cenařky.

Watch-outs:
- Spilka may now treat "BigHub will do the cenařky analysis" as a commitment ("can I remember that we agreed on a process analysis?"). Formally it's conditional on prioritization.
- Duo (likely Deloitte) is already in logistics as a parallel AI channel.

## Routing Log

- **project-assumptions**: Added ASM-230 (green-field tracker), ASM-231 (tracker AI + BigHub only), ASM-232 (conditional cenařky analysis), ASM-233 (automation budget, open). ASM-179 resolved; update note on ASM-187.
- **project-knowledge**: New entry "Cenařky (pricing clerks)"; Reklamace value caveat.
- **project-stakeholders**: Updated STK-014, STK-013, STK-003.
- **client-overview**: Ways of Working: parallel Duo AI channel in logistics.
- **project-daily**: 6 action items added; 2 closed.
- **project-lessons**: LL-78.
- **meeting-index**: Entry added.
