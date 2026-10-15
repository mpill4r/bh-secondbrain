---
last_updated: 2026-10-15
type: external
attendees: [Šárka Andělová, Kateřina Kadlecová, Jura Brázdil, Marek Pillár, Jindřich Tůma]
recording_link:
---

# Lexie / Max / Maxie Weekly Sync — Platform Live on Production, Max Feedback Walkthrough, Legal Green Light on SPC

**Date**: 2026-10-15
**Attendees**: Šárka Andělová (Dr. Max CC), Kateřina Kadlecová (Dr. Max CC, "Kaťo"), other CC colleagues in the meeting room (names not in the transcript), Jura Brázdil (BigHub, developer), Marek Pillár (BigHub, PM), Jindřich Tůma (BigHub, joined late after a call with Tomáš Dudaško)
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-10-02-lexie-max-maxie-weekly-sync](2026-10-02-lexie-max-maxie-weekly-sync.md)
**Meeting prep**: N/A

> **Transcript note**: The CC team joined from a different meeting room without Simona Mertová, so the invite couldn't be forwarded; they joined via one laptop on the room screen. Speaker labels are mixed: many lines under "ANDĚLOVÁ Šárka" are Jura Brázdil (technical answers on the platform, pharmacy filtering and Lexie rights), and some under "Jura Brázdil" are the CC (e.g. the X-Manager app offer). Attribution here follows the content. "Jiro" is Jura. Opening small talk (Marek and Jura) is omitted.

## TL;DR

Jura showed the AI Platform, now deployed on **test and production**: Max reporting is live, with a settings page (version switch, stable/test, tone, a red "stop" kill switch) and a technical health view. He admitted almost none of the CC's Max tickets are done yet, because MaxBuddy and Lexie migration came first. Next week MaxBuddy and Lexie move to production, then Max goes to the drmax.cz test domain (activated by a URL parameter); Jura estimates ~14 days. In-platform user management (approved by Dudaško on 10-14) means CC admins will add their own testers. The walkthrough of CC feedback produced a list of fixes, including a pharmacy filter by **type** from the branch API (no warehouses/labs). **Legal approved the SPC leaflet display**; a second legal meeting on customer data and consent is proposed for **Fri 2026-10-23, 9–10**. Machata is on holiday until 10-27, so CC will create the logistics X-Manager app for BigHub and hand it to him later.

## Key Discussion Points

### AI Platform live on test and production

Jura's "bad news": he has handled almost none of the CC's tickets. "Good news": the infrastructure finally moved. The platform, the front door to all BigHub apps for Dr. Max, is deployed on both test and production. Max is planned to go to production together with MaxBuddy and Lexie. The focus is still MaxBuddy (rollout to all ~600 pharmacies) and Lexie.

What he showed for Max:
- **Reporting** is live and connected to the same service the CC tests on, so their messages and ratings appear there. What to measure is still to be agreed.
- **Settings** (still "too technical", to be tidied): model choice, a **version dropdown** (all chatbot versions so far; test versions will get readable names), a **stable** version (what customers see), and tone/character. Anyone with rights, Jura or a CC admin, can switch to a new version once happy. He wants an interactive chat window in settings for testing tone and versions.
- **Documentation**: a changelog kept up to date with what's online.
- **Technical status** (admins): health of every connected service. On production it showed an active problem: Max can't load orders.
- **Kill switch**: a big red "stop" button that removes Max from drmax.cz if something goes badly wrong.

Andělová asked for a **notification when Max can't reach ServiceNow or Order Service**. Jura: the platform has a working e-mail server, so incident e-mails are easy. Today only he sees failures, in telemetry that's "unusable outside my terminal" `[translated from Czech]`.

### User management and CC access

Since Dudaško's thumbs-up on 10-14 (see [[2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek]]), Jura is building user management in the platform. The CC will get **admin access**, add testers by e-mail, and choose per person: chat, reporting, settings. The person then only needs adding to one "platform users" Entra group. Right now everyone in the group is treated as a superadmin, so Jura must finish the rights first; the CC will then see only the Max row. He hopes it's **done next week**. Andělová asked for access; Jura asked the CC to **send the tester e-mail list** so he can request the Entra group membership.

### Rollout sequence and Max on drmax.cz

1. **MaxBuddy and Lexie to production** first. Jura hopes everything is tested **by the end of next week**. The switch from old to new environment will likely be done at night, on the phone with BDC.
2. **Max on drmax.cz**: needs the infrastructure team to register Max under the drmax.cz domain. Since the service has been live in the new environment since yesterday, Jura will **send the domain request today**. Vladislav Tvarůžek is on holiday this week; Martin Dubina covers, capacity unknown.
3. **Test site first**: there is a test version of the website (**drmax-space**); Jura forgot it, Andělová had sent it (with tester e-mail addresses) in the chat. He'll ask for Max on the test site first, since the implementation is the same as on production.
4. Max is enabled on the site with a **URL parameter** (like `?chatbot=test`), invisible to customers. Once the CC is happy, the stable switch publishes it. Jura estimates **~14 days** of work, then more testing on the site before going public.
5. **Production eRecepty and orders**: Jura needs access to the production database. Production Max is still connected to test orders. He'll ask for the domain and the production eRecept/order data **in one request**.

### Max feedback walkthrough (CC tickets)

Jura read all feedback but fixed nothing yet. Item by item:
- **Prescription drugs can be reserved**: Max will say so. Add.
- **"What can you do?"**: not handled yet. Add. Andělová: it should also mention eRecepty.
- **Memory within a conversation**: should keep earlier details; if it doesn't, it's a bug.
- **Wrong prescription-ID pattern**: ticket exists, not fixed yet. Fix.
- **Gender-neutral replies**: the user had used a feminine verb form, yet Max used the masculine. Jura will try to detect feminine forms and remember the user's gender. Czech gender agreement is a known AI problem.
- **Product ordering**: Max orders search results itself, aiming for relevance and **variety** (Paralen tablets, syrup, suppositories, not 10/25/50-tablet packs). Jura asked what the CC wants to promote; MaxBuddy prefers own brand and promotions, Max could use any rules (margin, best fit). Open.
- **"Pregnancy guide" offered to everyone**: "What medicines can you find?" fired a product search that returned a pregnancy guide, for all CC testers. Jura: "a banal AI failure" `[translated from Czech]`, will investigate.
- **Loops**: after an error Max repeats "Please try again" or "I can't call or reserve" over and over. Max now runs on **"GPT-6 Luna"**, about 6× cheaper than the previous "5.4". Jura will test Luna **with reasoning switched on** and measure the cost. Andělová: stay at most at the GPT-5 cost level agreed earlier.
- **Widgets instead of answers**: Jura pushed Max to show widgets without comment when the intent is clear, to avoid repeating what the widget shows. Agreed: a very short polite line, plus an answer to any question asked, no duplicate info. For "What medicines can you find?" the CC expects a simple sentence and a follow-up question.
- **Phone number shown, then replaced**: Max wrote a number, then within a second swapped the message for "see the card". Jura doesn't know how the message gets rewritten ("built with Mr Robot"), will investigate. Also, the card's **"call" link opens a calling app** in a new tab and never shows the number on Windows. Jura "tried to be too smart"; the number must be shown.
- **Ending the conversation**: detected by a regex ("na shledanou", "děkuju", "to je vše"); "pa" was missing. Add "pa"; if it keeps failing, add an LLM check or an "end conversation" tool.
- **Pharmacies in Líšeň**: Max shows the named place plus nearby pharmacies by distance, which the CC is fine with. The problem: it sometimes shows a **warehouse** customers can't visit, and inconsistently. Dr. Max's branch data has a **type**: "standard" (type 1) is a regular pharmacy to show; empty, lab, "not on web" etc. must never be shown. Also exclude pharmacies **in preparation**, **temporarily closed** (e.g. revitalisation; exceptions and opening hours should be in the API) and **special regions**. Jura: any rule on the API's JSON is easy; send the field and rules in the X-Manager ticket. He also proposed an **on/off list of branches in Max settings** (a mirror of the API with a manual toggle). Andělová likes an ad-hoc switch but doesn't want manual records replacing the rules. The rules must also apply to **Maxie**. The CC will file a ticket with the code list.
- **Where do I find my order number?**: parked until Max gets the **document system (RAG)** with customer-facing methodology, the same engine as Lexie (which Jura showed running faster).
- **Tone**: Max sounded curt and said "I can't call the pharmacy for you" unprompted. Jura: the prompt's list of "can't do" items makes it fixate; he'll add positive counterparts and extend the golden-conversation set.
- **Order states**: the CC sent X-Manager order states and carrier info ~14 days ago. Jura looked: the format is fine and he'll implement it; payments aren't in yet. He can also read the CC PDFs in Lexie if anything's missing.

### Lexie: back-office agent

The CC met their back office today. They want a back-office Lexie agent on the back office's own SharePoint ([[ASM-238]]). The X-Manager ticket has the SharePoint link. The back-office supervisor is **Jana Vaňková**. Marek asked for her name because BigHub is collecting Lexie uses from other departments, and suggested connecting with her to see the files; Andělová pointed him to the ticket.

Jura: once the platform launches next week, Lexie admins can **add a department** in settings, give it a knowledge base and pick files. Back office must also see the **front-office (CCC) methodologies**: CCC has a front office and a back office that work together.

Two options: (a) back office gets its own agent and opens on it by default (Lexie remembers the last agent), switching to CCC when needed; (b) back office sees all files. Andělová prefers testing (a) first: mixing front- and back-office methodologies on the same topic could blur answers. Jindřich asked Jura to rethink the agent **switcher** logic if users get roles per department. Jura's model today: departments, sub-departments, knowledge bases per department. He may add **document sets** (front office, back office, legal) to assign as a bundle. He'll design the rights first.

### Legal update

- **SPC leaflet: approved.** Dr. Max lawyers gave a thumbs-up. Andělová confirmed it's the SÚKL leaflet shown as is, with no calculation. Updates: synced **every morning ~6:00** from the DVH team's SPC API (which mirrors SÚKL), the same source as MaxBuddy; the platform shows the last sync. Jura: no dosage, no paraphrasing, no highlighting; he only scrolls to the relevant section.
- **Customer data / consent**: Dr. Max's lawyer engaged an external law firm and now wants a meeting with BigHub on data flows and integrations. Proposed **next Friday (2026-10-23) 9:00–10:00**; Jura, Jindřich and Marek will join. Jura's position: today only error events (no message content) and the CC's ratings/feedback are stored; the test feedback form won't be in production. Chats pass through **Azure OpenAI** (legal guarantee: no access or training) back to the browser without storage. Any richer reporting (e.g. user region) becomes personal data, especially if linkable to eRecepty, and must be anonymised. He asked the CC to think about what they'd want to measure, since the lawyer will ask.

### X-Manager for logistics (Jindřich)

Michal Machata gave X-Manager the **green light** for BigHub projects; a reusable project template is still being solved (apps can only be duplicated). BigHub needs a table imported for the logistics project now, but **Machata is on holiday until 10-27**. X-Manager is a platform of many apps, and BigHub doesn't have one yet. **The CC offered to create an app**, give BigHub access, and create the table from BigHub's Excel; when Machata is back, ownership goes to him and the CC steps out. BigHub sends the Excel and the app name by e-mail.

## Decisions Made

- **SPC leaflet display is legally approved** as is (unmodified SÚKL leaflet, scroll to section, no dosage or paraphrase).
- **Max goes to the drmax-space test site first**, enabled by a URL parameter; the stable switch publishes it later.
- **Pharmacy filtering follows rules on the branch API** (type 1 "standard" only; exclude in-preparation, closed, special regions); an ad-hoc on/off toggle in settings is welcome but not a replacement. Rules apply to Maxie too.
- **Widgets come with a short polite line and an answer to any question**, never duplicated info.
- **Phone numbers must be shown as text**, not only via a call link.
- **Back-office Lexie: start with a separate agent** (default on open, switch to CCC when needed) and test before giving it all files.
- **The CC creates a temporary X-Manager app for BigHub's logistics table**; ownership passes to Machata after 10-27.
- **Model cost ceiling stays at the GPT-5 level** when testing Luna with reasoning.

## Action Items

- [ ] **Jura Brázdil**: Finish in-platform user management and rights (CC sees only Max), then give CC admin access — due next week — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Šárka Andělová**: Send Jura the list of tester e-mails for the platform Entra group — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Send one request (today) for Max under the drmax.cz domain (drmax-space test site first) and for production eRecept/order data access — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Move MaxBuddy and Lexie to production and test by end of next week — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Add incident e-mail notifications (e.g. Max can't reach ServiceNow / Order Service) — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Max fixes from CC feedback: reservable Rx info; "what can you do" (incl. eRecepty); in-conversation memory; prescription-ID pattern; gender detection; pregnancy-guide search bug; loops; short line with widgets; phone number shown as text (no message rewrite, no app-only call link); add "pa" to conversation end; tone/positive prompt counterparts — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Test Luna with reasoning on and measure cost (ceiling: GPT-5 level) — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **CC team (Šárka Andělová)**: File an X-Manager ticket with the branch-type code list and filter rules (type 1 only; in-preparation, closed, special regions) — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Implement the pharmacy filter on the branch API (Max and Maxie); consider an on/off branch list in Max settings — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Implement the X-Manager order states / carrier answers (payments later) — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **CC team**: Decide what they want to measure in Max reporting (flag anything touching personal data) — before 2026-10-23 — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Design Lexie rights for departments/knowledge bases (back office with own agent + access to CCC methodologies; possible document sets); revisit the agent switcher logic — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Šárka Andělová**: Set up the legal meeting (customer data/consent, external law firm) for Fri 2026-10-23 9:00–10:00 with Jura, Jindřich and Marek — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma / Marek Pillár**: E-mail the CC the logistics Excel and the X-Manager app name — from 2026-10-15-lexie-max-maxie-weekly-sync
- [ ] **CC team (Šárka Andělová)**: Create the temporary X-Manager app, give BigHub access, import the table; hand ownership to Machata after 10-27 — from 2026-10-15-lexie-max-maxie-weekly-sync

## Open Questions

- **Product promotion rules for Max**: what should Max prefer when ordering results (own brand, promotions, margin)? The CC hasn't said.
- **Pregnancy guide bug**: why does a generic question trigger a search that returns the same product for everyone?
- **Who covers infrastructure**: Tvarůžek is on holiday; does Dubina have capacity for the domain request?
- **Lexie rights granularity**: CCC / back office / front office only, or finer? Document sets or per-department knowledge bases?
- **X-Manager kick-off with Machata**: Marek proposed Tue 10-20 / Wed 10-21, but Machata is away until 10-27. The kick-off needs a new date.
- **What reporting is allowed**: depends on the CC's wishes and the 10-23 legal meeting.

## Sentiment & Tone

Friendly and constructive, with patience on the CC's side. The CC tests daily and files detailed tickets, and Jura opened by admitting none were done; they took it well, thanks to visible progress (production platform, reporting, kill switch). Andělová is now the clear lead voice for the CC in Mertová's absence: organised, detail-driven (code lists, JSON checked before the meeting) and practical about reducing manual records. The legal green light on SPC removes a long-standing blocker, and the CC is actively steering the next legal topic. Jindřich arriving late and asking a favour (the X-Manager app) was received generously; the CC offered more than asked.

**Relationship signals**: The CC expects their feedback to be worked through soon. Jura promised to sit down on it "as soon as possible", which should now happen after the MaxBuddy/Lexie migration. Marek's question about the back-office contact was politely deflected to the ticket: the CC sees itself as the owner of that relationship.

**Watch-outs**:
- The fix backlog for Max is long and competes with the MaxBuddy/Lexie production move next week.
- The ~14-day estimate for Max on drmax.cz depends on BDC/infra capacity while Tvarůžek is away.
- Marek's X-Manager kick-off proposal (10-20/21) clashes with Machata's holiday.

## Routing Log

- **project-assumptions**: Added ASM-292 (platform live, Max rollout sequence), ASM-293 (pharmacy filter), ASM-294 (widget line, phone as text), ASM-295 (back-office Lexie, open), ASM-296 (reporting vs. personal data, legal 10-23), ASM-297 (temporary X-Manager app). Updated ASM-020 (SPC legally approved), ASM-234, ASM-236, ASM-237, ASM-238, ASM-243, ASM-102. ASM-063 retired (superseded by ASM-290).
- **project-stakeholders**: Updated STK-050 (Andělová), STK-037 (Kadlecová), STK-026 (Jura), STK-003 (Jindřich), STK-039 (Machata); added STK-075 Jana Vaňková.
- **project-knowledge**: AI Platform for Max, branch types, SPC sync, data stored by Max, Lexie structure.
- **project-daily** (2026-10-15): 3 PM items (Excel + app name e-mail, legal meeting 10-23, re-plan Machata kick-off) and CC/Jura waiting items added; SPC Legal item done; role-switching test-user item closed; Machata kick-off item annotated (away until 10-27).
