---
last_updated: 2026-09-04
type: internal
attendees: [Jindřich Tůma, Viliam Gago, Jura Brázdil, Marek Pillár]
tldv_link:
---

# Dr. Max AI Platform Stand-up — X-Manager Ticket Triage & Lexie Demo

**Date**: 2026-09-04
**Attendees**: Jindřich Tůma, Viliam Gago, Jura Brázdil, Marek Pillár
**Type**: internal
**Recording**: N/A
**Previous session**: N/A — new recurring thread (references "yesterday's" Max chatbot demo, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync)
**Meeting prep**: N/A

## TL;DR

Working stand-up: triaged X-Manager's 6 open Lexie tickets and set today's priorities, Viliam walked the team through Lexie's admin/RAG interface live, and a significant scope clarification surfaced — the underlying AI platform is shared infrastructure reused across multiple BigHub clients (not Dr. Max-exclusive), with Marek's ownership scoped to Dr. Max only. Also flagged: an urgent, costly AKS node-pool cleanup issue at BDC.

## Key Discussion Points

### Urgent infra issue — orphaned AKS node pools costing money

Jura opened visibly frustrated: node pools exist that are actively costing money while idle, and there are only two ways out — BDC deletes them immediately, or every project gets redeployed with a node selector (non-trivial, cross-project work). No resolution reached in this meeting; flagged as needing urgent attention.

### X-Manager access and setup

Jindřich finally got X-Manager access after "fighting for 10 days"; Marek has partial access (email/link-based, not fully set up). Jura noted **X-Manager doesn't work over VPN**. The Lexie project is confusingly labeled "komunikace s dodavateli" (supplier communication) in the tool, and unrelated-looking tickets (from other suppliers) appeared and then vanished between views — unclear if a filter issue, not resolved. The team confirmed 6 open tickets under Lexie and reviewed each (see below). Jindřich wants to use X-Manager as the single tracking tool going forward for **all** Dr. Max project tickets, not just Lexie/chatbot — intends to check whether more custom fields/priority levels can be added (the tool's own UI for creating labels/categories is confusing; a "priority" category was attempted but didn't stick cleanly).

### Lexie ticket triage (priority scale: 1 low – 3 high)

1. **Document rename not reflecting in Lexie** — initially attributed to indexer lag; revisited later with a new theory (a diacritics-related issue, since created/modified timestamps matched exactly in one test case). Left open with a question mark, not fully diagnosed.
2. **"Product Scope" ticket** (Kateřina Karlecová asking for an MVP/roadmap) — assigned to Marek; overlaps directly with the MVP/roadmap work already underway for Thursday's sync with Mertová (see 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync).
3. **Thumbs-up/down feedback button broken on long responses** — confirmed root cause: the thumbs aren't real buttons, they sit on an action area that overlaps with the "regenerate response" control on long messages, so double-clicking selects text intended for regeneration instead. Priority 3. Viliam believes he already partially fixed this once before.
4. **Fixed/custom status announcement banner** (for outage-style messages, e.g. "web is down") — priority 3. Viliam has an idea but hadn't started; Marek suggested framing it as a fully custom, admin-editable banner rather than tied to automated health detection — Viliam confirmed that matches what the CC team described wanting.
5. **Test user creation** — turned into a longer architecture debate (see below); given priority 1 (low), punted to Lukáš Szücs (STK-012) to figure out.
6. **Document indexing** — Viliam reports ~99% done already; light follow-up only.
7. **Fix links in responses** — Viliam has it in test, needs merge to master + prod deploy; committed to same-day.

Two specific ticket numbers were referenced without clear 1:1 mapping to the above (**#147**, which Viliam commits to finishing today alongside the two priority-3 items, and **#148**, confirmed already done) — flagged as low-confidence on exact correspondence given transcript quality.

### Test-user auth architecture (unresolved)

Creating a test account for the CC team to try different roles turned out non-trivial: current accounts are Dr. Max-issued (Azure AD-based), and 2FA on those makes ad hoc testing painful. Floated options: a locally-managed admin/service-principal account with an ADO token (bypassing 2FA, since it's not a "real" identity) with role-limiting handled at the frontend; or a proper Dr. Max AD account, but role changes then require Dr. Max to move the account between AD groups manually. No resolution — explicitly deferred, punted to Lukáš Szücs (STK-012) to see if there's a workaround.

### Lexie platform walkthrough (Viliam, live demo)

Viliam demoed the admin view vs. what the CC team actually sees (a scoped-down department view). Two agent types exist: a general web-search agent, and the **Lexie RAG agent**, connected to Dr. Max's SharePoint via a periodic indexer — documents get embedded into a vector database, letting the chatbot answer directly from Dr. Max's internal knowledge base (policies, supplier info, etc.), with clickable source citations back to the origin document. Feedback (thumbs up/down) gets stored to BigHub's own database for later review. Confirmed on this call: the CC team wants the autocomplete/suggestion popup ("našeptávač") removed — consistent with what was already agreed at yesterday's client meeting.

Marek asked whether the CC team tests on desktop or mobile (relevant to design prioritization) — Jura and Viliam believe desktop-only, consistent with a call-center context (matches the "operators have this open on a monitor" framing from yesterday's fixed-status-banner discussion).

### Redesign discussion — explicitly deprioritized, but useful for morale

Jindřich raised whether to generate a rough visual mockup (not a real prototype — just an image, e.g. via ChatGPT) to give the CC team something to look forward to, since "the girls respond to visuals." Marek pushed back, questioning why design comes up at all before technical validation is fully done. Jindřich clarified: technical fixes (thumbs, tickets) remain the real priority — this is a low-cost, no-engineering-time gesture to manage expectations, not a redirection of effort. Jura confirmed the redesign ask itself was minor/in-passing at yesterday's meeting (the CC team liked the Max chatbot's look and casually said "make Lexie like that too"), not a hard requirement.

### AI platform architecture and cross-client scope — significant clarification

Viliam explained the platform's origin: it's a standardized internal BigHub solution (chatbot + RAG), already deployed for other clients — **Brněnská komunikace** (Brno communications), and in-progress variants for **Kooperativa** and **Unica** (for their accounting and legal departments). Dr. Max is one deployment of this shared "core" platform, not a bespoke build. This reframes earlier assumptions that the platform work was Dr. Max-specific — it's shared BigHub infrastructure with a central repo, released out to clients.

This raised an open strategic question, explicitly **not resolved in this meeting**: should the frontend/visual design stay centralized and standardized across all clients, or be customizable per client? Jura's inclination: default to one solid "muster" (template), let clients "wipe" in their own branding only if they explicitly want it and are willing to pay for the customization — keep it "Lego blocks" (separating visual from function) so this stays maintainable. Jindřich noted this is really a company strategy decision, not something to settle ad hoc.

**Scope clarification for Marek**: Marek's role is AI Analyst, representing/replacing Honza Sovka on the Dr. Max account specifically — he'll own the Dr. Max-side backlog and prioritize with the business. Whether Honza Sovka remains product owner of the **broader, cross-client** AI platform is unresolved — Jindřich doesn't know and will check. Marek confirmed his current explicit mandate is to focus strictly on Dr. Max for at least the first month, not take on other clients' work on the platform. Jura's practical take: Marek's Dr. Max onboarding alone is more than enough right now; taking on the whole platform across clients isn't realistic in the near term regardless of the org-chart answer.

### Viliam/Jura handoff — reconfirmed, not urgent

Consistent with 2026-09-03: Jura will take over the shared platform once the new AKS sandbox is ready, migrating MaxBuddy, the Max chatbot, and the new OCR prototype onto it alongside Lexie (four projects consolidated). Viliam's future role is still loosely defined — potentially shifting to more ad hoc/cluster-level support rather than day-to-day feature work, but explicitly described by Viliam as "a vision," not something starting now. Jindřich will discuss the strategic framing further with Alana and Ján Kabát.

### Cadence and next steps

Jindřich will call Mertová directly this morning to clear up confusion from a message Kateřina Karlecová sent the day before, where she seemed to conflate a harmonogram (timeline) document Honza Sovka had shared with a separate ask for an MVP definition — Jindřich reads this as a terminology mix-up on their side, wants to align expectations directly. Also flagged: a recurring sync Mertová will schedule for next Thursday covering all her streams (Max, Maxie, etc.) — consistent with the weekly Thursday sync already agreed 2026-09-03. Marek noted the rough roadmap already sketched for Dr. Max doesn't have much concrete detail yet to hang decisions on, so this Thursday meeting should help fill gaps.

Marek asked Viliam to export and send any existing product/platform documentation before formally handing things to Jura — Viliam acknowledged it's disorganized ("built under time crunch"), needs cleanup first, will prepare something.

## Decisions Made

- X-Manager becomes the single tracking tool for all Dr. Max project tickets going forward, not just Lexie/chatbot (Jindřich's stated intent, pending confirming the tool can support it).
- Lexie redesign work stays explicitly deprioritized behind technical fixes; a rough visual (not a real mockup) is an acceptable low-cost gesture to manage client expectations.
- AI platform frontend default: one standardized template reused across clients, with per-client customization only on explicit request — tentative direction, not a finalized company decision.
- Marek's scope is Dr. Max exclusively, at least for the first month — not the broader cross-client AI platform.
- Test-user creation approach is unresolved; punted for further investigation.

## Action Items

- [ ] **Jindřich Tůma**: Resolve the AKS node-pool cost/cleanup issue with BDC — either get idle node pools deleted, or coordinate a node-selector redeploy across all projects — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Viliam Gago**: Fix the thumbs-up/down feedback button overlapping the "regenerate response" control on long messages — due today — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Viliam Gago**: Build the fixed/custom status announcement banner (admin-editable, for outage-style messages) — due today — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Viliam Gago**: Merge and deploy the response-links fix to production — due today — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Viliam Gago**: Continue investigating the document-rename-not-reflecting-in-Lexie issue (diacritics theory) — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Lukáš Szücs**: Figure out a workable test-user/auth approach (local service account vs. AD group role management) — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Marek Pillár**: Own the "Product Scope" X-Manager ticket from Kateřina Karlecová (MVP/roadmap ask) — overlaps with the roadmap work already due for Thursday's sync — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Jindřich Tůma**: Call Simona Mertová this morning to align on MVP/harmonogram terminology and expectations — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Jindřich Tůma**: Check with Honza Sovka whether he remains product owner of the AI platform across all clients (vs. Marek owning Dr. Max only) — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Viliam Gago**: Clean up and export existing AI platform product/technical documentation for Marek/Jura — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo
- [ ] **Viliam Gago**: Report back to Jindřich today on whether the priority-3 fixes landed — from 2026-09-04-ai-platform-standup-xmanager-lexi-demo

## Open Questions

- Exact mapping between the numbered X-Manager tickets referenced (#147, #148) and the named issues discussed — transcript quality made this ambiguous.
- Whether Honza Sovka retains product ownership of the cross-client AI platform, or whether that responsibility is also shifting — explicitly unresolved, Jindřich to check.
- Why unrelated supplier tickets briefly appeared and disappeared from the Lexie X-Manager view — possibly a filter artifact, not investigated further.

## Sentiment & Tone

Practical, high-trust internal working session — candid about tooling frustration (X-Manager's confusing UI, the node-pool cost issue, general dislike of Teams) without it affecting collaboration quality. Viliam was open and collaborative about handing off ownership to Jura, framing it as "a great opportunity" rather than a loss of scope. Marek asked sharp, grounding questions (why prioritize design before technical validation; desktop vs. mobile testing) that kept the group focused on what's actually blocking the client. No friction between any of the four participants.

## Routing Log

- **project-stakeholders**: Enriched STK-001 (Marek Pillár), STK-003 (Jindřich Tůma), STK-012 (Lukáš Szücs — confirmed as "Lukáš CJ"), STK-017 (Simona Mertová), STK-026 (Jura Brázdil), STK-027 (Viliam Gago), STK-037 (Kateřina Karlecová).
- **project-assumptions**: Added ASM-023 (Open) — X-Manager as single tracking tool; ASM-024 (Decided) — Lexie redesign deprioritized; ASM-025 (Open, tentative) — standardized frontend template; ASM-026 (Decided) — Marek's scope is Dr. Max only.
- **project-knowledge**: Corrected Max/Maxie/Lexie's cross-client scope (platform also serves Brněnská komunikace, Kooperativa, Unica); enriched Lexie ticket triage detail; added the AKS node-pool cost issue; enriched BigHub entry with other clients on the shared platform.
- **project-daily**: Added 9 new action items; updated the existing "fix 3 blocking Lexie bugs" item with today's ahead-of-schedule progress.
