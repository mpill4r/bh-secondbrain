---
last_updated: 2026-09-08
type: internal
attendees: [Marek Pillár, Jindřich Tůma, Jura Brázdil]
tldv_link:
---

# AI Platform Technical Deep-Dive with Jura Brázdil

**Date**: 2026-09-08
**Attendees**: Marek Pillár (PM), Jindřich Tůma (PM), Jura Brázdil (Dev — MaxBuddy, Max Chatbot, Maxie, TEO; most technically familiar with the platform's current state)
**Type**: internal
**Recording**: N/A (transcript provided directly, no tldv link)
**Previous session**: Directly continues [2026-09-08-ai-platform-strategy-history-with-jan-sovka.md](2026-09-08-ai-platform-strategy-history-with-jan-sovka.md), held earlier the same day — Marek opens by asking Jura to fill in the technical reality behind what Jan Sovka described historically.
**Meeting prep**: N/A

## TL;DR

Jura gave the on-the-ground technical picture behind Jan Sovka's earlier history lesson: in practice, "the platform" today is just one product (a document-retrieval RAG system), MaxBuddy still isn't actually inside it (blocked on the new AKS since early August), and the current shared setup has real infra problems — a shared database with zero isolation between use cases and a single shared admin account. Jindřich confirmed this is a fully independent, custom-built project for Dr. Max (the shared-platform vision is dead — consistent with the earlier meeting), and the three agreed a concrete 3-phase plan: rework the UX into one consolidated landing page, migrate existing projects onto the platform on both test and production, then work Dudaško's backlog into an admin/reporting layer. Marek will have a mockup (built in Claude Design) ready by lunch tomorrow (2026-09-09).

## Key Discussion Points

### Current technical reality of "the platform" (Jura Brázdil)

Jura opened by noting he has no historical context — he joined BigHub after the platform's origin story (matches Jan Sovka's account from the earlier meeting). On its current state:

- In practice, the platform today equals **one implemented product: a RAG/document-retrieval system over internal documents.** Nothing else is meaningfully built out.
- It was handed to him with the premise that it would provide shared infrastructure that made deployment easy — in practice, not much of that is actually implemented.
- **Jura Brázdil: "For me it doesn't really simplify my life much, other than that billing is solved — that the LLM credits are properly tracked. That was basically the only reason we pushed MaxBuddy toward the platform in the first place."** [translated from Czech]
- The stated vision (not his) is that the platform should ideally absorb, painlessly, all the infrastructure work everyone currently burns time on individually with Vladislav Tvarůžek — but how far that can go depends on what permissions Dr. Max actually grants.

### MaxBuddy is not actually in the platform yet (correction)

Marek assumed MaxBuddy was the one thing already adapted to Dr. Max under the platform. Jura corrected this directly: **MaxBuddy is not in the platform's own namespace.** They've wanted to move it in, but have been waiting on the new AKS environment since early August — still not done. Other, newer projects are increasingly being built directly under the platform, which simplifies things somewhat for their devs, but Jura flagged concrete infra problems with the current shared setup:
- **A shared database / shared DB server** — e.g., MaxBuddy's process could technically reach in and delete Listing's data; there's no enforced separation.
- **A single shared admin account** used across all use cases.
- **Zero isolation between use cases** — Jura's own characterization: "infrastructural flaws," from his perspective.

### Role-based permissions — narrower than first described

Marek asked whether the row/role-based permission system Jan Sovka mentioned earlier is something Dr. Max has on their own side, or something BigHub's platform already has. Jindřich confirmed roles-by-department/person do exist. **Jura clarified this was built specifically for the RAG chatbot (Lexie) — it is not a general, platform-wide capability today.** This narrows Jan Sovka's earlier framing (see Routing Review — this qualifies rather than contradicts the earlier account). Jura added timeline context: Lexie was only handed to the client after he joined BigHub, roughly April/May 2026 — a fairly recent capability — coinciding with when many new use cases started ramping up and the platform was first intended as their eventual shared home.

### Strategic framing confirmed independent (Marek Pillár, Jindřich Tůma)

Marek asked Jindřich directly whether every Dr. Max use case is also expected to satisfy a BigHub-side use case, or whether they can build fully independently of BigHub's own platform interests. Jindřich confirmed: **this was mostly resolved before today's earlier call** — historically the open question was whether this becomes a true BigHub product (built once, rolled out and adapted per client) versus fully custom per client. **The unifying-product vision is dead; the green light is to build this fully custom for Dr. Max.** (Development nominally continues under that older shared vision only at Kooperativa, but even that is now custom, per Jindřich.)

Concrete near-term goals Dudaško wants, per Jindřich:
1. All BigHub streams/projects for Dr. Max need to live on the platform — in both test **and** production.
2. To get there, the UX needs reworking — partly so it looks professional/user-friendly, partly so multiple projects can be grouped sensibly (categories or similar) with a dedicated reporting section.

### Jura's vision for the unified platform

Today there's no spend/cost breakdown in the platform at all — just the legacy RAG. Jura's plan: once the new AKS lands, he'll bring the chatbot and MaxBuddy into the platform himself and unify it properly — a landing page functioning as a "crossroads" where each user sees the projects/products their group has access to, as one cohesive product rather than scattered links people currently have to individually ask for (dashboards, panels, etc. are all over the place today). He also wants to standardize engineering process — e.g. any pull request under the platform must update a shared, centralized changelog.

**Jura Brázdil: "I'd like to unify this and set firm rules — when you make a pull request under the platform, you have to update the changelog and put all changelogs in one place. Getting those formalities tidy."** [translated from Czech]

### Confirmed as an independent project; capacity question

Marek asked Jindřich to confirm this can be treated as a fully independent, standalone project built specifically for Dr. Max/Dudaško. Jindřich confirmed — a real project that needs real, deliverable output, not just an idea.

Open question raised: Jura is clearly the person who understands this best, but he's spread thin across many active streams — does he have capacity? **Jura's own answer: it'll be a crunch once the new AKS finally lands, but he does have some extra capacity — and since he'll be self-deploying MaxBuddy and the chatbot into the platform anyway as part of his own work, the platform effort may end up helping him rather than being pure overhead.** This meaningfully de-risks the capacity concern raised in the earlier meeting (see Routing Review).

### Three-phase plan agreed (Jindřich Tůma, summarizing)

1. **UX rework** — Jura reworks the platform so there's a proper place to land current and future projects. Marek prepares a visual/mockup of what it could look like; the two share ideas, Jura flags technical feasibility, and they aim for something they can propose to Dudaško for sign-off.
2. **Migrate existing projects onto the platform** — both test and production environments, explicitly for every project ("always both environments" — confirmed by Jura).
3. **Work Dudaško's backlog (from his Excel) into an admin/reporting layer** — once the UX is done and projects are consolidated, pull 3-4 tasks from that backlog into development as a normal project cadence.

Jura had to drop off partway through (phone call). After he left, Marek and Jindřich agreed to double- and triple-check feasibility with Jura before presenting anything to Dudaško, so nothing gets promised that can't realistically be delivered in a normal timeframe. Jindřich favors a simple, pragmatic first pass over anything elaborate — given how long platform work tends to stretch (potentially another half year), and the fact it will keep evolving regardless. **The immediate goal is framed explicitly as making sure Dudaško leaves the eventual presentation impressed and bought in** ("wow, I really want this").

### Mockup approach and timeline (Marek Pillár)

Marek will build the mockup directly in **Claude Design**, using the rough concept Jindřich already sent as a starting point and incorporating Jura's page-layout thinking. Concept: a homepage/"crossroads" where a user sees everything they have access to — different user groups see different things (e.g. warehouse staff wouldn't see MaxBuddy) — exact mechanics (hidden entirely vs. shown in a left-nav list vs. visible on the landing page) deliberately left undecided for now. Jindřich clarified his own sketch was only a 5-minute rough pass — a generic "dispatcher" concept, not meant to be prescriptive — which Jura confirmed agreement with before dropping off.

Marek's plan: also add a Test/Production distinction (badging on non-production, no badge on production), then look at the spend/cost views Dudaško wants — flagging he wants to loop in Jan Sovka and Jura on whether all of that spend data should even be shown, and whether someone with a broader view should sanity-check it before it's exposed. Target: ready by lunch tomorrow (2026-09-09), barring surprises.

**Jura's closing advice (before dropping off)**: don't over-invest time upfront — his own design process is iterative, sketching live with AI tools rather than over-planning, and discovering the right UX by playing with it as he goes. Recommended Marek do a rough first pass and iterate from there rather than trying to nail it perfectly upfront.

**Marek, closing**: reiterated the entire point of the exercise is to give Dudaško something concrete and clickable to react to at the meeting — that's the whole goal.

### Operational notes

- Marek requested AKS access; Vladislav Tvarůžek promised it by lunch today but it had not arrived as of this call. (Ties to the existing tracked item on Tvarůžek's AKS access work.)
- Jindřich confirmed he already sent Dudaško's requirements Excel to Marek (cc'd earlier the same day) — Marek confirmed receipt.
- A DevOps Kanban board is being set up in parallel so backlog items/tickets can be tracked there going forward.
- Marek separately flagged (not fully resolved in this call) that he wants to frame this internally, from a BigHub perspective, as: *"We're doing this in front of Dudaško for business reasons — anything we validate or learn here also feeds back into BigHub's own platform."* Otherwise the work risks looking like a fully bespoke, isolated build for one client with no BigHub-side benefit.

## Decisions Made

1. Confirmed (consistent with the earlier meeting): the AI platform is a fully independent, custom-built project for Dr. Max — the shared-product vision is dead.
2. Three-phase delivery plan agreed: (1) UX rework/consolidated landing page, (2) migrate existing projects to the platform on both test and production, (3) build Dudaško's backlog into an admin/reporting layer.
3. Jura will self-migrate MaxBuddy and Max Chatbot into the platform once the new AKS lands, as part of his own broader unification work.
4. Marek will build the first mockup in Claude Design, targeting ready-by-lunch tomorrow (2026-09-09), favoring a rough/iterative first pass over an over-engineered upfront design.
5. Spend/cost visibility for Dudaško will be sanity-checked with Jan Sovka and Jura before being included in the mockup — not just built as asked.

## Open Questions

- Exact mechanics of role-based visibility on the platform landing page (hidden vs. left-nav vs. main-page listing) — deliberately deferred.
- How much of the spend/cost data should actually be exposed to Dudaško — pending a conversation with Jan Sovka and Jura.
- How/whether to formally frame this project's learnings as feeding back into BigHub's own platform — raised by Marek, not yet resolved.

## Sentiment & Tone

Practical, momentum-building working session — noticeably more energized than the earlier history-focused meeting now that there's a concrete plan and a technical owner (Jura) engaged. Jura was candid and unromantic about the platform's current technical debt (shared DB, shared admin account, zero isolation) without being alarmist about it. Jindřich stayed focused on pragmatism and avoiding scope creep, repeatedly steering toward "simple first, iterate later." No friction; genuine collaborative energy toward a shared, achievable near-term goal (impressing Dudaško at the next presentation).

## Action Items

- [ ] **Marek Pillár**: Build a UX mockup/visual concept for the unified platform landing page in Claude Design, incorporating Jura's page-layout thinking — target ready by lunch 2026-09-09 — from 2026-09-08-ai-platform-technical-deepdive-jura-brazdil
- [ ] **Marek Pillár / Jindřich Tůma / Jura Brázdil**: Validate technical feasibility of the mockup with Jura before presenting anything to Dudaško — from 2026-09-08-ai-platform-technical-deepdive-jura-brazdil
- [ ] **Jura Brázdil**: Once the new AKS is available, migrate MaxBuddy and Max Chatbot into the platform and begin unifying the platform UX — from 2026-09-08-ai-platform-technical-deepdive-jura-brazdil
- [ ] **Jura Brázdil**: Establish a changelog convention for platform pull requests, centralized in one place — from 2026-09-08-ai-platform-technical-deepdive-jura-brazdil
- [ ] **Marek Pillár**: Loop in Jan Sovka and Jura Brázdil on how much spend/cost data should actually be exposed to Dudaško before including it in the mockup — from 2026-09-08-ai-platform-technical-deepdive-jura-brazdil
- [ ] **Vladislav Tvarůžek**: Grant Marek AKS access — promised by lunch 2026-09-08, not yet delivered as of this call — from 2026-09-08-ai-platform-technical-deepdive-jura-brazdil

## Routing Log

Confirmed 2026-09-08 (combined with 2026-09-08-ai-platform-strategy-history-with-jan-sovka). Written:
- **project-knowledge**: added "AI platform — current technical state"
- **project-assumptions**: ASM-039 (3-phase plan, shared), ASM-042 (Jura capacity resolved)
- **project-stakeholders**: enriched STK-026 (Jura Brázdil)
- **project-daily** (2026-09-08): 6 action items written (1 duplicate merged into an existing Vladislav Tvarůžek item rather than added separately)
