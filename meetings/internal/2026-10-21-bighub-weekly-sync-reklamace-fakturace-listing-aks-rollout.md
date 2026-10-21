---
last_updated: 2026-10-21
type: internal
attendees: [Jindřich Tůma, Filip Černý, Jura Brázdil, Juraj Kmec, Marek Pillár]
recording_link:
---

# BigHub Weekly Sync — Reklamace Phase 1.1 Close-out, Fakturace Mock Deploy, Listing Risk, AKS Switch & Pharmacy Rollout

**Date**: 2026-10-21 (Wednesday)
**Attendees**: Jindřich Tůma (BigHub / Dr. Max AI ambassador, host), Filip Černý (BigHub developer, logistics), Jura Brázdil (BigHub, AI platform / MaxBuddy / Lexie / Max), Juraj Kmec (BigHub, order prediction), Marek Pillár (BigHub, PM)
**Type**: internal
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: N/A (first recorded team-wide sync). Related: [2026-10-20 Fakturace doprav scanner call](../external/2026-10-20-fakturace-doprav-canon-scanner-zebra-kiosk-hyza.md)
**Meeting prep**: N/A

> Jindřich left at ~30:40; the last part (node pools, secrets) was Jura, Filip and Juraj only. Listing names in the transcript ("Tomincová", "Tiglová") are Michaela Vdovicynová and Týblová (confirmed by PM).

## TL;DR

Reklamace Phase 1.1 can close with the new UI, login and the shared-mailbox integration; BigHub's own remaining work is only login + mailbox, the rest waits on logistics (3 Swagger changes, X-Manager API key via Machata, Axapta readiness). The team sets an **internal target of end of October** and will ask logistics on Thursday to answer fast. Fakturace gets a **mock deployment without Axapta** so logistics can click through recognition and the UI. Listing is at real **risk of closing** (Magento import/export blocked, Neuman's team unresponsive); Jindřich will take Neuman to lunch. On the platform side, **MaxBuddy, Lexie and the platform shell now run on production**; after a ~20-min switch to the new node pools and a DB scale-up, **more pharmacies could be added at the end of next week**.

## Key Discussion Points

### 1. Reklamace — Phase 1.1 close-out and timeline

- **X-Manager**: the last piece is the **API key**. The team waits for **Michal Machata** (on holiday until the end of the week); **Jindřich** contacts him on Monday so as not to bypass him. Data and tables are already available; Filip found who provides the API.
- **Shared mailbox**: integration is ready on Dr. Max's side; finishing it is a short job for **Filip**. Open for Thursday: **how logistics wants to test the e-mails** (e.g. sending from fake suppliers).
- **Swaggers**: all three — **one for Fakturace doprav, two for Reklamace (inbound, outbound)** — need smaller or larger changes. **Filip** wants to do them in one structured go and send the proposals **by the end of this week**; open detail points (which data comes from where) are listed for Thursday.
- **Login**: in progress with Jura's user management. **Jura**: rights names can be arbitrary per app; Vladislav Tvarůžek is creating the **3 Entra groups (users, admins, superadmins)**, which act as ceilings; Filip is superadmin and assigns admins their rights.
- **Phase 1.1 scope** (Filip): everything logistics already had, plus the **new UI** (Jana Egrmaierová likes it), **login** and the **shared-mailbox integration**.
- **Timeline**: BigHub's own remaining work is only login + mailbox; the rest depends on logistics answering the Swaggers ("if they reply in 3 weeks, we can't finish next week"). **Jindřich**: present it Thursday as an **internal target to deliver by the end of the month** (end of next week) and ask logistics to respond quickly — the changes are small, Petr Sláma and **Jan Kopecký** should decide in ~2 hours.
- **Axapta readiness** (Filip): unclear what Axapta has built; likely **not ready for the inbound call** (a button in Axapta that triggers document generation on BigHub's side), which also blocks e-mail testing. **Jindřich**: today's roadmap/timeline meeting should state what Axapta must deliver now and in later phases; at the **steerco and management meeting with Rudolf Žůrek in ~2 weeks** he'll say, politely, that BigHub is on time and waiting on Axapta. Žůrek already puts pressure on them.

### 2. Fakturace doprav — scanners and a mock deployment

- **Scanner call (2026-10-20)** went well (Marek sent Jindřich the recap): the **Canon** representative picked a scanner that handles the load, plus a **Zebra** PC (same vendor as the Reklamace terminals). Screen size still open; **Dušan Hýža** is checking an extra monitor.
- **BigHub's role**: give minimum parameters; logistics decides the hardware. Filip: they want BigHub's view but will choose themselves; BigHub can work with several variants.
- **Device lifespan (5–10 years)**: Filip calls it irrelevant — it's a **web app**, so a new device just opens it. Phones were ruled out by Hýža for network-security reasons (as with order prediction earlier). Jindřich will say this at the steerco.
- **Mock deployment**: Filip offered last Thursday to deploy a version **without Axapta** (no saving or loading) so logistics can try recognition and the UI; ~half a day (separate branch). **Agreed** — Jindřich: useful for early feedback; Marek: "fan of iterative development".
- **Priority**: **Reklamace first**; within it, Filip picks where he can progress (login vs. Swaggers).
- **Swagger sign-off** (Marek): can Filip move on the Fakturace Swagger without Jan Žižka's written approval? The mapping Excel should reflect what was agreed (Sláma accepted, Žižka said "send it"), but Marek wants it **confirmed by e-mail** to avoid doing it twice. Filip will review the Excel today. Context (Filip): logistics argued internally and **Žižka won**; BigHub had already built it his way, so nothing needs redoing.

### 3. Listing — closure risk

- **Marek**: Michaela Vdovicynová wrote (2026-10-16) that Týblová should send the materials for the next category **this week**. Magento import/export still isn't passable, so BigHub can't move the main flow.
- **Risk**: Marek rated Listing **high risk** in the register: BigHub can do everything on its side and bill hours for Neuman, but without a working route into Magento it won't be an end-to-end project soon. Neuman himself expects it may fail on non-cooperation outside BigHub.
- **Listing 2.0** (bulk regulatory edits) is logged as a 2027 initiative, but Neuman's team doesn't reply to e-mails or review the spec despite reminders, so Marek hasn't opened further initiatives with Neuman.
- **Jindřich**: an all-team sync next week, and a **lunch with Neuman** to make clear that cooperation and faster feedback are on his side — or whether BigHub should focus elsewhere.

### 4. Team capacity

- A **new person at 0.5 FTE** joins (Jindřich aims for 1 FTE, split between logistics with Filip and Jura). Intro sync **today** with **Kuba Vodička**: Jindřich covers the business side, Jura the technical fit.
- **Jura** would use help on **Lexie / Max chatbot tickets** — he can't keep up with the chatbot.
- **Juraj Kmec** is free from **mid-November** (Mattoni ends in the first half of November; Albert is blocked). Jindřich plans to use him on other projects.

### 5. AI platform, AKS and the MaxBuddy rollout

- **Production**: network access for MaxBuddy appeared yesterday, so **MaxBuddy, Lexie and the platform shell are fully functional on production**.
- **User management**: Jura is wiring the 3 Entra groups (ceilings: superadmin everywhere; admin everywhere except platform settings; users everything except app settings, as assigned by an admin). Filip and Juraj will be added so they can register their apps.
- **Rollout to more pharmacies**: once users are done (hopefully today), switch to the new node pools — about **20 minutes of downtime** on production (delete services, re-point the namespace node selector, redeploy) — and scale up the DB in the same window (tested on test). No Dr. Max dependency. Jura: "**end of next week we can add more pharmacies**" — already told Dudaško and Luboš Vosmek. Jindřich will say the same, with caveats.
- MaxBuddy and Lexie roll out **only together with the platform**; Jura still owes a **handover document**.
- **Dudaško** is very happy with the platform and shows it around. He says his latest MaxBuddy documentation is from June; **Jura**: the latest is from **8 September**, in the platform under the Documentation tile (with a changelog), on test and production. Jindřich will clarify which document he means.
- **Lexie / Max chatbot tickets** haven't been handled since the last meeting; CC meeting is **tomorrow** — Jura to check them today.

### 6. Order prediction

- **Juraj**: no change; it runs and calculates correctly. He forgot the budget Excel and fills it in today. The product sleeps until a new release is wanted.

### 7. Node pools (after Jindřich left)

- The new isolated node pools (serving + batch) on test and production don't necessarily have the same network rules as the old pool. Juraj's order-prediction test already runs on the new pool (warehouse DB unreachable on test is expected); production is still on the old pool. Filip's test (Axapta/Boomi access only) works on the new pool; nothing of his is on production yet.
- Production uses a different GitOps setup (namespace-level node selector only); endpoints may clash, so new URLs are registered. The production switch is planned **around midnight with Vladislav Tvarůžek and someone from BDC**.
- Apps don't have to register in the platform; they can later register an endpoint for settings, docs and technical status (see MaxBuddy / chatbot / Lexie). User management lives in the `next-platform` branch; Jura pushes a commit so Filip can run it locally.
- **Juraj**: an alert says a **shared AI-platform secret expires around late October / early November**; he'll find which one and send it to Jura.

## Decisions Made

- **Reklamace Phase 1.1 = existing scope + new UI + login + shared-mailbox integration.** BigHub's internal target is the **end of October**; logistics is asked on Thursday to answer the Swaggers fast.
- **Fakturace: mock deployment without Axapta** for logistics to try recognition and the UI.
- **Priority for Filip: Reklamace first.**
- **Hardware: BigHub gives minimum parameters, logistics decides**; device choice doesn't affect the web app.

## Action Items

- [ ] **Jindřich Tůma**: Contact Michal Machata on Monday for the X-Manager API key — due 2026-10-26 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Filip Černý**: Send logistics the change proposals for all 3 Swaggers (Fakturace; Reklamace inbound + outbound) — due 2026-10-23 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Filip Černý**: Finish Reklamace login and the shared-mailbox integration (Phase 1.1) — due 2026-10-30 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Filip Černý**: Deploy the Fakturace mock version (no Axapta) for logistics to click through — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Filip Černý**: Review the Fakturace mapping Excel against the agreed scope — due 2026-10-21 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Marek Pillár**: Get written e-mail confirmation of the Fakturace agreement (mapping Excel) from Žižka / Sláma — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jindřich Tůma / Marek Pillár / Filip Černý**: Thursday ViaPharma sync — internal end-of-month target, fast Swagger answers (Sláma + Kopecký), e-mail testing approach, Axapta readiness for the inbound call — due 2026-10-22 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jindřich Tůma**: Schedule the steerco with Rudolf Žůrek (~2 weeks) — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jindřich Tůma**: Lunch with Petr Neuman on Listing cooperation and feedback speed; all-team Listing sync next week — due week of 2026-10-26 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jura Brázdil**: Check the Lexie / Max chatbot tickets before tomorrow's CC meeting — due 2026-10-21 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jura Brázdil**: Switch to the new node pools (~20 min downtime, with Tvarůžek + BDC) and scale up the DB; target adding more MaxBuddy pharmacies at the end of next week — due 2026-10-30 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jura Brázdil**: Write the platform handover document — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Jindřich Tůma**: Clarify which MaxBuddy documentation Dudaško means; point him to the platform Documentation tile (latest 8 Sept + changelog) — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout
- [ ] **Juraj Kmec**: Fill in the order-prediction budget Excel; identify the expiring shared AI-platform secret and send it to Jura — due 2026-10-21 — from 2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout

## Open Questions

- How does logistics want to test the e-mail flows (fake suppliers?) — Thursday.
- What has Axapta actually built (inbound call / document trigger), now and per later phase?
- Will logistics answer the Swaggers fast enough for the end-of-October target?
- Listing: is the next-category material really coming this week, and is there any route into Magento?
- Which shared platform secret expires, and when exactly?

## Sentiment & Tone

Upbeat and practical. Jindřich kept a positive line toward the client (BigHub on time, waiting on Axapta/logistics) and protected Filip's focus on Reklamace. Real concern only on Listing, where both Marek and Jindřich see closure risk from non-cooperation. Jura is stretched (platform migration since early August, tickets piling up), which the incoming 0.5 FTE should ease.

## Routing Log

Confirmed by PM 2026-10-21 ("confirm all"):
- **project-assumptions**: added ASM-317 (Decided: Reklamace Phase 1.1 scope + end-of-October target), ASM-318 (Decided: Fakturace mock deploy), ASM-319 (Decided: hardware — BigHub min params, logistics decides), ASM-320 (MaxBuddy pharmacy rollout end of next week), ASM-321 (Axapta inbound call not ready), ASM-322 (Listing closure risk).
- **project-knowledge**: AI platform production state + node pools; Fakturace hardware + mock deployment.
- **project-stakeholders**: Michal Machata, Jan Kopecký, Juraj Kmec, Kuba Vodička updated.
- **project-daily** (2026-10-21): 14 action items added; Fakturace mapping-Excel item checked off; Listing waiting item updated (Vdovicynová / Týblová confirmed).
