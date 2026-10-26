---
last_updated: 2026-10-23
type: external
attendees: [Lenka Henychová, Petra Kytýrová, Šárka Andělová, Simona Mertová, Lucie Fendrichová, Míra Švestka, Jura Brázdil, Marek Pillár]
recording_link:
---

# Max Chatbot — GDPR / Personal-Data Review with Dr. Max DPO and External Law Firm

**Date**: 2026-10-23 (Friday, 9:00–9:45)
**Attendees**: Lenka Henychová (Dr. Max CZE, data protection / DPO, organiser), Petra Kytýrová (external law firm, data-protection specialist), Šárka Andělová (Dr. Max CC), Simona Mertová (Dr. Max CC, Max business owner), Lucie Fendrichová (Dr. Max CC), Míra Švestka (Dr. Max Legal, joined ~35 min in), Jura Brázdil (BigHub, Max developer), Marek Pillár (BigHub, PM — present, silent)
**Type**: external
**Recording**: N/A
**Previous session**: N/A (first meeting of this group; set up in [2026-10-15-lexie-max-maxie-weekly-sync](2026-10-15-lexie-max-maxie-weekly-sync.md), see ASM-296 / ASM-102)
**Meeting prep**: N/A

## TL;DR

Dr. Max's DPO brought in an external data-protection lawyer (Petra Kytýrová) to set the GDPR framework for the Max web chatbot. Agreed: no consent as legal basis (contract performance + Art. 9 health-care exception). Instead, a clearly legible one-line notice with a link, shown at the start of each chat in the empty chat background. Chats may be kept ~30 days on legitimate interest for complaints. Kytýrová sends a first draft of the notice + chatbot privacy policy during the week of 2026-10-26, in time for the end-of-November production target. Open: whether a BigHub–Dr. Max data-processing agreement exists.

## Key Discussion Points

### Why the chatbot is a special-category case

Petra Kytýrová: most e-shops and chatbots get this wrong — few fulfil the information duty at all. A pharmacy chatbot is worse than an ordinary e-shop because, per EU case law, any product a person asks about counts as health-related data; eRecepty make it "beyond doubt". So even a simple chatbot falls under special categories of personal data.

### Legal basis: not consent

- Kytýrová: consent is "completely unsuitable" here. Legal basis = **performance of contract** — the chatbot is a sub-service of the pharmacy's overall service, replacing questions people would otherwise ask in the pharmacy or on the phone line.
- Health data: **Art. 9 exception for management of health-care systems**. Again no consent.
- Information duty ≠ consent: Dr. Max must demonstrably give customers the information up front, that's all. She liked **Alza's** solution as a reference.

### The notice: one legible line + link

- Kytýrová wants a short sentence like "Informace o zpracování osobních údajů jsou dostupné zde" + link, plus a short addition on special categories.
- The current small print under the input ("prototype… does not replace consulting a pharmacist…") is unreadable. Kytýrová: the pharmacist sentence would please the advertising-regulation colleagues; the privacy line must be **clearly legible** to prove the duty was met. Showing it **at the start of the conversation** is enough; it can disappear afterwards.
- Jura Brázdil flagged that a dark, readable line pulls attention (marketing cost). He proposed putting the text in the **empty chat background at the start of the chat**, visually separate from the bot's bubbles, scrolling away as the chat grows. Kytýrová agreed.

### Data flows (Jura's walkthrough + demo)

- **No database, no server-side storage** of conversations. Order / eRecept numbers are passed to other systems and the answer returned; only the **browser** keeps state (e.g. location after the user shares it, or a chosen city).
- The LLM runs on **Azure (Microsoft Foundry)** under EU administration with a legal guarantee that data doesn't leave. Kytýrová: still "processing" under GDPR, however short — duties apply. She would avoid any non-EU transfer (special categories); the Czech supplier is an advantage.
- **Medicines**: search (OTC + Rx), variant choice, stock by location. Usage questions (e.g. "is it OK for children") get a **fixed predefined refusal** (not LLM text) pointing to the pharmacist; the SPC opens with the relevant section highlighted (dosage, contraindications) — that's all it does with the SPC.
- **eRecepty**: via the **public SÚKL interface without a pharmacist certificate**, so no patient identifiers (birth number, date of birth) are returned (Mertová, Jura). Kytýrová: the eRecept number is still personal data — unique identifiers that others can resolve count, and truly anonymous data is almost never achievable.
- **Orders**: two-factor check — order number **plus** the phone or e-mail on the order, since order numbers are sequential (Mertová). Kytýrová praised it; a number-only lookup would be easily abused. Order detail can show items, delivery method and possibly address/phone. (Demo of order status failed on the test environment.)

### What Max stores today: aggregate statistics

Jura: aggregate counters only, not linked to any conversation — counts per query type (stock at pharmacy, product search, order-status click, eRecept-status click, variant chosen, where to buy Rx), count of factual answers that ended the chat, errors (e.g. no location, stock lookup failed, external errors), and number of conversations + messages per conversation. Mertová added the **star rating** (satisfied / not). Kytýrová: rating is the user's choice — by rating they agree to it becoming a statistic; fine.

### Keeping conversations: ~30 days, legitimate interest

- Mertová wants to keep full conversations for a while (first 14 days, then **30 days**) for complaints ("the chat told me X") and to check answer quality, then anonymise/delete. Storage is limited and nobody would pay for 10 years.
- Jura: the planned **operator handover** (future) will require storing the whole conversation server-side anyway, even for minutes.
- Mertová's plan: hand the conversation into the CC's operator system (mails, calls) under a "chat" channel. Paired with a customer only if they gave a phone/e-mail (order) or were handed over; otherwise just "a chat took place on 23. 10. at 9:27" + transcript. Henychová asked whether such chats would appear in a data-subject access request — Mertová: only when paired; mostly Dr. Max won't know who it was. Not fully thought through yet (Mertová).
- Kytýrová: the controller (Dr. Max) sets retention, but must justify it. Legitimate interest can cover up to the limitation period (10 years for health harm), but storing all chats for 10 years wouldn't pass a balancing test. **30 days** has no legal anchor but is defensible from practice (complaints come within 30 days). Needs a **balancing test, a RoPA entry and the notice**.

### What the privacy policy must cover

Kytýrová: statistics, satisfaction rating, location consent and how long location is kept, processor categories (cloud/suppliers), any non-EU access, and per activity the retention and data scope. Free text: customers may type anything (Mertová's example: date of birth for an anti-ageing cream). Kytýrová would set the data scope for product questions as broad as possible. An optional warning ("share only data related to your question") could go in the first or second layer; the policy can double as **chatbot terms of use** ("don't enter illegal content" etc.). Mertová doesn't want to overwhelm or scare customers. Kytýrová: "I don't think anyone reads legal texts" [translated from Czech] — maybe the Office for Personal Data Protection (ÚOOÚ).

### AI and advertising regulation

- Míra Švestka (Legal, joined late): Legal handles advertising and AI regulation **internally**. Their assessment so far: **no major AI-regulation risk**, given the SPC handling and refusal behaviour. Legal will add only an **AI disclaimer** (AI can make mistakes; verify the information). Advertising regulation: will check once more with the colleague responsible.
- Jura: high confidence Max can't give health advice — never succeeded so far; **dozens of golden conversations** test it from many angles; the refusal text is predefined and editable.
- Kytýrová (not her specialty): advertising colleagues would check product presentation — leaflet link, correct labelling.
- Mertová: no advertising in Max, no preferring the Dr. Max brand; not that far yet.

### Data-processing agreement and records

- Henychová asked whether Dr. Max and BigHub have a **data-processing agreement**. Jura signed only an NDA. Švestka thinks one was done with the **BigHub framework contract**; Legal will check.
- Mertová: Dr. Max will add Max to the RoPA/balancing tests before go-live — colleague **Horčica** is updating the existing production records (annual update) and moves on to Max next. Kytýrová will draft the policy first; Dr. Max adapts it into the records.

### Timeline

Mertová: production target **end of November**, before the Christmas season, with the four bubbles shown. Kytýrová had reserved time: **first draft during next week** (week of 2026-10-26), quick finalisation if feedback is fast. Then Henychová + Andělová + others comment, send back, possibly another meeting.

## Decisions Made

- **Legal basis**: performance of contract; Art. 9 health-care-system exception for health data. No consent as legal basis (rating and location remain user choices). — Kytýrová, unopposed.
- **Information duty**: short legible sentence + link to a chatbot privacy policy, shown at the start of each conversation in the empty chat background (Jura's proposal, Kytýrová agreed).
- **Conversation retention**: direction ~30 days on legitimate interest for complaints/quality, then delete or anonymise — subject to balancing test and RoPA entry.
- **Hosting**: stay on Azure EU; avoid any transfer outside the EU.
- **Drafting order**: Kytýrová drafts the notice + policy first; Dr. Max (Horčica) mirrors it into the records of processing.

## Action Items

- [ ] **Petra Kytýrová**: Send the first draft — short notice sentence, layered information, chatbot privacy policy (incl. special categories) — due week of 2026-10-26 — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova
- [ ] **Lenka Henychová**: Review the draft with Kytýrová, circulate to the CC (Andělová, Mertová) and BigHub for comments; set up a follow-up if needed — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova
- [ ] **Míra Švestka / Lenka Henychová**: Check whether a data-processing agreement with BigHub exists (framework contract) — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova
- [ ] **Míra Švestka**: Provide the AI disclaimer wording; check advertising regulation with the responsible colleague — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova
- [ ] **Horčica (Dr. Max)**: Add Max to the records of processing + balancing test (from Kytýrová's draft) before go-live — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova
- [ ] **Jura Brázdil**: Show the notice + link legibly in the chat background at conversation start once the text is ready; replace the unreadable prototype small print — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova
- [ ] **CC team (Simona Mertová) / Jura Brázdil**: Decide conversation storage (30 days, server-side, then delete/anonymise; hand-off to the operator system) and give legal the purposes/retention/data scope to confirm — from 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova

## Open Questions

- Does a BigHub–Dr. Max data-processing agreement exist? (Švestka believes yes, unverified.)
- How long does Max keep location (and other state) in the browser? Needed for the policy.
- Storing chats for 30 days needs server-side storage Max doesn't have today — where, and who pays?
- Do chats paired with a customer (order / handover) fall into data-subject access responses? Mertová: not thought through yet.
- Optional "share only relevant data" warning: Kytýrová open to it, Mertová wary of scaring customers.
- Advertising-regulation check outcome (Švestka's colleague).

## Sentiment & Tone

Productive and cooperative, under 45 minutes. Kytýrová was pragmatic and fast — she steered away from consent and kept the notice minimal. Mertová pushed for keeping customer-facing text light and for practical retention. Legal (Švestka) is relaxed about AI risk. Jura's technical answers (no storage, EU hosting, public SÚKL API, golden conversations) built confidence. Henychová (camera off, ill) chaired and owns the follow-up loop. No tension; the end-of-November target looks feasible from the legal side.

Transcript notes: the lines at 17:13 ("I'm used to getting the data from MaxBuddy…") and 17:21 ("just so the lawyers know we don't have the data") are attributed to Kytýrová but are likely Jura Brázdil / Simona Mertová. The DPO's surname is "Henychová" in Teams (harness had "Henichová").

## Routing Log

Confirmed by PM (2026-10-23, "confirm all"):

- **project-assumptions**: ASM-102 and ASM-296 → Decided; added ASM-340 (30-day retention), ASM-341 (notice in chat background), ASM-342 (DPA existence), ASM-343 (AI/advertising regulation); "Henichová" corrected to "Henychová".
- **product-requirements**: added REQ-008, REQ-009, REQ-010.
- **project-stakeholders**: added STK-087 Lenka Henychová, STK-088 Petra Kytýrová, STK-089 Horčica; updated STK-017 Mertová, STK-050 Andělová, STK-026 Brázdil, STK-085 Švestka; duplicate STK-085 (Mrdlička) renumbered STK-090.
- **project-knowledge**: new "Max chatbot — GDPR framework" entry + pointer in the Max section.
- **project-daily**: 7 action items added; legal-meeting attendance and invite closed; Max reporting item annotated.
- **project-lessons**: LL-108.
