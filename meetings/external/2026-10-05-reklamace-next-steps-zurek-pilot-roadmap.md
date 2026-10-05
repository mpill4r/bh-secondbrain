---
last_updated: 2026-10-05
type: external
attendees: [Rudolf Žůrek, Petr Spilka, Tereza Foltová, Jana Egrmaierová, Jindřich Tůma, Marek Pillár]
recording_link:
---

# Reklamační proces — další kroky: Žůrek Sets Direction (Finish the Pilot, Ideal Process, Dates & Roadmap)

**Date**: 2026-10-05 (Monday), 10:00, in person
**Attendees**: Rudolf Žůrek (STK-024, head of logistics), Petr Spilka (STK-014, head of ViaPharma warehouses, Reklamace business owner), Tereza Foltová (STK-013, ViaPharma logistics, organiser), Jana Egrmaierová (STK-044, ViaPharma), Jindřich Tůma (STK-003, BigHub/Dr. Max coordination), Marek Pillár (STK-001, BigHub PM). Tomáš Dudaško (STK-010) didn't attend and asked for the meeting to be recorded.
**Type**: external
**Recording**: Teams transcript (~50 min, Czech/Slovak). **Every line is labelled "FOLTOVÁ Tereza"** because the recording ran on her account. Speakers below are attributed from content and language (Slovak = Marek, grammatical gender, role). Treat the attribution as an inference.
**Previous session**: N/A. This is the first management-level Reklamace meeting. Related: [2026-10-01 ViaPharma Reklamace sync](2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review.md), [2026-10-02 logistics green-field / cenařky](2026-10-02-logistics-initiatives-green-field-cenarky-analysis.md)
**Meeting prep**: [2026-10-05-reklamace-next-steps-zurek-dudasko-meeting-prep](../prep/2026-10-05-reklamace-next-steps-zurek-dudasko-meeting-prep.md)

## TL;DR

The feared continue-or-close question didn't come up. Rudolf Žůrek set the direction himself:
- Finish the running phases (Phase 1 / 1.1) as a **pilot**, without rushing under time pressure, and specify the next phases in parallel.
- Design towards an ideal future process rather than copying today's, and stay away from Axapta.
- Above all, give **dates and a roadmap**, because the Group CEO asks monthly and "where is your AI?" pressure is building across the holding.

"AI or digitisation" stopped mattering: both logistics and Žůrek care about the benefit. Žůrek pictures AI in the outside communication (watching replies, reminders, an agent for incoming emails).

Agreed next steps:
- warehouse visits with logistics' process person;
- a roadmap of all phases with dates;
- the initiative mapping opened this week, to decide the 2027 "unicorns" in Q4;
- a monthly 30-min status with Žůrek on Mondays at 10:00.

Žůrek offered to switch focus to transport (Fakturace doprav) if Reklamace stays stuck. BigHub's answer: the way out is found, and the running phases get finished first.

## Key Discussion Points

### Pre-meeting (Jindřich, Tereza, before Žůrek and Spilka arrived)

- **Sláma's data-map feedback**: he hasn't done it yet. He was tied up launching the A-frame and promised it at the start of this week. Tereza will chase him tomorrow so it is ready for Thursday.
- **X-Manager** (Jindřich): it is internal to Dr. Max and used by the call centre. It was adjusted for testing requests and is becoming a data source. At the last meeting the idea came up to use it for Reklamace, so a meeting with the product owner is set to check whether it fits. If it meets the requirements, it gets presented as an option ([[ASM-243]]).
- **Framing the meeting** (Jindřich): with Dudaško absent, he wanted to calibrate, because last week's "digital or AI?" noise had reached Žůrek through different channels. Tereza: walk Žůrek and Petr (Spilka, the owner) through the whole process and the phase it's in, including what is being solved with Sláma, "and straighten it out". Logistics sees it as an IT project where they are "just the customer"; Dudaško decides. Jindřich: Tomáš doesn't even assume BigHub wouldn't do it; it's only about not calling it AI when logistics doesn't see AI.
- **Costs vs. benefits** (Tereza): AI costs tokens and licences (Power Automate). Could an agent end up costing more than the clerk it replaces? Jindřich:
  - First wave: clean benefits.
  - Second wave: costs, both development investment and operating costs. Operating costs can be shared across projects.
  - Result: benefit minus cost. Further development is separate and can be forecast per year, e.g. "Reklamace changes in 2027".
- **New legal obligation** (Tereza): after a SÚKL inspection of medical devices, Dr. Max must notify the actual manufacturer (factory) of a defective device such as a tonometer, not only the supplier. One brand (e.g. Hartmann) can be produced in 2–3 factories, varying by batch, and Dr. Max has no manufacturer database. The notice can be a predefined email, even in Czech. Other product classes (e.g. veterinary) have their own rules, so the supplier/claim matrix will keep evolving.
- Dudaško sent word he wouldn't attend; the meeting is recorded for him.

### Where the project stands (Tereza, confirmed by BigHub)

- **On the table**: Phases 0, 1 and 1.1, i.e. receiving claims to the supplier.
- **Phase 1**: the receiver photographs in the app, the photos are stored, and the app talks to Axapta.
- **Phase 1.1**: the claim agent builds the email from the photo, the description and the supplier matrix (recipient, text, return address) and a label gets printed for the box. At first a person checks the email and sends it. Once the agent is "trained" enough, it sends automatically.
- **Naming**: Tereza flagged that supplier, customer and warehouse claims are named inconsistently.

### AI vs. digitisation: closed as a non-issue

- **Jindřich**, who also covers AI adoption:
  - The textbook order is data cleaning → automation → AI. This project skips a step, which is fine because the benefits come either way.
  - The project is ~80% automation, and the AI part is the email thread agreed on 10-01.
- **Logistics side** (likely Spilka): "for us as the customer it doesn't matter whether it's AI".
- **The real friction is Axapta**: the knowledge base. "You say put it all in Axapta, we say we don't want to because it's expensive." Nobody from the Axapta side was in the room.

### Rudolf Žůrek: the strategic frame

- **Reklamace today is ~25% of the topic.** Supplier claims are one coherent process, but there are 4–5 claim streams (supplier, customer/pharmacy, warehouse…). They all end with the supplier, from different sources.
- **AI belongs in communication with the outside world.** Today's email is simple and maybe human-filtered, but 2–4 more processes will use the same thread. Build for that now, so it isn't sitting in Axapta later and "useless", forcing an agent to be built three more times.
- **Knowledge outside the WMS/ERP**:
  - Use AI to bypass "hard" WMS/ERP development.
  - Put the knowledge in one maintained place valid for everyone, not four versions: a wiki, SharePoint, even a well-structured Excel ("I don't like it, it isn't a database").
  - The WMS is to be replaced in **2–3 years**, so anything built into it now is thrown away.
- **No rushed solution under time pressure**: "if it takes another three months, fine".
- **Scale**: "we won't scale it wide; let's do this one claims process reasonably, because we'll learn". Token inflation is real; at a budget meeting they discussed whether people may become cheaper than tokens.
- **Where he sees AI value**:
  - The clerk shouldn't have to watch replies. Of 10 emails a day, 7 get answers, and the AI chases the other 3 with reminders (could also be algorithmic).
  - Aim for maximum replacement of work.
  - "Not 1:1 into AI. We want an ideal, polished, maybe utopian process", where in the end "maybe nobody sits there".
- **It's a pilot**: "the costs probably won't return". What matters is moving forward: try it, and if it doesn't do what we thought in a month, change it.
- **Success measure**: the system does something it didn't do before, and people stopped doing something. Headcount savings may come in the 3rd or 4th iteration, possibly with a completely different process.
- **Away from Axapta**: strategically they'll get rid of it, and the Axapta people are overloaded, so no development that isn't necessary.
  - His e-com experiment: instead of heavy WMS development (people releasing orders into the line), put "Duo or something" in that logs in as the users and does the work.
  - Reklamace is also a test of whether AI can "hack around" heavy WMS/ERP development.
- **The real pressure is to show something.**
  - Across the holding, "where is your AI? you've been fiddling with it for three quarters of a year".
  - Deliver a small part in reasonable time, so the experience "materialises" into an AI process with lessons learned.
  - "Not freestyle any more."
- **Development debt in back-office systems.** Example: pharmacy returns.
  - The pharmacy enters the return in **Pharmis** (pharmacy POS), but no data reaches the warehouse; a box arrives with a handwritten A4.
  - 99% of these end up as supplier claims.
  - Options: integrate into the WMS, or export from Pharmis into Axapta and convert the customer claim into a supplier claim. To discuss with Tomáš and the DAX team.
  - Map all inefficiencies, whoever owns them, but logistics needs a counterpart who admits them.
- **Go to the warehouses**: logistics has a **process person ("procesák")** who can redraw the process. "Tell us what you need and when, and let's move."
- **Dates are mandatory.**
  - The Group CEO asks in a monthly review, and the "old school" leadership can't accept "I don't know when".
  - Either "this phase is done on X" or "in a week we'll tell you when". Even "January 2028" is fine; he just needs dates.
  - They have been fed incomplete information for three quarters of a year.
- **Two running streams, no internal competition.**
  - He doesn't want Reklamace and transport (Fakturace doprav) competing for BigHub capacity.
  - If Reklamace "has run aground" (too much Axapta, no room for AI), switch to transport, "sit in another boat". He offered it as an option, not a demand.
  - BigHub (Jindřich): it got stuck, but "we found the way out". The running phases get finished, then decide how to continue.
- **Even the SharePoint List alone is a win**: a shared file for five people, one source of truth, data cleanliness and an improved process, whatever the future use.
- **New topics**:
  - Don't chase "a thousand hares". Finish the two running ones.
  - For new ones, look at headcount: a 15-person back office has more to optimise.
  - Cenařky is ~3 people per warehouse, "cut to the bone", but has synergies with accounting and document extraction.
- **PV logic** (how warehouses react to pharmacy demand, forecasting shipments): a business topic BigHub should eventually take over. He didn't open it.
- **Scale of logistics**: hundreds of thousands of transactions a day, so small improvements have a big impact. Marketing (Marek Dvořák) wants to optimise too. Collect all topics.
- **Challenge the operation**: the business is conservative and bound by legislation. "When you've done something for 20 years…" An outside challenge is valuable.

### Marek Pillár

- **Knowledge base**: BigHub already has a proposal. Ideally not Excel but SharePoint or similar, which is user-friendlier and the foundation for the agent's communication.
- **After Phase 1.1 / testing**, BigHub can deliver a coherent piece of Reklamace. He'd have "no problem" pausing Phases 2–5 in favour of a discovery of new opportunities, since BigHub's expertise is data and AI: email communication, a claim search on Max/Lexie, any small chat use case.
- **Spec as a contract with Sláma**: comments will come, but changes during development are fine once communicated and priced.
- **His approach**: product manager with a startup background. Go straight to the user ("what's bothering you, what can I give you?"), define the problem, not the solution. The outcome may be FTE savings, time, quality or coverage.
- **Savings**: they don't necessarily mean fewer people. They can mean better quality and more cases processed.
- **Human in the loop**: always somewhere in the process. Exceptions get collected and drive further development.
- **Three options**:
  1. Finish Reklamace and Fakturace doprav with continuous discovery.
  2. Jump to a new initiative.
  3. Map and quantify all initiatives first (e.g. cenařky), because "we still don't know what the biggest win in logistics is".
- **Proposal**: open all initiatives this week (write them down, break them down, list what they bring and cost, prioritise), and decide Phases 2–4 vs. something else.

### Petr Spilka (attributed)

- Cenařky doesn't depend on the physical product. It is internal, mostly a deterministic task (price list → invoice → booking) and talks to purchasing and accounting.
- "I honestly thought we'd do cenařky before Reklamace."

### Next phases, roadmap and the AI strategy (Jindřich)

- Understanding: **continue Phase 1.1, push it through, and specify the next phases in parallel** (correct them, add things). Marek, and Jindřich too, go physically to the warehouses.
- **Roadmap of all phases**: most detailed for the phase being specified, with dates that may slip. Žůrek accepted slips, as long as BigHub can explain the plan.
- **AI strategy**:
  - Every department gets a list of AI initiatives that make sense, starting as a short table.
  - The team expands next year, and Tomáš must know the "unicorns".
  - BigHub can send an analyst to specify a candidate (e.g. cenařky) while the running projects continue.
- **Logistics initiative table**: 10–25 rows already ("the table is endless"). Reklamace and doprava are pulled out, the others are in "maintenance mode", and BigHub has to add **cost** to them.
- **Holistic view**: as in marketing, avoid isolated solutions that don't talk to each other.

### Next meetings

- **Wednesday**: the logistics session goes through the initiatives Excel.
- **Thursday**: the regular sync. Phase 1 UAT testing is finished on BigHub's side. Feedback will show how much development is left, and the timeline will be re-answered after that.
- **Next week**: walk through the claims (Reklamace) themselves.
- **Before rolling out to users**: Tereza proposed a pre-meeting on the claim structure and reasons (Jana's material), so the app doesn't turn into a "goulash".
- **Q4**: map the initiatives and decide the biggest for 2027, with slides for what can go in.
- **Monthly 30-min status with Žůrek + BigHub**: simple, "these are the topics we're solving", to also cut down WhatsApp traffic. **Monday 10:00** suits Žůrek, since management meets at 11:30.

## Decisions Made

1. **Reklamace continues.** The running phases (Phase 1, 1.1) are finished and tested as a **pilot**. The next phases are specified in parallel, with no rushed solution under time pressure. A switch to transport is only a fallback if Reklamace stays stuck.
2. **The goal is a visible, working AI process in reasonable time, with lessons learned.** Costs and immediate headcount savings are secondary for the pilot. Success is "the system does something new, and people stopped doing something".
3. **"AI vs. digitisation" is no longer a question.** The customer cares about the benefit. Reklamace is ~80% automation, plus AI in the email thread.
4. **Design target is the ideal future process, not today's process 1:1.** That means warehouse visits, logistics' process person, and challenging the operation.
5. **Knowledge stays outside Axapta/WMS** in one maintained store (SharePoint List / wiki). No unnecessary Axapta development. A single source of truth counts as a win on its own.
6. **Dates are required.** BigHub delivers a roadmap of all phases with dates (slips accepted), or says when it will have one. It feeds the Group CEO's monthly review.
7. **Monthly 30-min status Žůrek + BigHub**, Mondays at 10:00.
8. **New logistics topics**: finish the two running streams first. Map and quantify the rest (cost added) and pick the 2027 "unicorns" in Q4. Headcount is a key lens.
9. **Benefits first, then costs (development + operating)**, giving a net figure per initiative.

## Action Items

- [ ] **Jindřich Tůma / Marek Pillár**: Deliver a Reklamace roadmap of all phases with dates (most detail for the next phase), or say by when it will be ready; re-answer the timeline after Thursday's UAT feedback — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Marek Pillár / Jindřich Tůma**: Plan warehouse visits with logistics' process person to map all claim streams (supplier, pharmacy/customer, warehouse) towards an ideal future process — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Marek Pillár**: Open all logistics initiatives this week (Wednesday session): write them down, break them down, state benefits and cost, prioritise; decide Phases 2–4 vs. other initiatives — due 2026-10-07 — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Marek Pillár / Jindřich Tůma**: Add development and operating cost to the logistics initiatives (second wave after benefits); prepare slides for the Q4 decision on 2027 initiatives — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Tereza Foltová**: Chase Petr Sláma tomorrow for the data-map (column J) feedback, so it's ready for Thursday — due 2026-10-06 — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Tereza Foltová**: Send the monthly 30-min status invite (Žůrek + BigHub, Mondays 10:00) — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Tereza Foltová / Jana Egrmaierová**: Hold a pre-meeting on the claim structure and reasons before the app goes to more users — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Tereza Foltová**: Send details of the new legal obligation to notify the medical-device manufacturer (SÚKL finding) for the supplier matrix — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Jindřich Tůma**: Meet the X-Manager product owner on whether it fits Reklamace; present it as an option if it does ([[ASM-243]]) — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap
- [ ] **Tereza Foltová / Jindřich Tůma**: Make sure Tomáš Dudaško gets the recording or a summary — from 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap

## Open Questions

- **Axapta/WMS timeline conflict** (kept open per PM, [[ASM-250]]):
  - Dudaško on 2026-09-23: Axapta retired in ~6 months.
  - Sláma on 2026-10-01: the WMS part gets replaced, the ERP part stays.
  - Žůrek today: the WMS is changed "in 2–3 years".
  - Which horizon does the roadmap assume?
- Pharmacy returns (Pharmis → warehouse): integrate into the WMS, export from Pharmis into Axapta, or work around it? Žůrek: discuss with Tomáš and the DAX team.
- Medical-device manufacturer notification: who knows the factory per batch? Does it change the supplier matrix and the email agent's recipients?
- Does Phase 1.1 need a reply-monitoring / reminder function (7 of 10 answered → chase 3) earlier than planned, since that is where Žůrek sees the AI value?
- Who is logistics' process person, and when can warehouse visits happen?
- What does Dudaško take from the recording? He wasn't there for the "AI or digi" calibration.

## Sentiment & Tone

**Much better than feared.** No continue-or-close question, no blame for the Sláma comments, and no value challenge on the ~425k Kč figure. Žůrek was direct, strategic and supportive: he sees Reklamace as a pilot and a learning vehicle, accepts that costs may not pay back, and explicitly wants BigHub to challenge the operation. His two hard asks are **dates** and **something visible**, both driven by Group CEO and holding pressure ("where is your AI?"), not by doubts about BigHub. Offering a switch to transport was a release valve, not a threat. He made clear twice he isn't saying it should happen.

Tereza came in anxious about framing ("am I talking nonsense"). She was reassured that the AI/digi question doesn't matter to the customer, and she took ownership of practical follow-ups (Sláma chase, monthly invite). Spilka was quiet. His one clear signal: cenařky would have been his first pick. Jindřich steered calmly: AI adoption framing, roadmap, the analyst offer. Marek positioned BigHub as a product/discovery partner (go to the user, define the problem) and found Žůrek on the same wavelength ("don't go into solutions").

**Relationship signal**: strong. Žůrek opened a direct monthly channel to himself, invited warehouse visits with his process person, and offered whatever resources are needed ("tell us what and when, and let's move").

**Watch-outs**:
- Dates promised now must be kept or re-baselined openly. Žůrek is accountable upward monthly.
- The cenařky pull is real: Spilka favours it, and Žůrek sees synergies.
- Marek's "no problem stopping Phases 2–5" was heard. Make sure it's framed as re-prioritisation through discovery, not abandonment.

## Routing Log

Confirmed by PM 2026-10-05:
- **project-assumptions**: added ASM-247 to ASM-253; ASM-242 → Decided; updates on ASM-243 (X-Manager), ASM-190 (costs, Q4 2027 pick).
- **project-stakeholders**: STK-024, STK-014, STK-013, STK-010, STK-044.
- **client-overview**: Ways of Working (holding AI pressure / dates mandatory; monthly Žůrek channel).
- **project-knowledge**: Reklamace management direction.
- **product-requirements**: REQ-002 (medical-device manufacturer notification), REQ-003 (reply monitoring / reminders).
- **project-daily**: 10 action items, 3 progress notes, status Amber re-confirmed.
- **project-lessons**: LL-82.
