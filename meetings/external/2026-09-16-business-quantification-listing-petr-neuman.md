---
last_updated: 2026-09-16
type: external
attendees: [Marek Pillár, Petr Neuman]
tldv_link:
---

# Business Quantification / Discovery Kickoff Call with Petr Neuman — Listing

**Date**: 2026-09-16
**Attendees**: Marek Pillár (BigHub, running the interview), Petr Neuman (Dr. Max — Listing business owner)
**Type**: external
**Recording**: N/A (docx transcript export via fireflies.ai, no separate recording link provided)
**Previous session**: N/A — first direct meeting between Marek and Petr Neuman. Related prior context: [2026-09-01-dr-max-listing-introduction](../internal/2026-09-01-dr-max-listing-introduction.md) (Filip Černý's handoff briefing to Marek), [2026-09-02-logistics-listing-team-sync](../internal/2026-09-02-logistics-listing-team-sync.md) (Discovery agreed as the path forward — see [[ASM-011]])
**Meeting prep**: N/A

## TL;DR

First live 1:1 between Marek and Petr Neuman (Listing's business owner) — part Business Quantification interview, part relationship-building ahead of a formal Discovery phase. Neuman gave a well-grounded JTBD origin story and real quarter-over-quarter Fermi data (Q1 → Q2 2026: ~3,600 → ~6,000 listing items processed, ~230 Kč → ~130 Kč per item), but the framing of the initiative's primary driver shifted mid-call: the original "poor supplier data quality" problem is now secondary to Magento's growing instability, which he wants the tool to solve by getting the listing team out of Magento for day-to-day work entirely. No final KPI was committed. Michaela Vdovicynová was nominated as the practical domain-expert/testing contact.

## Key Discussion Points

### Rapport and framing

Informal opening — Neuman (introduced as "Neumann" in prior notes, confirmed here to prefer being addressed as "Petr") offered to go by first names. Marek explained the purpose: BigHub is compiling a corporate KPI Excel across all Dr. Max AI initiatives for Tomáš Dudaško, and explicitly normalized uncertainty upfront — "you don't need to know it off the top of your head, if you don't know something now, just say so and I'll send the sheet over" — before starting the JTBD questions.

### Objective (JTBD) — origin story

Neuman started addressing the listing problem when he joined his current role at the start of 2026 and began discovering how the team actually worked; he's confident the underlying problem "should have been solved years ago." He identified two related but distinct frustrations:

- **Original driver**: supplier-submitted product data arrives low-quality — often just the basic logistics fields (product name, category, a short description) with none of the ~15 target parameters needed for filtering/discoverability. The listing team ("holky") would read a short supplier description and guess at classification (e.g. "probably a face product, probably for women"), typically filling only ~2 of 15 desired parameters.
- **Current, now more urgent driver**: Magento itself is becoming unstable at Dr. Max's scale — "**it's currently around 80,000 SKUs, maybe 100,000 in the Czech Republic — frankly, it just doesn't run on [Magento] anymore**" [translated from Czech]. The team works product-by-product directly inside Magento (no batch Excel-import workflow exists today), and saves routinely take ~30 seconds and then fail with an error, discarding the completed work and forcing a redo. Neuman was explicit that this — not the original data-quality problem — is now his primary reason for wanting the tool: "**if we'd had this yesterday, I'd be thrilled — and yesterday was already late for me**" [translated from Czech].

An additional near-term complication: Magento is removing parametric grouping (today only the ~10-15 relevant parameters show per category; soon all ~100 parameters will show regardless of category), which will make manual entry inside Magento meaningfully worse.

### Target architecture — getting the team out of Magento

Neuman's core ask: listing staff (5-6 "holky") should complete products entirely inside BigHub's tool, with a batch export/import to Magento roughly once every two weeks — never touching Magento directly for day-to-day work. He does not expect a major technical blocker on the import side itself (Dr. Max already runs imports regularly and sees no big technical problem there); what's still needed is to define the export format/template Magento expects. He is bringing in a colleague from his team who owns Dr. Max's import/export configuration to define this precisely with BigHub in a follow-up session — she was not on this call. The real pain point he's optimizing against is the *constant* interaction with Magento during manual listing work (many times a day), not the eventual periodic import step.

### Business value (Fermi estimate, quarter-over-quarter)

Neuman walked through real figures he'd already been tracking on a quarterly basis:

- **Q1 2026** (before he joined/before any process changes — team only did mandatory work): ~2,600 new listings + ~1,000 other items (call-center-driven corrections, revisions) ≈ **~3,600 items/quarter**, at **~230 Kč/item** (~45 min/item).
- **Q2 2026** (after he took over and began process changes, still pre-tool): **~6,000 items/quarter** at **~130 Kč/item** — achieved despite the team being one person smaller (offset by supplementing with agency/temp staff), by pushing harder on process. This total includes ~430 "protein" category redefinitions and ~760 medication redefinitions done as extra work beyond normal listing.
- Neuman frames ~6,000 items/quarter as roughly the current ceiling under today's (still largely manual) process — he expects **Q3 to be worse**: vacation season, plus a new EU environmental-claims regulation (surfaced ~2 weeks before this call) that Dr. Max discovered affects ~10,000+ products (~4,000 flagged critical), against a current compliance-work capacity of only ~1,000 items/quarter — a clear capacity gap he called "impossible, way too little."
- His stated goal ("kápéčko" — his personal cap/target metric) is to keep raising quarterly throughput while lowering cost-per-item, but he deliberately avoided committing to a firm ceiling, since he doesn't yet know what's achievable once the tool is live.

### KPI — no final number committed

Marek proposed an illustrative starting KPI (~20% improvement within 3 months of deployment, tied to the ~6,000-items/quarter baseline). Neuman pushed back on providing a precise number this far out: "**I don't like doing that, because it feels like I'm just making it up**" [translated from Czech]. He gave qualitative texture instead — today's per-item time ranges enormously by task complexity (a full new listing ~30 min; a small compliance-driven text fix, e.g. an environmental-claim wording change, plausibly ~2 min) — and said he can't set a real benchmark until he sees the tool's actual performance. He floated ~20% faster / ~20% more throughput in the tool's first live quarter as directionally reasonable, expecting the rate of improvement to compound each subsequent quarter, tempered by the fact new listings will always take longer than edits. Marek acknowledged some number will ultimately be needed for the KPI sheet; this was left as an open item rather than resolved on the call.

### Domain expert / practical contact

There is currently no single "head of listing" role on Dr. Max's side — an internal gap Neuman said is being worked on but isn't resolved yet. In the meantime, he is personally involved at the direction-setting level but nominated **Michaela Vdovicynová** — a member of the listing team with a pharmacist's-assistant background who does the listing work herself — as the practical, day-to-day contact for BigHub: she'll run team testing sessions, collect and relay feedback, and handle the operational side he doesn't have time for. Neuman has a separate internal Monday sync with her on the current data-import/feed status; he characterized the pilot category (proteiny) as "reasonably satisfied" so far.

### Next steps

Marek plans to reach out toward the end of this week / start of next to formally kick off the Discovery phase (per [[ASM-011]]) — likely combining an intro/connection with Michaela Vdovicynová, a walkthrough of the existing tool demo (unclear if Neuman has seen it), and a review pass on the existing `listing-specifikace.md` spec, inviting Neuman's comments.

## Decisions Made

- The tool's primary near-term driver is reframed: getting the listing team **entirely out of day-to-day Magento use** (batch import ~biweekly instead) is now Neuman's top priority — ahead of the original supplier-data-quality problem, which he now considers secondary.
- **Michaela Vdovicynová** confirmed as the practical domain-expert/testing point of contact for Listing, distinct from Neuman's business-owner role.
- No final KPI definition or target number was agreed — explicitly left open pending real tool performance data.

## Action Items

- [ ] **Marek Pillár**: Send Petr Neuman the pre-filled Business Quantification/KPI Excel for review and completion — from 2026-09-16-business-quantification-listing-petr-neuman
- [ ] **Petr Neuman**: Review and complete the KPI Excel — traveling for the next two days, expects to get to it around Friday — from 2026-09-16-business-quantification-listing-petr-neuman
- [ ] **Marek Pillár**: Formally kick off the Listing Discovery phase — reach out end of this week/early next, connect with Michaela Vdovicynová, walk through the existing demo and `listing-specifikace.md` spec for review/comments — from 2026-09-16-business-quantification-listing-petr-neuman

## Open Questions

- Final KPI definition/target for Listing — only a directional "~20% faster, compounding quarter over quarter" placeholder was floated, not agreed.
- Exact Magento export/import template requirements — pending a follow-up session with Dr. Max's own import/export technical contact (not yet named, on Michaela Vdovicynová's team).
- Whether/when Dr. Max will formally fill the "head of listing" role gap Neuman flagged — and whether this is the same "second listing business owner" previously referenced (2026-09-02, name not yet known) — not confirmed either way.
- Per-MD/hourly cost rate breakdown beyond the aggregate Q1 (~230 Kč/item) / Q2 (~130 Kč/item) figures was not requested or given.

## Sentiment & Tone

Warm and cooperative throughout — a genuine first-contact rapport-building call as much as a data-gathering one; Neuman offered first-name terms unprompted and was visibly relieved by Marek's "it's OK not to know" framing early on. He came across as candid and self-critical about the state of the listing process ("something we've clearly been sleeping on for years") rather than defensive, and pushed back constructively on being pressured into an unfounded KPI number — a good signal of engagement with getting the numbers right rather than just filling in a form, consistent with the pattern seen in the other Business Quantification calls this week (Tereza Foltýnová, Radim Švarc). His tone noticeably sharpened with urgency when describing Magento's current instability — this reads as the real emotional driver behind the initiative now, more than the original data-quality framing. No friction of any kind on the call.

## Routing Log

- **project-stakeholders**: Enriched STK-023 (Petr Neuman — JTBD origin story, reframed Magento-exit priority, sentiment/communication preference/expectations filled). Added STK-048 (Michaela Vdovicynová — domain-expert/testing contact).
- **project-assumptions**: Added ASM-073 (Listing's primary driver reframed: Magento-exit now outranks the original data-quality framing), ASM-074 (Michaela Vdovicynová confirmed domain expert), ASM-075 (Listing KPI target not yet committed — directional placeholder only).
- **product/solution-space/listing-specifikace.md**: Replaced the unverified "300 000 Kč" placeholder in "Kvantifikovaný přínos" with the real client-sourced Q1/Q2 2026 baseline gathered on this call.
- **project-daily**: 3 action items added to 2026-09-16's daily (created today).
- **project-lessons**: LL-035 (problem framing can shift between an initiative's origin and its business-quantification interview) and LL-036 (cloud-synced Office files open live in-app can silently revert direct scripted writes) captured autonomously.
- **Related**: Listing row (E-commerce BQ sheet) in `~/Library/CloudStorage/OneDrive-BigHubs.r.o/2. Business Quantification/businessQuantificationWorskop.xlsx` filled with corporate-register content from this call, per separate PM request.
