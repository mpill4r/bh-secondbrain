---
last_updated: 2026-10-08
type: external
attendees: [Jindřich Tůma, Marek Pillár, Filip Černý, Petr Sláma, Tereza Foltová, Petr Spilka]
recording_link:
---

# ViaPharma Reklamace Sync — Data-Map Slip, "All Five Phases" Reconfirmed & Sláma's Capacity Limit

**Date**: 2026-10-08 (Thursday)
**Attendees**: Jindřich Tůma (STK-003, BigHub PM), Marek Pillár (STK-001, BigHub — Reklamace spec owner), Filip Černý (STK-006, BigHub — Reklamace / Fakturace dev); Petr Sláma (STK-034), Tereza Foltová (STK-013), Petr Spilka (STK-014, ViaPharma CZE — Reklamace owner, newly joining the Thursday sync). Jana Egrmaierová (STK-044) excused.
**Type**: external
**Recording**: N/A (transcript, ~37 min, Czech/Slovak)
**Previous session**: [2026-10-01 ViaPharma Reklamace sync](2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review.md) · related: [2026-10-05 Žůrek next steps](2026-10-05-reklamace-next-steps-zurek-pilot-roadmap.md)
**Meeting prep**: N/A

> **Transcript note**: two lines are mislabelled by the tool. At 27:03 the first half ("presne… my pokračovať rátame s tým…", Slovak) is Marek Pillár; Petr Sláma takes over from "Pan Sláma se hlásí". At 32:32 "No ne, Terko… tohle jsme slíbili a dodáme" is Jindřich Tůma, not Tereza. "Jan Eger" = Jana Egrmaierová; "Ruda" = Rudolf Žůrek; "pan Dudačko" = Tomáš Dudaško.

## TL;DR

The data map didn't move: Petr Sláma paused all Reklamace work this week because he assumed the management meetings might stop or reshape the project, and nobody had told him otherwise. He'll review the data-map Excel early next week, then the spec, then the simplified Fakturace Swagger, so the spec (and the 10-09 knowledge-base target) slips by about a week. A mid-meeting misunderstanding (Tereza heard "put Phases 3–5 to sleep") was closed firmly by Jindřich and Marek: **all five Reklamace phases are finished**, because the savings in the tracker assume all five; BigHub's work on Phases 2–5 is just much smaller, which frees capacity for other initiatives in parallel. Sláma put on record that the project is ~6 months behind its original April plan and he can work on only one thing at a time; anything in parallel needs logistics to reprioritise his other projects.

**Continuity with 2026-10-01**: Sláma's column-J feedback (due early week of 10-05) was not delivered, and Tereza's chase didn't unblock it. Phase 1 testing (extended by a week) is still not closed. The mailbox moved forward (created, reading works; write rights pending). Overall: delivery is stalling on the client side, and the "is BigHub continuing?" doubt resurfaced for the third time in three weeks.

## Key Discussion Points

### 1. Reklamace — data-map Excel and spec sequence

**Jindřich Tůma** asked whether Sláma had looked at the data-map Excel (the supplier-data sources table).

**Petr Sláma**: he did nothing this week. He was waiting for the outcome of the management meetings (IT and logistics management) that were supposed to decide "whether to continue at all, and how", including whether this stays an AI activity or becomes something else. "I honestly did nothing, because I was waiting." [translated from Czech]

**Tereza Foltová**: Tomáš Dudaško didn't attend in the end, so it became a logistics + BigHub meeting, and no decision was taken to stop or change anything. "We're carrying on."

**Jindřich**: Dudaško only wanted an information calibration, which happened. Whether the project is labelled AI or digital doesn't change the tasks: "nobody is stopping, moving or shifting anything." He listed Sláma's three open items: (1) the data-map Excel, the most urgent because BigHub needs to plan the data source and start building against it; (2) comments on the Reklamace spec; (3) the same for Fakturace doprav.

**Marek Pillár** clarified the sequence: the Reklamace spec (which he calls "the contract") is ready and reviewed with Filip, but sending it makes no sense while many points depend on the Excel's outcome. Once the Excel decisions are in, he'll send the spec for comments. He expects far fewer comments than in May, since much has been settled in these meetings. For Fakturace doprav, Filip has sent the simplified Swagger (built to Sláma's request); Sláma should look at it after the Excel.

**Filip Černý**: everything is in his cover note. The first proposal was "too complex" per Sláma, so this is a simplified one: "see if it's workable". Not the top priority.

**Sláma**: will look at the Excel "straight away" next week, then everything else, and let them know. He apologised: he hadn't been invited to the management meetings and didn't know the status.

**Marek** closed the topic: with Žůrek and Tereza it's agreed that BigHub continues on both initiatives, at least for the agreed phases, and then Phases 3, 4, 5 need specifying. "Nothing suggests this should end; quite the opposite." [translated from Slovak]

### 2. Phase 1 testing

The testing extension ended tomorrow (2026-10-09). **Tereza** hasn't closed it yet: she needs to confirm with Jana Egrmaierová, who spent many days in Prague on a large WMS project. She'll set a separate ~15-min wrap-up with Filip and Sláma.

**Jindřich**: Jana has already logged bugs and Filip has been fixing them; there's one bigger one. Plan the wrap-up so Filip can take it all on.

**Filip** is on vacation tomorrow (Friday), so the wrap-up goes to **Monday 2026-10-12**. Everyone agreed.

Not discussed: whether the 10-15–16 full UAT start still holds.

### 3. Shared mailbox (email agent)

Set up via Microsoft Graph API. BigHub only has **read** rights so far and has asked for **write** rights; still waiting. **Filip**: the mailbox exists and reading emails from it works. He'll chase again this afternoon if nothing happens.

### 4. Test phone

**Tereza** is chasing the test phone. It went through IT as a ticket (via Dušan), is processed and "on its way" to Brno, but with no delivery date. (Ms Zhurakivská isn't involved.)

### 5. Fakturace doprav — Canon scanner

**Tereza** thanked Filip for his scanner write-up and will contact the Canon person for a call. She asked who from ViaPharma should join to judge "what kind of scanner and what it must meet".

- **Sláma**: requirements must be defined by BigHub. He doesn't do technical hardware.
- **Filip**: the scanner won't talk to Axapta. It talks to BigHub's API, which talks to Axapta, so nothing changes for Axapta. ViaPharma needs someone from **operations** (screen size, where it's placed), not a technical person.
- **Sláma**: agreed. Jan Žižka should say where and how he wants it.

**Outcome**: Tereza arranges a call with Jan Žižka and the Canon contact, with Filip for BigHub, to get at least an offer. She finds Canon "quite capable".

### 6. Reklamace next phases — scope, value and whether 3–5 continue

**Tereza** wanted to use the time to map the next phases. The spec covers the base up to Phase 2, but she thinks even Phase 2 needs a broader review because claims "keep swelling under our hands" and the problem is bigger than what's specified.

**Marek**: Phase 1 / 1.1 (Excel, email threads) is specified well. Two questions on Phases 3–5:
1. **Value**: do Phases 3–5 add to the savings in the BQ tracker, or are they an extension?
2. **Scope**: how big are they on BigHub's side?

He framed it against Žůrek's comments: either continue those phases now (and start discovery), or finish what's started and look at a bigger pain point elsewhere (e.g. cenařky, warehouses, or the claims diagram Tereza is preparing for Dudaško).

**Tereza** (confirmed by **Petr Spilka**): the Reklamace savings in the tracker were calculated assuming **all five phases** are delivered. They aren't split by phase. It was a structured estimate; nobody measured actuals. Not finishing everything would change the savings calculation.

**Filip**: "Phase 2" is misleading in size. For BigHub it's a fraction of Phase 1, and warehouse claims are largely done. The bigger work may be on the **Axapta side**: BigHub reads the label and sends EAN, batch and expiry, but Axapta has to look up the goods from that. Count that internal development when weighing it.

**Marek** shared the roadmap (work in progress):
- Phase 1.1: mostly done, some items blocked on the Excel.
- Phase 2: far fewer tasks; much still in backlog.
- **Okamžité avízo**: proposed as lower priority. Manual handling covers most cases.
- Nice-to-haves: deprioritised.
- Phases 3–5: not defined; each marked "needs scoping". If their BigHub scope is as small as Phase 2's, "I see no reason not to do them" [translated from Slovak].

Marek proposed BigHub could then put most of its capacity in the coming weeks and months (into the new year) on higher-value work, while **supporting** the remaining phases (e.g. Axapta-side development) as a secondary activity, so all five are delivered in time.

**Tereza** read this as "let's put 3, 4, 5 to sleep and pick another topic". Logistics' job is to split the savings valuation and, alongside it, deliver the other initiatives so they can compare and prioritise.

**Jindřich** (firmly): "No, no, no." It was agreed with Žůrek that **Reklamace gets finished, and that means all five phases**, to meet the benefit in the tracker. He suggested specifying the rest with Marek first, to learn the real scope. BigHub's work on Phases 2–5 will be "substantially less", so BigHub can also work on other initiatives. But "whether to continue isn't even on the table. For me, definitely continue." [translated from Czech]

**Marek** confirmed: he never meant "we're not doing 3, 4, 5".

### 7. Petr Sláma's capacity

**Sláma** put on record:
- The project has slipped badly. By the original plan, everything should have been done around **April**.
- He's hitting capacity conflicts with other projects, e.g. **"BrightPig" in Ostrava** (as transcribed; possibly Brightpick, the warehouse-robotics project, to confirm).
- He **can't work on two things in parallel**, and isn't sure he has capacity for even one.
- He'll now work on "příjmy" (receiving; unclear whether this means Reklamace Phase 1 receiving claims or a separate project) and do what he can.
- Logistics can't expect him to work on receiving or Reklamace plus transport at the same time. If that's required, his manager / logistics (Petr Spilka) must deprioritise other projects.
- He had capacity in May–August, when he promised he could work on two things at once.

**Jindřich**: "completely legitimate". The slip hits BigHub's capacity too.

### 8. Roadmap and planning horizon

**Jindřich**: as agreed with Žůrek, Spilka and Tereza, BigHub will deliver a roadmap. Realistically BigHub can plan **2–4 weeks ahead**. A full roadmap can follow best practice (e.g. two weeks for UAT), but any extra specification or longer testing will shift it. He can plan **windows** where testing or cooperation is needed. The open question is whether ViaPharma can plan its side to match.

**Marek**: when analysing the next phases, factor in Sláma's capacity and take an **MVP / Pareto** approach (80% of the value for 20% of the effort) rather than aiming for perfection.

**Tereza**: worried that, as Ruda (Žůrek) said, they can't move without a roadmap, even one that will shift. Every Thursday they agree the lack of a roadmap is bad and that it only covers 14 days; she feels "we're standing still". She acknowledged ViaPharma owes the Excel and asked for "a plan for the planning".

**Jindřich**: promised and will be delivered. But for the last three statuses BigHub has been moving while waiting on ViaPharma for some items, and the slips are significant. He'll present the dates as an estimate at the monthly steering with Žůrek, with the reasons for each slip.

**Marek**'s action for ViaPharma: Tereza (with Spilka) gathers all inputs for Phases 2–5 at least at a high level, then writes to Marek. He'll schedule the discovery and walk through it with them. Goal: at one of the next joint meetings (not necessarily next week), the team knows what's in those phases, and BigHub can build a longer roadmap (internally at least) beyond 2–4 weeks. Once he has the inputs, it depends only on him.

**Tereza** agreed: she and Spilka will write down what belongs in Phases 3, 4, 5 so they don't arrive at a session "looking at each other", then go through with BigHub how it should go into the spec.

**Marek** closed: nobody on BigHub's side wants the takeaway to be "BigHub doesn't want to continue". BigHub wants to finish the project, while keeping in mind Žůrek's point that other initiatives exist and must be weighed in the roadmap.

## Decisions Made

1. **All five Reklamace phases will be finished.** The tracker's savings assume all five, so whether to continue is not in question. Proposed and confirmed by Jindřich Tůma and Marek Pillár; accepted by Tereza Foltová and Petr Spilka.
2. **BigHub's capacity follows the scope.** Phases 2–5 are expected to need much less BigHub work (more on the Axapta side). BigHub supports them as secondary work and can take on other logistics initiatives in parallel. To be confirmed once the phases are specified.
3. **Sláma's review order**: data-map Excel first (early week of 2026-10-12), then the Reklamace spec, then the simplified Fakturace doprav Swagger.
4. **The Reklamace spec goes to ViaPharma only after the Excel decisions are in.** It is not sent with open questions now.
5. **Phase 1 testing wrap-up**: a separate ~15-min call (Tereza, Filip, Sláma) on **Monday 2026-10-12**, not Friday.
6. **Scanner requirements**: BigHub (Filip) defines the technical ones. ViaPharma's operational input comes from **Jan Žižka**. The scanner integrates with BigHub's API only, so nothing changes in Axapta.
7. **Next-phase discovery is input-first**: logistics (Tereza + Spilka) writes up Phases 2–5 at a high level, then Marek runs the discovery. Use an MVP / Pareto lens and factor in Sláma's capacity.
8. **Roadmap expectations**: the dates are an estimate with planned cooperation windows. Slips and their reasons are reported monthly at the Žůrek steering.

## Action Items

- [ ] **Petr Sláma**: Review the Reklamace data-map Excel (column J) — due early week of 2026-10-12 — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Petr Sláma**: Then comment on the Reklamace spec, then review the simplified Fakturace doprav Swagger — after the Excel — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Marek Pillár**: Once the Excel decisions arrive, finalise the Reklamace spec ("contract") and send it to Sláma for comments — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Tereza Foltová**: Confirm Phase 1 test results with Jana Egrmaierová; schedule the ~15-min testing wrap-up with Filip Černý and Petr Sláma — due 2026-10-12 — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Filip Černý**: Chase write rights to the shared mailbox (Graph API) — due 2026-10-08 — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Tereza Foltová**: Chase the delivery date of the test phone to Brno (IT ticket via Dušan) — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Tereza Foltová**: Arrange a call with Jan Žižka, the Canon contact and Filip Černý on the Fakturace doprav scanner, aiming for an offer — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Tereza Foltová / Petr Spilka**: Write up what belongs in Reklamace Phases 2–5 (high level) and send it to Marek — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Marek Pillár**: Once the inputs arrive, schedule and run discovery on Phases 2–5 (MVP / Pareto lens, Sláma's capacity in mind) to size BigHub vs. Axapta work and feed a longer roadmap — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity
- [ ] **Jindřich Tůma**: Deliver the Reklamace roadmap (dates as an estimate, with test / cooperation windows); report slips and reasons at the monthly Žůrek steering — from 2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity

## Open Questions

- Does the **10-15–16 full UAT start** still hold, given the open Phase 1 testing and the wrap-up moving to 10-12?
- **Sláma's capacity**: will logistics (Spilka) reprioritise his other projects ("BrightPig" in Ostrava, "příjmy"), or does Reklamace move at one item at a time? What does "příjmy" mean here?
- How much **Axapta-side development** do Phase 2 and later phases need (label → EAN / batch / expiry lookup), and who on ViaPharma's side does it if Sláma is at capacity?
- **Okamžité avízo**: Marek proposes lowering its priority. Does logistics agree?
- How does the per-phase savings split (logistics' homework) change Reklamace's ranking against the other logistics initiatives?
- Who tells working-level ViaPharma staff (Sláma, Jana) what management meetings decide, so work doesn't pause again?

## Sentiment & Tone

**Cordial on the surface, but with a recurring trust wobble and visible client-side frustration.**

- **Petr Sláma**: apologetic and frank. He paused because he was out of the loop ("I wasn't invited… didn't know the status"), not out of resistance, and promised to act next week. His capacity statement was the most important signal of the call: calm but firm, and on record. He positions any parallel work as logistics management's decision. He is a real bottleneck, and the April-vs-October slip is his framing of whose delay this is.
- **Tereza Foltová**: anxious and pushing. She heard "BigHub wants to drop 3–5" even after it was clarified twice, which shows how primed the client side is for that narrative (third time since 09-23). Her "we're standing still" and "plan for the planning" reflect pressure from Žůrek's ask for dates. She also acknowledged ViaPharma owes the Excel.
- **Petr Spilka**: almost silent. He joined as Reklamace owner and confirmed only the savings assumption. Whether he attends regularly is open.
- **Jindřich Tůma**: steady, then firm on continuity and fair on capacity. He pushed back gently that the slips are partly ViaPharma's and will name the reasons to Žůrek, which sets up a fair narrative for the steering.
- **Marek Pillár**: product framing (MVP / Pareto, input-first discovery). His capacity-reallocation idea was correct but easy to mishear: "focus elsewhere" lands as "stop".

**Watch-outs**:
- Any message about moving BigHub capacity to other initiatives must lead with "all five phases get delivered", or it will be heard as abandonment.
- Decisions from management meetings need to reach Sláma and Jana explicitly. This week's pause came from a communication gap, not a decision.
- The client's roadmap anxiety is real. The roadmap needs to land soon, even as an estimate with windows.

## Routing Log

Confirmed by PM on 2026-10-08 (confirm all).

- **project-assumptions**: added ASM-255 to ASM-259; updates on ASM-229, ASM-227, ASM-240, ASM-248, ASM-190, ASM-184 (knowledge-base target ~2026-10-16), ASM-056 (UAT at risk)
- **project-stakeholders**: STK-034, STK-013, STK-014, STK-015
- **project-knowledge**: Reklamace status sync (2026-10-08)
- **client-overview**: Ways of Working (management decisions not trickling down; recurring continuation doubt)
- **project-daily**: 1 PM-owned item added (Phases 2–5 discovery); data-map and spec-send items re-dated; "Phases 2–4 vs. other initiatives" resolved; Amber re-confirmed with the new rationale. Other people's items stay in this note.
- **project-lessons**: LL-85, LL-86
