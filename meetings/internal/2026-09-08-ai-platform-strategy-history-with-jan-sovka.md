---
last_updated: 2026-09-08
type: internal
attendees: [Marek Pillár, Jindřich Tůma, Jan Sovka]
tldv_link:
---

# AI Platform Strategy & History Walkthrough with Jan Sovka

**Date**: 2026-09-08
**Attendees**: Marek Pillár (PM), Jindřich Tůma (PM), Jan Sovka (Original consultant / account owner-manager, BigHub — Marek's line manager)
**Type**: internal
**Recording**: N/A (transcript provided directly, no tldv link)
**Previous session**: Related context in 2026-09-04-ai-platform-standup-xmanager-lexi-demo.md, which first surfaced that the AI platform is shared across multiple BigHub clients rather than Dr. Max-exclusive. This meeting goes much deeper into that history and resolves the open question left in today's earlier `project-knowledge` note about whether "AI platforma" is the same platform.
**Meeting prep**: N/A

## TL;DR

Jan Sovka walked Marek and Jindřich through the full history of BigHub's "AI platform": an ~1.5-year-old vision to sell it as a shared, white-labeled B2B product across clients, which never got internal traction and was formally killed ~4 months ago in favor of fully custom per-client builds. This resolves the open question from today's earlier `project-knowledge` entry — the "AI platforma" Tomáš Dudaško wants investment in **is** the same underlying platform/codebase already running Max/Maxie/Lexie for Dr. Max, not a separate new system. Agreed near-term focus: a UX/visual overhaul so all Dr. Max BigHub projects can be consolidated onto it (test + prod), with Jindřich and Marek distilling Dudaško's large requirements Excel into a small, realistic ticket set to validate with Jura Brázdil before bringing a shaped proposal back — rather than answering the Excel's governance-heavy questions line by line.

## Key Discussion Points

### The investment ask (Jindřich Tůma, opening context)

Jindřich relayed a conversation from the previous day with Tomáš Dudaško (STK-010): Dudaško wants visible investment in the AI platform — unifying test/production environments, improving the visual polish/UX for client-facing use, and consolidating all BigHub-delivered Dr. Max projects onto it. During that conversation Dudaško also showed Jindřich a large requirements Excel ("Honza's Excel") that Jindřich had not seen before; they agreed to forward it to Marek, review it with Tomáš Dudaško, and extract real priorities from it.

### Platform origin story (Jan Sovka)

Jan gave the full backstory, unprompted, to make sure Marek and Jindřich had the context before going further:

- ~1.5 years ago, BigHub's internal strategy was to build a single unified AI platform as a "passive revenue" B2B product — one core, white-labeled and wrapped per client. It was sold to clients (including Dr. Max) on that premise: a shared roadmap, common feature releases, unified administration and cost reporting, and a mix of user-facing outputs (e.g. Lexie-style knowledge assistants) and invisible ones (APIs other systems consume).
- **It never actually got internal traction or investment** — no team was ever properly resourced to build it as a real product — and the concept was effectively killed in an internal management evaluation **~4 months ago** (i.e. ~2026-05).
- Current internal direction: build fully custom solutions per client, optionally inspired by each other's code, with no shared product roadmap. Jan noted this is increasingly happening via AI-assisted ("vibe coding") builds — citing a colleague (name unclear in transcript, phonetically "Tomáš Fokus") building a similar platform for Unica this way.
- **Jan Sovka: "I'm not saying it's a decision I'm happy with, but that's just where things personally landed for me. That's simply how it is."** [translated from Czech]
- The underlying codebase today is deployed across **Dr. Max, Brněnská komunikace (Brno communications), Kooperativa, and Unica** (heavily modified). The Kooperativa deployment in particular is built almost entirely around Kooperativa-specific needs (integrates with something Jan referred to as "XLET" — term unclear/unconfirmed in transcript) — **Jan flagged this as a sensitivity: if the platform is demoed to Dr. Max, care is needed that Kooperativa-specific traces aren't visible/recognizable.**
- Following the internal decision to drop the shared-product concept, Ján Kabát (STK-005) went back to Dudaško and told him there would be no shared roadmap going forward. Dudaško's response was to ask what he specifically wants the platform to do for Dr. Max — and he then sat down and worked through requirements with an AI assistant, producing the large Excel now in circulation.

### What the platform already supports today (Jan Sovka)

In response to Marek's initial read that this seemed like a fairly small/simple product to build: Jan pushed back, noting the codebase represents **~2 years of development** inherited/adapted from the Kooperativa build — custom agent definition, custom RAG, SharePoint integration, Warehouse integration, and more. He conceded that Azure AI Foundry has since caught up on a lot of this ground, so a from-scratch build today would likely cost less — but this is the existing, already-built asset.

Specific capabilities confirmed already live in both test and production across the client base:
- **Role-based permission system** — granular per-agent / per-department, e.g. a CC-department user can only converse with an agent, while other tiers get reporting or admin access.
- **Entra ID integration** for permissioning (no separate access management needed).
- Existing (if less granular) spend/cost-management reporting.

**Jan Sovka: "For me this has personally been a painful point, but I already treat it as a closed chapter, and I'll be glad you're adding something new to it."** [translated from Czech]

### What Dudaško actually wants near-term (Jindřich Tůma, clarifying)

Jindřich corrected an assumption Marek raised (that this was about default-prompting/config for individual chatbots) — Dudaško's stated near-term interest is **dependency visibility, cost visibility, and usage metrics** (how many people are using each initiative) that could double as future business-case/ROI ammunition, not primarily the governance/compliance minutiae the Excel implies.

### Requirements Excel — shared quality concern (Marek Pillár, Jan Sovka)

Marek flagged that the Excel reads as uncontrolled/auto-generated and said he'd want to actually sit with Dudaško on it rather than take it at face value. Jan independently corroborated this: **roughly 70% of the Excel is governance/compliance content, written from an IT-leadership perspective**, asking BigHub to state as-is capability against a long list of IT/compliance concerns — and it says nothing about which actual use cases should run on the platform, which Jan considers the critical missing piece (a "universal platform" can't be designed without knowing what it needs to support). Jan said this is why the Excel hasn't moved since it was created, and that the current internal agreement is to focus on the individual product cases first and let them gradually consolidate onto the platform (~1 month timeframe estimated) — which naturally resolves permissions and spend visibility without an upfront platform build.

Jan noted the Excel's content is AI-generated but that he has personally reviewed and stands behind everything in it.

### Path forward agreed

- Marek proposed treating the AI platform as a real, formal project with Dudaško as owner/sponsor, and running a standard prioritization/Discovery session with him rather than answering the Excel's questions line by line.
- Marek's own early scoping read: this doesn't look like an especially complex build from a UI standpoint — near-term needs look like UX/visual polish (described as a low-cost, high-goodwill move), a kill-switch, a role-based dashboard, and cross-project/cross-role/cross-LLM visibility. Jan partially pushed back given the platform's actual depth (see above), but didn't disagree that UX-focused near-term investment is the right first move.
- Jindřich confirmed the immediate goal is redoing the platform's UX so all BigHub-delivered Dr. Max projects can be logically added to it, on both test and production simultaneously — the first concrete milestone.
- Rather than answering the Excel directly, Jindřich and Marek will read it, distill it into a small, realistic ticket set (Jindřich estimated **"3, 4, 5 tickets"** as a starting slice), sit with Jura Brázdil to validate feasibility and timing, and then bring a shaped proposal back to Dudaško.

### Resourcing risk flagged (Jindřich Tůma)

Today only 2-3 people work the individual product cases — nobody is dedicated to platform work itself. The likely owner is Jura Brázdil, currently allocated roughly **0.25 FTE** to something not specified in the transcript; taking on platform work would likely require moving him to full FTE, which affects billed hours. Jindřich said he'll need to explain this cost impact to Dudaško proactively so it isn't a surprise later.

### Ján Kabát alignment needed (Jan Sovka)

Jan recommended Jindřich and Marek sync with Ján Kabát (STK-005) before going further with Dudaško — Kabát was the one who originally delivered the "no shared roadmap" message and has been shaping how Dudaško frames this ask. Jan's concern is avoiding conflicting messaging between BigHub people talking to the same client contact.

### Marek's availability (logistics)

Marek shared that there has been a death in the family and he will need to travel to Slovakia today after work, with reduced/uncertain availability from tomorrow through early next week (possibly a partial or full day of PTO). He confirmed he'll continue working remotely where possible (including on the roadmap prototype) but flagged that any pre-scheduled slots — specifically mentioned one involving a contact referred to only as "Bohrem" (name unclear/unconfirmed in transcript) — may need to be worked around. Jan Sovka confirmed standard process: put time off in the shared calendar (visible to everyone, auto-respected), and use the Vacation Tracker for anything longer than one day.

## Decisions Made

1. **"AI platforma" is confirmed to be the same shared BigHub platform/codebase** already powering Max/Maxie/Lexie for Dr. Max (and also deployed for Brněnská komunikace, Kooperativa, and Unica) — not a separate, new system. This resolves the open question in today's earlier `project-knowledge` entry.
2. BigHub's platform strategy going forward is fully custom-per-client; the earlier shared-roadmap / white-labeled B2B-product vision is retired, killed internally ~4 months ago (~2026-05).
3. Near-term platform investment is scoped to a **UX/visual redesign** enabling all Dr. Max BigHub projects to be added to the platform on both test and production — the agreed first milestone.
4. Rather than answering Dudaško's Excel line-by-line, Jindřich and Marek will distill it into a small (~3-5) realistic ticket set, validate feasibility/timing with Jura Brázdil, then bring a shaped proposal back to Dudaško.
5. Marek will treat the AI platform as a formal project with Dudaško as owner/sponsor, running a standard prioritization/Discovery session rather than a reactive Excel response.

## Open Questions

- Jura Brázdil's allocation for platform work — currently ~0.25 FTE on an unspecified other stream; may need to move to full FTE. Cost/hours impact to Dudaško still needs to be explained.
- Exact scope and timing of the Jindřich/Marek ↔ Ján Kabát alignment sync (recommended but not yet scheduled).
- Identity of "Tomáš Fokus" (phonetic, unconfirmed) building a similar Vibe-coded platform for Unica — not a Dr. Max contact, flagged only as internal color.
- Identity/context of "Bohrem" (phonetic, unconfirmed) — a contact Marek wants to avoid scheduling conflicts with during his reduced availability.

## Sentiment & Tone

Candid, slightly weary internal debrief. Jan Sovka was unusually open that the platform's product strategy has been a personal "painful point" for him, but he's made peace with it as a closed chapter and seemed genuinely glad to see fresh investment happening. No friction between the three — Marek's early skepticism about the requirements Excel's quality was independently corroborated by Jan rather than pushed back on. The mood shifted briefly at the end when Marek shared the family bereavement; both Jindřich and Jan responded supportively and without any pressure.

## Action Items

- [ ] **Jan Sovka**: Send Marek and Jindřich the platform history/background materials referenced during the call — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] **Jindřich Tůma / Marek Pillár**: Read through Dudaško's requirements Excel for awareness of where it's heading — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] **Jindřich Tůma / Marek Pillár**: Distill the Excel into a small, realistic ticket set (~3-5 tickets) as a starting slice — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] **Jindřich Tůma / Marek Pillár**: Sit with Jura Brázdil to validate feasibility and timing of the distilled tickets — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] **Jindřich Tůma**: Bring the shaped ticket proposal back to Tomáš Dudaško — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] **Jindřich Tůma**: Resolve Jura Brázdil's allocation for platform work and explain the resulting cost/hours impact to Tomáš Dudaško — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka
- [ ] **Jindřich Tůma / Marek Pillár**: Sync with Ján Kabát before further platform conversations with Dudaško, to avoid conflicting messaging — from 2026-09-08-ai-platform-strategy-history-with-jan-sovka

## Routing Log

Confirmed 2026-09-08 (combined with 2026-09-08-ai-platform-technical-deepdive-jura-brazdil). Written:
- **project-knowledge**: rewrote "AI platforma (new initiative)"; added "BigHub's shared-platform strategy (retired)"
- **project-assumptions**: ASM-038 (custom-per-client strategy), ASM-039 (3-phase plan), ASM-040 (distill Excel into tickets), ASM-041 (formal project framing), ASM-043 (BigHub feedback-loop framing, open)
- **project-stakeholders**: enriched STK-002 (Jan Sovka), STK-005 (Ján Kabát), STK-010 (Tomáš Dudaško)
- **project-daily** (2026-09-08): 7 action items written (1 marked done same-day)
