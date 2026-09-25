---
last_updated: 2026-09-24
type: external
attendees: [Jindřich Tůma, Marek Pillár, Jura Brázdil, Simona Mertová, Kateřina Kadlecová, Lucie Fendrichová, Šárka Andělová]
recording_link:
---

# Lexie/Max/Maxie Weekly Sync — Max Chatbot Fix Review, Model Ceiling, Methodology/RAG & Maxie IVR Alignment

**Date**: 2026-09-24
**Attendees**: Jindřich Tůma (BigHub, running the call), Marek Pillár (BigHub, shared X-Manager screen), Jura Brázdil (BigHub, Max chatbot dev), Simona Mertová (Dr. Max CZE, product/operational owner of Max/Maxie/Lexie), Kateřina Kadlecová (Dr. Max CZE), Lucie Fendrichová (Dr. Max CZE), Šárka Andělová (Dr. Max CZE)
**Type**: external
**Recording**: N/A
**Previous session**: [2026-09-17-lexie-max-maxie-weekly-sync.md](2026-09-17-lexie-max-maxie-weekly-sync.md)
**Meeting prep**: N/A

## TL;DR

Jura walked through a large batch of Max chatbot fixes and additions: opening hours rebuilt around search, a "stable/candidate" version switch, a context header showing the location and product being discussed, an end-conversation flow, and ~50 "golden conversation" regression replays. He then warned that the bot is at the ceiling of its current model (GPT-5 mini, ~10–12 instructions). Tone-prompt input from Dr. Max now has to be short keywords, and Jura will bring a cost projection for bigger models next week. Two blockers dominated the second half. Infra has been blocked for more than 6 weeks and is escalated to Dudaško ("nám na tom stojí úplně všechno" [translated from Czech: "everything hinges on it"]), which puts the end-of-September internal go-live phases at real risk. Mertová also objected that Dr. Max was left out of the Atlantis/SIP-trunk discussion: she wants Maxie built as an exact copy of the IVR solution they already have, and Jindřich committed to a joint meeting with Atlantis (Tecl) and Honza Zelený.

## Continuity from 2026-09-17

- **Tone brief for the system prompt**: delivered by Dr. Max, but too long. Jura reversed the 09-17 guidance ("~2 paragraphs, first-person") and now asks for short comma-separated keywords, because a long brief overloads the small model. Kadlecová noted the first-person format itself caused the bloat.
- **Resend the analytics dashboard link (Jura)**: still outstanding; Kadlecová reminded him ("URL s analytikou, nám bylo slíbený").
- **Connect to test orders / phone-number order lookup**: still not done. Order data is currently mocked. Jura has production order-DB access (tested lightly) but has not yet requested test-DB access; he committed to doing it right after the meeting.
- **GDPR consent/anonymization**: Kadlecová says Dr. Max Legal is still working out what is required. One confirmed legal requirement so far: the AI Act disclosure in the opening message.
- **New-conversation / idle handling**: partly delivered as an explicit end-conversation button plus detection of goodbye/thanks in the text.
- **Conversation rating**: the end-conversation flow currently asks for free-text feedback. Mertová confirmed free text is for testing only and must not reach the public, which matches [[ASM-017]].
- **Lexie design/UX polish**: Marek closed the loop. Lexie's redesign will be folded into the platform-wide redesign, and padding/border tweaks are low priority.
- **Not revisited this session**: MVP vs. full-product scoping mismatch, Paralen/Bašty and Brno-Líšeň retests, Lexie user documentation (due today, not mentioned), BDC ticket for the 4 Lexie test accounts, X-Manager Kanban restructure, Lexie fallback-message and English-title bugs.

## Key Discussion Points

### X-Manager hygiene

Jura couldn't share X-Manager while on VPN (the chatbot needs VPN, X-Manager rejects it), so Marek shared it. Kadlecová asked BigHub to update ticket statuses and write feedback in ticket comments: about five people on her side test in parallel and need to split the work without duplicating it. Jura apologized, saying he had spent his time on fixes and hadn't got to X-Manager. Jindřich owned it as BigHub's mistake and asked Jura to fill in replies and statuses right after the meeting.

### Max chatbot: fixes walked through

- **Opening hours / "open at 7am" queries**: rebuilt. The official API reports one pharmacy as not non-stop even though its hours are 0:00–23:59, which confused the model. Instead of getting every pharmacy and sorting them itself, the model can now issue search queries. It can now answer "which pharmacies in Prague open earliest" (non-stop first, then 6:00, 7:00, 8:00...) and no longer returns the same four central Brno pharmacies every time. It shows 3–4 nearby results with a "show all" expander. Andělová had hit a case where it said none of the four shown were open at 7am and didn't offer more; Jura says the rebuild fixes that.
- **Gender-neutral address**: Jura added a hard filter that catches gendered phrases ("byl/byla jste" etc.) and sends the reply back to the model to rewrite. He was candid that Czech makes this hard to catch deterministically and that GPT-5 mini isn't reliably able to rephrase into neutral forms ("mohl byste" → "můžete"). He asked testers to report concrete failures. He floated asking "Jak vás mohu oslovovat?" at the start, but noted it adds friction and could itself offend.
- **Using the logged-in profile for salutation** (Kadlecová): many doktormax.cz users are logged in and have a gender set in their profile. Jura said this could help, but only once the widget is integrated on doktormax.cz. It needs technical work to pass profile data to the one-line embed, and probably consent. Deferred.
- **"Show X more" carousel**: now freezes the carousel in place and appends results. Tested in Safari, Chrome and Firefox, but not on a phone because Jura can't reach VPN from mobile. Mobile testing was requested from Dr. Max.
- **Clickable phone numbers**: tap-to-call now works on cards and inline in messages.
- **"Remembered location across chats"**: not a memory leak. The system prompt used a real branch as an example, and the model hallucinated it into conversations. The example is now a fake, non-existent address.
- **Multi-drug queries** ("Paralen and vitamin C in stock?"): Jura spent a long time on this and got stuck. It's hard because the user may care which exact Paralen but not which vitamin C. Not solved.
- **Prescription (Rx) drug stock lookup without an e-recept**: Mertová flagged that the bot claimed it can only look up OTC products, and Andělová confirmed Rx lookups without a prescription fail. Jura: the capability exists but isn't wired to that path. He will connect it directly.
- **Hallucination creep**: Jura sees the bot starting to hallucinate more as the prompt grows. For example, it offers to "show on a map" even though the cards already have a route. He is adding prohibitions and watching the side effects.

### Max chatbot: new features

- **Stable/candidate switch** (top right): "stable" is what Dr. Max tests; "candidate" is Jura's work-in-progress. It stops his live changes from disrupting their testing. Dr. Max testers should stay on stable unless told otherwise.
- **Context header**: shows the currently tracked location and product (e.g. "Brno Bašty", "Paralen čípky") as removable chips. The bot keeps these across turns (a follow-up drug question checks the same pharmacy), so showing them makes it transparent, and the user can clear them.
- **End-conversation flow**: a header button ends the chat and shows a feedback box and a goodbye. The end is also detected from text ("děkuju", goodbyes, "už dobrý"). Mertová: the free-text feedback is fine for testing, **not for the public**; Jura agreed to remove it. Known bug: text is being copied into the feedback field.
- **Golden conversations**: ~50 recorded problem conversations are replayed live against the model on every publish, so known failures don't come back. Jura was clear this reduces regressions but isn't a guarantee.
- **Contextual proactive bubbles** (built last week, shown now): the teaser message changes with the doktormax.cz page (product page → stock lookup, branches → nearest pharmacy, orders → order status). The context is inferred from the URL, so no integration with the site is needed.

### Model ceiling, tone prompt and cost

Jura's core message: the Max chatbot runs on **GPT-5 mini**, which he describes as roughly able to follow 10–12 instructions before some start randomly dropping. BigHub's own system prompt (~1,200 characters) already covers the key rules (vykání, no medical advice, tool use). A client tone prompt as long as the one Dr. Max sent would overload it. His guidance: "klidně jenom klíčový slova" [translated from Czech: "just keywords is fine"], comma-separated ("buď zdvořilý, vykej"). Kadlecová noted the first-person format they were told to use inflates the text.

Kadlecová raised tone problems that keywords won't fix:
- **"Přátelská připomínka"**: a literal translation of "friendly reminder". It reads as passive-aggressive in Czech and could annoy sensitive customers.
- **Handling abuse**: when users swear, Max apologizes repeatedly. Dr. Max's human operators instead set a boundary ("let's keep it civil or I'll end the call").

Jura's answer: for cases like these, the only real fix is a bigger model. Starting on the cheapest model was right for development, but they are now at its edge. He offered to bring a **cost projection for different models** to the next meeting (and asked for expected traffic volume). He also offered a **model switcher on the test page** so Dr. Max can compare quality side by side (e.g. GPT-5.4 full vs. mini). Spend can be **capped monthly**, with the widget auto-hiding once the cap is reached. Kadlecová accepted both, noting Dr. Max holds a high bar for responses because they know their customers.

**Opening message**: it is hardcoded, not controlled by the prompt (which is why their prompt edits didn't change it). Dr. Max will send the exact wording. Legal requires an AI Act disclosure, along the lines of "Dobrý den, jsem Max, AI virtuální asistent" [translated from Czech: "Hello, I'm Max, an AI virtual assistant"].

### Quick-reply bubbles and layout

Kadlecová: the bot keeps listing everything it can do, which won't scale to 10+ topics. Dr. Max will shorten the opening line to the AI disclosure plus a greeting. The question is whether customers will understand the bottom bubbles as a menu. Jura argued that without bubbles users type "Ahoj" and the bot lists its capabilities anyway, and offered an A/B test. Kadlecová: keep the bubbles; the question is **placement**. Andělová proposed two options: move the bubbles up under the intro text, or move the intro text down just above the bubbles. Jura preferred the second as proper chat behavior (newest message at the bottom, history scrolling up). Kadlecová will write it into the ticket.

### Methodologies → RAG

Kadlecová asked when Max can use Dr. Max's public methodologies: customer-safe versions of the internal CC playbooks for follow-up questions such as "you can reserve it on the web; we hold reservations for 4 days". The order-tracking/reservation methodology (highest priority) is essentially done in Word. Sizes range from ~2 pages (opening hours) to ~20 (order tracking/returns); none are near 150. Jura: "send me PDFs, format doesn't matter". At tens of pages they won't fit in the prompt, so this means connecting to the **AI platform's RAG/search** from the neighboring platform project. That's a bigger piece of work, but possible.

Mertová asked whether Dr. Max can manage these documents themselves and choose which ones Max draws from. Jura: yes. The platform rewrite will give them one place with **usage reporting, an instant kill switch to pull the chatbot off the site, and document settings**.

### Order status data

Order data is currently mocked ("našvindlované" [translated from Czech: "faked"]). Jura has production order-DB access but not test-DB access, and is unsure who at Dr. Max infra to ask (he doubts Tvarůžek will know); he'll find out. Fendrichová asked whether he needs guidance per order status. Jura said yes: he had assumed only "delivering / delivered / cancelled". She will supply data on statuses, including combinations with specific carriers, so Max knows what to tell customers.

### Package leaflet (příbalový leták)

Andělová reminded Jura of an earlier discussion: showing the package leaflet in Max, with a specific section such as dosage highlighted. Jura had it as a low-priority bonus. It will be logged as a ticket so it's tracked.

### Testing constraints on Dr. Max's side

- Dr. Max work laptops can't test location/geolocation, and mobile testing is blocked. Kadlecová is asking their IT to allow it.
- Jura: nothing to worry about. Once phase 2 is deployed (the widget live on doktormax.cz but hidden, manually enabled), everything can be tested outside VPN, on personal phones, exactly as customers would see it.

### Infra blocker (production deployment)

Mertová asked about progress on moving into Dr. Max's environment. Jura: still waiting on "centrála"; the most important item, database access, still doesn't work, so nothing has moved. Jindřich: it is escalated "úplně nejvíc, jak to jde" [translated from Czech: "as high as it can go"], and Dudaško and others are involved. It has been waiting more than 6 weeks. MaxBuddy is top priority on the infra queue and this project is right behind it. Jura: "Nám na tom stojí úplně všechno" [translated from Czech: "everything hinges on it"].

### Maxie: Atlantis/SIP trunk and IVR design

Five infra requests are queued. AKS for MaxBuddy is first and Atlantis second; both are with BDC. Jindřich chased Vladislav Tvarůžek about it yesterday.

Mertová (also chasing it from her side) raised a process gap. A BigHub–Atlantis meeting happened without Dr. Max, and colleagues told her they "didn't know you had an existing solution". Dr. Max already runs "Maxí" in their IVR on Atlantis, built ~2–3 years ago with another vendor, and she wants this vendor to **replicate it exactly**. The PBX is rented from Atlantis, and Tecl at Atlantis knows the setup. She had already told Lukáš this when he owned it. Jindřich explained that he set up the Atlantis meeting ~3 weeks ago to verify a claim that a SIP trunk couldn't be configured. Honza Zelený represented BigHub; the goal was to get Atlantis's list of requirements. He confirmed the direction is to reuse the existing design, not invent a new one, but the SIP trunk still has to be configured.

Kadlecová added that Maxie must be **split by IVR topic branches** (order tracking in one branch, prescriptions in another). It shouldn't be one Maxie that answers everything.

Jindřich will gather all materials and set up a joint meeting with Honza Zelený, and, at Mertová's request, Tecl from Atlantis, so everyone is on the same page.

### Maxie: barge-in and voices

- **Barge-in**: Mertová heard at a conference that "you can't do this" and asked whether Maxie can stop talking when interrupted and respond to what the caller said (e.g. "stop, answer in one sentence"). Marek: on ElevenLabs it will certainly stop and listen ("to viem na 100 %" [translated from Slovak: "I'm 100% sure of that"]). Whether it picks up the interrupting context and answers correctly is likely but unconfirmed ("za toto ruku do ohňa nedám" [translated from Slovak: "I wouldn't swear to that"]). Marek and Jura will investigate.
- **Voices**: Dr. Max wasn't happy with the sample voices. Jura: those were ElevenLabs marketing samples. The product has many more voices, adjustable character settings, voice cloning from recordings and a voice designer, and pricing varies (probably thousands of Kč, not budget-breaking, he estimated). Marek: three voices are natively optimized for Czech/Slovak, and custom training is possible. Kadlecová expects the extended options are behind payment.
- **Licensing budget**: Mertová asked whether BigHub buys the ElevenLabs licences within this project or she needs to find budget herself. Jindřich didn't know, having joined mid-stream. He will find out, possibly with an ElevenLabs meeting to answer Dr. Max's questions.

### Closing: Marek

- **Lexie design**: the whole platform will be redesigned at some point, and Lexie's redesign will be part of it. Padding/border-type tweaks are lower priority; the focus now is the technical side. They can go into X-Manager as low-priority tickets so they aren't forgotten.
- **Mertová's email confirmation**: Marek had asked Mertová for an email confirmation, needed for the meeting he and Jindřich were heading to straight after (likely the Dudaško session that was waiting on Mertová's figures). She hadn't got to it and will try by tomorrow at the latest. Marek let the deadline go.

## Decisions Made

- Client tone-prompt input for Max is limited to short keywords, replacing the 09-17 "first-person ~2 paragraph tone brief" approach, because GPT-5 mini is at its instruction ceiling.
- Max's opening message stays hardcoded. Dr. Max supplies the exact wording, which must include an AI Act disclosure ("jsem Max, AI virtuální asistent").
- Free-text feedback on the end-conversation screen is for testing only and will be removed before public launch.
- Quick-reply bubbles stay. Layout changes to chat-style: intro text moves down directly above the bubbles, newest content at the bottom.
- Dr. Max's public methodologies (PDF) will be served through the AI platform's RAG rather than stuffed into the prompt. Dr. Max will get self-service document management in the platform.
- Maxie will replicate Dr. Max's existing Atlantis IVR "Maxí" solution exactly, split per IVR topic branch. Not a new design.
- Using the logged-in profile (e.g. gender for salutation) is deferred until the widget is integrated on doktormax.cz. It needs technical plumbing and likely consent.
- Lexie's visual polish folds into the platform-wide redesign. Minor padding/border requests are low priority.
- Package-leaflet display gets an X-Manager ticket (previously an untracked verbal "bonus").

## Action Items

- [ ] **Jura Brázdil**: Update X-Manager ticket statuses and add written replies to each ticket commented on today — due today (after the meeting) — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Request access to Dr. Max's test order database (find the right infra contact) and connect Max to it — due today — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Prepare a cost projection for running Max on different models (needs expected traffic from Dr. Max), and add a model switcher to the test page — due next weekly sync — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Wire prescription (Rx) drug stock lookup without an e-recept — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Remove free-text feedback from the end-conversation screen for the public version; fix the bug copying text into the feedback field — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Resend the Max analytics dashboard URL (outstanding since 2026-09-17) — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Create an X-Manager ticket for package-leaflet display with a highlighted section (e.g. dosage) — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová / Dr. Max CC team**: Send the exact wording of Max's opening message, including the AI Act disclosure — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová / Dr. Max CC team**: Shorten the tone prompt to comma-separated keywords — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová**: Write the bubble-placement change (intro text down above the bubbles, chat-style) into the X-Manager ticket — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová**: Get Dr. Max IT to enable mobile and geolocation testing on work devices — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová / Dr. Max CC team**: Send public methodologies as PDFs, starting with order tracking/reservations — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Lucie Fendrichová**: Provide order-status definitions and customer messaging, including combinations with specific carriers — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Test the "show X more" carousel fix on mobile phones — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Gather Maxie/Atlantis materials and schedule a joint meeting with Simona Mertová, Honza Zelený and Tecl (Atlantis) to align on replicating the existing IVR Maxí solution — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Find out whether ElevenLabs licences and voices are paid within the project or by Dr. Max; set up an ElevenLabs Q&A meeting if needed — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Marek Pillár / Jura Brázdil**: Check whether ElevenLabs barge-in can pick up the interrupting context and respond to it (not just stop and listen), and report back to Mertová — from 2026-09-24-lexie-max-maxie-weekly-sync
- [ ] **Simona Mertová**: Send Marek the requested email confirmation — due 2026-09-25 — from 2026-09-24-lexie-max-maxie-weekly-sync

## Open Questions

- Which model Max should run on in production, and at what monthly cost and cap. This depends on Jura's cost projection and Dr. Max's traffic estimate.
- How to get reliable gender-neutral Czech address on a small model. Options: the hard filter, a bigger model, profile data after integration, or asking how to address the user.
- How Max should handle abusive users. Dr. Max wants operator-style boundary-setting, not repeated apologies.
- Multi-drug stock queries: Jura attempted them and they're unresolved.
- Who at Dr. Max infra grants test order-DB access.
- Whether BigHub's end-of-September internal deployment phases ([[ASM-100]]) are still achievable, with infra blocked >6 weeks.
- Who pays for ElevenLabs licences and custom voices.
- Whether ElevenLabs barge-in handles the context of an interruption.
- "Pane Kotko?" (Jindřich, 52:46): an unidentified name, possibly a transcription artifact. Kadlecová spoke next.
- What exactly Mertová is confirming by email. Likely the Business Quantification figures awaited for the Dudaško session; not stated on the call.

## Sentiment & Tone

Cooperative and engaged. Dr. Max's CC team came well prepared with notes and specific cases, and their testing volume was explicitly praised by Jindřich. There was mild friction early on over X-Manager discipline. Kadlecová politely but firmly pointed out that five parallel testers were duplicating effort because BigHub hadn't updated ticket statuses. Jindřich took ownership immediately, which defused it.

Jura's candor about GPT-5 mini's limits ("je to malinkatej model a je hloupej" [translated from Czech: "it's a tiny model and it's dumb"]) was well received. It reframes future quality complaints as a cost/model decision for Dr. Max rather than a BigHub delivery gap, which is strategically useful ahead of the cost projection. Dr. Max signalled a high bar ("jsme poměrně náročný na ty odpovědi" [translated from Czech: "we're fairly demanding about the answers"]) and real sensitivity about customer tone (gender, "friendly reminder", abuse handling).

The most important relational signal came from Mertová on Maxie. Her tone was frustrated but constructive: Dr. Max was left out of the Atlantis meeting, BigHub colleagues were unaware of the existing IVR solution, and she had already told Lukáš the same thing. It reads as a trust dent from lost continuity during the ownership handover. Jindřich handled it well: he acknowledged the communication broke down, explained the original intent, confirmed the reuse direction, and committed to a joint meeting including Tecl. Following through on that meeting quickly matters.

The prolonged infra blocker is a shared frustration rather than a source of tension between the two companies for now. Mertová is chasing it herself. Mertová was also visibly stretched (called away by her boss, late for her next meeting, behind on Marek's email request). That fits the pattern of CC-side bandwidth limits alongside Kadlecová's upcoming maternity leave ([[ASM-091]]).

## Routing Log

- **project-assumptions**: Added ASM-149 (Max GPT-5 mini ceiling, Open), ASM-150 (keyword-only tone input), ASM-151 (hardcoded opener + AI Act disclosure), ASM-152 (free-text feedback test-only), ASM-153 (methodologies via platform RAG), ASM-154 (Maxie replicates existing Atlantis IVR solution), ASM-155 (ElevenLabs licence budget, Open), ASM-156 (Lexie polish folded into platform redesign), ASM-157 (bubble layout; profile personalization deferred). Annotated ASM-100 as at risk (infra blocked >6 weeks).
- **project-knowledge**: "Max / Maxie / Lexie" gained a 2026-09-24 status block plus corrections (Max runs on GPT-5 mini, not 5.4; tone brief superseded by keywords; Maxie SIP trunk still unconfigured). "Atlantis": existing IVR Maxí context. "ElevenLabs": barge-in, voice options, licensing question.
- **project-stakeholders**: Updated STK-001 (Marek), STK-003 (Jindřich), STK-017 (Mertová), STK-026 (Jura), STK-029 (Honza Zelený), STK-033 (Tecl, "Techl" in transcript), STK-037 (Kadlecová), STK-045 (Fendrichová), STK-050 (Andělová).
- **project-daily**: Added 18 action items to 2026-09-24's daily; marked Marek's Lexie padding push-back done; annotated the combined Dudaško meeting item with Mertová's pending email.
- **meeting-index**: Added entry for this meeting.
