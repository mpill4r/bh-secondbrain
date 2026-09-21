---
last_updated: 2026-09-21
type: external
attendees: [Marek Pillár, Jindřich Tůma, Tomáš Dudaško]
recording_link:
---

# Dr. Max AI Platform — Vision Discovery with Tomáš Dudaško

**Date**: 2026-09-21
**Attendees**: Marek Pillár (BigHub, AI Analyst), Jindřich Tůma (BigHub, PM), Tomáš Dudaško (Dr. Max, Head of IT — STK-010)
**Type**: external
**Recording**: N/A
**Previous session**: N/A — first meeting where Dudaško personally walks through his AI Platform vision end-to-end (previously only relayed secondhand via Jan Sovka / Ján Kabát, see 2026-09-08-ai-platform-strategy-history-with-jan-sovka)
**Meeting prep**: [2026-09-17-ai-platform-ux-dudasko-prep.md](../prep/2026-09-17-ai-platform-ux-dudasko-prep.md) — originally prepped for 2026-09-17, appears to have slipped to today (both cover the same UX-diagnosis + phasing purpose)

> **Note on date**: no explicit date was stated in the transcript. 2026-09-21 is inferred from strong contextual match with the PM's own stated week plan (Žižka/Neuman follow-ups "today," Listing KPI Excel, Fakturace doprav doc due Tue/Wed) — please correct if wrong.

> **Note on transcript accuracy**: the diarization/transcription tool renders Tomáš Dudaško's name as "DUDAŠKO Tomáš (DrMax CZE)" throughout, but one line mid-call has Marek address him as "Tomáš Blažko" — treated here as a verbal slip, not a second person; all content attributed to Dudaško (STK-010).

## TL;DR

Tomáš Dudaško laid out his AI Platform vision directly for the first time, in three parts: (1) the platform must behave like a true platform — every AI-consuming tool, chat or not, routes through it so usage/cost (FinOps) is visible; (2) one role-based home screen/directory linking out to every AI tool, including ones with their own frontend; (3) one unified Lexie chat instead of per-department instances, gated by role with a public-document tier. Marek's proposed 3-phase sequencing (UX/access unification → backend token visibility → work through Dudaško's capability-matrix Excel) was agreed. After Dudaško left, Jindřich flagged he's visibly frustrated by past unmet promises and pushed for a fast, visible next step (mockup variants to him by Wednesday); separately Jindřich and Dudaško aligned on splitting the AI adoption campaign into a BigHub-owned comms/awareness track and a Dr. Max-owned training/rollout track (routed through Dr. Max's own training center and "expert group" leads, not BigHub).

## Key Discussion Points

### 1. The platform-as-service vision (Dudaško)

Dudaško opened by explicitly setting aside the reporting website Marek had asked about earlier — "different topic" — and framing his actual ask simply: *"platformu, která funguje jako platforma"* [translated from Czech] — it provides services to other tools rather than being a product itself.

- **FinOps / AI gateway**: everything that consumes AI "mechanically" (not just a chat interface) should route through the platform so usage is visible and controllable — eventually including a GDPR-controls layer ("AI gateway"). Concretely: *"jestli pálíme třeba nějaký tokeny na počet... toho forecastu pro e-commerce, tak by ty tokeny měly bejt vidět v tý platformě"* [translated from Czech]. He gave MaxBuddy as the standing example of the current gap — he doesn't know what MaxBuddy costs in tokens because it doesn't burn them through the platform at all.
- He was explicit that the current platform ("dodaná jako že to bude chat, a tady si můžete dělat chat agenty") has limited value on its own — the value comes when the backend serves other AI agents/tools, not when it's just another chat product.

### 2. Unified, role-based tool directory

Dudaško wants a single entry point that acts as a directory ("rozcestník") to every AI tool Dr. Max has, not just chat-style ones embedded in the platform:
- Tools with their own frontend (e.g. the e-commerce forecast dashboard, the listing/copywriting tool) should get a direct link out from the platform, with a short explanation that it's part of a separate product.
- Today, not knowing a tool's exact URL means he effectively can't reach it — there's no anchor point anywhere.
- Visibility into this directory should be role-based: an IT person sees their Lexie instance and public docs; a pharmacist role never sees an admin-facing switch they shouldn't.

### 3. One unified Lexie, not one per department

Dudaško was firm that per-department Lexie instances (IT, "kasťák"/POS, an upcoming Legal instance) are the wrong direction: *"já bych chtěl mít jednu Lexi, jeden chat, do kterýho podle role a toho, co můžu vidět, dostanu odpovědi"* [translated from Czech]. Some documents (e.g. certain Legal notices) should be marked public and visible to everyone regardless of role; access to the rest should be classified the same way SharePoint already governs his own document access — i.e. inherit existing SharePoint permissions rather than build a parallel access model.

### 4. The capability-matrix Excel

Dudaško characterized his earlier requirements Excel as a "golden grail" checklist (data governance, AI Act, data-interface provisioning, etc.) — the platform this would describe if every item were checked off, not a near-term deliverable. He was clear it's still important ("raz to budeme musieť dosiahnuť" — Marek's own framing, agreed by Dudaško) but explicitly deprioritized behind getting the platform to behave like a platform first: *"Prvně se to musí chovat jako platforma... a v tom okamžiku si můžeme říkat, jak to ještě vylepšíme u dalších capability."*

### 5. Agentic workflow builder (deferred, both sides)

Dudaško raised a longer-term want: a drag-and-drop agent-orchestration builder (configurable per-step models/prompts, an orchestrator) — motivated partly by frustration that this was part of the original pitch for choosing BigHub, before BigHub moved off building it as a product. He referenced an unnamed external tool (MCP servers, agent builder, agent registry, attractive pricing) purely as inspiration, not a literal spec, and volunteered this applies beyond the platform to PRO more broadly ("každej, kdo má... tu dírku, by si udělal rukávy od agenta").

Both Marek and Jindřich pushed this to a future initiative: Marek logged it as "one bullet/one slide" for a future roadmap conversation (tentatively November), explicitly not near-term work. Marek's own read (not yet shared with Dudaško): building this custom is likely the wrong call given how many commercial workflow-orchestration tools already do this cheaply (he named Make and Gumloop as examples) — worth surfacing only if Dudaško wants to formally scope it, since a custom build would be large and expensive.

### 6. Agreed phasing

Marek proposed and Dudaško agreed to: **Phase 1** — unify the UX into one entry point with role-based access and basic cost/usage metrics (the near-term design-brief work already in flight); **Phase 2** — deeper backend/token FinOps integration; **Phase 3** — work through the capability-matrix Excel together, jointly prioritized, likely a separate dedicated session. Dudaško's own framing matched this but stressed the platform-behavior work (Phase 1) is the precondition for the rest, not a parallel track.

### 7. AI adoption campaign — scope split (Jindřich ↔ Dudaško, after Marek's business left)

Jindřich asked whether the platform should also become the home for guides/FAQ/knowledge base content — Dudaško agreed readily ("Ano, klidně. To tam může být taky v nějaké sekci.").

Jindřich then raised his in-progress adoption-campaign draft (previously sent to Dudaško). Dudaško's feedback: broadly fine, but two gaps — (1) it currently has no PR/communications layer around it at all, and (2) beyond Ján Kabát's proposed newsletter, he wants people to have a standing reason to keep visiting the platform itself (guides/FAQ live there), not just be pushed content externally.

This surfaced a scope question Jindřich pressed on: does BigHub's adoption campaign end at "raise awareness" (Part A), or extend to end-to-end ownership of rollout — pharmacist training, hypercare, usage evaluation (Part B)? Jindřich cited a concrete worry: during the MaxBuddy 20-pharmacy pilot, a pharmacist contacted via a Max colleague didn't know whether or how to use it.

Dudaško's answer was unambiguous: **training stays entirely with Dr. Max's own training center** — pharmacist-facing rollout is handled the same way any other Armis feature rollout is handled, by "provoz" (operations) on their own channels/e-learning; BigHub has no role there. For the "is it actually landing" concern, the right contact is not the training center but the relevant **"osmec"** (expert-group lead) — Dr. Max runs standing "expertní skupiny" (expert groups) responsible for consistent network-wide rollout of anything new (Dudaško's example: a new dermocosmetics line gets a dermocosmetics expert group). For MaxBuddy specifically, that person is **"Luca"** — the operational owner with escalation authority and direct access to the training center, i.e. Jindřich's actual point of contact for feedback/evaluation, not the training center itself.

Dudaško separately named "Lukáš Syček" as the person who should already know Dr. Max's expert-group structure end-to-end — see Open Questions; this is a new, third spelling of a name already flagged as ambiguous in `project-stakeholders` (STK-031).

### 8. Standing reporting gap (MaxBuddy)

Dudaško repeated a complaint he says he's raised "for several months": there is no regular, reliable reporting for MaxBuddy to evaluate it against — one report was generated via Claude at some unknown point in the past, with no known owner or cadence since. Jindřich says he saw current reporting last week and committed to sending it over, separately committing that every AI initiative should end with defined KPIs/reporting to assess whether it met its original goals — consistent with the Business Quantification/OKR work already running in parallel (`ai-initiatives-okr-framework.md`).

### 9. Design ownership approach (Marek ↔ Jindřich, after Dudaško left)

Marek's plan: turn this meeting into a written brief ("zadanie") for Jura Brázdil to design against, rather than Marek prescribing a design himself — citing Jura's own stated preference (from a previous round) for a brief over a ready-made design, and wanting to avoid a repeat of Marek producing something Jura then flags as infeasible. Jindřich pushed back partially: a fully open brief risks Jura taking the path of least resistance; some directional steer should be baked into the brief itself. Marek agreed to build that steer into the assignment.

Marek's stated plan for the rest of the week: draft the platform brief today, get it to Jura (timing dependent on Jura's capacity — Marek could not commit an exact date), aiming for Wednesday if possible so Dudaško sees something concrete this week; in parallel, close out already-tracked Listing/Fakturace doprav work (unchanged from `project-daily`, not new here).

## Decisions Made

- Dr. Max AI Platform's core direction is confirmed as "platform-as-a-service": every AI-consuming tool (chat or programmatic) should route through it for usage/cost visibility, not just host chat products.
- Platform home screen becomes a unified, role-based directory to every AI tool — including tools with their own separate frontend, via deep links, not just chat tools embedded natively.
- Per-department Lexie instances are being collapsed into one unified, role-gated Lexie chat, with a public-document tier layered on top; access modeled on existing SharePoint permissions.
- Delivery sequencing agreed: Phase 1 (UX/access unification + basic metrics, already in flight) → Phase 2 (backend FinOps/token integration) → Phase 3 (capability-matrix Excel, jointly prioritized, likely November).
- The agentic-workflow/orchestrator builder idea is explicitly deferred to a future roadmap conversation, not scoped now.
- AI adoption campaign scope: BigHub/Jindřich owns awareness/comms (intranet, PR, platform-hosted guides/FAQ); pharmacist training and hypercare stay entirely with Dr. Max's training center; post-rollout evaluation/escalation routes through the relevant expert-group lead ("osmec"), not through BigHub directly or the training center.
- Marek will produce a written brief for Jura Brázdil (not a ready design) to drive the Phase 1 UX work, with some directional steer included per Jindřich's request.

## Action Items

- [ ] **Marek Pillár**: Draft the AI Platform design brief/assignment for Jura Brázdil, incorporating directional steer per Jindřich's request — today, 2026-09-21 — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] **Marek Pillár**: Share the brief with Jura Brázdil and push for UX variants Dudaško can react to as early as Wednesday 2026-09-23 — exact timing depends on Jura's capacity, not yet confirmed — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] **Marek Pillár / Jindřich Tůma**: By end of this week, prepare a work-in-progress AI Platform spec/roadmap with open questions to show Dudaško — sequencing: design phase (~1 week), admin/role-views phase (~2-3 weeks), agentic-workflow follow-up conversation tentatively November — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] **Jindřich Tůma**: Send Tomáš Dudaško the current MaxBuddy reporting Jindřich saw last week — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] **Jindřich Tůma**: Schedule a follow-up session to properly work through the AI adoption campaign draft/strategy — from 2026-09-21-ai-platform-vision-discovery-dudasko
- [ ] **Jindřich Tůma**: Align with the relevant expert-group lead ("osmec," per Dudaško possibly "Luca" for MaxBuddy) as BigHub's actual contact point for post-rollout adoption feedback, rather than the training center — from 2026-09-21-ai-platform-vision-discovery-dudasko

## Open Questions

- ~~Is "Lukáš Syček" (this call), "Lukáš Sýč" (Vosmek's MaxBuddy IT liaison, STK-031), and "Lukáš Síč" (Jindřich's order-prediction BigHub-side contact) one person or several~~ — **resolved 2026-09-21**: PM confirms correct spelling is "Lukáš Szücs" (see STK-031).
- Who exactly is "Luca," the MaxBuddy "osmec" (expert-group lead) Dudaško named — not yet a tracked stakeholder; unclear if this is the same person as Lukáš Szücs/STK-031 or a distinct role-holder.
- Whether Dudaško's "agentic workflow builder" want should ever be formally scoped as a custom build, or steered toward an existing commercial tool (Marek's untested personal view) — deferred to a future (~November) conversation.
- Exact ETA for the first UX mockup variants — contingent on Jura Brázdil's capacity, not yet confirmed by him directly.

## Sentiment & Tone

Dudaško was direct, occasionally blunt, but substantive and collaborative throughout — corrected Marek's Claude analogy immediately and firmly ("určitě nechci, abyste přepisovali Claude"), but engaged constructively on every topic and agreed cleanly to the proposed phasing without pushback. His MaxBuddy reporting complaint carried real, sustained frustration ("to já to už opakuju několik měsíců... já nevím, kde to jako hnije").

The more significant read came from Jindřich after Dudaško dropped off: he assessed Dudaško as having "the right vision" but being noticeably worn down by past unmet promises from predecessors on this account — explicitly warned Marek against letting a week pass with no visible communication, and pushed for something concrete (even partial, with open questions flagged) by Wednesday rather than waiting for a polished result. This reinforces the existing stakeholder note (STK-010) that Dudaško is "a bit frosty" after months of paying without enough visible delivery — today's call did not resolve that, but gave both sides a concrete, mutually-agreed next step to point to.

## Routing Log

Routed on PM confirmation ("route everything"), 2026-09-21:

- **project-assumptions**: ASM-112 (platform-as-a-service/FinOps), ASM-113 (unified role-based tool directory), ASM-114 (single unified Lexie + public-doc tier), ASM-115 (3-phase delivery sequencing), ASM-116 (agentic workflow builder, deferred), ASM-117 (adoption-campaign scope split), ASM-118 (MaxBuddy reporting gap)
- **project-stakeholders**: STK-010 (Tomáš Dudaško) — vision + sentiment; STK-003 (Jindřich Tůma) — commitments; STK-001 (Marek Pillár) — brief-drafting action; STK-031 (Lukáš Sýč, ambiguous identity) — further name-variant corroboration + new "Luca"/osmec reference
- **project-knowledge**: new entries "Expertní skupiny," "Osmec," "Tréninkové centrum"; updated "AI platforma (new initiative)" entry
- **project-daily (2026-09-21)**: created (did not yet exist); 6 new action items added, carried forward from 2026-09-19's close
- **meetings/index.md**: entry added
