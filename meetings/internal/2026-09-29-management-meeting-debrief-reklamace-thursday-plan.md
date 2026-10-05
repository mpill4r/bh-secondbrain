---
last_updated: 2026-09-29
type: internal
attendees: [Jindřich Tůma, Marek Pillár, Alana Sihelská]
recording_link:
---

# Internal Sync — Management-Meeting Debrief, Reklamace Thursday Plan & Spec-as-Contract

**Date**: 2026-09-29
**Attendees**: Jindřich Tůma (BigHub↔Dr. Max coordination lead, STK-003), Marek Pillár (AI Analyst / PM, STK-001), Alana Sihelská (BigHub, outgoing PM, STK-004; joined at ~07:10). Ján Kabát (STK-005) was expected but didn't join. Jan Sovka (STK-002) was away at workshops in Austria (UNIQA).
**Type**: internal
**Recording**: N/A (Fireflies transcript)
**Previous session**: [2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers](2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers.md)
**Meeting prep**: N/A

## TL;DR

Jindřich debriefed today's Dr. Max management meeting (CEO plus all department heads). The BQ benefits table landed very well. He escalated the BDC turnaround problem to the CEO, who stepped in, and BDC is already reaching out. He also flagged quiet competitive pressure from Deloitte, which is running its own AI initiatives at Dr. Max. The team locked the 2026-10-01 Reklamace agenda: Filip's AI email-thread demo, the data-source options Excel with a BigHub recommendation, and a spec sent by Friday 2026-10-02 with agreed changes or open questions. Decisions will be confirmed in writing, and the signed-off spec is treated as a contract, with later changes going through change requests. Tereza Foltová misrepresented Jindřich's words for a second time; the team will keep her close but put everything in writing.

**Continuity with 2026-09-23**: the two escalation items from last week are done. The AKS/BDC bottleneck was raised at today's management meeting and reached the CEO. The Reklamace reframe was discussed with Tereza on Friday. The continue-or-close management decision meeting wasn't mentioned; instead, Thursday's 10-01 session is now framed as the fix. The rozvozový list gap and the Sláma contract push weren't revisited.

## Key Discussion Points

### Management-meeting debrief (2026-09-29)

Jindřich attended in person: the top Dr. Max management meeting with the CEO and all department heads, 4 slides. He had two goals.

1. **Show what BigHub delivers.** The room's default narrative was "we've been waiting over a month for MaxBuddy and nothing is happening". He countered with two releases, order prediction deployed to production, the Max chatbot demo running, CC testing, and so on.
2. **Escalate BDC communication as high as possible.** He framed it as "not a negative escalation": BigHub has five requests open for MaxBuddy AKS, has been waiting ~6 weeks, and has no idea whether resolution is tomorrow or a month away. The CEO stepped in, and BDC people are already messaging Jindřich to set up a call.

**BQ benefits table**: management was "enthusiastic" about the benefits table, "a big plus". Jindřich said BigHub is already working on more AI projects through the benefits/KPI definition: logistics now, marketing and other departments next.

### Competitive pressure — Deloitte

Jindřich senses "a bit of jostling". Deloitte is running its own AI initiatives at Dr. Max, including something like an LLM platform. He compared it to what "Čuper" built at Rohlík (the name came out as "Duvo"/"Duvio", uncertain). Where it runs is unknown and he'll find out. There is also a request to hand BigHub's architecture write-up to Deloitte. Jindřich wants to validate with Tomáš (Dudaško) first that sharing it is OK, and reads the request itself as a signal that Deloitte is designing something. He was explicit that "it's definitely not that we'd be ending here in a month", but "we have to be very good at the work so they have no reason to replace us" [translated from Czech].

### MaxBuddy AKS and Maxie voicebot — BDC

Jindřich treats AKS as BDC's problem, not a BigHub delivery issue, now that it's escalated to the CEO. The **voicebot** is a separate open problem. Its BDC ticket has been open for 4 weeks. Instead of "it's configured", BigHub heard that BDC doesn't understand the request and asked for a meeting with Atlantis. Jindřich will schedule a joint meeting with Atlantis, ElevenLabs, BigHub and BDC ("for the hundred-and-fiftieth time"). He doesn't know whether the delay is really BDC's fault, missing inputs, or priority.

He worries the blame could land on Vláďa (Vladislav Tvarůžek, STK-016), who is "a really nice person" and acts as BigHub's communication buffer. BigHub can't see any tickets, so it can't track, escalate or prioritise its own requests. BigHub needs a ticket it manages itself.

### Reklamace — the one real problem, and the Thursday 2026-10-01 plan

Jindřich sees Reklamace as the only real problem across the portfolio. Logistics didn't understand what is and isn't needed or which decisions are open. The Thursday session has **three topics**:

1. **Show them their AI**: Filip Černý's email-thread logic, i.e. how emails fall through the thread. Filip said it should be done by Monday and it should be ready by Thursday; Jindřich will check the status. This answers logistics' complaint that they "don't see any AI".
2. **Settle the long-running data-source problem** with Marek's options Excel, which makes the options visible to everyone. Framing: "we've been talking about a solution for a while and neither side quite understands the other; here's a table; the decision is yours as the customer; our recommendation is in it" [translated from Czech].
3. **Commit to sending the spec by Friday 2026-10-02**, including the agreed changes, or open questions where nothing was agreed.

**Marek's Excel status**: he has expanded it heavily, with many where-to-store questions plus his recommendations. It goes to Filip by lunch for a technical-feasibility check, and the documentation should reach Filip by end of day. Bottom line of his recommendation:
- **Axapta** holds all critical data: accounts, addresses, main contacts.
- **Confluence or SharePoint** holds larger documents (the knowledge base) and references to Axapta keys.
- **Excel as a database** "definitely makes no sense; it's archaic" [translated from Slovak].

Sequencing: Marek reviews with Filip first, then a three-way sync with Jindřich before Thursday. Either Marek or Filip presents on Thursday; Filip's technical background is stronger.

Jindřich's reflection: the core difficulty was that everyone used "knowledge base" to mean something slightly different. Even his 1.5-hour session with Filip showed how interlinked it all is. Marek's read: the problem was never technical or delivery-heavy ("delivery is trivial"). It was a decision that was never actually made with the client, and it could have been made earlier. Marek admitted he partly got stuck because he didn't yet understand the domain himself.

Jindřich: "let's not cry over spilt milk." Talking to the client "like an idiot" ("I don't know why we're discussing this, it's in the spec") isn't OK. If they still don't understand the knowledge base after the fourth meeting on it, assume BigHub is explaining it badly and find another way. Recommend and explain the positives, meet them halfway, and be a partner without "crawling up their backside" [translated from Czech].

### Tereza Foltová — keep close, write everything down

Jindřich asked the team to keep Tereza close: communicate and give her whatever she needs. He feels she passes information on "a bit differently than it is", though he doesn't see a motive. On Friday she told him that he had told her BigHub doesn't want to do Reklamace. He denied saying it and, in case anything he said could be read that way, clarified his point: the AI project turned into a digitization project, and the people above should know and decide how to proceed. If they're fine continuing, BigHub continues. "My goal is that we don't meet in a month and someone tells me 'Sir, this isn't AI.'" [translated from Czech]. He says this is about the second time she has twisted information.

Alana: write everything down in emails or notes. "This has saved our asses about four times." [translated from Slovak]. Jindřich agreed that this needs to become standard practice. Marek confirmed the internal agreement: map all Axapta / knowledge-base problems, open them on Thursday, and email them for confirmation by Friday, so decisions and then the spec are on record.

### Fakturace doprav and logistics prioritisation

Alana worried that the Reklamace friction could spill over into the second logistics use case, carrier invoicing (fakturace doprav). If BigHub ended up leaving Reklamace, she was sure invoicing wouldn't happen either. Jindřich disagreed. Because he also sits on the Max side, he knows logistics *must* run AI initiatives and therefore has to cooperate with BigHub. The issue is misunderstanding and communication, which Thursday should fix.

Marek added that on Friday Tereza herself asked whether invoicing would be deprioritised. She proposed that once the Reklamace **blockers** are cleared, the team can move to invoicing: Marek defines it, hands it to development, and walks logistics through it. Marek's open question: developer capacity and allocation. Initiatives in the table are more financially interesting for Max than invoicing.

Jindřich: this is politics. BigHub wants to meet everyone's needs but keep priorities it can actually deliver. **The business sets priorities**; BigHub can recommend and steer. Be open from the start: "you're in the priority list, a bit lower, which means this tempo, and we can hold that tempo for the whole collaboration" [translated from Czech]. His longer-term goal ("shooting from the hip") is more FTEs and more projects at Max, but only after stabilising what's running: deliver at least half of the current items and get adoption going.

### Timelines and phase value for logistics

Per Jindřich, Tomáš Dudaško is "very satisfied with everything". The AI platform is running, and he has the benefits Excel and the per-project timelines he asked for. Tereza wants a timeline for the **whole** project. Jindřich tried to sell a rolling 4-week outlook because everything will change, but they want the full picture, so he'll produce a high-level version.

Marek connected this to the Reklamace spec. It still carries phases 1–4 with notes (e.g. Egrmaierová's comments: no SP label exists, visible vs. invisible defect). The later phases aren't properly specified or agreed and need discovery sessions. What is missing, at least for logistics, is each phase's "system seller": the main value driver that justifies doing the phase. He'll give them outlook anchor points next week, but those aren't load-bearing yet. Marek wants to do this with every initiative owner, as he's doing with Neuman tomorrow. He'll own it but needs close cooperation with Jindřich on capacity, so he doesn't promise anything BigHub can't staff.

### Spec approach — comments, open items, and spec-as-contract

Jindřich asked how the spec handles comments. His habit is a clean final document with no comments, with outstanding items tracked separately, e.g. by email.

Marek's approach:
- Take Honza's (Jan Sovka's) original file.
- Work in the comments; unanswered ones become questions for Sláma or the business owner.
- Fold in the roadmap comments.
- Leave every open item for the business-owner discussion (meeting, email or comments).

The goal is a final file that is agreed and then developed against. After that, the original isn't edited. Changes go through syncs and email, as change requests and tickets. If a summary is needed at the end, write a short product spec, like the one Jura is doing now. "The base spec is the contract between us and the client and should be as complete as possible at the start" [translated from Slovak].

Undecided items, such as where Reklamace data lives (Confluence, SharePoint Lists, …), stay **yellow-highlighted** until Thursday and the client's email reply. Marek doesn't expect a 100%-approved spec by the end of the week, but it should be with the client, open questions included. He doubts Sláma can answer between a Thursday-morning Excel walkthrough and Friday.

Jindřich agreed the process is right: open points become questions, get filled in by agreement, and go out by email ("these parts changed, please check"). He briefly considered a hard "no progress until confirmed" rule and dismissed it as too radical. What he wants to avoid is the recent pattern: logistics keeps urging, then Sláma doesn't accept or react to the comments. Marek: keep it simple, ideally email: "what's written is given". His practical CR example: Sláma finds in testing that something doesn't suit him although it was specified that way. BigHub says it can fix it for +3 MD, and Sláma replies in writing that he's OK with the MDs.

### Adoption campaign

Jindřich has to push harder on the adoption campaign strategy, which slipped last week. He needs to check whether Sony (Sony Vu Hong, STK-022) is back from ~2 weeks of vacation. Sony should prepare a newsletter for Max. Sony doesn't know yet, but it was promised to Dudaško.

### Logistics / Listing — Marek's 2026-09-30 schedule

Marek will be at Max until lunch tomorrow. First a quick meeting with Tereza, where she shows what she has collected on initiatives since Friday. Then the quasi-workshop with Petr Neuman and Michaela Vdovicynová (Listing). He'll likely go to BigHub for lunch.

### Admin — calendars, meeting reshuffle, Fireflies

- Jindřich is reshuffling meetings. Alana will cancel her Tuesday/Wednesday internal sync and the Thursday logistics invite; Jindřich sends new invites. Alana held "the board" this morning, and it went well.
- Marek will put blockers and personal time in his calendar so Jindřich can plan against it. Jindřich: as the team grows, the calendar is the source of truth.
- Alana asked Marek to send a four-point Fireflies summary to the business group, so the absent Kabát and Sovka aren't left uninformed.
- Fireflies: Jindřich wants it for his own meetings too. Only one Fireflies bot joins a meeting regardless of account count, but anyone with an account can view recaps and recordings. Marek offered a shared login but was wary of it being flagged, and noted it costs only ~$10/month. Jindřich will look into it.

## Decisions Made

- **Reklamace 2026-10-01 agenda is fixed at three topics**: (1) Filip's AI email-thread demo; (2) the data-source options Excel with BigHub's recommendation, decision left to the client; (3) a commitment to send the spec by Friday 2026-10-02 with agreed changes or open questions.
- **Decisions go on record in writing**: after Thursday, agreed decisions are emailed to logistics for confirmation by Friday 2026-10-02. Team-wide practice from now on: write everything down, per Alana's advice after Tereza's misrepresentations.
- **Spec is the contract**: once agreed, the base Reklamace spec isn't edited. Later changes go through syncs and email as change requests with MD cost and written client approval. Open items stay yellow-highlighted in the spec until answered.
- **Marek's recommendation for supplier data**: Axapta holds critical data (accounts, addresses, main contacts). Knowledge base and larger documents go to Confluence or SharePoint. Excel isn't used as a database. Filip validates feasibility before Thursday.
- **Business sets priorities across logistics initiatives**: BigHub recommends and states openly the tempo each priority level gets. Fakturace doprav follows once the Reklamace blockers are cleared, pending capacity.
- **Tereza's whole-project timeline**: Jindřich will deliver a high-level whole-project version on top of the rolling 4-week view.

## Action Items

- [ ] **Marek Pillár**: Send the expanded Reklamace options Excel to Filip Černý by lunch for a technical-feasibility check — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Get the Reklamace spec draft to Filip Černý by end of day — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Set up a Marek / Filip / Jindřich sync on the options Excel before Thursday — due before 2026-10-01 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: After the Thursday session, email logistics the agreed decisions for confirmation, and send the Reklamace spec with agreed changes or open questions (yellow-highlighted) — due 2026-10-02 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Meet Tereza Foltová at Max to review the initiatives she has collected since Friday — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Run the Listing workshop with Petr Neuman and Michaela Vdovicynová — due 2026-09-30 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Define the value driver ("system seller") of each later phase with each initiative owner, via discovery sessions; give logistics outlook anchor points next week; coordinate capacity with Jindřich Tůma before promising anything — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Put blockers / personal time into the calendar so Jindřich can plan meetings around it — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Marek Pillár**: Send a four-point Fireflies summary of this meeting to the BigHub business group (for Ján Kabát and Jan Sovka) — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Check the status of Filip's AI email-thread demo for Thursday — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Validate with Tomáš Dudaško whether BigHub's architecture write-up may be handed to Deloitte; find out where Deloitte's LLM platform runs — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Schedule a joint voicebot meeting with Atlantis, ElevenLabs, BigHub and BDC — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Restart the adoption campaign: check whether Sony Vu Hong is back and brief Sony on the Max newsletter promised to Dudaško — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Produce a high-level whole-project timeline for Tereza Foltová — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Reshuffle the team's meetings and tell Alana Sihelská which invites to cancel — due 2026-09-29 — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan
- [ ] **Jindřich Tůma**: Look into a Fireflies licence / shared setup — from 2026-09-29-management-meeting-debrief-reklamace-thursday-plan

## Open Questions

- What exactly is Deloitte building (the "Duvo"-like LLM platform), where does it run, and does it overlap with the BigHub AI Platform?
- Is sharing BigHub's architecture write-up with Deloitte acceptable to Dudaško?
- Is the 4-week voicebot delay really on BDC's side, or were inputs or priority missing?
- How does BigHub get its own view of and control over BDC tickets?
- Developer capacity for Fakturace doprav after Reklamace, versus higher-value initiatives in the table ([[ASM-167]]).
- Does the continue-or-close Reklamace management meeting from 2026-09-23 still happen, or has Thursday's session replaced it?
- What did Tereza collect on initiatives since Friday (to be seen 2026-09-30)?

## Sentiment & Tone

Upbeat and collegial. Jindřich came out of the management meeting confident: "everything is going well so far", positive vibe everywhere except Reklamace. He was also sober about Deloitte and wants the team to stay sharp rather than complacent. The Tereza thread carried real frustration, voiced carefully ("strange", "I'm not saying it must be so"). Alana answered pragmatically, with some hard-won cynicism: write everything down. When Marek owned part of the Reklamace stall, Jindřich defused it immediately and redirected to partnership with the client, not blame. Marek clarified he wasn't upset, just describing the ideal. Overall aligned and supportive, with a clear shared plan for Thursday.

## Routing Log

Routed on PM confirmation ("confirm all"), 2026-09-29:

- **project-assumptions**: added ASM-185 (written confirmation of decisions), ASM-186 (spec-as-contract / CRs), ASM-187 (Deloitte), ASM-188 (voicebot BDC ticket), ASM-189 (business-set priorities; Fakturace after Reklamace), ASM-190 (later-phase value drivers; whole-project timeline); updated ASM-184 (spec sent 10-02 with open questions) and ASM-169 (BigHub storage recommendation)
- **project-stakeholders**: STK-003, STK-004, STK-006, STK-010, STK-013, STK-016, STK-022, STK-034, STK-051
- **project-knowledge**: added Deloitte, Spec-as-contract & change requests; updated BDC
- **project-daily (2026-09-29)**: 9 PM-owned action items (Jindřich's kept in this note only), Key Event, audit entries
- **project-lessons**: LL-68
- **meetings/index.md**: entry added
