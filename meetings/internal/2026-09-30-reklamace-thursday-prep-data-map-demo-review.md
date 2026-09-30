---
last_updated: 2026-09-30
type: internal
attendees: [Marek Pillár, Jindřich Tůma, Filip Černý]
recording_link:
---

# Reklamace Thursday Prep — Data-Map Walkthrough & Email-Agent Deck Review

**Date**: 2026-09-30
**Attendees**: Marek Pillár (AI Analyst / PM), Jindřich Tůma (BigHub↔Dr. Max lead, STK-003), Filip Černý (Developer, STK-006). Jindřich left before the last ~10 minutes.
**Type**: internal
**Recording**: N/A (transcript, ~41 min, Czech/Slovak)
**Previous session**: [2026-09-29 email-agent demo review](2026-09-29-reklamace-email-agent-demo-review-filip.md), where this three-way sync was agreed. Related: [2026-09-29 management-meeting debrief](2026-09-29-management-meeting-debrief-reklamace-thursday-plan.md).
**Meeting prep**: N/A

> **Transcript note**: speaker labels are heavily scrambled. The tool mixed all three names, and Slovak speech labelled "Filip Černý" or "Jindřich Tůma" is mostly Marek. Attribution here is from content and language: Marek speaks Slovak; Filip and Jindřich speak Czech. Some Czech lines between Filip and Jindřich are best-effort.

## TL;DR

This was the final internal prep for the 2026-10-01 logistics meeting.

**Data-map Excel:**
- The target columns now explicitly mean **"is it possible", not "do we want it"**. Everything *can* live in Excel, SharePoint Lists, Confluence and even Axapta. AX is blocked by agreement and politics, not technology ("don't confuse content with form").
- Recommendation for Thursday: offer that BigHub **doesn't need from AX anything AX doesn't already hold**. AX supplies the supplier account, what it already owns, and the case fields only it has (reklamace no., RD, issue date). Everything else goes into one **SharePoint List** linked by supplier account, set up by Dr. Max's side to BigHub's column definition.
- Open risks: who owns that list as business owner (BigHub may become the de facto owner), and reading it via Graph API is another infra request.
- Marek sends the Excel **today** as a soft prep email ("read if you have time"), careful not to push Sláma.

**Filip's deck:** approved. Marek asked him to **highlight the keywords** in each example email that drove the classification, and to trim the "next steps" slide to ~3 points, with the rest sent by email.

**Login:** the per-user login Sláma asked for will come via **one shared Entra registration** for logistics and platform apps, with Jura next week.

## Key Discussion Points

### Listing debrief (Marek)

Marek summarised the morning with Neuman and Vdovicynová as "the same pattern as everywhere":
- The MVP assumed pushing a product and parameter set into Magento, but Magento won't let BigHub import or export.
- So the MVP became enrichment plus an own export.
- The target system itself will be replaced eventually.
- "But it turned out quite well." See [2026-09-30 Listing reset](../external/2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy.md).

### Data-map Excel walkthrough

Marek shared the data map ("marek sheet v2"). It covers every piece of supplier and case data: current location, candidate stores, and past decisions from meetings. He had gone through it with Filip in the morning.

**The biggest item is E13, the follow-up email sequence.** It was never in the original scope; Sláma commented on it in the spec and nobody responded. BigHub is "on the same boat" to eventually deliver it (that's why the POC exists), but the tracking location still needs choosing. SharePoint Lists looks most capable: "it looks like Notion, a nice table, not archaic, with overview and traceability" [translated from Slovak].

**What the columns mean (Jindřich's question, Filip's answer).** The store columns say whether something is *possible*, not whether BigHub *wants* it:
- Everything that fits in SharePoint Lists also fits in Excel; Excel is just strongly disfavoured.
- Axapta could technically hold everything too. The "Ne / nedomluveno" (no / not agreed) marks are **political, not technical**: "we mustn't confuse content and form… with Axapta the problem is political: they don't want to put it there, not that it can't be done" [translated from Czech].
- Marek will fix the AX column: "possible, not agreed" instead of "?" or "—".

**Contacts.** The current API contract carries **one contact** because that's what's agreed. The API will change anyway and could carry ten. Filip strongly doubts AX has actually implemented even the agreed contacts: "Kuba pushed hard; they probably nodded but certainly didn't implement it… I'd be very surprised" [translated from Czech].

**Ownership principle (Filip).** Supplier know-how is Dr. Max's business knowledge. Dr. Max should maintain it and hand it over in a secure, structured way; *how* doesn't matter to BigHub.
- "We need the information but in no case want to own it." BigHub could build a database tomorrow, but then Dr. Max staff couldn't change anything or manage permissions: "a vicious circle".
- AX looked logical to Filip and Kuba: an app with a database where a new "knowledge base" table could live.

**Proposal for Thursday** (Filip, backed by Marek's result paragraph):
- Since AX is "not agreed" and likely not done anyway, offer that BigHub **doesn't need from AX the information AX doesn't hold today**.
- AX provides the supplier identifier plus what it already owns. Everything else lives in another table linked by supplier account: "we only care that the information is linked".
- The **case fields for the rozvozový list** (reklamace number, RD, issue date) exist only in AX, which is the source of truth, so some AX development is unavoidable. Filip called it "our and their oversight" that nobody noticed they were missing before.

**Business owner of the external store.** Marek: going halfway means BigHub builds it, but it's undefined who the business owner of a SharePoint List (or Confluence) would be. There will be a lasting commitment: "they'll come to Filip Černý whenever something changes".

**Confluence.** Marek suggested dropping Confluence and offering only SharePoint Lists. The counter-view (likely Jindřich, who raised Confluence on 2026-09-25): keep it, since it has already been mentioned, and admit it wasn't analysed. Recommend SharePoint Lists as preferred, and have Dr. Max's side set it up to BigHub's column definition.

**The "minimal AX development" wording** in the result paragraph. Jindřich flagged that the client claims heavy AX development, so "minimal" may be disputed. Filip's view: "minimal" is accurate. BigHub needs *some* AX work no matter what, because some information exists only there. Marek will review the generated result paragraph; he had focused on the table.

**Sending it.** Marek will check the Excel for errors and send it today as a friendly prep mail: "if they don't read it, we open it tomorrow", with no decision asked by email. Jindřich: be careful with Sláma, "he's always sensitive to us pushing him"; say we're just sharing it, great if they have time, otherwise we'll discuss at the meeting. The spec won't be approved this week, but the Excel feeds the documentation.

### SharePoint Lists: setup and access

Filip: a SharePoint List needs no Dr. Max development, but BigHub must read it via **Graph API** (the same as for email drafts). That means another infra request and probably waiting; Filip has never set it up.
- Someone must create the list, manage it and take responsibility.
- Filip could create it with his external Dr. Max account (permissions and so on) and hand it over later. The bigger blocker is the recurring import and read via Graph, not who clicks it together.

Jindřich: from today, all infra requests go through **ServiceNow tickets**. Tvarůžek gets ServiceNow access ("Láďa" too), so requests are tracked in one place. When needed, BigHub defines the columns and asks Dr. Max's side to set it up.

### Per-user login for UAT (Filip)

Sláma asked last Thursday for working login in UAT. Filip agreed with Jura Brázdil to do **one Entra registration** covering logistics and the platform apps (Lexie, Max bot, …), rather than asking Tvarůžek for four separate registrations. Juraj's e-commerce registration will migrate later. Jura does it next week; Filip will say on Thursday that it's in progress.

### Email-agent deck (Filip)

Deck flow:
1. What the prototype does: opens the thread, waits, analyses the reply, sets the next step.
2. Terminal states: disposal, send to warehouse, carrier pickup. Plus waiting, and hand-off to a person.
3. The deterministic first email, e.g. "v příloze posílám reklamační protokol a fotodokumentaci k reklamaci RD…" ("attached are the claim protocol and photo documentation for claim RD…").
4. Real examples: disposal; "please send to our warehouse"; "we'll collect, wait for the pickup label" → waiting → label arrives → own pickup; an internal forward → waiting → colleague offers to swap expired stock → hand-off to a person.
5. Next ideas: more test threads, automatic reminders, supplier-specific first emails. Filip: that is "more toward the ten MD".

Marek's feedback:
- **Trim the ideas slide.** Mention three and send the rest by email; tomorrow is ~30 minutes that will stretch to an hour (5 min ops, 10–20 min Excel, then the demo).
- **Highlight the keywords** in each example email that drove the decision (e.g. "přeposílám" = forward), so the audience sees the logic without reading, "even if it's a bit of faking".

Jindřich was fine either way ("sort it out between you two"). Filip agreed it's a good idea, quoting Honza Sovka: "a good demo doesn't have to be fully real". Marek apologised in case the feedback sounded sharp; Filip said it didn't.

### After Jindřich left (Marek + Filip)

- **Sample size.** 7 threads mean nothing statistically, and Jana's selection may be biased either way. With ~100 conversations BigHub could estimate the share of one-question-one-answer cases (currently "around half or more").
- **Why logistics wants this so badly.** Marek asked. Filip: Dr. Max pushes AI restructuring "without really knowing what it's good for". Humans read these emails instantly. The real saving is **digitization**: no retyping AX numbers, downloading WhatsApp photos, printing and scanning the rozvozový list. "That's not AI, that's digitization… connecting systems and automating processes" [translated from Czech]. Marek noted a Claude agent could triage such mail in minutes. Filip is most curious about Egrmaierová's feedback ("this never happens" vs. "this saves us 10 minutes a day").
- Filip described himself as fresh out of school and wary of technical nitpicking. Marek: nobody in logistics will challenge it technically; the point is to show the business value.
- Marek told Filip not to review the spec today: focus on Thursday and take it Thursday/Friday.

## Decisions Made

- **Data-map store columns mean feasibility, not preference.** All stores are technically possible, including AX. AX blockers are labelled "possible, not agreed".
- **Recommendation for 2026-10-01:** AX supplies the supplier account, what it already holds and the case fields only it has (reklamace no., RD, issue date). All other supplier data goes into one SharePoint List linked by supplier account, set up by Dr. Max's side to BigHub's column definition. Confluence stays as an option but isn't analysed; SharePoint Lists is preferred.
- **The data map goes to logistics today** as a soft prep email, with no decision requested by email and deliberately low pressure on Sláma.
- **Deck changes:** highlight the deciding keywords in each example; trim the next-steps slide to ~3 points and send the rest by email.
- **Infra requests go through ServiceNow tickets** (Tvarůžek to get access).
- **One Entra registration** for logistics and platform apps; the UAT per-user login follows next week (Filip + Jura).

## Action Items

- [ ] **Marek Pillár**: Fix the AX column in the data map ("possible, not agreed" instead of ?/—), review the whole sheet and the result paragraph for errors (incl. the "minimal AX development" wording) — due 2026-09-30 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review
- [ ] **Marek Pillár**: Send the data map to logistics today as a friendly prep email (read if time allows, discuss tomorrow; soft tone for Sláma) — due 2026-09-30 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review
- [ ] **Filip Černý**: Highlight the deciding keywords in the example-email slides; trim the next-steps slide to ~3 points; send the full list after the meeting — due 2026-10-01 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review
- [ ] **Filip Černý / Jura Brázdil**: Implement the shared Entra registration and enable per-user login for Reklamace UAT — due week of 2026-10-05 — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review
- [ ] **Jindřich Tůma**: Set up ServiceNow ticketing for infra requests with Tvarůžek — from 2026-09-30-reklamace-thursday-prep-data-map-demo-review

## Open Questions

- Who is the business owner of the SharePoint List (or Confluence) holding supplier data? How is BigHub's ongoing commitment bounded?
- Has AX actually implemented the agreed fields (supplier account, address, main contact)? Filip doubts it.
- How long will Graph API read access to SharePoint Lists take through infra?
- Will logistics provide ~100 real threads to measure the share of simple cases?
- Is the Reklamace value really in AI, or mostly in digitization? (It feeds the continue-or-close framing, [[ASM-122]].)

## Sentiment & Tone

Collaborative and a bit tired before a big day. Jindřich was supportive ("super udělaný", "great work") and focused on clarity and Sláma's sensitivity. Filip was engaged and candid, with some self-doubt as a recent graduate, and showed quiet scepticism about the AI value of the email agent. Marek drove the logistics (send today, simplify the deck) and was conscious of tone, apologising for feedback that might have sounded sharp. The team is aligned on the Thursday narrative: go halfway toward AX, recommend SharePoint Lists, show the demo simply.

## Routing Log

Confirmed by PM on 2026-09-30.

- **project-assumptions**: ASM-213–ASM-217; update notes on ASM-170, ASM-174, ASM-205, ASM-206, ASM-188, ASM-182, ASM-122
- **project-knowledge**: Reklamace entry, email-agent prototype
- **project-stakeholders**: STK-034, STK-016, STK-026, STK-006
- **project-daily**: 2 PM-owned action items; 2 items closed; others' items stay in this note
