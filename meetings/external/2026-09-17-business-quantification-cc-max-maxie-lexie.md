---
last_updated: 2026-09-17
type: external
attendees: [Marek Pillár, Simona Mertová]
tldv_link:
---

# Business Quantification Call with Simona Mertová — Max Chatbot, Maxie, Lexie

**Date**: 2026-09-17
**Attendees**: Marek Pillár (BigHub, running the interview), Simona Mertová (Dr. Max — business owner, Max/Maxie/Lexie)
**Type**: external
**Recording**: N/A (Marek recorded the call himself; transcript export only)
**Previous session**: N/A — first direct 1:1 Business Quantification interview with Mertová. Related prior context: [2026-09-03-max-chatbot-demo-lexi-maxi-status-sync](2026-09-03-max-chatbot-demo-lexi-maxi-status-sync.md), [2026-09-10-lexie-max-maxie-weekly-sync](2026-09-10-lexie-max-maxie-weekly-sync.md)
**Meeting prep**: N/A

## Transcription Note

The source transcript is heavily garbled (mixed Croatian/Czech/Slovak rendering of what was actually spoken in Czech) — normal for this recording pipeline, but one substantive correction was needed: in the third topic, Marek's spoken word was transcribed as "Maxie" a second time, but Mertová's own words a few lines later ("Leksi se bude koristiti...", "upotrijebi leksi dvaput mjesečno") clearly say **Lexie** — and the described product (a SharePoint-methodology search assistant for CC agents) matches Lexie, not the Maxie voicebot already covered as the second topic. Treated below as Lexie. All quotes are `[translated from Czech]`.

## TL;DR

First live run of the Business Quantification/OKR interview for Dr. Max's three CC-owned AI initiatives (Max chatbot, Maxie, Lexie) — due to Marek tomorrow (2026-09-18) for Tomáš Dudaško. Mertová confirmed business ownership of all three, gave solid JTBD framing for each, but could not cleanly quantify business value in Kč for any of them since none reduce call volume or headcount (pharmacy call volume is roughly fixed) — the real value is capacity/coverage increase and reduced agent cognitive load, which she and Marek agreed to frame as brand/experience value rather than cost savings. Mid-call, Mertová revealed that Kateřina Kadlecová (STK-037), the domain expert for all three initiatives, is leaving on maternity leave with no successor yet named — a new continuity risk.

## Key Discussion Points

### Housekeeping and Kadlecová's departure

The call opened with a brief mix-up (Mertová expected a call to her mobile) before starting. Marek explained the purpose: a business-quantification interview across Dr. Max's AI initiatives, output due to Tomáš Dudaško (STK-010) tomorrow. He confirmed the process: he records and pre-fills a shared Excel from the call, Mertová reviews/edits/green-lights it, then he shares with Dudaško.

Marek asked who the formal business owner and domain expert are for this area. Mertová confirmed she is the business owner for all three ("Jeste to vi? Ano, većih treh" — "Is that you? Yes, all three"). On domain expert, she disclosed that **Kateřina Kadlecová (STK-037)**, who has been playing the lead role on this project, **is going on maternity leave**, and the team needs to reassign ownership internally before she can name a replacement — she'll follow up with a name.

### Max Chatbot

**Objective (JTBD)**: Two drivers — competitive parity ("all e-shops today have some kind of chatbot, we didn't want to fall behind technologically") and 24/7 availability without expanding the phone line's FTE headcount (staffed weekdays until 5pm; expanding it further isn't cost-effective). The chatbot opens an additional, low-cost communication channel for simple queries that would otherwise become emails or calls.

**Escalation threshold**: Handled today via a fixed "bubble" (button-menu) structure covering order status (via API); anything outside that structure gets routed to a specialist rather than attempted in free text, to avoid increasing agent load. Dissatisfied users are redirected to call during business hours. No measurement yet exists of how much load this actually removes from human agents — "we don't have anything like that, because we don't have anything similar" `[translated from Czech]`.

**Business value**: Mertová was explicit the chatbot **does not reduce call/email volume or headcount** — the call center serves the whole pharmacy network and would see the same volume regardless, just on different topics not resolvable by chatbot. The real value is serving **more** customers at the same agent headcount (24/7 vs. 8-hour coverage) and freeing agents from routine queries to focus on higher-complexity issues, reducing what Marek framed as "cognitive load" on agents. Mertová agreed with this framing. She could not translate this into Kč or FTE savings on the spot, floating only a hypothetical: running a live call center 24/7 would require ~20 additional agents for shift coverage. She committed to sending Marek a **blended/average agent (FTE) cost rate** from a corporate table to help quantify this.

**KPI**: No chatbot is in production yet, so there is no baseline. Mertová does **not** want to collect open-text feedback (thumbs/comments), because past experience shows people use it to raise unrelated complaints, not answer-quality feedback. She also flagged that conversation ↔ follow-up-call correlation is essentially impossible today (no email/phone captured except for order-status lookups). The one KPI she committed to conceptually is a **conversation success/resolution rate**. On target number, Marek proposed ~80% (8/10); Mertová set expectations lower for a first version — happy starting around **50%** (5/10), aiming toward 80% once the chatbot moves beyond its current fixed-menu structure to a fuller LLM-based model: "I'll be happy once I reach 5 out of 10, and I'll be happy when it reaches 8" `[translated from Czech]`.

### Maxie (voicebot)

**Objective**: Same underlying motivation as the chatbot, applied to the phone channel — extending live-agent-equivalent service to 24/7 without added FTE, for customers who prefer calling over checking the website (e.g. "are you open on Sunday?" out-of-hours queries) or don't trust self-service.

**Business value**: Same non-headcount-reduction pattern as the chatbot — total call volume stays roughly fixed. The value is coverage: Dr. Max currently answers **~60%** of the pharmacy network's calls at current agent headcount; Maxie is expected to raise that to **~100%** coverage at the same headcount, i.e. quantity *and* comfort improve together rather than one trading off against the other.

**KPI**: Existing measured data (pre-BigHub, from the current voicebot): **~70%** of callers say they're satisfied with Maxie's answer, and **~90%** don't call back within 7 minutes of hanging up (used as a proxy that the need was actually resolved). For a forward-looking containment target (% resolved by Maxie without transfer to a live agent), Mertová first proposed an ambitious **90%** contained / 10% transferred. Marek pushed back that an untested first version promising only 10% escalation risks looking bad if actual performance lands closer to 30%, and suggested being more conservative up front. Mertová revised live on the call to **50/50** — "let's put 50/50 there then... let it land where it lands" `[translated from Czech]` — explicitly flagging this as a soft placeholder, and noting the measurement itself is ambiguous (was a transfer because Maxie failed, or because the caller changed topic mid-call?). Secondary KPI carried over from existing practice: ≤10% of callers call back again within 10 minutes.

### Lexie (internal knowledge assistant)

*(See Transcription Note above — this is the topic mislabeled "Maxie" a second time in the transcript.)*

**Objective (JTBD)**: CC agents handle an extremely broad scope — e-shop orders, loyalty program, pharmacy-type matters, even ad hoc police inquiries about vehicles registered to Česká lékárna holding — against a large, fragmented knowledge base: individual methodology documents on SharePoint, some later condensed into shorter "product cards," others only ever clarified ad hoc by email when there wasn't time to properly update the methodology. Agents were searching by filename keyword, opening the document, and using Ctrl-F. Mertová's framing: "let's save people the stress of digging through folders by name and doing Ctrl-F through a wall of text" `[translated from Czech]` — Lexie was built to make this lookup fast and effortless.

**Business value**: The hardest of the three to quantify. Mertová's own rough estimate: roughly **~30 minutes/day** saved per agent, but she immediately and explicitly resisted turning that into a cost-savings narrative herself, unprompted: "I wouldn't want someone hearing 'saves 30 minutes a day' and then telling me I can let 3 people go, because that's not true" `[translated from Czech]`. Marek agreed and reframed the value as qualitative — plainer customer experience (no long holds while an agent digs for an answer), improved professionalism, and (Mertová's own addition) a **faster onboarding ramp for new agents**: new hires currently take **~1–1.5 (up to 2) months** before handling calls independently; she believes Lexie could shorten this by roughly **~14 days**. Experienced agents (5–6 years' tenure) barely use it (~2x/month, only on genuinely unusual cases) — short, routine calls are unaffected either way. She stated plainly: "these are very soft skills that can't be converted into money — increased confidence, expertise, better customer experience. Nothing else comes to mind" `[translated from Czech]`.

**KPI**: No number was set. Marek floated two candidate directions: (1) reduced average call-handling time (e.g. 10 min → 6 min) and/or more calls handled per shift, or (2) reduced new-agent ramp-to-independence time (currently ~1–1.5 months) — the latter is the more concrete, credible lever raised on the call, but neither was finalized with a target.

### AI platform UX (tabled, off-agenda)

With ~10 minutes left, Marek raised the AI-platform UX feedback thread from his session with Tomáš Dudaško later the same day. Mertová gave a quick personal reaction — the platform currently "feels like an old Form 602 — very utilitarian, plain, no color, no icons" `[translated from Czech]` — but said she's only used it a handful of times herself and deferred detailed pain points to her CC colleagues who use it daily. She offered to have Marek raise this directly with them in a dedicated session rather than relay it secondhand.

## Decisions Made

- Business value for Max chatbot and Maxie will be framed as **capacity/coverage increase and reduced agent cognitive load**, not FTE/headcount cost savings — both agreed the call center's total volume is fixed regardless of chatbot/voicebot adoption.
- The same non-headcount-reduction framing applies to Lexie — Mertová explicitly rejected a "time saved → fewer people needed" narrative for her team.
- Maxie's forward-looking containment-rate target was revised down live on the call from an initial 90% to a placeholder **50/50** split, flagged as not final.
- AI-platform UX feedback will be gathered directly from Mertová's CC colleagues (the actual daily users) in a separate session, rather than through Mertová.

## Action Items

- [ ] **Marek Pillár**: Fill in the Business Quantification/KPI Excel for Max chatbot, Maxie, and Lexie from this call and send to Mertová for review — from 2026-09-17-business-quantification-cc-max-maxie-lexie
- [ ] **Simona Mertová**: Review, edit, and green-light the completed Excel (or comment inline) — due 2026-09-18, ahead of Marek's sync with Tomáš Dudaško — from 2026-09-17-business-quantification-cc-max-maxie-lexie
- [ ] **Simona Mertová**: Reassign and name a new domain expert for Max chatbot/Maxie/Lexie to replace Kateřina Kadlecová, who is departing on maternity leave — from 2026-09-17-business-quantification-cc-max-maxie-lexie
- [ ] **Simona Mertová**: Send Marek a blended/average agent (FTE) cost rate at the corporate level, to convert time-based estimates into Kč for the chatbot/Maxie business case — from 2026-09-17-business-quantification-cc-max-maxie-lexie
- [ ] **Marek Pillár**: Convene a separate AI-platform UX feedback session with Mertová's CC colleagues who use the platform daily — from 2026-09-17-business-quantification-cc-max-maxie-lexie

## Open Questions

- Who replaces Kateřina Kadlecová as domain expert for Max chatbot/Maxie/Lexie — unresolved, pending Mertová's internal reassignment.
- Agent/FTE cost rate — pending from Mertová; needed to convert the 20-extra-agents-for-24/7 hypothetical and the ~30 min/day Lexie estimate into Kč figures.
- Final Max chatbot KPI target — directional only (~50% initial, ~80% aspirational conversation-resolution rate), not committed.
- Final Maxie containment/transfer-rate KPI — provisional 50/50 placeholder, explicitly flagged by Mertová as "wherever it lands," not a real target.
- Lexie KPI/business-value quantification — the least resolved of the three; two candidate directions proposed (handle-time reduction vs. new-agent ramp-time reduction), neither finalized.
- Whether/how to express the shared "reduced agent cognitive load / call quality" benefit across all three initiatives in the KPI Excel, given it's qualitative and Mertová can't put a number on it.

## Sentiment & Tone

Warm and cooperative throughout, with genuine give-and-take rather than passive compliance. Mertová pushed back constructively multiple times rather than accepting whatever Marek proposed: she resisted his suggested Maxie containment framing as too ambitious for a first version (talking herself down from 90% to 50/50 live on the call), and — more notably — proactively resisted her own instinct to frame Lexie's time-savings in cost terms, worried aloud that it could be misused to justify headcount cuts on her team. This reads as real ownership and protective advocacy, not just data-gathering compliance, consistent with the pattern seen in this week's other Business Quantification calls (Tereza Foltýnová, Petr Neuman). She was candid about her own numeracy limits ("I admit I don't know how to calculate this") without becoming defensive, and volunteered concrete data unprompted (Maxie's existing 70%/90% stats, the new-agent ramp-time figure) rather than waiting to be asked. She thanked Marek warmly for "the sparring" (`"djekuju za oponenturu"`) after the chatbot section, suggesting the JTBD/Fermi interview style landed as a genuine collaborative exercise. The mid-call disclosure that Kadlecová — her most engaged domain expert across all three initiatives — is leaving on maternity leave with no successor yet named is a real continuity risk worth tracking, raised candidly rather than buried.

## Routing Log

- **project-stakeholders**: Enriched STK-017 (Simona Mertová — confirmed owner of all three initiatives, JTBD framing, Kadlecová succession disclosure, Last interaction → 2026-09-17). Enriched STK-037 (Kateřina Kadlecová — Status updated to reflect departure on maternity leave, successor not yet named).
- **project-assumptions**: Added ASM-091 (Kadlecová's domain-expert role vacant pending reassignment), ASM-092 (Max chatbot/Maxie value framed as capacity/coverage, not FTE savings — Decided), ASM-093 (Max chatbot KPI ~50%/~80% directional), ASM-094 (Maxie containment KPI walked back to 50/50 placeholder), ASM-095 (Lexie business value/KPI unresolved), ASM-096 (agent/FTE cost rate pending from Mertová).
- **project-daily**: 4 action items added to 2026-09-17's daily; the standing highest-prio item to schedule this interview marked done.
- **meetings/index**: Entry added.
- **Related**: `CC BQ` sheet in `~/Library/CloudStorage/OneDrive-BigHubs.r.o/2. Business Quantification/businessQuantificationWorskop.xlsx` filled directly with this call's content, per PM request.
- **project-lessons**: Triggered autonomously — see project-lessons.md for any captured entries.
