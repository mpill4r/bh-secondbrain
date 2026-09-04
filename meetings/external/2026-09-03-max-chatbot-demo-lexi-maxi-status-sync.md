---
last_updated: 2026-09-03
type: external
attendees: [Jindřich Tůma, Jan Sovka, Jura Brázdil, Marek Pillár, Kateřina Karlecová, Simona Mertová]
tldv_link:
---

# Max Chatbot Demo & Lexie/Maxie Status Sync with Dr. Max CC Team

**Date**: 2026-09-03
**Attendees**: Jindřich Tůma (BigHub, running the call), Jan Sovka (BigHub), Jura Brázdil (BigHub, demoed Max chatbot), Marek Pillár (BigHub, mostly silent), Kateřina "Kačka" Karlecová (Dr. Max CC team — see Open Questions on attribution), Simona Mertová (Dr. Max, present per introduction, no clearly attributed lines)
**Type**: external
**Recording**: N/A
**Previous session**: N/A — new thread
**Meeting prep**: N/A

## TL;DR

Jura Brázdil demoed a working Max chatbot prototype (order status, pharmacy locator, e-recipes, medication lookup, all LLM-backed) to a very enthusiastic Dr. Max CC team ("no one has shown me this before"). Lexie (Lucie) testing is paused on 3 blocking bugs BigHub owns; team pivots full focus to Max in the meantime. Maxie (voicebot) is technically unblocked and moving. Recurring Thursday syncs agreed, with the long-promised MVP/roadmap table to appear next week.

## Key Discussion Points

### Max chatbot live demo

Jura walked through a working prototype embedded on a mock Dr. Max page, four button-driven functions plus free-text LLM chat:
- **Order status**: enter order number + email (or just the number — auto-detected and pre-filled); returns status, order date, and a direct tracking link.
- **Pharmacy locator**: by device location or city name; shows hours, route, and a call button.
- **E-recepty**: demoed all four states — prescribed/not yet issued, multi-item, already issued (greyed out, non-interactive), and expired.
- **Medication/stock lookup**: searches Dr. Max's public API, then re-ranks results through BigHub's own AI so variants group sensibly by form (tablets vs. suppositories) rather than just pack size; checks live stock across 561 pharmacies. Guardrail demoed live: asking whether Paralen is safe in pregnancy gets refused as medical advice, not answered.
- **E-recept direct lookup by ID**: demoed with a morphine example — deliberately chosen since scarce/controlled stock makes location-agnostic reservation genuinely useful (found in Mělník and Zlín, reservable directly).

Reception was immediately and strongly positive — spontaneous congratulations, "I've never had anyone show me something like this."

Current deployment: running provisionally on Jura's own machine/test environment, to avoid burdening Dr. Max's infra team before the new AKS sandbox (BDC-provisioned) is ready — expected this/next week. Once ready, Dr. Max gets hands-on test access via Dr. Max VPN.

### Feedback & access process

Jindřich proposed a ~1-week test window: Dr. Max explores and funnels requests/bugs together rather than ad hoc, so BigHub can batch-process toward production. The in-app feedback form auto-captures the full conversation transcript on submit — useful for bug reproduction even independent of X-Manager tickets. Feature/change requests should go into X-Manager, but **routed through one point of contact** (Mertová) rather than arriving from many individual testers — Jindřich's explicit ask, based on past experience where aggregate individual requests outpace what the actual business owner wants.

### In-chat feedback mechanism — design debate

Dr. Max wants an unobtrusive, end-of-flow feedback prompt (not an always-on floating widget) — likely a small button in the action-button row, or a header "?" info panel. Strong UX preference from Kateřina Karlecová's own prior chatbot experience: **stars/emoji only, no free-text field** — users abandon free-text forms, and a green→red color-ordered rating scale (click order matters — green-to-red tested better than red-to-green) is what's actually proven out in her data. Jura agreed to design it to avoid re-prompting the same user repeatedly.

### Regulatory guardrail — reusing the MaxBuddy SPC pattern

Karlecová flagged: if a user asks something like correct Paralen dosing, the bot must not answer directly — same legal restriction that reshaped MaxBuddy ("AI can't provide [medical] information at all," per legal). Jura confirmed the chatbot can safely display (even auto-scroll to the relevant section of) the full official package leaflet (SPC) via the same SPC API already built for MaxBuddy, without generating any medical content itself.

### Usage dashboard

Jura demoed an already-built analytics dashboard (chat opens, questions asked, products viewed, stock queries, conversations/day) — currently synthetic data, goes live post-deployment. No purchase-conversion signal yet (can't tell if a lookup led to a sale); floated a future "reserve" button as a proxy, pending clarity on how Dr. Max's own systems would use that.

### Production-readiness framing

Jindřich: bar for the current phase is functional correctness against agreed scope, not full polish — non-blocking refinements queue for a later release rather than delaying production. Dr. Max agreed, adding real urgency: an unspecified upcoming "competition" (soutěž) makes going live soon valuable, and may require ad hoc reprioritization of one scenario ahead of others.

### Expectation-setting on feedback volume

Jindřich pre-empted disappointment: based on experience, actual end-user feedback volume tends to be very low regardless of mechanism — most users get their answer and leave. Still worth building, just don't expect a lot of it.

### MVP/roadmap table — recurring ask

Karlecová explicitly named this her standing ask at every meeting: an MVP / full-version / nice-to-have scope table (previously discussed with "pan Sladký") and a roadmap. Jindřich: actively being worked on with Marek this week; the existing tracking Excel is outdated and not well-suited to how fast things change, actively looking for a better tool. Committed to a **weekly recurring sync, Thursdays**, starting next week — covering testing results, ticket status, and the roadmap's first showing.

### Business-case metrics ask

Jindřich asked Mertová (via this meeting) for lightweight time/cost-savings metrics per initiative early next week — explicitly framed as a resource-reallocation argument, not a headcount-reduction one, so BigHub/Dr. Max can quickly redirect effort away from low-value directions rather than as an HR justification.

### Lexie (Lucie) — testing paused on 3 blocking bugs

Karlecová (summarizing for her team, several of whom are on rotating vacation) confirmed no progress since the last sync — testing has stalled. Three items, all logged in X-Manager, are blocking further testing:

1. **Feedback button broken specifically on long/large responses** — reproducible, re-confirmed same-day before this call, video attached in X-Manager. Not present on short responses.
2. **Remove the autocomplete/suggestion popup ("našeptávač") entirely** — pops up unpredictably, including mid-response-generation, visually covering the answer an operator is actively relaying to a customer. Team decided operators don't need it; requested outright removal over an admin toggle, to avoid more configuration surface.
3. **Configurable fixed/canned status messages, outside the prompt** — for outage-style announcements ("web is down," "e-recepty unavailable"). Explicitly do not want to hand-edit the prompt directly (risk of doing more harm than good) — want a safe, contained mechanism for this.

Jura noted the GPT model was upgraded yesterday (5.1 → 5.4) by Viliam Gago — advised holding off further prompt tuning since response length/quality will shift again on its own.

Jura also floated a well-received idea: an automatic, role-gated API-health indicator inside the CC platform — reusing the per-service dashboard he already built for MaxBuddy (Farmis, SPC, e-recepty, orders APIs). Supervisors would see more detail (red/amber/green semaphore); operators see less, to avoid unnecessary panic. Karlecová tied this directly to Maxie too — wants the same outage-awareness surfaced to customer-facing messaging (e.g. proactively telling callers "we know the site is down") to pre-empt call volume during incidents.

Decision: **pause all Lexie testing/design work until the 3 bugs are fixed**; team refocuses fully on Max chatbot in the meantime. Jindřich committed to fixing the 3 bugs by Tuesday/Wednesday so testing can resume, then alternate focus back to Lexie.

### Maxie (voicebot) update

Jindřich: the blocking technical issue (missing SIP trunk on the phone line) is resolved — met with Atlantis last Thursday, no remaining technical blocker. A request list has been handed to Dr. Max's own BDC infra team (main contact: Vladislav Tvarůžek), who are prioritizing the new AKS first, then this. Targeting technical readiness within ~14 days. Maxie is being built by Honza Zelený, sharing infrastructure with the Max chatbot — functionally the same capability, voice instead of text, once complete.

**Scope clarification**: Maxie currently answers exactly one topic via a fixed IVR branch (order status, "press 1"). Karlecová flagged that expanding Maxie to more topics would require reworking Dr. Max's own IVR tree and phrasing — non-trivial on their side. Jura: BigHub can flexibly restrict or expand which topics Maxie is allowed to answer, so Dr. Max can adopt incrementally — start with order status only, open further topics as their IVR is ready.

**Open, unresolved**: whether Max chatbot conversation summaries should be forwarded to Dr. Max's CC platform for operator visibility — raised as a "did we already discuss this?" question, not previously agreed. Jura confirmed conversation memory is already retained for analytics and could be exposed once Dr. Max specifies what they want to see. Also floated, well received: have the AI log a note whenever it can't answer something (an unmet capability), so BigHub/product owners learn what's actually being asked for.

## Decisions Made

- In-chat feedback mechanism: lightweight star/emoji rating only, no free-text field, green→red color order.
- X-Manager feature/change requests for Max/Lexie/Maxie route through one point of contact (Mertová), not individual testers.
- Production-readiness bar for Max chatbot: functional correctness against agreed scope now; non-blocking polish deferred to a later release.
- Medical/dosage questions get redirected to the official SPC package leaflet (displayed via the existing MaxBuddy SPC API), never answered directly — same legal guardrail as MaxBuddy.
- Lexie testing and design work paused entirely until the 3 blocking bugs are fixed; team refocuses on Max chatbot in the meantime.
- Maxie (voicebot) scope starts at order-status only, expands incrementally as Dr. Max's IVR is updated.
- Weekly recurring sync established, Thursdays, starting next week.

## Action Items

- [ ] **Jindřich Tůma**: Send a summary email with the Max chatbot test-environment URL and access instructions — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Jura Brázdil**: Stand up test-accessible version of Max chatbot on the new AKS sandbox — due tomorrow, latest Monday — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Dr. Max CC team**: Test Max chatbot over the coming week; log requests/bugs into X-Manager, routed through Mertová — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Jindřich Tůma**: Fix the 3 blocking Lexie bugs (feedback button on long responses, remove našeptávač, add configurable fixed status messages) — due Tue/Wed — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Jindřich Tůma**: Schedule the recurring Thursday sync starting next week — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Simona Mertová**: Provide lightweight business-case/time-savings metrics per Max/Lexie/Maxie initiative — due early next week — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Marek Pillár / Jindřich Tůma**: Prepare and present the MVP/full-version/nice-to-have scope table and roadmap at next week's Thursday sync — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Jura Brázdil**: Explore a role-gated API-health status indicator on the CC platform, once Dr. Max specifies what they want visible — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync
- [ ] **Jura Brázdil**: Explore having the chatbot log a note whenever it can't answer a user's question, to surface unmet needs — from 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync

## Open Questions

- Who exactly is speaking under the "CZ-BRN-TIT-CCManager" transcript tag — most likely Kateřina "Kačka" Karlecová (named explicitly near the end and matching the detailed bug-report content), but Simona Mertová was also introduced as present, and it's unclear whether any lines under this tag are actually hers or she stayed silent throughout. Flagging rather than guessing per-line.
- Whether/how Max chatbot conversation summaries should be forwarded to Dr. Max's CC platform for operator visibility — raised, not resolved.
- What the "soutěž" (competition) is that's motivating urgency around getting Max live — mentioned but not explained.

## Sentiment & Tone

Strongly positive and high-trust. The Max chatbot demo landed as a genuine high point — spontaneous, unprompted praise and congratulations, described as unlike anything shown to them before. Lexie frustration was voiced candidly but constructively (detailed, well-documented bug reports, a clear ask rather than a complaint) — no hostility, and explicit acknowledgment ("we're all agreed" on the polish-later approach) that BigHub is prioritizing correctly. Karlecová in particular reads as a detail-oriented, UX-literate stakeholder actively advocating for her own operators (feedback-mechanism design informed by her own prior data, concern about avoiding operator "panic"). Jindřich proactively apologized for a delay in reacting to Lexie's testing feedback — a small but genuine trust-building gesture.

## Routing Log

- **project-stakeholders**: Added STK-037 (Kateřina Karlecová), STK-038 (Martin Hrášek), STK-039 ("Machata", low-confidence); enriched STK-001, STK-002, STK-003, STK-011, STK-012, STK-016, STK-017, STK-026, STK-027, STK-029.
- **project-assumptions**: Added ASM-017 through ASM-022 (all Decided).
- **project-knowledge**: Corrected and substantially enriched the Max/Maxie/Lexie entry; enriched MaxBuddy with regulatory/deployment detail; added Communication Channels & X-Manager coverage gap entry.
- **project-daily**: Added 9 action items.
