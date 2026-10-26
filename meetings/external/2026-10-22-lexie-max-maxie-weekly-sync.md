---
last_updated: 2026-10-22
type: external
attendees: [Šárka Andělová, CC colleagues, Jura Brázdil, Marek Pillár]
recording_link:
---

# Lexie / Max / Maxie Weekly Sync — Max Fixes on a Candidate, CC Gets Platform Admin, Lexie "Next" Libraries, Temporary Notes in Lexie & SÚKL Shortages

**Date**: 2026-10-22 (inferred: Marek refers to the Legal call as "yesterday", 2026-10-21; Jura leaves for the finance/accounting Lexie call, the 14:00 Švarcová follow-up)
**Attendees**: Dr. Max CC team in the room "CZ-BRN-TIT-CCManager" (Šárka Andělová named; other CC colleagues, individual speakers not separable), Jura Brázdil (BigHub, developer), Marek Pillár (BigHub, PM). Jindřich Tůma had a clash; Simona Mertová not present.
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-10-15-lexie-max-maxie-weekly-sync](2026-10-15-lexie-max-maxie-weekly-sync.md)
**Meeting prep**: N/A

> **Transcript note**: all CC lines come from one room microphone and are attributed to "the CC team"; Šárka Andělová is named once. "Paní Vertová" = Simona Mertová; "pan Dudáček" = Tomáš Dudaško; "Vláďa" = Vladislav Tvarůžek; "Max Body" = MaxBuddy; "Nestada" = reporting; "Čumeta" unclear (left as is).

## TL;DR

Jura has addressed all the open Max tickets and put the fixes on a **candidate version** on test. He hasn't fully tested it yet and asked the CC to help test against the tickets before switching to stable. The CC now has **access to the AI Platform frontend**, but was wrongly added as **superadmins** in Entra, so it will be **lowered to admins**, which may cause a short loss of access today. Jura demoed **"Lexie Next"** (rewritten core, faster, citations) with new **libraries**: document sets per department that can be shared and switched on or off per agent. That covers the back-office need. Agreed new features:
- an **admin-managed banned-word list** for Max, with prompts cleaned of "skladovost" and "pobočka" first
- **temporary priority notes in Lexie** for methodology changes, visible to operators, with attachments

The CC asked for stock from **Magento (sellable quantity)** instead of the public e-shop API, product links, and pharmacy prices. It also asked about **drug shortages from SÚKL**, which Marek tied to Legal's SÚKL request. On Max's **end-of-November rollout**, the CC doubts it is realistic; Jura thinks it is, with a new BigHub colleague joining him.

## Continuity (vs. 2026-10-15)

- **Done / progressing**:
  - Max feedback fixes ([[ASM-293]], [[ASM-294]]): all addressed on the candidate. Done items include:
    - SKU pharmacy search
    - widget line
    - no more "focus" / "in stock" leaks
    - phone number on the card
    - a "what can you do" list
    - the pregnancy-guide search bug, explained and fixed
  - Pharmacy filter: type 1 only on the branch API; labs, warehouses and HQ removed.
  - CC admin access to the platform ([[ASM-290]]): given, but at the wrong level.
- **Still open**:
  - Production switch of the new environment: next week. Jura is finishing user management first.
  - Max on drmax.cz / drmax-space ([[ASM-236]]): blocked on a contact via Tvarůžek; the service address changes next week.
  - X-Manager order states: the CC adds a "customer wording" column and a payment-methods table.
  - The CC's reporting wish-list: not discussed.
  - Legal meeting on 23. 10.: not discussed.

## Key Discussion Points

### 1. Max — feedback fixes (candidate on test)

- Jura addressed all tickets over the last 3 days and deployed them to the test server as a **candidate**, not yet switched to stable because he hasn't tested everything himself. **He asked the CC to test the candidate against the tickets** and close or comment them; otherwise he'll do it himself.
- Fixed:
  - **SKU search**: the CC confirmed it works.
  - **Product results**: now come with an accompanying sentence, e.g. "Paralen comes in several variants, pick yours".
  - **Leaked internal terms ("focus", "in stock")**: caused by naming those parameters in the prompt; removed from the prompt. Jura: "not mentioning it in the prompt is stronger than forbidding it" `[translated from Czech]`.
  - **Phone number appearing then turning into a card**: a hard post-filter catches phone numbers and addresses and swaps them for a card. It was rewritten so a sentence is checked by the filter before display. The pharmacy card now shows the number and a call button; clicking it starts a call. An alternative is copy-on-click, which works universally on phones.
  - **"What can you do"**: Max now lists find a product, check stock, find a pharmacy, order status, eRecept status, and should no longer offer to call anyone. New topics (Reklamace, preventive care) must be added to these prompts when they ship.
  - **Pregnancy guides returned for "can you search for medicines"**: plain text search matched a manual containing "léky"; fixed by the capabilities instruction.
  - **Pharmacy filter**: only type 1 in the API; labs, warehouses and headquarters removed. The CC warned that "viewed" (region 996) is a special case among the filters.

### 2. Max — banned words

- The CC writes methodologies with internal wording Max shouldn't use, for example **"skladovost"** (should be "skladová dostupnost" / "dostupnost produktu") and **"pobočka"** (should be "lékárna").
- **Agreed**:
  - Jura first removes these words from his prompts, since Max copies his wording.
  - He then adds a **banned-word list in Max settings** on the platform. The CC maintains it and can extend it as topics grow.
  - The list feeds the hard filter: a sentence containing a banned word is sent back to the model to be reworded, so the word never shows.
  - The filter is the "bigger weapon", used sparingly, because each catch costs a round trip and slows the chat.
- **CC files tickets** for the settings list and for removing "skladovost" / "pobočka".

### 3. AI Platform — CC access and roles

- Jura added the CC's e-mails to the platform frontend on test, with rights to Lexie and Max. They logged in and see "Platform admin". **Mistake**: they're in the **SuperAdmins** Entra group. They should be **Admins**, which means product admins for Lexie and Max. Tvarůžek will move them, so **access may drop briefly today**.
- Role model ([[ASM-290]]):
  - The 3 Entra groups (SuperAdmins / Admins / Users) are a **ceiling**.
  - SuperAdmins are only Jura, Dudaško and the people running the platform.
  - Admins can give any Dr. Max account up to their own rights.
  - Users only use the apps and never see settings.
  - An admin can switch roles **down, not up**.
- Adding a user takes two steps:
  1. **In the platform**: add the e-mail, then tick chat access, department / agent access and reporting access.
  2. **In Entra**: add the person to the platform Users group, via Tvarůžek. Without it the user sees "we know you, but you're not a platform user in Entra".
- An operator with only Lexie access lands straight in Lexie; tiles and the header status appear only with more apps.
- The **technical health view** shows API, indexer, last document sync (e.g. 23 min ago) and database. It can be shown to users if wanted.
- A **broadcast message** for all users in platform apps (a request from Dudaško or Vosmek) is planned, shown at the top or in the welcome area.
- **Test users / "view as user"** are on Jura's list before the production release next week; the CC needs it for procedures and operator training. User management is the last thing Jura must finish before the production switch next week.

### 4. Lexie Next — libraries

- "**Lexie Next**" runs next to the original Lexie: rewritten core, noticeably faster, citations working, everything Lexie did before should still work. **The CC should use the platform version from now on.** They had noticed the old link suddenly showing all agents.
- New concept, **libraries**:
  - A library is a named set of documents picked from the SharePoint folders, with an optional description. Jura's example: a "Legal" library for the legal department, with HR also given access.
  - A **knowledge base / agent gets one or more libraries**, each **on or off by default**. Example: the CC agent uses CC documents by default and can switch on IT documents.
  - Users see the active libraries in the chat and can toggle optional ones.
  - This answers cross-department sharing ([[ASM-295]]), e.g. a shared library for documents used by several departments.
- Jura is still polishing the UI; libraries and knowledge bases look different in settings, and things may change under their hands.
- **The CC will try creating the back-office agent** with libraries and come back with questions.

### 5. Lexie — temporary notes for methodology changes

- **Problem (CC)**: there are many long methodologies with repeated content. Small changes (e.g. per warehouse, from a date) are announced by e-mail long before the documents are updated, and operators lose them among ~150 e-mails. Kadlecová earlier suggested a "sticker" or update flag.
- **Jura**: conflicting documents can't be solved inside RAG; the model "hallucinates something in between" `[translated from Czech]`. Proposal: a **list of temporary notes in Lexie admin settings**. Lexie checks the notes on top of retrieved documents and treats them as **priority**. The CC deletes a note once the documents are updated.
- **Agreed extras**:
  - Lexie must **explicitly point out** the note in its answer. Example: "advance invoices for warehouse 750 are issued in … from date X".
  - Notes are shown to operators as a **pull-down list** in the chat, next to the active documents.
  - Notes are editable and deletable, and **visible per department**.
  - **Attachments** (PDF / image) are for operators to open. Lexie reading them is harder and not needed.
- **CC files a ticket.**

### 6. Max — order states, payment methods, timing

- The X-Manager order-state tables are in. The CC adds a column with **customer-friendly wording** (no internal states like "send to", "was done") and a **payment-methods** table, so the order detail shows carrier, payment and state. More needs per "bubble" come in a file after review with Mertová; it's not a ticket.
- Sequence confirmed: platform first, then staging (drmax-space), then eRecepty, order status and SPC leaflets.
- **Timing (Jura)**: the new environment goes live **by end of next week**; user management is the last item. Max on the website needs:
  - **one line of JavaScript** on drmax.cz / drmax-space, needing a contact via Tvarůžek, who is slow to answer (security incidents across the internet in the last 72 hours). The service address changes with next week's switch, so he doesn't want to request it twice.
  - **network openings** (SPC, orders, internal APIs), usually hours.
- Hope: something on drmax-space next week, more the week after. **The CC offered to nudge** on its side and pass a contact to Jura.

### 7. Max — stock source, product links, prices

- The e-shop stock shown comes from the **public e-shop API** (search-service / stock-status endpoints the drmax.cz site calls; Jura "pretends to be the e-shop").
- **CC**: the correct value is **Magento "sellable quantity"**, which already deducts open orders. **Agreed**: connect to Magento internally, which Jura agrees is more correct. Jura arranges it with Tvarůžek, possibly via a BDC ticket; the **CC files a ticket** with the exact field.
- **Product card → e-shop product link** for products sold on the e-shop (Rx drugs aren't): technically possible; Jura needs to find the link, possibly via Magento. A reservation link exists today for eRecept drugs; direct reservation from Max is a wish.
- **Pharmacy prices** (with / without loyalty card, co-payment): customers ask about price in ~90 % of availability calls, and pharmacy prices differ from e-shop prices. Jura doubts the stock JSON carries prices (it has SKU, quantity and pharmacy IDs). He'll check; otherwise they'd come from the **DVH data warehouse**, which MaxBuddy already mirrors. The CC first decides internally whether Max should tell prices at all.
- The CC was told to **write down all wishes**, harder ones included; Jura: "anything your website does, the chatbot can do" `[translated from Czech]`.

### 8. Max — drug shortages (SÚKL)

- **CC**: callers often ask whether a drug in a nationwide shortage (supplier outage, listed on SÚKL) is orderable yet. Could Max say so?
- **Jura**: he must check whether SÚKL data can be read programmatically. Dr. Max IT already runs an **SPC mirror** (the DVH SPC service MaxBuddy uses), so the same service could store more SÚKL data (shortages, end and restart dates, reimbursement). He'll **file a ticket to the data warehouse** now, since DWH changes took weeks last time.
- **Marek**: Legal asked about SÚKL yesterday too (marketing compliance). SÚKL connected to the AI platform has now come up in several departments; it's likely a **separate, shared service** rather than a Lexie feature, usable by every app ([[ASM-328]]).
- Jura: the platform's point is reusable tools, e.g. extracting Lexie's document core for Max and MaxBuddy's SPC access for others.

### 9. 2027 initiatives and the Max deadline

- **Marek**: he raised 2027 initiatives with Mertová on Friday; she said CC capacity is small. Did she mention it? **CC**: yes, and asked back how BigHub sees the timeline. Max has an **end-of-November** deadline, which the CC personally doesn't find realistic given the technical work left before they can even test.
- **Marek**: the initiatives are independent of current delivery. It's only collection and prioritization, delivered possibly in the second half of 2027, and costs a few minutes of their time in November–December. Mertová will answer, perhaps next week.
- **Jura**: end of November **is realistic**. A new BigHub colleague joins him on the Dr. Max projects and takes one or two whole projects off him; the last three weeks were consumed by the migration, and "after next week it's a different story" `[translated from Czech]`.

## Decisions Made

- **Max banned-word list** in platform settings, maintained by the CC, enforced by the hard filter; Jura first cleans "skladovost" and "pobočka" from his prompts.
- **CC uses the AI Platform** (Lexie Next, Max) from now on; CC users are lowered from SuperAdmins to Admins.
- **Lexie libraries** are the way to share documents across departments; the CC tries them on the back-office agent.
- **Lexie temporary notes**: admin-managed, per department, treated as priority and explicitly called out in answers, visible to operators as a list, with attachments for operators.
- **Max stock** moves from the public e-shop API to Magento sellable quantity.
- **SÚKL data** (shortages etc.): Jura files a data-warehouse ticket; treated as a shared capability, not Max-only.

## Action Items

- [ ] **CC team**: Test the Max candidate against the open tickets; close or comment each — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Finish testing the Max candidate and switch it to stable — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **CC team**: File tickets: (1) banned-word list in Max settings; (2) remove "skladovost" / "pobočka" from prompts; (3) Lexie temporary notes with attachments; (4) Magento sellable quantity (exact field) — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Remove "skladovost" / "pobočka" from Max prompts; add the banned-word list to Max settings, wired to the hard filter — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Fix CC roles: SuperAdmins → Admins via Tvarůžek; admins see only what they may change; add test users / "view as user" before next week's production release — due week of 2026-10-26 — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Switch the new environment to production — due end of week of 2026-10-26 — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **CC team**: Try creating the back-office agent with Lexie libraries; send questions — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Build Lexie temporary notes (admin list, per department, priority, explicit callout, operator pull-down, attachments) — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Get a drmax.cz / drmax-space contact via Tvarůžek for the JS snippet and network openings (after next week's address change) — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **CC team**: Nudge internally and pass Jura a contact for adding Max to the website — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **CC team**: Add a customer-wording column to the order-state tables and send the per-bubble requirements file (after review with Mertová) — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Connect Max stock to Magento sellable quantity (with Tvarůžek; possibly a BDC ticket) — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Check whether pharmacy prices (with / without loyalty card, co-payment) are available in the stock data, else via DVH; tell the CC — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: File a data-warehouse ticket for SÚKL shortage data (alongside the SPC mirror) — from 2026-10-22-lexie-max-maxie-weekly-sync
- [ ] **CC team / Simona Mertová**: Decide whether Max should tell prices; answer on 2027 initiatives — due week of 2026-10-26 — from 2026-10-22-lexie-max-maxie-weekly-sync

## Open Questions

- Will the CC's end-of-November Max deadline hold? CC doubtful, Jura optimistic.
- Who adds the JS snippet to drmax.cz, and when?
- Can SÚKL shortage data be read programmatically / added to the DVH mirror?
- Are pharmacy prices available anywhere BigHub can read?
- Should Max state prices to customers (CC decision)?
- Who is the new BigHub colleague joining Jura, and which projects move to them?

## Sentiment & Tone

Friendly, hands-on and productive, a working session more than a status call. The CC is engaged and thinking ahead (banned words, notes, prices, shortages) and appreciates the platform access ("úplně skvělý"). Underneath there's **timeline anxiety**: the CC openly doubts the end-of-November Max date and is stretched (little capacity for 2027 initiatives). Jura is candid about his workload ("pekelné" three weeks of migration) and about the superadmin mistake, and optimistic that things free up after next week. Dependence on Tvarůžek (Entra, website, network openings) is the recurring bottleneck.

## Routing Log

Confirmed by PM 2026-10-22 ("confirm all"):
- **project-assumptions**: added ASM-332 (banned words), ASM-333 (Lexie libraries), ASM-334 (Lexie temporary notes), ASM-335 (Magento stock), ASM-336 (SÚKL shared capability), ASM-337 (Max end-of-November doubt); updated ASM-290, ASM-292, ASM-293, ASM-294, ASM-295, ASM-236.
- **product-requirements**: REQ-006, REQ-007.
- **project-stakeholders**: STK-050 Andělová / CC, STK-026 Jura, STK-016 Tvarůžek, STK-017 Mertová.
- **project-knowledge**: Lexie Next + libraries; platform roles + user onboarding; Max internals.
- **project-daily** (2026-10-22): 15 items added, 3 closed, 6 annotated.
