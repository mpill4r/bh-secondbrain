---
last_updated: 2026-09-17
type: external
attendees: [Jindřich Tůma, Marek Pillár, Jura Brázdil, Viliam Gago, Šárka Andělová, Kateřina Kadlecová, Simona Mertová, Lucie Fendrichová]
tldv_link:
---

# Lexie/Max/Maxie Weekly Sync — Timeline Review, Max Testing Feedback & Go-Live Negotiation

**Date**: 2026-09-17
**Attendees**: Jindřich Tůma (BigHub, running the call), Marek Pillár (BigHub), Jura Brázdil (BigHub, Max chatbot dev — dropped off the call before the end), Viliam Gago (BigHub, Lexie), Šárka Andělová (Dr. Max CZE), Kateřina Kadlecová (Dr. Max CZE), Simona Mertová (Dr. Max CZE, product/operational owner of Max/Maxie/Lexie), Lucie Fendrichová (Dr. Max CZE)
**Type**: external
**Recording**: N/A
**Previous session**: [2026-09-10-lexie-max-maxie-weekly-sync.md](2026-09-10-lexie-max-maxie-weekly-sync.md)
**Meeting prep**: N/A

## TL;DR

Recurring weekly Lexie/Max/Maxie sync: a unified cross-project timeline view was reviewed and accepted (with a flagged MVP/full-product scoping mismatch to resolve), extensive Max chatbot bug-fix feedback was walked through (pharmacy-location search, false call-transfer claims, city-recognition, GDPR consent gap), and the meeting's center of gravity was a go-live negotiation — Mertová held firm on an end-of-October public launch target over Jura's end-of-September push, landing on BigHub targeting its internal deployment milestones by end of September while the public date stays October. Lexie has 3 tickets ready for retest and a resolved (if scaled-back) plan for multi-role test accounts.

## Continuity from 2026-09-10

- **X-Manager Kanban as roadmap-visibility solution** — held; Kadlecová's team has now gone a step further and drafted a proposed column/status restructure to send to Jindřich for review.
- **Test-account mechanics for Lexie's 4 CC roles** — resolved (partially): BigHub is stepping back from the in-app role-switcher (Option B from 2026-09-10) in favor of 4 separate accounts without 2FA, citing BDC permission complexity/risk. Mertová accepted this as workable. The role-switcher isn't fully dead — Jura is still poking at it — but it's no longer the committed path.
- **Cross-project harmonogram (Lexie + Max + Maxie)** — delivered. This meeting's timeline review is that harmonogram in use.
- **Lexie design/UX polish ("find a compromise" ticket)** — not yet opened; instead, Jindřich and Marek re-framed the ask, requesting Dr. Max articulate concrete pain points (not solutions) first.
- **AI platform documentation (Jura's internal doc)** — not mentioned this meeting; still outstanding.
- **Ticket RITM0797678 follow-up with Lukáš** — not mentioned this meeting; still outstanding.
- **Mertová's owed business-case/time-savings metrics** — not mentioned this meeting; still outstanding.
- **New this meeting, not from 2026-09-10**: Max chatbot went from "test environment demo" to active multi-person testing with real bug reports, and a full go-live timeline negotiation — the project moved a full phase forward.

## Key Discussion Points

### Timeline review

Jindřich shared a simplified, package-level (not per-ticket) Kanban-style timeline covering all three projects (Max, Lexie, Maxie), with Dr. Max's testing windows visually aligned against BigHub's dev windows so testing effort doesn't get split awkwardly week-to-week. Kadlecová confirmed the team understood the format and would welcome a live walkthrough. She flagged one open discrepancy: some items in the shared product scope appeared to belong to the full product rather than MVP. Jindřich acknowledged this and said Marek ("Mára") might have visibility into it, but the specific items were never identified or resolved in this meeting — **open item**.

### Max chatbot — testing feedback triage

Jura had proactively converted every feedback-form submission into a visible "pseudo-ticket" directly under the feedback widget, addressing Kadlecová's 2026-09-10-era complaint about duplicate testing effort across colleagues. Bugs walked through:

- **7 reports of failed pharmacy-location search** ("Vinohrady v Brně" and similar) — root cause: an overly aggressive input-validation check defaulted searches to Brno city-center. Fixed; some geocoding edge cases remain (Brno-Vinohrady vs. Vinohradská ambiguity even in Google Maps/Mapy.cz — Jura called it "poměrně tolerantní už teďka").
- **Paralen stock-lookup false negative** (Mertová: asked directly about stock at "Bašty 2," 302 units on hand, Max said none available) — same root cause (searched near city-center default instead of the reported location). Fixed for the reported scenario; Mertová to retest.
- **False call-transfer claims** — Max was telling users it was transferring them to a pharmacist by phone, which it cannot do. Explicitly disallowed in the system prompt now.
- **Phone-number-based order lookup** — currently untestable; BigHub's test environment isn't connected to production orders. Fendrichová offered to connect BigHub to Dr. Max's staging/test order environment instead.
- **Minor punctuation fix** — done.
- **City/district recognition** (Fendrichová: asked about Brno, told "not available anywhere in Brno," but it *was* available in Brno-Líšeň) — Jura explained two contributing factors: Czech declension (Brno/Brně) makes literal string matching unreliable (mitigated by upgrading the underlying model from GPT-5.1 to GPT-5.4 and switching to fuzzy/syllable-based matching), and a possible memory/context-pollution bug where the bot's own earlier context can override a later correct lookup. Asked Fendrichová to retest and report back.
- **GDPR/consent gap** (Andělová) — no consent checkbox exists for the personal data (phone, email) the chat collects, and no anonymization step. Jura confirmed BigHub hadn't planned for this yet. Jindřich flagged this needs Lenka Henichová (DPO) involved before any copy is drafted — a ticket was opened and left open, owned by Dr. Max to bring back guidance. Jura clarified the current architecture: nothing is stored server-side today — conversations live only in the browser and never leave the user's machine; future analytics will only ever store aggregate statistics, never individual conversation content. The one genuinely new sensitive-data touchpoint is e-recepty (e-prescriptions), which carry data not previously consented elsewhere in Dr. Max's systems.
- **Medical-advice guardrail** (Kadlecová) — tested asking for medical advice; correctly declined and redirected to a pharmacist consultation. Working as intended.

### Max chatbot — UX requests

- Ability to stop/edit an in-flight response while it's still generating (like a "regenerate" affordance) — Jura: with the GPT-5.4 upgrade responses are fast enough that this matters less, but a message-edit/rewind control is feasible and will be considered.
- New-conversation/reset button in the chat header — agreed, straightforward to add.
- Idle/timeout handling — an automated "still there? / ending conversation" message after ~10 minutes of inactivity, with "continue" / "start over" options, plus a separate passive notification (e.g. a pill/badge on the collapsed widget) if the user has minimized the chat without closing it. Jura agreed to build both together for better coverage, since users often leave the tab open and walk away.
- Terminology/tone consistency — the bot inconsistently switches between formal (vykání) and informal (tykání) address, and uses both "lékárna" and "pobočka" for the same concept. Jura asked Dr. Max to write a short first-person "tone brief" (~2 paragraphs, written as if the bot itself were describing its own voice/terminology/formality rules) that he can feed directly into the system prompt — explained this works better for the underlying language model than a list of rules. Can also include functional guidance (e.g. how to phrase search-result summaries), not just tone.
- Conversation-rating/star system — discussed on 2026-09-10 but no ticket was ever created; Jindřich to open one now.

### Go-live timeline negotiation

The most substantial discussion of the call. Mertová proposed targeting the last week of October for putting the chatbot live on the public website, explicitly wanting a fixed target to plan around rather than open-ended slipping — while acknowledging she'd rather launch later with confidence than rush and lose trust ("jakmile to nebude dobře udělané, tak jsme si vykopali vlastní hrob").

Jura pushed for end of September instead, and Mertová held her position: testing so far has covered only 4 sample e-recepty, hasn't touched production data variety (order states, delivery methods, prescription codes, availability edge cases), and infra dependencies make end-of-September tight. Jindřich did not contest this and reframed the commitment: BigHub will aim to complete its side (see phased plan below) by end of September and will try to earn an earlier public launch through demonstrated quality and testing — but end of October stands as the agreed target, not something BigHub will force.

Jura laid out the 3 technical deployment phases:
1. **Production backend connection** — once infra unblocks (expected this week or next), can be done within hours: live orders, e-recepty, etc.
2. **BDC security clearance to exist on doktormax.cz, invisible to the public** — dependent on BDC turnaround, targeted for end of September; once live, Dr. Max can manually enable the widget on the real site for internal testing exactly as end users would experience it.
3. **Public visibility toggle** — a single switch, whenever Dr. Max decides.

Mertová confirmed she wants exactly this: to test phase 2 against real production data for several hours before signing off on public visibility.

**Launch posture**: Mertová wants a quiet/soft launch — no promotional push initially, trusting customers will discover it organically; monitor satisfaction, and only actively promote once the tool is fully mature (all 4 planned capabilities solid, and potentially with the current chat-bubble UI removed in favor of a cleaner integration). Jindřich agreed to hold off on defining promotion channels (intranet, internal newsletter, etc.) until given a green light.

**Reporting/analytics**: Jura confirmed a live analytics dashboard already exists (shown at a previous meeting) — click paths, time-in-chat, whether recommended medications were shown, etc. — and will resend the link. Expected to eventually consolidate into a future unified cross-project platform dashboard (alongside Klexee for Lexie).

**Impact measurement**: Jindřich relayed a conversation with David Mendl about whether Mertová tracks call-desk contact-reason volumes, to later quantify chatbot offload. Mertová confirmed she does track email/call volume by topic, but expects the chatbot to mostly *add* throughput capacity rather than reduce total call-desk volume 1:1 — call volume tracks external factors (shipping speed especially) more than channel availability, and stays roughly constant regardless of staffing mix. She expects the separate Voicebot project to be the bigger lever for genuinely offloading live agents, since it extends coverage outside business hours in a way the web chat doesn't change for phone-based demand.

### Lexie status

Three tickets ready for Dr. Max retest, all done on BigHub's side: našeptávač (autocomplete popup) removal, document-rename-in-storage index fix, and the "oznámení pro všechny uživatele" (all-user announcements) feature.

Two items still open:
- **User documentation/manual** — committed for next Thursday's meeting.
- **Multi-role test accounts** — resolution of the 2026-09-10 open question. BigHub is stepping back from the in-app role-switcher due to BDC permission-system risk/complexity, proposing instead 4 separate accounts (one per CC sub-department group) without 2FA. Mertová accepted this as workable for now. A ticket will be filed with BDC to provision the 4 accounts.

### Lexie design/UX refresh

Carried over from 2026-09-10 as a "nice to have," not MVP-blocking. Jindřich reopened it, explicitly asking Dr. Max to articulate what's actually wrong or missing (not proposed solutions) so BigHub can apply current design standards rather than risk building something off-brief. Marek reinforced this directly: *"my nepotrebujeme vedieť riešenie od vás, my potrebujeme zistiť, čo je váš problém... iba definujte ten problém, maximálne s nejakým screenshotom, možno screen recordingom."* Kadlecová agreed to run an internal "vibe check" exercise tying feedback to concrete pain points and send the output to Marek, who will set up a follow-up working session once there's something concrete to react to.

### X-Manager (open floor)

- Kadlecová's team drafted a proposed restructure of the Kanban's status/column setup (to better match conventional tools like Jira/Trello) in a spreadsheet, to be sent to Jindřich for thumbs-up/down review.
- Jindřich separately praised BigHub's own turnaround on a recent X-Manager configuration request — same-day.
- **X-Manager reuse for other Dr. Max streams** — Mertová confirmed ownership has moved to "Míša Machata" in Prague; Marek will coordinate directly. *(Possible name collision with existing STK-039 "Machata," a DVH/data-warehouse contact from a 2026-09-03 mention — flagged for stakeholder-routing review, not confirmed same person.)*
- Andělová asked whether BigHub needs @-mention notifications on new tickets — Jindřich: no, status-column monitoring is sufficient.

### Two new Lexie bugs (raised ad hoc, end of call)

- The documented "second" fallback message (shown when Lexie truly has no source/answer, distinct from the first "I don't know" message) has apparently never triggered for Fendrichová in practice — unclear under what conditions it's supposed to fire. Viliam Gago wasn't certain of the answer live; to be filed as a ticket.
- Some Lexie conversation titles save in English instead of the expected Czech, inconsistently. Unclear if this is a bug or situational. Jura had already dropped off the call by this point ("podpásově se odpojil") — to be filed as a ticket for him to investigate.

## Decisions Made

- The unified Max/Lexie/Maxie timeline Kanban is confirmed as the working format going forward; testing window extended to next Thursday's meeting, with further orientational adjustments expected week to week.
- Go-live: public launch target is end of October (Mertová's ask); BigHub commits to completing its 3 internal deployment phases by end of September and will attempt to earn an earlier public date through demonstrated testing/quality, but will not force an earlier public launch.
- Launch posture: quiet/soft launch with no active promotion initially; promotion channels to be defined later, contingent on Mertová's sign-off.
- Lexie multi-role testing: 4 separate department accounts without 2FA, not the in-app role-switcher (still being explored separately, not committed).
- GDPR consent/anonymization for the Max chatbot requires Lenka Henichová's (DPO) input before any copy is drafted; ticket opened and left with Dr. Max to bring back direction.
- Lexie design/UX refresh stays deferred; next step is Dr. Max submitting a concrete problem list (not proposed solutions) to Marek.
- False call-transfer claims and unauthorized medical advice are both explicitly disallowed in Max's system prompt (the latter already working correctly in testing).

## Action Items

- [ ] **Jindřich Tůma / Marek Pillár**: Resolve which timeline items were mis-scoped as MVP when they actually belong to the full product — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Simona Mertová**: Retest the Paralen/Bašty 2 stock-lookup scenario now that the location-search fix is in — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Lucie Fendrichová**: Connect BigHub's test environment to Dr. Max's staging/test orders so phone-number-based order lookup can be tested — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Lucie Fendrichová**: Retest the Brno/Brno-Líšeň district-recognition scenario and report back — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Set up a meeting with Lenka Henichová (DPO) on GDPR consent/anonymization copy for the Max chatbot — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Simona Mertová / Dr. Max CC team**: Bring back DPO guidance on required consent language once available — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Dr. Max CC team**: Write a short first-person "tone brief" (terminology, formality, voice) for the Max chatbot's prompt — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Open a ticket for a conversation rating/star system (carried over from 2026-09-10, never ticketed) — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Resend the link to the Max chatbot's existing analytics/reporting dashboard — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: File a ticket with BDC for 4 separate Lexie test accounts (one per CC sub-department) without 2FA — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jura Brázdil**: Continue investigating (not committing to) whether an in-app role-switcher for Lexie test accounts is technically feasible — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma / Jura Brázdil**: Deliver Lexie user documentation/manual by next Thursday's meeting — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová / Dr. Max CC team**: Run a "vibe check" exercise on Lexie's UX and send concrete pain points (not proposed solutions) to Marek Pillár — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Marek Pillár**: Set up a follow-up working session on Lexie design once Dr. Max's pain-point list arrives — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Kateřina Kadlecová**: Send the proposed X-Manager Kanban column/status restructure spreadsheet to Jindřich — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Jindřich Tůma**: Review and give thumbs up/down on Dr. Max's proposed X-Manager Kanban restructure — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Marek Pillár**: Coordinate directly with "Míša"/Michal Machata (Prague) on X-Manager reuse for other Dr. Max streams — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Viliam Gago / Dr. Max CC team**: File a ticket investigating why Lexie's "second" no-source fallback message never appears to trigger — from 2026-09-17-lexie-max-maxie-weekly-sync
- [ ] **Lucie Fendrichová / Jura Brázdil**: File a ticket investigating why some Lexie conversation titles save in English instead of Czech — from 2026-09-17-lexie-max-maxie-weekly-sync

## Open Questions

- Which specific roadmap items are mis-scoped as MVP when they belong to the full product — raised by Kadlecová, never itemized in this meeting.
- Whether an in-app role-switcher for Lexie's 4 CC testing roles is technically sound — no longer the committed path, but not ruled out either.
- Whether "Míša Machata" (new X-Manager owner, Prague) is the same person as the existing STK-039 "Machata" (DVH/data-warehouse contact, low-confidence single mention from 2026-09-03) — needs confirmation.
- Under what conditions Lexie's "second" fallback (no-source) message is actually supposed to trigger.
- Whether Lexie's English-language conversation-title bug is a real defect or situational.
- "Speaker 10000" (00:14, a single generic greeting) — unidentified, likely a dial-in/room identity artifact rather than a distinct person; not investigated further.
- Mertová's owed business-case/time-savings metrics per initiative and Jura's two previously-floated CC-platform ideas (still outstanding since 2026-09-03/2026-09-10, not revisited again this meeting).

## Sentiment & Tone

Warm and collaborative throughout, consistent with prior sessions in this recurring series. The go-live timeline discussion carried real tension — Mertová was direct and unmoving about not compromising on testing thoroughness, and Jura's counter-push for an earlier date was reasonable but firmly declined — yet it resolved constructively with an explicit, mutually understood compromise (BigHub's internal milestones vs. the public date) rather than a forced agreement. Mertová's framing throughout was notably risk-aware and protective of the customer relationship ("jsme si vykopali vlastní hrob"), which reads as strong ownership rather than obstruction. The extensive bug-triage segment had a genuinely productive, high-trust rhythm — Jura's proactive pseudo-ticket build was well received as directly responsive to a complaint raised last session. Early-call audio/connectivity friction (first ~3 minutes) was handled patiently and didn't affect the rest of the tone. Marek's framing of the design-feedback ask ("we need your problem, not your solution") was accepted without pushback and set a clear, low-friction process for the next design round.

## Routing Log

- **project-stakeholders**: Added STK-050 (Šárka Andělová). Enriched STK-001 (Marek Pillár), STK-003 (Jindřich Tůma), STK-017 (Simona Mertová), STK-026 (Jura Brázdil), STK-027 (Viliam Gago), STK-037 (Kateřina Kadlecová), STK-045 (Lucie Fendrichová). Flagged a possible identity overlap between STK-039 ("Machata," DVH/data-warehouse contact) and today's "Míša Machata" (new X-Manager owner, Prague) — unconfirmed.
- **project-assumptions**: Added ASM-100 (go-live: Oct public launch / Sept internal deployment phases), ASM-101 (quiet/soft launch, no promotion until mature), ASM-102 (GDPR consent/anonymization open, blocked on DPO), ASM-103 (Lexie test accounts: 4 separate, no 2FA), ASM-104 (MVP/full-product scoping mismatch, open), ASM-105 (call-transfer/medical-advice guardrails decided).
- **project-knowledge**: "Max / Maxie / Lexie" entry updated with the 3-phase go-live plan, current data-storage architecture, the GPT-5.1→5.4 upgrade and fuzzy location matching, the tone-brief prompting mechanism, and the resolved Lexie test-account approach.
- **project-daily**: Added 19 action items to 2026-09-17's daily.
- **meeting-index**: Added entry for this meeting.
