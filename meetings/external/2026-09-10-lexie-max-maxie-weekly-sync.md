---
last_updated: 2026-09-10
type: external
attendees: [Jindřich Tůma, Jan Sovka, Jura Brázdil, Marek Pillár, Kateřina Kadlecová, Lucie Fendrichová, Simona Mertová]
tldv_link:
---

# Lexie/Max/Maxie Weekly Sync — Ticket Triage, Kanban Review & Test Account Planning

**Date**: 2026-09-10
**Attendees**: Jindřich Tůma (BigHub, running the call), Jan Sovka (BigHub), Jura Brázdil (BigHub, demoed the Max chatbot test environment), Marek Pillár (BigHub, mostly listening), Kateřina Kadlecová (Dr. Max CC team — see Open Questions on the "CZ-BRN-TIT-CCManager" tag), Lucie Fendrichová (Dr. Max CZE, new to the harness — active on X-Manager/Kanban UX), Simona Mertová (Dr. Max, product/operational owner of Max/Maxie/Lexie)
**Type**: external
**Recording**: N/A
**Previous session**: [2026-09-03-max-chatbot-demo-lexi-maxi-status-sync.md](2026-09-03-max-chatbot-demo-lexi-maxi-status-sync.md)
**Meeting prep**: N/A

## TL;DR

This is the recurring weekly Lexie/Max/Maxie sync with the Dr. Max CC team: the last blocking Lexie bug (thumbs-up/down feedback) is fixed and testing has resumed, the X-Manager Kanban view (grouped by scope: MVP/Full Version/Nice to Have) was confirmed as a workable replacement for a static Excel roadmap, and Jura demoed a live (VPN-gated) Max chatbot test environment with sample test scenarios. Most of the meeting's time went into unresolved testing-account mechanics for Lexie's four CC sub-department roles, and Mertová raised a design-quality gap between Lexie and Max that Jindřich tied to a pending platform-wide design decision rather than something CC can request independently.

## Continuity from 2026-09-03

- **Thumbs-up/down feedback bug (blocker #1 of 3)** — resolved. Kadlecová confirmed she can now retroactively evaluate conversations she'd been unable to rate before; testing has resumed.
- **Našeptávač (autocomplete popup) removal (blocker #2 of 3)** — not yet done; now tracked as its own higher-priority ticket rather than folded into the general bug list.
- **Configurable fixed/canned status messages (blocker #3 of 3)** — in progress as ticket 150 ("oznámení pro všechny uživatele"), marked "ready for dev." Kadlecová hit a permission-scope error while testing the input ("cesty mimo působnost vašeho oddělení nelze nastavit") and already logged it with a screenshot in the ticket.
- **Max chatbot test environment** — the 2026-09-03 promise to stand this up slipped on infra issues; it is now live behind Dr. Max's VPN, with mock test scenarios (sample e-recepty and order numbers) ready for the CC team to try.
- **MVP/roadmap table (Kadlecová's standing ask)** — reframed this meeting: rather than a separate Excel deliverable, the X-Manager Kanban view grouped by scope was demoed and both Kadlecová and Mertová indicated it satisfies the need, pending Mertová's business-side sign-off.
- **Weekly Thursday sync** — held as committed.
- **Still not revisited**: Mertová's owed business-case/time-savings metrics per initiative, and Jura's two floated CC-platform ideas (role-gated API-health indicator, chatbot logging of unanswerable questions) — none of these came up again this meeting.

## Key Discussion Points

### Lexie ticket triage

Kadlecová confirmed the team split ticket review among themselves and isn't fully certain of every item's status, but covered what she owns directly:
- Thumbs feedback bug: resolved, testing resumed.
- Ticket 150 (fixed-message announcements): flagged as "ready for dev," with a screenshot of a permission-scope error already attached.
- Tickets 148 and 147: "ready for deployment" — completed on BigHub's side.
- Ticket 152 (thumbs up/down): initially appeared missing from the board — turned out to be hidden by an active filter; visible once filters are cleared. A duplicate of the 150 ticket was cancelled to avoid confusion.
- Document renaming in storage / Lexie's index update: Mertová hasn't tested it yet, will do so before next session.
- A new, higher-priority ticket was opened for removing the našeptávač (autocomplete/suggestion popup) entirely.

Jindřich flagged William Gago is on vacation until Monday and asked whether ticket #154 could still be tested this week — Kadlecová said it's possible, but Jindřich noted this depends on what gets picked up in Monday's planning with William.

### X-Manager Kanban / product scope review

Kadlecová and Fendrichová both confirmed the Kanban setup generally works for their side — their main concern is that it keeps communication and status updates flowing smoothly for both parties, and Kadlecová said she had the identical question queued for Jindřich. Jindřich's own position: rather than producing a periodic Excel export, it's better to have the system itself always reflect current state, viewable on demand. Grouping the Kanban by "scope" (MVP / Full Version / Nice to Have) reproduces the structure of Kadlecová's own Excel tracker. Fendrichová added a UX detail: a "hide empty columns" toggle exists near the group-by control, so scope types with nothing in them don't clutter the view. Kadlecová said this would be sufficient for her personally, but the business side (Mertová) should also weigh in since the same view needs to work for non-technical stakeholders and future developers. Jindřich noted an Excel export likely exists if ever needed for a presentation, but the system itself should be the source of truth going forward. Jindřich will review further today/tomorrow (working from home) and may add refinements.

### Harmonogram (cross-project timeline) request

Kadlecová and Mertová both asked for at least an orientational roadmap/timeline across all three projects — not just ticket-level tracking — so the business side can plan capacity, since CC isn't only working this one initiative. Mertová specifically wants visibility into expected deployment, testing, and revision windows for Lexie, and timing for when Maxie will be ready. Jindřich committed to preparing this: all three projects on one timeline, broken down by week and then by individual workday, including testing windows so Dr. Max can plan which days their team needs to test. Explicitly framed as directional, not a fixed commitment, given dependencies on Dr. Max's own side.

### AI platform documentation request

Kadlecová asked whether documentation exists for the broader AI platform Lexie runs on (not just Lexie itself) — motivated by a past experience where she and a colleague weren't sure what the platform could or couldn't do and had to figure it out by trial and error; she wants this available for onboarding new colleagues. Jura confirmed he maintains an internal technical doc (screenshots + descriptions of platform capabilities), close to complete — last verified true before the team could determine e-recept stock-by-location — and offered to finish updating it and send it out via Jindřich to the full group.

### Design gap between Lexie and Max

Mertová raised that Lexie looks noticeably less polished than the newer Max chatbot and asked what's planned. Jindřich clarified this is purely visual/UX preference (colors, field sizing), not functional, and explained why it's not a simple per-app change: design authority sits one level up, at the AI-platform level, owned by Tomáš Dudaško — an individual app can't diverge from the platform's eventual unified design without risking rework. Jura reinforced this: BigHub is actively working on consolidating all the Dr. Max apps under one central platform entry point first (near-term priority); only once that shell is agreed will per-app design cascade down from it — redesigning Lexie now, ahead of that, risks having to redo it. Jindřich committed to finding a middle ground with Jura and opening a ticket for a design compromise rather than leaving it as-is or doing a full redesign now. Mertová accepted this, asking only that user-facing polish happen before end users (not just CC) get access.

### Usability testing offer

Marek offered to sit in on a short usability-testing session with the Dr. Max team in the coming weeks — observing how they actually use the app, to catch friction points directly rather than through ticket reports, and feed findings into the roadmap with Jura. Mertová described their own phased testing plan, which frames why this is more nuanced than it sounds: round 1 (in progress now) is the CC colleagues on today's call testing directly; round 2 will shadow a live phone operator handling real customer questions to validate answer accuracy; round 3 opens to supervisors; round 4 opens to the wider operator/user base. Each round surfaces different feedback because each group has a different vantage point — operators, for instance, need an already-reliable app since not everyone can recognize a subtly wrong AI answer.

### Test account for role-based testing

The most extended discussion of the call. Mertová confirmed access was granted today and forwarded to colleagues, but is unsure how to proceed — permissions and "agent" creation under the test account are unclear to her team.

Jura raised a concern up front: if the test account uses 2FA (Microsoft Authenticator), it won't be practical for multiple people to authenticate simultaneously across devices. Mertová clarified their existing "CZ UCC školení" training account has no 2FA — but the real requirement is that a tester needs to run two roles/agents side-by-side on one screen (their own role + the test role) for it to be useful, and the process for setting that up was never explained to them.

Jan Sovka and Jindřich confirmed permissions are controlled entirely by Entra ID groups on Dr. Max's side (max.bt.cz), not configurable by BigHub — the specific groups the test account was assigned to need to be verified before anyone can reason about what it can/can't do. Jan suggested a practical workaround for concurrent testing: one browser window with the tester's own admin login, and a separate anonymous/incognito window with the test account.

Mertová then clarified the actual functional need: her team spans four CC sub-departments (call centre agent, back office agent, a "testing" role, and a fourth), each needing a distinct document-access scope — critically, a front-office agent role must never surface back-office-only information. Jura laid out two technical options:
- **Option A**: four fully separate accounts, requiring logout/login to switch between roles.
- **Option B**: one account placed in all relevant Entra groups, with BigHub building an in-app "role switcher" so the tester picks which group/role is active at a given moment — avoiding full re-authentication, but requiring new BigHub-side work.

Mertová's preference is Option B, and Jura raised a real technical caveat as he described it: if the test account belongs to every group simultaneously, that doesn't actually test the role-restriction behavior a real operator experiences (BigHub's app queries Entra for one specific group per session and grants access accordingly — a real operator has exactly one). Mertová then surfaced a further open question: if her team of four testers all use the same shared account concurrently, each selecting a different role in the switcher, would their sessions collide or conflict? Jura didn't have an answer and committed to researching this and reporting back.

Separately, Mertová still can't locate the original ticket that requested the test account (RITM0797678) — it was reassigned away from her (created by "Lukáš," briefly assigned to her, then removed) and search isn't surfacing it. She recalls the ticket's original text was a single generic line ("chci vytvořit testovací účet pro AI") with no group/role specification at all, which is presumably why nobody downstream had detail to act on. Jindřich will follow up with Lukáš directly to retrieve and clarify the ticket's actual content.

### X-Manager reuse across other Dr. Max streams

Marek asked Mertová whether X-Manager (the ticket tool currently used for Lexie/Max/Maxie) could be extended to other Dr. Max departments/streams. Mertová deferred to Jindřich as the cross-stream coordination lead. Jindřich's original instinct was yes, but Tomáš Dudaško has separately mentioned a future dedicated DevOps environment is coming — Jindřich is waiting on that project being created before deciding whether to extend X-Manager or move CC onto the new environment instead. For now, CC keeps using X-Manager as-is since it's working well.

### Max chatbot test environment (demo)

Jura confirmed the chatbot is deployed to a test environment; access requires Dr. Max's VPN (all attendees present confirmed they have it). He shared a link in chat to a mocked front-end page containing sample test scenarios: several e-recepty numbers in different states (ready for pickup, multi-item, already issued/greyed out, expired) and several order numbers, each requiring a matching test email address (format: a sample name @example.com) to look up. The environment is not yet wired to live production data — Jura is not fully certain whether it will surface a real order if queried yet. Once Dr. Max's production infra is ready, the test environment will be swapped to live data across all connected systems, matching reality.

For feedback, Jura asked that one-off chat issues go through the in-app feedback form rather than X-Manager where possible — it automatically captures the full conversation history on submission, so he can see exactly what happened without the tester needing to copy/paste anything; larger, structured requests should still go to X-Manager as before.

### Infrastructure status (unchanged)

Jindřich reported no new progress on Dr. Max-side infra blockers this week — AKS access, network "prostupy" (access grants), and the Atlantis/ElevenLabs voicebot telephony integration are all still pending, owned by Vladislav Tvarůžek, who is described as overloaded with requests. Jindřich asked all attendees to continue logging any gaps or errors they find as tickets, using the same process already established for the Knowledge Base work.

## Decisions Made

- Lexie's thumbs-up/down feedback blocker is resolved; Lexie testing has formally resumed.
- The X-Manager Kanban view (grouped by scope: MVP / Full Version / Nice to Have, with a hide-empty-columns option) is confirmed to satisfy Kadlecová's standing roadmap-visibility ask — no separate Excel deliverable is planned; the live system is the source of truth going forward, pending Mertová's business-side confirmation.
- Lexie's design/UX polish stays at a "find a compromise" level for now — a dedicated ticket will be opened, but a full redesign is deliberately deferred until the AI-platform-wide design consolidation (owned by Tomáš Dudaško) lands.
- A cross-project harmonogram covering Lexie, Max, and Maxie will be built by Jindřich, broken down by week and then by workday, including testing windows — explicitly framed as orientational, not a fixed commitment.
- X-Manager will not be extended to other Dr. Max streams yet — deferred pending Tomáš Dudaško's promised DevOps environment project.
- Test-account approach for Lexie role testing: two technical options identified (four separate accounts, or one shared account with an in-app role switcher); Dr. Max prefers the shared-account/role-switcher option, contingent on BigHub confirming it's technically sound — including whether concurrent multi-user use of one shared account would conflict.

## Action Items

- [ ] **Jindřich Tůma**: Resend the recurring meeting invite from a Dr. Max-domain BigHub account so Dr. Max attendees can forward it internally without the invite-approval block — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Finish updating and send the AI platform/Lexie technical documentation (internal doc with screenshots + descriptions) to the full group, via Jindřich — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma / Jura Brázdil**: Find a design compromise for Lexie's visual polish and open a dedicated ticket, without a full redesign ahead of the platform-wide design consolidation — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Follow up with Lukáš to retrieve and clarify the content of ticket RITM0797678 ("testovací účet pro AI") — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Research whether the shared-account/in-app-role-switcher testing approach is technically sound, including whether concurrent multi-tester use of one account would conflict — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Build the cross-project harmonogram (Lexie + Max + Maxie, weekly/workday granularity, testing windows included) — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Marek Pillár**: Follow up on scheduling a short usability-testing session with the Dr. Max CC team in the coming weeks — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Simona Mertová**: Test the document-rename-in-storage / Lexie-index-update flow before next session — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Continue testing the Max chatbot test environment (VPN-gated) using the provided sample e-recepty/order test scenarios; log bugs/gaps via ticket or the in-app feedback form — from 2026-09-10-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Confirm with William Gago on Monday whether ticket #154 can still be picked up for testing this week — from 2026-09-10-lexie-max-maxie-weekly-sync

## Open Questions

- Whether the shared test-account/role-switcher approach (Option B) will actually support four CC sub-department testers switching roles concurrently without collisions — Jura researching.
- Original intent/scope of ticket RITM0797678 ("testovací účet pro AI") — Mertová recalls no group/role detail was ever specified in it; Jindřich checking with Lukáš.
- Whether ticket #154 can realistically be tested this week given William Gago's vacation (back Monday).
- Mertová's owed business-case/time-savings metrics per initiative (outstanding since 2026-09-03) and Jura's two previously-floated CC-platform ideas (role-gated API-health indicator, chatbot logging of unanswerable questions) were not revisited this meeting — still open.
- Attribution: the "CZ-BRN-TIT-CCManager" transcript tag again speaks briefly and separately from Kateřina Kadlecová, who has clear, detailed, named attribution throughout this meeting (matching the bug-report behavior previously attributed to "Karlecová" under that same tag on 2026-09-03). This suggests the 2026-09-03 note's STK-037 name may be a transcription-spelling error ("Karlecová" vs. the correctly-spelled "Kadlecová" seen here as a distinct named speaker), and that the "CZ-BRN-TIT-CCManager" tag itself may be a generic dial-in/room identity rather than one fixed person. Flagged for the routing review rather than silently corrected.

## Sentiment & Tone

Warm, constructive, and collaborative throughout — genuine thanks exchanged in both directions (Kadlecová for the fast X-Manager fix turnaround, Jindřich for the Kanban build). The design conversation could have been an awkward mismatch of expectations but stayed cooperative: Mertová raised it plainly without frustration, and Jindřich/Jura's platform-level explanation was accepted without pushback. The testing-account discussion ran long and got technically tangled, but everyone stayed patient and solution-oriented, explicitly agreeing to research open questions rather than force a premature answer. Minor early-call friction (meeting-invite/access issues for several minutes at the start) was handled matter-of-factly and didn't affect the rest of the tone.

## Routing Log

- **project-stakeholders**: Added STK-045 (Lucie Fendrichová), STK-046 ("Verča" Strnisková, low-confidence). Corrected STK-037 name from "Karlecová" to "Kadlecová" (kept alias "Kačka"). Enriched STK-001, STK-002, STK-003, STK-017, STK-026.
- **project-assumptions**: Added ASM-058 through ASM-063 (5 Decided, 1 Open plus ASM-059/ASM-063 Open).
- **project-knowledge**: Enriched the "Max / Maxie / Lexie" entry with the 2026-09-10 ticket triage, design-gap decision, and test-account mechanics.
- **project-daily**: Added 10 action items to 2026-09-11's daily (processing date).
