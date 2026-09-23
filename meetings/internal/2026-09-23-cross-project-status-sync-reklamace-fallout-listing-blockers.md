---
last_updated: 2026-09-24
type: internal
attendees: [Jindřich Tůma, Alana Sihelská, Juraj Kmec, Filip Černý, Marek Pillár]
recording_link:
---

# Cross-Project Status Sync — Reklamace Fallout, Fakturace Doprav Friction & Listing Blockers

**Date**: 2026-09-23
**Attendees**: Jindřich Tůma (BigHub↔Dr. Max coordination lead), Alana Sihelská (BigHub), Juraj Kmec (BigHub — order prediction), Filip Černý (BigHub — logistics/listing developer, STK-006), Marek Pillár (AI Analyst). Jakub Turner (STK-007) was expected but did not join — Filip had spoken to him in the morning with no indication he wouldn't be there.
**Type**: internal
**Recording**: N/A
**Previous session**: [2026-09-16-devops-kanban-rollout-status-sync](2026-09-16-devops-kanban-rollout-status-sync.md) (closest prior instance of this recurring cross-project status format — same core attendee group)
**Meeting prep**: N/A

## TL;DR

Jindřich briefed the team on a client-side calibration meeting he ran today with Petr Spilka and Tereza Foltýnová to correct a circulating narrative that "BigHub doesn't want to deliver" Reklamace's AI scope — both understood the digitization reframe, but the continue-or-close decision now needs a management-level meeting (Dudaško, Žůrek, Spilka, Žižka), complicated by Dudaško's plan to retire Axapta within ~6 months. Fakturace doprav's API-contract renegotiation with Petr Sláma remains stuck (no counter-proposal, slow replies); Listing stays deliberately paused pending Petr Neuman's input; order prediction is in good shape modulo one blocked Excel ask (Šimoník now on vacation). Marek's cross-portfolio Business Quantification tracker is ~99% done, pending final owner sign-off.

## Key Discussion Points

### Reklamace reframe — calibration meeting and the "BigHub doesn't want to deliver" narrative

Jindřich ran a meeting today with Petr Spilka (STK-014) and Tereza Foltýnová (STK-013) specifically to address information he says has been circulating — that BigHub doesn't want to do or deliver something on Reklamace. He explained openly that the project shifted to a digitization framing for reasons that emerged over its course: the supplier Excel was cleaned up and consolidated, and it makes sense for the supplier data source to be Axapta alone (more stable than Excel); similarly, the "knowledge base" need turned out to be overstated — really just two sentences of warehouse-worker procedure, solvable with one added Axapta parameter rather than a genuine knowledge-base build. Spilka and Foltýnová both understood this framing when explained directly.

The next step — a decision meeting with Jindřich, Dudaško, Žůrek (STK-024), Spilka, and Žižka (STK-015) — is complicated by new information: Dudaško wants Axapta retired within roughly the next 6 months (calling it too expensive to keep developing against) and is willing to accept **higher near-term dev cost now** for a Reklamace solution that can carry over cleanly onto whatever replaces Axapta — "even at the cost of more expensive development here, having a solution I can then reapply on another platform behind Axapta is a go for me" [translated from Czech]. Jindřich flagged this decision is now bigger than what he can resolve alone, hence the need for that management-level meeting.

Separately, Tereza Foltýnová wants to communicate with Rudolf Žůrek directly first, before that group meeting — Jindřich reads this as her having her own reasons, not something to push back on. She had also been the source of the "BigHub doesn't want to" framing; Jindřich corrected this with her directly today: if BigHub actually wanted to under-deliver, the play would be integrating an external knowledge base and padding time/cost — instead, whenever a more efficient solution exists, BigHub says so, explains why, and does so on the record in weekly statuses. His view: everything here was handled correctly from a vendor standpoint — the project's nature genuinely changed mid-flight (from an initial AI-leaning prediction concept to something else), and now the conversation should be about what happens next, not about blame.

Foltýnová's own reaction, per Jindřich, showed some confusion — she asked whether this means someone else would now handle it, or whether it would move onto Dr. Max's own infra and get "tuned up" there. Jindřich was explicit this is **not** what changing AI→digitization means — it only means the project's character changed; whether BigHub finishes it or someone else takes over is a decision for the management meeting, not something to resolve by chat with her alone. Jindřich asked the team to present this openly and consistently to logistics stakeholders going forward (it's already known after today's meeting, not a secret), and — critically — to flag it to him directly if anyone feels Tereza is pushing a decision or a claim onto them that isn't accurate, rather than resolve it individually. He noted the communication channel around this is currently running largely through her, and wants the team aligned rather than getting inconsistent messages from different angles.

### Business Quantification tracker — near final, one number worth double-checking

Marek's consolidated cross-portfolio value tracker is, per Jindřich, "99%" ready — content built by Marek with each business owner, now waiting on a final sign-off ("thumbs up") from each owner before being presented at a future status (tentatively next week). Jindřich previewed one figure: MaxBuddy's annual saving at **~130M Kč**. **Note**: this differs from the ~81M Kč MaxBuddy figure discussed directly with Marek on 2026-09-22 (see [[ASM-098]], [[ASM-099]], and that session's meeting note) — flagged as an open discrepancy to resolve before the tracker is finalized, not assumed to be an update superseding the earlier number. Jindřich also previewed the intended use of this data: initiatives modeling out at only ~700k Kč/year will get deprioritized given limited team bandwidth (particularly on the Max side) — consistent with the >1M Kč/year priority filter already discussed with Marek (see [[ASM-125]]).

### Reklamace — testing status and a resolved integration bug

Testing is proceeding via a shared SharePoint Excel Jana Egrmaierová (STK-044) and Petr Sláma (STK-034) set up — 3-4 entries logged so far, all marked "PAV" (presumed pass/OK), but no formal written feedback yet. Separately, the PUME-integration bug Filip had flagged as his own mistake last week (involving Jan Kopecký, STK-032) is now fixed and tested.

### Reklamace — email-draft group still blocked on Vláďa; escalating the pattern

The email-draft creation group setup is still queued behind Vladislav Tvarůžek (STK-016) — Jindřich chased him again yesterday with no movement. He's already raised the broader pattern with Tomáš Dudaško directly (not about Vláďa personally, but the process): it's untenable that AKS-related requests sit 6-7 weeks in a queue behind one person also juggling BDC work. Jindřich will present the AI portfolio at Tuesday's (2026-09-29) large management meeting and plans to push this issue up to CEO level ("pan Žák," generální ředitel) if needed, framing it as a real limiter on delivery speed.

### Reklamace — warehouse WiFi/mobile access

Terka (Foltýnová) has committed to sorting out the mobile/Wi-Fi access question for the warehouse — Jindřich expects an update at tomorrow's logistics status call.

### Reklamace — new gap: rozvozový list free-text data source

Filip flagged a previously-unaddressed problem: the "rozvozový list" (delivery/dispatch list) — already working end-to-end with PUME for the supplier address field — also needs free-text fields filled in by warehouse workers themselves (e.g. a complaint/reklamace number). In the old Excel-based process, workers could type anything directly; now that BigHub generates this document, there's no defined source for that operator-entered text. Nobody had accounted for this gap before. To be raised at tomorrow's logistics status meeting.

### Fakturace doprav — stuck API-contract renegotiation with Petr Sláma

Filip has been trying to get Petr Sláma (STK-034) to agree to a revised API contract so the freight-invoicing spec is actually deliverable — the original contract didn't provide enough information to validate certain checks. Filip drafted a proposal (consulted with Jan Sovka, who backed pushing for BigHub's preferred format), sent it, and Sláma rejected it outright as something they simply won't do — no counter-proposal, no technical reasoning given. Filip then sent a further simplified version "down to the bone" yesterday, flagging some tradeoffs he personally wouldn't recommend but didn't feel strongly enough to block; Sláma's reply (about an hour before this meeting) was that he has no time and will look at it next week. Filip's frustration: when he sends a concrete proposal with reasoning and gets back either silence, a flat "no capacity," or a two-sentence refusal with no technical counter-argument, there's nothing to iterate on. He also noted Sláma has previously said things like "this should have been done by AI" in a way that doesn't reflect what AI can actually do — it can't produce information nobody has.

Jindřich's response: logistics timelines will start explicitly factoring in these client-side response delays — if BigHub is waiting a week-plus on a decision, that time shows up in the schedule, the same way BigHub would expect its own delays to be accounted for. He'll raise this with Sláma directly tomorrow, asking Filip beforehand to brief him on the technical specifics so he can push knowledgeably rather than vaguely. Marek separately coached Filip (referencing a conversation from Friday): frame these asks to non-expert counterparts in terms of the cost of *not* deciding — "if you don't respond, we're blocked and it costs X; if you unblock us, we save time and get better quality" — since BigHub, not Sláma's side, holds the AI/delivery expertise here and should be steering the ask, not just waiting for one back.

### Fakturace doprav — backlog near-complete, Swagger resolved, one ID gap remains

Filip is finishing the backlog today (~95% done, being clicked into the board/Kanban) — remaining fakturace doprav work is genuinely blocked on Sláma's side agreeing the new Swagger contract, not on anything BigHub controls; testing and deployment still lie ahead once unblocked. The Swagger approval itself is confirmed resolved. A **unique document ID is still not resolved** — carried as an open item. Marek will send Filip the Listing spec shortly so Filip can comment inline on backlog-relevant items.

### Order prediction (predikce objednávek) — Juraj Kmec update

Juraj is using last week's session as an informal task list, which works fine given the small, stable contact set (Petr Ondráček, STK-035; Marek Šimoník, STK-019). E-commerce stakeholders are described as happy and low-maintenance — nobody needs chasing. The one open item: the per-channel budget Excel Marek Šimoník previously said he'd send — not yet received, and Šimoník is now on vacation, putting it at risk before next Tuesday's (2026-09-29) follow-up (Monday 2026-09-28 is a public holiday, so Tuesday is the first working day). Jindřich will try reaching Petr Ondráček directly via Teams to see if he can supply it instead, flagging the deadline pressure explicitly.

Also revisited: the mobile/phone VPN-bypass access Ondráček wanted for viewing reports on his phone, discussed at last week's infra meeting with Vláďa — status: not approved. Jindřich's take: a reasonable "nice to have," but granting phone-based access without a VPN compromises security; the answer stays laptop + VPN. Juraj was relieved this wasn't approved, calling open-to-the-world access stressful from his side.

### Listing — status and the case for staying paused

The spec remains with Petr Neuman (STK-023), who is currently away/unavailable; Marek hasn't heard back yet and is waiting to schedule a kickoff call. Cross-reference: Marek Šimoník separately told Juraj he intends to step back from order prediction going forward and redirect that budget/effort toward Listing — Neuman reportedly has a vision to expand Listing's scope. Development itself is fully paused — blocked on the more basic question of whether real Listing data exists at all, versus today's dummy/static data — and the team agreed this is the right call: Filip noted there are enough open questions that continuing now is "a gamble that gets thrown in the trash." Marek's plan: hold the spec meeting with Neuman and bring Filip along so technical feasibility questions get answered live; Neuman had committed last week to scheduling this week but warned his calendar is very fragmented. Marek will call him, spec things out, and give at least a progress update sometime next week. Jindřich noted good sequencing: as fakturace doprav work winds down, Filip's freed-up capacity should line up naturally with Listing ramping up.

## Decisions Made

- Reklamace's AI-vs-digitization framing was calibrated directly with Petr Spilka and Tereza Foltýnová; both understood it. The continue-or-close decision is deferred to a management meeting (Jindřich, Dudaško, Žůrek, Spilka, Žižka) — complicated by Dudaško's ~6-month plan to retire Axapta.
- The team will present the Reklamace reframe openly and consistently to logistics stakeholders, and flag directly to Jindřich (rather than resolve individually) if Tereza Foltýnová pushes a decision or an inaccurate claim onto them.
- Logistics delivery timelines will now explicitly factor in client-side response delays, not just BigHub-side ones.
- Listing development stays fully paused until data-availability and scope questions are resolved with Neuman — a deliberate choice to avoid wasted work.
- Ondráček's mobile/phone report-access request stays declined — laptop + VPN only, for security reasons.

## Action Items

- [ ] **Jindřich Tůma**: Schedule the Reklamace continue-or-close decision meeting with Tomáš Dudaško, Rudolf Žůrek, Petr Spilka, and Jan Žižka — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Jindřich Tůma**: Escalate the AKS/BDC request-turnaround bottleneck (6-7 week queue behind Vláďa) at Tuesday's (2026-09-29) management meeting, up to CEO level if needed — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Jindřich Tůma**: Raise the rozvozový list free-text data-source gap at tomorrow's logistics status meeting — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Jindřich Tůma / Filip Černý**: Push Petr Sláma tomorrow on the fakturace doprav API-contract revision — Filip to brief Jindřich on the technical specifics beforehand — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Filip Černý**: Finish the fakturace doprav backlog entry in the board/Kanban today — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Marek Pillár**: Send Filip Černý the Listing spec draft for backlog-relevant inline comments — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Marek Pillár**: Schedule the Listing spec kickoff meeting with Petr Neuman (bringing Filip Černý) once Neuman responds; give at least a progress update next week — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Jindřich Tůma**: Reach out to Petr Ondráček directly via Teams for the order-prediction per-channel budget Excel, since Marek Šimoník is on vacation — needed before the 2026-09-29 follow-up — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Filip Černý**: Continue chasing Petr Sláma / Jana Egrmaierová for formal written testing feedback on Reklamace — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers
- [ ] **Marek Pillár**: Reconcile the MaxBuddy annual-value discrepancy (~130M Kč cited here vs. ~81M Kč discussed 2026-09-22) before the Business Quantification tracker is finalized — from 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers

## Open Questions

- MaxBuddy's annual business-value figure: ~130M Kč (this session) vs. ~81M Kč (2026-09-22 walkthrough) — not yet reconciled.
- What "jejich IT" means in Tereza Foltýnová's suggestion that the digitization work could move to Dr. Max's own team — Jindřich himself was unsure whether she meant Max, BDC, or something else.
- The unique-document-ID gap for fakturace doprav — still unresolved, no owner or timeline mentioned.
- Whether Jakub Turner was actually expected at this meeting or informed of it — the opening exchange was inconclusive.

## Sentiment & Tone

Informal and warm at the open (light banter about a client party that evening, running jokes about mixing up names), but the Reklamace segment carried real weight — Jindřich was noticeably deliberate and a little defensive-by-necessity, walking through his reasoning in detail as if rehearsing the same explanation he'd need to give again to Dr. Max management. Filip's frustration with Petr Sláma was genuine but controlled ("já nevím, proč to nejde, jakože proč se mu nechce" — translated: "I don't know why it doesn't work, whether he doesn't want to or can't"), and Jindřich validated it directly rather than downplaying it, matching the pattern from other logistics-side friction this account has seen. Marek's coaching moment to Filip was constructive, not corrective. Overall a working, collaborative status call with one clearly higher-stakes political thread (Reklamace/Tereza) handled transparently rather than swept aside.

## Routing Log

Routed on PM confirmation ("confirm both"), 2026-09-24:

- **project-assumptions**: ASM-139 (Axapta retirement plan), ASM-140 (MaxBuddy value discrepancy), ASM-141 (client-delay timeline policy), ASM-142 (Fakturace doprav contract stuck with Sláma), ASM-143 (rozvozový list data-source gap)
- **project-stakeholders**: STK-003 (Jindřich), STK-006 (Filip), STK-009 (Kmec), STK-010 (Dudaško), STK-013 (Foltýnová), STK-014 (Spilka), STK-016 (Tvarůžek), STK-019 (Šimoník), STK-023 (Neuman), STK-024 (Žůrek), STK-034 (Sláma), STK-035 (Ondráček); added STK-051 ("pan Žák," low-confidence)
- **project-knowledge**: "Reklamace" entry updated with the digitization-reframe fallout and Axapta-retirement context
- **project-daily (2026-09-24)**: 10 action items added; Key Events and Audit Log entries written
- **project-lessons**: LL-056 captured
- **meetings/index.md**: entry added
