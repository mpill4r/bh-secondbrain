---
last_updated: 2026-09-22
type: internal
attendees: [Marek Pillár, Jindřich Tůma]
recording_link:
---

# AI Portfolio Business-Value Review & Reklamace Digitization Reframe

**Date**: 2026-09-22
**Attendees**: Marek Pillár (PM), Jindřich Tůma (BigHub, client-side coordination)
**Type**: internal
**Recording**: N/A
**Previous session**: N/A (new thread)
**Meeting prep**: N/A

## TL;DR

Jindřich reframed Reklamace's real value driver to Dudaško as digitization/data-consolidation rather than AI — a decision on continuing or closing the project now awaits a Dudaško + head-of-logistics alignment meeting. Marek walked Jindřich through a consolidated Business Quantification tracker across all initiatives with concrete annual CZK figures — most notably Petr Neuman finally giving hard Listing numbers (~34M CZK/year) that supersede his earlier declined-to-commit placeholder — and a portfolio priority ranking emerged by dollar value (MaxBuddy ~81M > Listing ~34M > Max/Maxie ~13-14M), though Marek pushed back that Listing should stay top priority regardless, per Honza/Alana/Neuman's consistent view. A combined session with Dudaško (reklamace decision + full priority review) is being scheduled for Thursday or Friday this week.

## Key Discussion Points

### Reklamace reframed as digitization, not AI

Jindřich told Dudaško directly that Reklamace's real efficiency gain has turned out to be digitization and data consolidation, not AI — the knowledge base underlying it isn't robust enough to support meaningful AI features beyond "drobotina" (minor add-ons, e.g. historical email-status summarization). This holds for the current phase and all planned future phases, since the same digitization flow will just be reapplied to different complaint types. Dudaško is "trochu šlape" (pushing back a bit) on this framing and wants to align with the head of logistics on next steps — Jindřich reads two live options: continue as a digitization-only project, or close it. Jindřich is scheduling that alignment meeting, bringing in Jan Sovka for historical context ("why certain things were originally intended — neither of us knows"), and will loop Marek into every future session on this thread so Marek can build context from scratch, as if it were a new project.

Marek noted he already had a similar read reflected in his own tracker, and flagged Phase 1.1 is the only phase currently confirmed in motion, with 4 further phases behind it whose future now looks uncertain given this reframe.

### Consolidated Business Quantification tracker walkthrough

Marek merged Jindřich's separate "Ideas" and "Active" sheets into one expanded tracker (state columns: Deployed → In Phase → Idea/Prioritized/Development, per Jan Žižka's requested phase split; ~54 backlog ideas below the active initiatives, including a new one from Šimoník). For each active initiative he re-derived JTBD-style goals, cost figures (per-mandate, per-hour, or per-month depending on what stakeholders gave), and a business-value figure with a documented calculation trail (250 working days/year basis for CZ).

Headline annual figures discussed (all Kč):
- **Reklamace**: ~400–700k (uncertain range as discussed live; excluded from the >1M filter below)
- **Fakturace doprava**: ~780k (25% reduction)
- **MaxBuddy**: ~81M — 60% of expedition cases, 75% MaxBuddy coverage, 1.2% conversion (~540 units/year) — largely predictive/preventive value ("nothing goes wrong") rather than realized savings
- **Max chatbot + Maxie (voicebot)**: ~13–14M — from Mertová's illustrative calc of 20 extra 24/7 agents avoided (260 Kč/hr × 20 → ~13M/year); **Mertová explicitly refuses to have this treated as an accepted FTE-based business case** — "the number is purely illustrative per the given methodology, not an accepted business case," her stated reason being to avoid her operator headcount being cut on the back of it
- **Lexie**: ~1.2M — 30 min/day saved × 23–28 operators; same non-FTE caveat from Mertová applies
- **Listing**: ~34M — see below, a major update
- **TEO/OCR (servisní protokoly)**: ~273k — analyst time per document down from ~10 to ~3 minutes (~5 mandays/month saved on a 6,500-manday analyst base), auto-import rate up to 80% without manual intervention

**Listing — Petr Neuman finally committed to hard numbers.** Where he previously declined to give a KPI figure (see [[ASM-075]]), he now has a concrete report: +1 percentage point conversion per optimized listing (better SEO/discoverability/filtering), quarterly throughput rising from 6,000 to 8,000–10,000 processed items, and cost-per-item dropping from 200 Kč to 100 Kč (automation lets one worker do 2 items/hour instead of ~1.3). Combined, these three effects total ~34M Kč/year. Jindřich initially didn't follow how "conversion" applied to a content-authoring tool; Marek clarified it's driven by better SEO/discoverability on the optimized listings themselves, distinct from the throughput and per-item-cost effects.

### Priority ranking tension — dollar value vs. stakeholder consensus

Filtering to initiatives above 1M Kč/year, Jindřich read off a priority order by dollar value: **MaxBuddy full 600-pharmacy rollout is must-have (biggest figure by far)**, then Max chatbot/Maxie, then Listing. Marek pushed back: Listing has been the consistent top-priority ask from Honza (Sovka), Alana (Sihelská), and Neuman himself, independent of this quarter's modeled dollar figure — his argument being that at Dr. Max's ~10,000-SKU, multi-billion-Kč revenue scale, even a 1% optimization on any item compounds into very large money that this particular model doesn't fully capture. This tension was raised but not resolved in the meeting — see Open Questions.

### MaxBuddy backlog readiness

Jindřich relayed (uncertain of the original source — possibly "Rubeš", possibly conflated with another conversation) that Luboš Vosmek (STK-011) is ready to fill and plan MaxBuddy's backlog. Jindřich asked Marek to schedule a meeting with Vosmek this week if possible, leaving the exact approach to filling the backlog to Marek's judgment, with the goal of eventually getting it into Azure DevOps.

### Combined Dudaško session

Jindřich wants to merge two threads into one Dudaško meeting: presenting the reklamace continue-or-close decision, and walking him through the full portfolio priority ranking (dollar figures and all — deliberately not pre-empting whether Dudaško will want development-cost figures added alongside the value figures; that's left for him to ask). Targeting Thursday 2026-09-24 or Friday 2026-09-25 this week; Marek is free either day except tomorrow (2026-09-23, already committed to the Filip/fakturace check and Dudaško prototype work). Jindřich leans toward Friday, since Thursday already has the recurring CC status sync where they'll make one more push for Mertová's missing precise numbers — hoping to have everything finalized by Friday.

### Honza Kabát's Microsoft/Azure backlog request

Marek flagged that Ján "Honza" Kabát (STK-005) asked him directly for a full list of everything in the backlog/pipeline — including effort and expected Azure spend — for Microsoft partnership costing purposes. Marek shared the existing rough backlog but was explicit it isn't cost-planned. Jindřich considers this premature ("trošku overkill") — BigHub isn't pushing the wider backlog yet; that's "part B" once the current confirmed initiatives are locked in with their owners and Dudaško gives his sign-off (expected Friday). Jindřich will coordinate directly with Kabát on how to proceed and loop the Friday meeting in.

### Fireflies workspace access

Jindřich wants his own Fireflies access — both to record his own meetings that Marek doesn't attend, and because Marek's meetings benefit him too. Discussed mechanics: joining the same BigHub workspace Marek uses means Marek would see all of Jindřich's recordings by default (as currently configured, transparency by design) regardless of being invited to those meetings; a separate, self-paid account would keep it fully separate but Jindřich would then only see meetings he's explicitly invited to. Jindřich will think it through and follow up with a preferred approach.

## Decisions Made

- Reklamace's real value driver is being reframed internally and to Dudaško as digitization/data consolidation, not AI — future direction (continue as digitization-only vs. close) is pending a Dudaško + head-of-logistics alignment meeting.
- Petr Neuman's Listing KPI figures are now committed and concrete (superseding the earlier declined-to-commit placeholder) — ~34M Kč/year combined value.
- Max chatbot/Maxie/Lexie business-value figures from Mertová stay explicitly illustrative-only per her own request, never to be presented as an accepted FTE-based business case.
- A combined Dudaško meeting (reklamace decision + full portfolio priority review) will be scheduled for this Thursday or Friday, leaning Friday.
- Honza Kabát's Microsoft/Azure backlog-costing request is deprioritized until after Dudaško's priority sign-off.

## Action Items

- [ ] **Marek Pillár**: Follow up with Simona Mertová for the missing average monthly request-volume figures needed to complete the Max chatbot/Maxie/Lexie KPI methodology (today/tomorrow, reminder again at Thursday's CC status sync) — due before Friday — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] **Marek Pillár / Jindřich Tůma**: Hold the combined Dudaško meeting (reklamace continue-or-close decision + full portfolio priority review) — targeting Friday 2026-09-25 (Thursday 2026-09-24 as alternative), contingent on Mertová's numbers landing in time — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] **Jindřich Tůma**: Schedule the Reklamace alignment meeting with Tomáš Dudaško and the head of logistics (plus Jan Sovka for historical context); include Marek on this and all future reklamace-thread meetings — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] **Marek Pillár**: Schedule a MaxBuddy backlog-planning meeting with Luboš Vosmek this week, if it fits his calendar — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] **Jindřich Tůma**: Coordinate with Honza Kabát on the Microsoft/Azure backlog-costing request and next steps, looping in Friday's Dudaško outcome — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe
- [ ] **Jindřich Tůma**: Decide how to get his own Fireflies workspace access (join Marek's shared workspace vs. separate paid account) and confirm the approach with Marek — from 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe

## Open Questions

- Whether Reklamace continues as a digitization-only project or is closed outright — pending the Dudaško + head-of-logistics alignment meeting.
- Portfolio priority ranking: Jindřich's dollar-value read puts MaxBuddy first, Listing third; Marek (and Honza/Alana/Neuman previously) maintain Listing should be top priority regardless — not resolved in this meeting, likely surfaces again at Friday's Dudaško session.
- Whether Dudaško will want development-cost figures added alongside the business-value figures once he sees the priority review — deliberately not pre-empted.
- Who exactly said Vosmek is ready to plan the MaxBuddy backlog — Jindřich named "Rubeš" but was visibly unsure, possibly conflating two separate conversations.
- Whether Mertová will actually provide a real (non-illustrative) average request-volume figure in time for Friday, given her repeated reluctance to let CC numbers be used as an FTE-savings case.

## Sentiment & Tone

Warm, efficient working session between two people who've built real shorthand — fast Czech/Slovak code-switching throughout, several light asides (a Fireflies logistics tangent, a "kde to hnije" turn of phrase from Marek). Jindřich was visibly impressed by the consolidated tracker ("moc hezky udělaný," "je to krásně jako rozpitovaný") and engaged substantively with the numbers rather than rubber-stamping them — caught himself misattributing the KPI methodology to the wrong initiative twice (Max vs. Maxie) and corrected in real time, and pushed twice for methodological rigor (splitting Mertová's illustrative figure from a harder measured-volume KPI; questioning how "conversion" applies to a listing tool). The one substantive disagreement — priority ranking by dollar value vs. Listing's qualitative priority — was raised without friction and explicitly deferred rather than argued out, consistent with this pair's working style throughout the account so far.

## Routing Log

Routed on PM confirmation ("confirm all"), 2026-09-22:

- **project-assumptions**: ASM-122 (Reklamace reframed as digitization, not AI), ASM-123 (Petr Neuman's committed Listing figures — supersedes ASM-075), ASM-124 (Max/Maxie/Lexie business-value methodology — measured-volume KPI added alongside Mertová's illustrative figures), ASM-125 (portfolio priority-ranking tension), ASM-126 (Honza Kabát's Microsoft/Azure backlog request deprioritized); updated ASM-075 (marked superseded by ASM-123) and ASM-006 (further corroboration on Fakturace doprava naming/ownership, point 1)
- **project-stakeholders**: STK-003 (Jindřich Tůma — new commitments), STK-005 (Ján Kabát — Microsoft/Azure ask), STK-010 (Tomáš Dudaško — reklamace pushback, relayed), STK-011 (Luboš Vosmek — backlog readiness), STK-017 (Simona Mertová — illustrative-only stance reinforced), STK-023 (Petr Neuman — committed Listing figures)
- **project-knowledge**: new entry "Business Quantification tracker" under Project Conventions
- **project-daily (2026-09-22)**: 6 action items added; Key Events and Audit Log entries written
- **meetings/index.md**: entry added
- **product-brief**: flagged as a possible candidate (reklamace AI→digitization reframe, dollar-value portfolio prioritization) but not written — PM's "confirm all" was read against the concrete drafted candidates above; this one was posed as an open question rather than a drafted candidate. Revisit if wanted.
