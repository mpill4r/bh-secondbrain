---
last_updated: 2026-09-02
type: internal
attendees: [Marek Pillár, Jindřich Tůma]
tldv_link:
---

# Roadmap Tracking & Listing Onboarding Sync with Jindřich Tůma

**Date**: 2026-09-02
**Attendees**: Marek Pillár (AI Analyst), Jindřich Tůma (Project Manager / AI Manager — BigHub↔Dr. Max coordination lead)
**Type**: internal
**Recording**: N/A
**Previous session**: [2026-09-01-jindrich-marek-introduction.md](2026-09-01-jindrich-marek-introduction.md)
**Meeting prep**: N/A

## TL;DR

Marek presented a first-pass roadmap view (built on a tool called VHT.org.sk, sourced from Jindřich's Excel) breaking the ~9 Dr. Max streams down by department/area; Jindřich validated the direction but pushed to simplify the business-facing columns to Ideas/Active only (dropping Task/TaskGant/Gantt as dev-only detail to be tracked separately in Easy Project or similar) and proposed a VBS (work-breakdown-structure) framework for the underlying detail. Listing onboarding remains stalled — no champion introduction has happened yet — but Jindřich committed to personally introducing Marek to both listing developers and to Tomáš Dudaško once scheduling lands, likely this week.

## Progress Since Previous Session

Of the six action items from the 2026-09-01 introduction meeting: **Jindřich sharing the roadmap Excel** is now clearly done — Marek used it as the direct source for today's roadmap draft. **Marek populating a project overview** also progressed — today's roadmap tool is that work in visible form. The remaining items are still open and resurfaced today: **Honza Sovka/Kabát introducing Marek to the client team** (champion contact for Listing) is still not scheduled — Jindřich messaged Honza Kabát mid-meeting and is waiting on a reply; **documenting the Majenta ↔ e-shop source-of-truth problem** was not discussed today; **sharing past Discovery-session recordings** was not discussed today. Marek explicitly flagged that Listing discovery is now his top blocker — he has no substantive input beyond scrolling a chat channel Filip Černý pointed him to.

## Key Discussion Points

### Roadmap visualization approach

Marek shared two artifacts built off Jindřich's Excel: a rough Excel-based cut, and a cleaner tool (VHT.org.sk) presenting a department/operations-style breakdown with responsibility split between Dr. Max and BigHub. Jindřich confirmed the direction is "absolutely correct" for a business-facing view — the department/area split is right — but flagged a constraint: whatever they land on needs to be publishable somewhere Tomáš Dudaško and team can see it, so the tooling choice matters. Jindřich is separately checking whether their existing tool, **Easy Project**, can already generate this kind of roadmap view from the WBS he needs to maintain anyway for time tracking and estimation — he'll report back, possibly as soon as tomorrow, and they'll then decide which base to build on to minimize ongoing team effort.

### VBS / work-breakdown-structure framework

Jindřich introduced **VBS** (a project work-breakdown-structure framework he favors) as the mechanism for the detailed layer beneath the business roadmap: a tree breakdown of a project (e.g. "infrastructure" → "Azure setup," "Azure access," "licensing"). He wants to hold that structure at multiple granularities — coarse for the business roadmap timeline (e.g. "infrastructure — 14 days," no ticket-level detail needed), and fine-grained for actual estimation and time tracking against individual tickets.

### Column/field trim for the business-facing sheet

Reviewing Marek's sheet live, Jindřich proposed cutting **Task**, **TaskGant**, and **Gantt** entirely from the business-facing view — those are internal dev/delivery detail that belongs in a proper system (Easy Project or similar), not in an Excel the business also sees. He'd keep only **Ideas** and **Active**:
- **Ideas** = the full list of every AI initiative ever conceived at Dr. Max, each with a business owner, a short description, a category, and both estimated and (once known) real cost.
- **Active** = the subset currently being worked, described by project name, business owner, description, an estimation/pricing slot (approach still tbd), and status.

He also proposed dropping the existing **Stage** field (Proof of Concept / Pilot / Solution) and **Priority** score as currently defined — calling Priority in its current form essentially meaningless (*"to je takový to, když nevíš, co dáte"* [translated from Czech: "that's the kind of thing you put when you don't know what else to put"]) — in favor of a much simpler status-only view: business only needs to know what phase a project is in, not a detailed internal breakdown.

### Roadmap ownership and cadence

Jindřich asked Marek to own the "Ideas/Active" sheet going forward — Marek offered to keep it as a running backlog in his head/tooling and pull it out when there's room for a business conversation (e.g. an upsell discussion with Dudaško), rather than actively maintaining it as a shared live artifact for now. Separately, Jindřich wants one additional top-level roadmap line summarizing that Dr. Max is running across nine streams overall, without needing per-stream detail at that level.

### Spec structure follow-through

Building on the Spec 1/Spec 2 structure agreed on 2026-09-01, Jindřich elaborated on why specs matter as a delivery-protection mechanism: without a written, business-signed-off description of exactly what will be built and how it will look, requirement creep is inevitable (*"tady se to děje, jako protahuje se to, protože ty požadavky jsou furt"* [translated from Czech: "this is what happens — it drags on, because the requests never stop"]). He wants specs to include an explicit "hypothesis + acceptance criteria" section — description of the problem, description of the solution, and a lightweight acceptance framing the business owner signs off on before build starts, so scope disputes ("the button should have been pink") have a clear reference point. Marek connected this to what he saw in Juraj Kmec's Azure repo documentation earlier today, which already has strong doc practices worth learning from.

### Listing onboarding — still blocked

Marek has made no progress on Listing discovery beyond what he already had; Filip Černý pointed him only to a chat channel to scroll through. He asked directly who he should approach for a listing-focused workshop. Jindřich acknowledged Dr. Max business owners generally aren't yet treating their initiatives as "owned" — BigHub has to play pioneer here — but confirmed **Petr Neuman** ("pan Neumann") and a second person are the listing business owners and are receptive when approached directly. Jindřich doesn't yet know when Marek will be formally introduced to Tomáš Dudaško (pinged Honza Kabát live during the call, no reply yet) but committed to personally walking Marek over to introduce him to the two listing developers directly once that happens, likely as early as this week (Marek confirmed general availability through end of week, with 2026-09-21 to 2026-09-28 blocked for Slovakia).

### Working rhythm and team structure

Marek raised wanting clarity on internal vs. external meeting structure and BigHub developer relationships, and floated a regular sync between him and Jindřich (not necessarily attending every developer stand-up). Jindřich said this is currently still under outgoing PM Alana's cadence during handover and didn't want to disrupt that in his first week, but is open to establishing clearer internal/external meeting days and a lightweight ~15-minute stand-up once things settle. Both agreed in-person visits to the client site should be batched into single days rather than one-offs, and that remote work is fine day-to-day as long as check-ins happen and in-person presence is used deliberately for higher-stakes moments (upsells, presenting numbers). Marek also proposed moving the shared tracking artifact into Notion instead of ad hoc HTML/Excel; Jindřich agreed.

## Decisions Made

- Business-facing roadmap sheet will drop Task/TaskGant/Gantt columns entirely; those live in a separate dev-facing system (Easy Project or equivalent) using a VBS breakdown.
- Business-facing sheet keeps only Ideas (full initiative backlog) and Active (currently worked projects) tabs, each simplified to: project name, business owner, description, cost estimate, status — Stage and the current Priority score are dropped as not business-meaningful in their current form.
- Marek owns the Ideas/Active roadmap content going forward, held as a backlog rather than a constantly-maintained live artifact, surfaced when there's a business conversation opportunity with Dudaško.
- Spec documents (Spec 1 → Spec 2 per the 2026-09-01 agreement) will include an explicit hypothesis + acceptance-criteria section that the business owner signs off on before build starts.
- Client visits will be batched into single days rather than scattered; day-to-day remote work is fine as long as check-ins happen.
- Shared tracking artifact will move into Notion.

## Action Items

- [ ] **Jindřich Tůma**: Confirm whether Easy Project can natively generate the needed roadmap/WBS view, and report back — from roadmap-tracking-and-listing-onboarding-sync
- [ ] **Jindřich Tůma**: Follow up with Honza Kabát on scheduling Marek's introduction to Tomáš Dudaško — from roadmap-tracking-and-listing-onboarding-sync
- [ ] **Jindřich Tůma**: Once introductions are scheduled, personally introduce Marek to the two listing business owners/developers on-site — from roadmap-tracking-and-listing-onboarding-sync
- [ ] **Marek Pillár**: Move the shared roadmap/tracking artifact into Notion — from roadmap-tracking-and-listing-onboarding-sync
- [ ] **Marek Pillár / Jindřich Tůma**: Establish a lightweight regular internal sync cadence (stand-up or similar) once handover from Alana settles — from roadmap-tracking-and-listing-onboarding-sync

## Open Questions

- Can Easy Project already produce the roadmap/timeline view they need, avoiding a second parallel tool?
- Who is the second Listing business owner alongside Petr Neuman ("pan Neumann")?
- When will Marek actually be introduced to Tomáš Dudaško — still unscheduled as of this call?

## Sentiment & Tone

Constructive and low-friction — Jindřich was explicit that nothing needs to arrive as a finished solution ("you don't need to come with a ready answer") and repeatedly validated Marek's instincts before refining them. Some visible frustration from Marek surfaced about being stuck on Listing with no clear path forward, but it read as problem-solving energy rather than complaint, and Jindřich responded with concrete ownership ("that's on me") rather than deflection. Genuine peer dynamic — Jindřich treats Marek as equally senior and trusts him to self-manage rather than prescribing a rigid onboarding path.

## Routing Log

- **project-stakeholders**: Enriched STK-003 (Jindřich Tůma — VBS proposal, roadmap decision, spec approach), STK-023 (Petr Neuman — second listing owner noted), STK-019 (Marek Šimoník — dashboard trial period).
- **project-assumptions**: Added ASM-008 (Decided) — roadmap sheet trimmed to Ideas/Active; ASM-009 (Decided) — specs require business-signed hypothesis + acceptance criteria.
- **project-knowledge**: Added VBS work-breakdown-structure framework to Project Conventions.
- **project-daily**: Added 5 action items (Jindřich: Easy Project check, Dudaško intro follow-up, listing dev intro; Marek: Notion migration, sync cadence).
