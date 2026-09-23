---
last_updated: 2026-09-24
type: internal
attendees: [Jura Brázdil, Marek Pillár]
recording_link:
---

# AI Platform Prototype Walkthrough — Navigation, Modular Reporting & Lexie/Platform Separation

**Date**: 2026-09-23
**Attendees**: Jura Brázdil (BigHub — platform/TEO-OCR developer, STK-026), Marek Pillár (AI Analyst)
**Type**: internal
**Recording**: N/A
**Previous session**: [2026-09-21-ocr-progress-ai-platform-prototype-sync](2026-09-21-ocr-progress-ai-platform-prototype-sync.md) (Jura's first prototype build, shown same-day as Dudaško's own vision call)
**Meeting prep**: N/A

## TL;DR

Jura walked Marek through his AI Platform prototype in detail — super-admin navigation, per-project modular reporting/docs/technical-status, role-based views driven entirely by Dr. Max's existing AD groups, and a cost/incident dashboard designed so Dudaško sees BigHub already knows about a problem before he has to ask. Explicitly deferring all visual/design work until the navigation and infrastructure fundamentals are validated with Dudaško, targeting a demo this Friday. Surfaced an important framing fix — separating "the platform" from "Lexie" as a concept, since conflating them explains some of Dudaško's frustration — and a real security gap (MCP server secrets leaking to any agent that reads server descriptions) that needs sealing before further build-out. Jura remains fully blocked on further real deployment until database access comes through.

## Key Discussion Points

### Super-admin navigation and platform-level panels

Jura demoed the top-level "platform" view a super-admin sees: a status/incident panel (consistent styling across all projects — every project gets reporting, docs, and technical-status sections, though not all have content yet), a technical-status view (per-project uptime, external dependencies, active and historical incidents), a cost breakdown per project (currently mocked, but a real breakdown is feasible if BDC grants read access to Azure billing — could show OpenAI/Kubernetes/AI Search costs specifically), a permissions view (which AD groups can access what — uncertain whether BDC will allow this to be read programmatically; worst case, a manually maintained list still works), an audit log (logins, settings changes — e.g. someone disabling a chatbot), and a roadmap section (pilot/test/production status per project). The explicit intent behind the incident panel: when Dudaško hears about a problem from a pharmacy, he can check the panel and see BigHub already knows and is on it, rather than looking uninformed.

### Modular per-project structure

Each project (Lexie, MaxBuddy, Chatbot Max, Maxie, OCR, etc.) will expose its own modules to the platform via a manifest (its reporting page, its docs page, its technical-status page) — the platform itself doesn't dictate what those pages contain, only surfaces them consistently. Role-based visibility is driven entirely by Dr. Max's own existing AD/IdM group definitions — BigHub doesn't redefine permissions, it consumes the existing group structure and shows only the modules a given group has access to (e.g. a "MaxBuddy Ops" login sees only MaxBuddy's reporting and case-argument tiles; a "MaxBuddy Admin" login sees everything for that project).

### Deliberately deferring design — infra and navigation first

Marek recapped an alignment made with Jura the day before: this MVP explicitly does not address colors, visual design, or design language — the goal is to validate with Dudaško whether the navigation and interaction split *feels* right, as a first pass ahead of the real decision meeting. Jura's sequencing: get platform infrastructure fundamentals working first (cost/FinOps reporting, projects surfacing what they currently actually have), get sign-off on that direction, then iterate on visual design. His planned framing for Dudaško if design gets raised prematurely: "we hit 9/10 of your requirements fast; categorization and visual polish come next, this is a quickly-deliverable first version" — and more generally, that the platform is deliberately built to be infinitely scalable/modular, which handles most design pushback without committing to specifics early. Marek's own client-work heuristic, offered as guidance: show less now and layer on top later — showing Dudaško too much too early (e.g. a full RAG agent) invites him to demand it immediately rather than let it land as a natural next phase.

### Homepage/UX questions Marek raised

1. **"Pilot" label meaning**: does "pilot" on the homepage mean test or production? Jura clarified it means live-in-production but only at a subset of pharmacies (e.g. MaxBuddy is in pilot at 20 of 60 branches) — a separate axis from the test/prod environment split, which will each show only their own environment's data.
2. **Platform adoption reporting**: Dudaško will want visibility into platform usage/adoption itself (how many people access it, at what rate) — not yet built, needs to be added as its own reporting concern.
3. **Scalability of the tile layout**: with only ~3 active projects today, the flat tile list works, but Marek flagged concern about a future with ~30 projects. Dudaško had floated a layered categorization (e.g. "reporting" as one layer, "agents" as another). Jura confirmed this is technically buildable (search, even an HTML-generating reporting agent that answers status questions directly) but explicitly out of scope for now — not worth solving for 3 projects, worth flagging to Dudaško as "we're aware and it's planned" without building it yet.

### RAG-style cross-platform agent — kept in reserve, not built

Jura independently proposed (echoing an idea from Marek's own earlier Databricks-styled artifact, not yet discussed with Jura directly before this) an eventual RAG agent with access to everything a given user can already click into — reporting, docs, roadmap — so a user could just ask "how's AKS doing?" and get an answer instead of navigating there. Both agreed this is valuable long-term and explicitly not worth building now, given so few active projects — kept "in reserve" as something to offer only if Dudaško specifically asks for it, consistent with the show-less-first principle above.

### Test/prod cost reporting — no clean answer yet

Dudaško has previously indicated he'll want combined AOAI/token cost visibility across both test and prod environments (at one point suggesting test projects could appear as grayed-out tiles within the production view). Jura's proposed mechanism: rather than a full network bridge between test and prod clusters, restrict it to a single reporting endpoint — either prod pulling directly from a narrow test-side endpoint, or test periodically pushing stats to an intermediary store that prod reads — whichever avoids a genuine security exposure. Marek asked about a simple global test/prod environment switcher (common SaaS pattern); Jura pushed back mildly — a global switch implies "everything I'm now seeing is test-only," which could conflict with Dudaško wanting a *combined* cost view across both. Tentative alternative: keep cost views combined by default, and add a clear "you are in TEST" banner when browsing test-specific functional screens. Not finalized — flagged as a topic to open directly with Dudaško.

### Role-based UX for non-admin, multi-product end users

Marek asked Jura to prepare a simulated account representing a real end-user with access to multiple products but no admin/reporting/docs/technical-status rights (e.g. Customer Care staff using Chatbot Max + Lexie + Maxie). Jura demoed logging in as a limited "Lexie admin, chatbot CC" account: sections the account has no rights to (like Administration) show as visible-but-empty gaps rather than being removed, which Marek flagged looks like a layout bug. Jura agreed — the fix is either to reflow the layout to remove the gap entirely, or to explicitly show those sections in a disabled state with a tooltip explaining why, rather than leave unexplained blank space. Not fully resolved; Jura will prepare a fuller "plain end-user, several products, no admin rights" simulated account for Marek to review, since real end-users (unlike admins) will never have those permissions at all.

### Multi-department Lexie knowledge bases — UX for switching context

With Lexie split into ~5-6 separate department knowledge bases today, Marek asked how a user with access to more than one department's KB should navigate between them. Jura's proposed pattern: skip an upfront department picker — the chat opens directly and is usable immediately, with a bottom-of-input selector (like ChatGPT's model picker) to switch department/KB context if needed, rather than forcing a selection before the user can do anything. Marek agreed this is the right MVP-level answer; a full cross-everything RAG agent (see above) remains overkill for this.

This surfaced a more important framing point: **"platform" and "Lexie" need to be explicitly separated as concepts** going forward. The team had previously been calling Lexie itself "the platform," which Jura believes explains part of Dudaško's frustration — he wants an actual platform, and what existed under that name was really just Lexie wearing the label. Going forward, platform-level navigation/reporting is one concern; Lexie's own internal behavior (including a possible future single cross-department knowledge base with full access, which Jura would treat as a Lexie-level feature request, not a platform one) is separate and lower-level.

### Jura's blockers and near-term priorities

Jura remains **fully blocked on further real deployment work until he gets database access** — already requested from Vláďa/BDC, still pending (Marek noted Dudaško sometimes messages him twice a week asking if it's done yet; Marek's standard answer is "not yet, Vláďa knows," suggesting Dudaško has some other, informal channel feeding him status too). Ahead of that, Jura still has prep work: reworking parts of the platform for security before wiring in real projects, and migrating MaxBuddy and Chatbot Max directly under the platform once he can. He flagged a genuine security gap found along the way: **MCP server registration currently leaks secret/header values** to any agent that reads MCP server descriptions — needs sealing before this goes further. His prioritization: platform infrastructure and security first, then design — he'll compress this if the team is under real pressure, but this is his preferred order.

### Chatbot Max bug-fix status (on track for tomorrow)

Jura confirmed he's on track for tomorrow's status meeting — the OCR work given to him was turned around within about an hour yesterday, and he has the rest of today plus tomorrow morning for Chatbot Max fixes. Existing convention with the CC testers: once Jura marks an item "Doctor Max" with a resolution comment, the testers know to retest immediately without waiting to be told separately.

### Small Lexie design-tweak request — recommend deferring

A minor client email asked for border/padding adjustments in Lexie's UI (color-scheme consistency around the chat bubbles). Marek wasn't sure he could scope it without more detail from the requester; Jura is reluctant to make small visual changes now given a larger redesign is coming — it would be wasted work unless the business explicitly asks for it ahead of that redesign. Marek agreed this is clearly lowest priority (not MVP, at most "nice to have"/full-version scope) and will raise it directly at tomorrow's status to push it back rather than quietly do it.

### Excel/backlog reality check

Marek asked Jura to give Jindřich a summary of the requirements/backlog Excel Dr. Max compiled, ahead of a fuller conversation. Jura's read: a large portion of it is currently unworkable given Dr. Max's actual IT constraints — e.g. isolating every individual agent/chat/tool completely from each other would take roughly the same two months BigHub is already spending just isolating its own environment from Dr. Max's payroll system; several asks would require either extremely broad Azure privileges or effectively having 2-3 dedicated BDC people on call 24/7. Marek recalled Jura previously saying it *would* be possible with three additional BDC people — Jura confirmed that's the (unrealistic) threshold implied. Marek's view: this reflects the backlog being written from an owner/user wishlist perspective, and should be reasoned through carefully with Jindřich/Dudaško rather than dismissed outright — a realistic-scoping conversation is needed.

### Scheduling the Dudaško demo

Targeting **Friday** to present the updated prototype to Dudaško — tomorrow doesn't fit his calendar per Marek's check. Marek will schedule it; presenter wasn't pre-agreed (Jura offered to walk through it himself). Plan: review the refreshed prototype together the day before finalizing (with Jindřich), and all three likely attend the actual Dudaško session, since Dudaško is "sharp"/can be moody but is manageable with good arguments, per both Marek's and Jura's read of him.

## Decisions Made

- This MVP stage explicitly excludes visual design/color work — validate navigation and interaction structure with Dudaško first, iterate on design after.
- Platform-level features (navigation, cross-project reporting, adoption metrics) and Lexie-level features (its own internal KB/UX behavior) will be treated as explicitly separate concerns going forward, not conflated as "the platform."
- The cross-platform RAG "ask anything" agent concept stays in reserve, not built now — offer only if Dudaško asks for more than the current navigation-based approach.
- Test/prod cost-reporting mechanism (endpoint pull vs. periodic dump to an intermediary) is not finalized — to be resolved as a discrete follow-up topic, not blocking the Friday demo.
- The minor Lexie border/padding design request will be pushed back at tomorrow's status rather than actioned now.
- Dudaško demo targeted for Friday; Jura, Marek, and likely Jindřich will all attend.

## Action Items

- [ ] **Jura Brázdil**: Prepare a simulated end-user account with access to multiple products but no admin/reporting/docs/technical-status rights, for Marek to review the resulting UX — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Jura Brázdil**: Fix the visible-but-empty admin-section gaps for non-admin accounts (reflow layout or add an explicit disabled/tooltip state) — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Jura Brázdil**: Seal the MCP server registration security gap (secret/header leakage to any agent reading server descriptions) before further build-out — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Jura Brázdil**: Finish Chatbot Max bug fixes (today + tomorrow morning) ahead of tomorrow's status meeting — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Jura Brázdil**: Give Jindřich a realistic-constraints summary of the Dr. Max requirements/backlog Excel, ahead of a fuller scoping conversation — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Marek Pillár**: Push back on the minor Lexie border/padding design request at tomorrow's status meeting — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Marek Pillár**: Schedule the Dudaško prototype demo, targeting Friday — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting
- [ ] **Jura Brázdil / Marek Pillár (/ Jindřich Tůma)**: Review the refreshed prototype together the day before the Dudaško demo — from 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting

## Open Questions

- Final UX for test/prod cost-reporting: combined view with a TEST banner, vs. a global environment switcher, vs. something else — not resolved.
- Whether BDC will actually grant read access to Azure cost/permissions data programmatically, or whether this stays a manually maintained list.
- Final tile-grouping/categorization approach once the project count grows well beyond the current ~3 — acknowledged as needed eventually, not designed yet.
- Whether Dr. Max's requirements Excel should be pushed back on line-by-line, or handled as a broader realistic-scoping conversation with Jindřich/Dudaško.

## Sentiment & Tone

Highly collaborative, technical working session — genuine back-and-forth problem-solving rather than a status report, with Marek repeatedly pausing to sanity-check UX implications ("otázka je čo to znamená", "ako by to vyzeralo pre...") rather than accepting Jura's first answer. Jura was visibly energized about the platform architecture work ("brutál pokrok" was Marek's closing assessment, which Jura didn't dispute), while also candid about current limitations (openly flagging the security gap, the fake/mocked cost data, and being fully blocked on DB access). No friction between the two; disagreements (e.g. the test/prod switcher UX) were treated as open design questions to resolve together, not points of conflict.

## Routing Log

Routed on PM confirmation ("confirm both"), 2026-09-24:

- **project-assumptions**: ASM-144 (platform/Lexie separation), ASM-145 (MCP secret-leak security gap), ASM-146 (RAG agent kept in reserve), ASM-147 (design deferred until nav validated), ASM-148 (test/prod cost-reporting undecided)
- **project-stakeholders**: STK-010 (Dudaško), STK-016 (Tvarůžek), STK-026 (Jura, major update)
- **project-knowledge**: "AI platform — current technical state" entry updated with the prototype architecture walkthrough
- **project-daily (2026-09-24)**: 8 action items added; Key Events and Audit Log entries written
- **project-lessons**: LL-055 captured
- **meetings/index.md**: entry added
