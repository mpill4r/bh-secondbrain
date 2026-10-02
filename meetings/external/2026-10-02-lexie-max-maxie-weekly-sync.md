---
last_updated: 2026-10-02
type: external
attendees: [Jindřich Tůma, Jura Brázdil, Viliam Gago, Marek Pillár, Simona Mertová, Kateřina Kadlecová, Lucie Fendrichová, Šárka Andělová, Veronika Strmisková]
recording_link:
---

# Lexie / Max / Maxie Weekly Sync — Cheaper Model Trial, Staging Orders & Order-Status Source Tables

**Date**: 2026-10-02
**Attendees**: Jindřich Tůma (BigHub/Dr. Max coordination), Jura Brázdil (BigHub, developer), Viliam Gago (BigHub, platform), Marek Pillár (BigHub, PM), Simona Mertová (Dr. Max CC, business owner; left at ~33 min), Kateřina Kadlecová (Dr. Max CC, domain expert), Lucie Fendrichová (Dr. Max CC), Šárka Andělová (Dr. Max CC), Veronika Strmisková (Dr. Max CC)
**Type**: external
**Recording**: N/A (Teams transcript, ~55 min, Czech; some speaker labels are wrong: Marek's line at 37:50 and Šárka's/Lucie's lines at 41:29 and 43:15 are tagged "Jura Brázdil")
**Previous session**: [2026-09-24 Lexie/Max/Maxie weekly sync](2026-09-24-lexie-max-maxie-weekly-sync.md)
**Meeting prep**: N/A

## TL;DR

Jura showed a widget-history fix, Max connected to staging orders and Rx stock, and a placeholder SPC (package-leaflet) card. He proposed trialling a newer small model (heard as "GPT Luna", about half the price of GPT-5 mini). Mertová approved going cheaper herself, but any upward cost needs Dudaško. Fendrichová presented three source tables in X-Manager (order categories, carriers, statuses × categories) for order-status answers. Jura will rebuild order status and carriers on them, so testers should pause testing those. Kadlecová announced she leaves on maternity leave at the end of October; her colleagues take over and a main contact will be named later. Infra/BDC friction blocks Maxie, and an Atlantis/BDC meeting is set for Monday.

## Continuity from 2026-09-24

- **Test order DB**: done. Max now reads the staging order database. Testers were asked to check courier tracking numbers.
- **Rx stock lookup without e-recept**: done. Rx products are found and flagged as prescription-only.
- **Cost projection + model switcher**: cost breakdown sent to Jindřich and shown. A switcher to compare models is promised.
- **Package leaflet (SPC)**: UI shown with placeholder content (every drug shows the Paralen 500 SPC). Real data needs the SPC database on the test server. Dr. Max will run it past Legal on Tuesday.
- **Mobile/geolocation testing**: IT enabled geolocation; mobile testing is still blocked until the widget is reachable outside VPN.
- **Order-status definitions (Fendrichová)**: delivered as three X-Manager tables (see below).
- **Methodologies → RAG**: still waiting on the platform's document-search deployment in the new environment. Jura wants to reuse Viliam Gago's indexing rather than build it twice.
- **Hallucinations, bracketed instructions in replies**: Kadlecová considers them fixed per the release notes.
- **Maxie/Atlantis meeting** (Jindřich's item): BDC came back after ~4 weeks asking for another Atlantis meeting. It is scheduled for Monday 2026-10-05 with Mertová added.
- **Not revisited**: analytics dashboard URL, opening-message wording, tone keywords, free-text feedback removal, ElevenLabs licences and barge-in, Mertová's email confirmation.

## Key Discussion Points

### Max chatbot: changes shown

- **Widget history fix**: popup widgets (pharmacy cards etc.) weren't stored correctly in conversation history, so the bot didn't know what it had shown. For example, it showed 15 pharmacies and then 30. Jura expects this to fix many odd behaviors. Andělová confirmed her last 2–3 reports look resolved.
- **Staging orders + Rx**: connected to the staging order DB; prescription drugs are found and labelled Rx-only.
- **SPC leaflet card**: the card states the bot can't give dosage advice and links the SPC section. Content is a placeholder until the SPC database is connected on the test server. Jura's guidance for Legal on Tuesday: ask specifically whether the bot may jump to a given SPC section. It uses no patient data, only the drug the user names, and leaflets are shown unmodified as received from SÚKL.
- **Other**: new opening line, bubbles moved down (per 09-24), broader goodbye detection ("to je vše").
- **Lexie**: clicking a citation is now instant instead of slow. Otherwise no changes.

### Testing feedback

- **Geolocation timeout** (Kadlecová): "find nearest pharmacy" sometimes times out and works only on the 2nd–4th try. Jura thinks it's a frontend timeout setting and will ticket it.
- **Route uses Prague as origin** (Fendrichová): nearest pharmacies are correct, but "show route" always starts from Prague. It also sometimes navigates to a different shop at the same address (e.g. in a shopping centre). Jura admitted he never tested routes: "that will be on us". Fendrichová will ticket it with examples.

### Model cost and trial

- Current model: GPT-5 mini ("fairly small and dumb", Jura).
- **Trial model**: a newer small model heard as "GPT Luna" / "GPT-6 Luna" (exact name unclear). Jura says it is ~half the price, faster and more capable. He'll add a switcher on the test page so testers can compare models, especially on problem cases.
- **Cost figures shown** (10,000 conversations × 5 user turns, each turn several model calls): current ~$100. "Luna" ~$43. A much larger model (heard as "Soul") ~$800–850, which Mertová put at roughly 15,000 Kč.
- **Mertová's call**: going down in cost doesn't threaten the IT budget, so she can decide that herself: "let's put a switch on Luna and try it". Anything costlier needs Dudaško (IT holds the budget), so she asked Jindřich to discuss expected costs and the allowed range with him.
- **Hybrid option** (Jura): the small model can escalate to a large one for hard cases. Once the platform is live, a budget cap can be set (e.g. "8,000 Kč a year for extra-smart answers") and escalation stops once it's used up.

### Abuse and cost protection

Mertová asked about protection against off-topic chatting (competitors, children, "how are you"). Jura: off-topic answers are largely blocked now (the old pancake-recipe case shouldn't happen anymore). Two options:
- **Auto-end the chat** after repeated off-topic requests (e.g. 3 in a row). Mertová: worth considering, not needed now; decide after monitoring.
- **Per-IP throttling**: missing and "an absolute standard". Jura will add it so nobody can hammer the bot from code and run up costs.

### Knowledge base, Lexie back-office agent, agent switching

- **Methodologies**: Kadlecová will wait for the RAG deployment, the same mechanism Lexie uses for CC methodologies. Meanwhile CC prepares more: order tracking, reservations (claims already done), and opening-hours notes.
- **Lexie for back office (new request)**: Dr. Max's back-office department wants its own Lexie agent, separate from the CC front-office agent, drawing on its own SharePoint. Kadlecová is unsure whether CC can set it up themselves; they certainly can't do the SharePoint connection. Viliam Gago: realistic, but it needs BigHub work today, not self-service. Jura: likely Entra group membership and Dr. Max permission for the SharePoint. BigHub will review the steps and aim to make it user-configurable later.
- **Agent switching for testing** (Mertová): Jura has a lead on a test user that can switch roles. He found it while building end-to-end browser tests during the platform migration, but isn't certain. He'll know by the next meeting.

### Maxie, infra and deployment

- **Maxie**: Jindřich ("I'm bringing this unpleasant topic") explained the Atlantis requirements went via Vláďa Maruška to BDC. After ~4 weeks, BDC said it isn't set up and wants another Atlantis meeting to clarify. It was escalated at Tuesday's management meeting, including by CEO Žák. BigHub wants to talk to BDC directly. Meeting Monday 2026-10-05 with Mertová; Jindřich wants the setup delivered next week. Jura: a call with Vladislav Tvarůžek and Štěpán from BDC yesterday on deployment, "communication is finally flowing".
- **Platform migration**: Jura is moving MaxBuddy (pushed hard, ~14 days behind, target all ~600 pharmacies), Lexie and Max into the new environment. Max is on test; certificates/DNS are the last step and should land next week (only the URL changes for testers).
- **Testing on drmax-space.cz** (Mertová): Dr. Max's staging website, reachable via VPN or the Dr. Max network. Testers can test there without hiding the widget from customers. Jura: ideal; put it there. Separately, getting onto live drmax.cz needs network/certificate work and should start now. Jura floated embedding it hidden on drmax.cz, toggled via the dev console, and will ask Vladislav Tvarůžek.

### Order-status source tables (Fendrichová)

Fendrichová showed a new yellow "AI" module in X-Manager with three tables, meant as the source Max (and later Maxie) generates order-status answers from. The goal is no hand-written reply per case:
1. **Categories**: order vs. reservation vs. a parent transaction grouping sub-orders, where only sub-orders have a status. Each has an internal name, API name, the term the bot should use, a number-series hint (Dr. Max orders start with 5; others such as benu.cz differ), a meaning, and what may or may not be said.
2. **Carriers (doprava)**: ID (some IDs are shared; the Rx/"ARIX" reservation carrier has none), description and customer messaging. Today's Maxie IVR derives OTC vs. Rx reservation from category, then carrier.
3. **Statuses × categories**: status name, meaning, and a template answer.

Discussion:
- Jura will export the tables himself (format doesn't matter) and build them in, asking for gaps as he goes. **Testers should pause testing order status and carriers**, since it will be rewritten.
- Andělová: replies currently show the raw API value (`drmax_pickup_place_drmax-box`); use the human text field. Jura: will fix it in the rewrite.
- **Process questions** ("how do I change delivery?") depend on category, carrier and status. These belong in a separate Word methodology, not the tables, which are only for status answers. CC is working on it; no date promised.
- **Payment methods** (planned extension): Fendrichová wants Max to know whether an order was paid. For example, for "return transporting", say the refund comes within 14 days instead of a generic "if you paid" line. Jura: payment status should be in the API; configurability unsure until he sees it.
- **Status order / history**: an ordering column isn't necessary. An actual status history would enable a "show history" view. Fendrichová says orders have history but doesn't know if the API exposes it. Jura will check; it's a nice-to-have.
- **Self-service config** (Andělová): new carriers appear every year or two, and CC wants to add them (and payment methods) themselves. Jura: once the new platform has a settings interface, carriers can be user-editable (API name, internal name, bot term). He's confident for carriers, less so for payment methods.
- **Marek** offered to go through the source tables with CC async before the filtered set goes to Jura, as the business/product contact.

### Boxes as a future topic (Kadlecová)

Dr. Max boxes (its own boxes, plus Z-BOX delivery) are a recurring CC pain. Kadlecová wants a **box troubleshooting topic** for Max and Maxie later, as low priority behind order status and e-recepty. It's a methodology of customer tips (e.g. toggle Czech↔English to wake the screen), with no system integration. For Maxie the box line has a **separate phone number**, so it could be the first full-AI line without the click-through IVR, as a low-traffic "first swallow". Jura likes it as an isolated test use case; scheduling is Jindřich's call, and Honza Zelený would implement it. Kadlecová: CC already has base notes, the old IVR and old voice there need sorting out anyway, and given current Maxie troubles it could well go first. Jura: once ElevenLabs traffic is allowed through infra, the specific branch matters less.

### Kadlecová's maternity leave

Kadlecová leaves at the end of October. Her colleagues (Šárka Andělová, Lucie Fendrichová, Veronika Strmisková) take over her agenda. A one-to-one replacement is being hired but doesn't exist yet. Mertová will name one main contact later. Kadlecová added BigHub to the CC group chat for ad hoc operational matters (e.g. moving meetings).

## Decisions Made

- **Trial a cheaper newer small model ("Luna") alongside GPT-5 mini via a test-page switcher.** Mertová approved; lower cost is within her authority. Any higher-cost model or hybrid escalation budget needs Dudaško's agreement (via Jindřich).
- **Per-IP throttling will be added** to Max to prevent spam and cost abuse. Auto-ending chats after repeated off-topic requests is deferred, to be decided after monitoring.
- **Max will be deployed for testing on Dr. Max's staging website drmax-space.cz.** Work toward live drmax.cz (network and certificates) should start now.
- **Order-status answers will be generated from CC's three X-Manager source tables** (categories, carriers, statuses × categories). Order status and carrier testing is paused until Jura's rewrite. Process questions (e.g. changing delivery) go in a separate methodology document.
- **Carriers (and possibly payment methods) should become self-service configurable** in the new platform's settings.
- **Back-office Lexie agent is feasible but needs BigHub work** (SharePoint connection, Entra groups, Dr. Max permission). It is not self-service for now.
- **Kadlecová's agenda passes to Andělová, Fendrichová and Strmisková from the end of October.** Mertová names a main contact later.

## Action Items

- [ ] **Jura Brázdil**: Add a model switcher on the Max test page (GPT-5 mini vs. "Luna") — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Discuss Max/Maxie model costs and the allowed spend range (incl. hybrid escalation budget) with Tomáš Dudaško — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Add per-IP throttling to Max — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Ticket and fix the geolocation timeout on "find nearest pharmacy" — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Lucie Fendrichová**: Ticket the route bug (origin always Prague; navigates to another shop at the same address) with examples — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Test courier tracking numbers from staging orders — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Šárka Andělová / Dr. Max CC team**: Run the SPC leaflet display past Legal on Tuesday 2026-10-06 (can the bot jump to a specific SPC section; no patient data used; leaflets unmodified from SÚKL); report back — due 2026-10-06 — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Rebuild order status and carrier answers on the three X-Manager source tables; show human carrier names, not API values; check whether the API exposes payment status and order history — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Marek Pillár**: Offer CC async review of the order-status source tables before the final set goes to Jura — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Write the order-process methodology (changing delivery, what to offer, when to escalate) as a separate document — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil / Viliam Gago**: Review what a back-office Lexie agent needs (own SharePoint, Entra groups, Dr. Max permission) and report the steps — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Confirm whether a role-switching test user for Lexie is possible — due next weekly sync — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Deploy Max for testing on drmax-space.cz (Mertová sent the link) and ask Vladislav Tvarůžek about starting the network/certificate work for drmax.cz — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Hold the Atlantis/BDC Maxie meeting on Monday 2026-10-05 (Mertová invited) and push for delivery of the setup within that week — due 2026-10-05 — from 2026-10-02-lexie-max-maxie-weekly-sync
- [ ] **Simona Mertová**: Name the main CC contact replacing Kateřina Kadlecová from the end of October — from 2026-10-02-lexie-max-maxie-weekly-sync

## Open Questions

- Exact name and pricing of the "Luna" and "Soul" models (transcription unclear).
- Dudaško's allowed spend range for Max/Maxie models and whether a hybrid escalation budget is acceptable.
- Whether the order API exposes payment status and order history.
- Who at Dr. Max will be the main CC contact after Kadlecová ([[ASM-091]]).
- Whether the box line becomes Maxie's first full-AI branch. Jindřich to plan with Honza Zelený.

## Sentiment & Tone

Warm and productive. Dr. Max came well prepared (the order-status tables impressed Jura: "no e-shop does this"), and Jindřich thanked them for the "perfect preparation". Kadlecová's announcement was received warmly. Her framing that "the cooperation will continue exactly the same, just without me" is reassuring, but CC loses its most organized coordinator at a critical time (public launch target end of October). Mertová was decisive on cost (yes to cheaper, Dudaško for anything more) and cost-conscious about abuse.

Infra remains the sore point. Jindřich was openly apologetic about Maxie and the BDC loop, but the CEO-level escalation and the first direct BDC call give some momentum. Jura is stretched thin: at a conference two days, juggling MaxBuddy (14 days behind), Lexie and Max migration. He hadn't yet processed the latest test feedback.

## Routing Log

- **project-assumptions**: Added ASM-234 (cheaper model trial), ASM-235 (throttling), ASM-236 (drmax-space.cz testing), ASM-237 (order-status source tables), ASM-238 (back-office Lexie agent, open), ASM-239 (box topic / Maxie first branch, open). Update notes on ASM-091, ASM-188, ASM-100 (slipped), ASM-203.
- **project-knowledge**: Max/Maxie entry: model costs, order-status sources, SPC leaflet legal stance.
- **project-stakeholders**: Updated STK-037, STK-045, STK-050, STK-046 (name corrected), STK-017, STK-026.
- **project-daily**: 15 action items added.
- **project-lessons**: LL-79.
- **meeting-index**: Entry added.
