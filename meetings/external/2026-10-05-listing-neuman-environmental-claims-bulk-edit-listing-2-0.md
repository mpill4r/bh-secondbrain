---
last_updated: 2026-10-05
type: external
attendees: [Marek Pillár, Petr Neuman]
recording_link:
---

# Listing 2.0 Idea with Petr Neuman — Environmental-Claims Case & Rule-Based Bulk Catalogue Edits

**Date**: 2026-10-05 (Monday)
**Attendees**: Marek Pillár (AI Analyst / PM, BigHub), Petr Neuman (Listing business owner, Dr. Max, STK-023)
**Type**: external
**Recording**: N/A (transcript, ~29 min, Czech/Slovak)
**Previous session**: [2026-09-30 Listing Reset with Petr Neuman](2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy.md)
**Meeting prep**: N/A

## TL;DR

Petr Neuman used the new EU environmental-claims rules (~10,000+ SKUs affected) to show a recurring need. Once the Listing tool holds the whole catalogue, the team should be able to define a rule ("find / replace / edit this") and run it across the catalogue. His own Claude chat PoC handled 1,500 critical SKUs in ~12 h, with ~12% needing human edits. Both agreed this is not an AI CMS but a flexible, owned bulk-automation capability. It is a candidate add-on for a next-year "Listing 2.0" initiative and not urgent: Dr. Max will finish the current claims wave itself. Marek will check with the developers whether the Listing foundation should account for it now.

## Previous Session Follow-Up

- **Scraping cost research** (Marek / Filip): still open. Marek promised an update this week.
- **Scraping legal check** (Neuman): still open. Marek reminded him.
- The other 09-30 items (supplement data from Michaela, PIM timeline, spec comments, export) were not discussed.
- Progress: no regression. This call added a future-scope topic rather than unblocking the MVP.

## Key Discussion Points

### The case: EU environmental claims (greenwashing)

Petr Neuman described the new EU regulation:
- Any environmental claim about a product ("šetrný k planetě" and similar greenwashing terms) must be clearly proven or removed.
- Member states have to put it into effect. In Czechia it was due to take effect on 27. 9. 2026, but it is stuck in government negotiations. "The only luck we have" [translated from Czech].
- It affects **10,000+ SKUs, about a quarter of the 1P catalogue**. Deadlines in such cases are typically very short.
- Of these, **~4,000 SKUs contained critical terms** that must be fixed first:
  - **2,000+** could be fixed "technically", because the same text (e.g. a brand mention) is shared across hundreds of SKUs, so one fix can be copied across.
  - **~1,500** needed contextual rewriting so the sentences still make sense. The original plan was to do these by hand.
- **Second wave**: non-critical terms, ~6,000–10,000 SKUs, still ahead for his team.

How it works today:
- A colleague builds keyword lists, exports SKUs from Magento, and searches them in Excel (direct / indirect match).
- This "data mining" alone takes a lot of time, before any rewriting starts.
- False positives are common, e.g. "ohleduplný" (considerate) matches "ohleduplný k pokožce" (gentle on skin) as well as environmental uses. They only show up when someone reads the SKU.
- Product text in Excel is HTML spread across several columns, which makes editing hard.

### Neuman's Claude PoC

With under two weeks for 1,500 SKUs, Petr Neuman did it himself with Claude (the company's standard Pro plan, in chat, with markdown files):
- **Setup**:
  - ~2 h defining the rules and working method with Claude.
  - A running journal (markdown) of all rules and changes.
  - A pilot on 10–20 SKUs.
- **Batches**: 10 waves of 150 SKUs. Claude asked about 10–20 unclear SKUs per batch, and he decided those, which became new rules. He added independent checks and audits along the way.
- **Speed**: by the last batches, ~110–150 SKUs in ~10 minutes. **1,500 SKUs in ~12 h in total.**
- **Human review**: the team checked everything (it is legislation, and they wanted a quality read). This took about 2–3 days.
  - **~12% needed edits**, and at least half of those were outside the scope he gave the AI (problematic but non-critical terms were deliberately skipped, to avoid scope creep).
  - He was "disappointed it wasn't zero", but done by hand it would have taken ~1.5 months ("at best by the end of October"). Instead it was done in about a week.
- **Output**: he also made a line-by-line original vs. correction file for reviewers, but the team didn't use it.
- **Self-assessment**: he knows his process "wasn't efficient" and was a proof of concept. He did it partly to show his team it can be done smarter.

### What he wants from the platform

- Not just new listings or "half the content is missing, fill it in". Often the need is a catalogue-wide scan for terms, or replacing one thing with another, driven by regulation.
- **Earlier example**: cosmetics containing a specific substance at ≥ ~4% of the composition must be reclassified from cosmetics to a medicine.
- He expects such cases to keep arriving: "this year we've had to do many of these" [translated from Czech].
- Once the tool holds the whole catalogue, he wants to define "find this / replace / edit" himself and get help with the execution. Otherwise "it gets solved on the side, by hand, again" [translated from Czech].

### Framing: not an AI CMS, but owned bulk automation

- **Marek's question**: is this one more parameter in a "verified AI-powered CMS" (search a SKU, regenerate its text), or a tool where the team defines rules for a new regulation and runs them across a category?
  - As a single-purpose feature he sees little ROI, because such regulations come "once every few years".
  - As a flexible rule-based automation tool (like Make or n8n), with an owner and time for tuning, he finds it far more sellable to senior management, and useful beyond e-commerce.
- **Petr Neuman agreed**: "our goal shouldn't be to build a quasi-AI CMS; that's what CMSs are for" [translated from Czech]. Marek's framing is "the right view".
- **Value Marek named**:
  - Time saved.
  - Lower cognitive load and anxiety about AI output quality on thousands of SKUs.
  - Avoiding fines and the bureaucratic tangle around them.
  - Each new case wouldn't need the business team to re-learn and re-define rules from scratch; BigHub can carry that, and the team only checks the results (2 days instead of a month).

### AI adoption insight

- Petr Neuman sees the main adoption blocker as people's first try: one prompt, a weak text, and the verdict "AI can't write, it's useless".
- The up-front setup time (a day of tuning to save ~400 hours) feels like wasted time to them.
- He had the team review everything so they could see the quality for themselves.
- Marek agreed: the owner of the process owns the result. Hallucinations that reach a deliverable are the owner's failure, not the AI's.

### Constraints on Neuman's side

- Dr. Max staff can't publish anything: **GitHub is forbidden**. Without IT/security help he also can't let Claude call the API.
- So a quick front-end built with Claude Code for the second wave may not be possible for him.
- **Fallback**: a markdown + skill package, so each team member takes ~1,000 Excel rows and runs the same method.

### Next steps and positioning

- **No urgency**: Dr. Max will finish the environmental claims themselves. This is an add-on to consider after the main Listing case. BigHub is not expected to "rescue" the current wave.
- **Listing 2.0**: Marek will treat it as part of a next-year Listing extension ("Listing 2.0"), which would go to Dudaško as an initiative row (as with the current Listing).
- **Developers**: Marek will check with them whether the foundation being built now should already account for catalogue-wide rule-based operations.
- **Neuman's PoC as input**: it can stand in for user-journey mapping; BigHub would then cover edge cases.
- **Marek will follow up twice**:
  - This week: external scraping-service costs, plus a reminder about the legal check.
  - Within the month, November at the latest: further initiatives, with at least this one sized and a very rough estimate, so BigHub can prepare a plan for Tomáš Dudaško.

## Decisions Made

1. Catalogue-wide rule-based bulk editing (find / replace / edit driven by regulation) is framed as a flexible, owned automation capability, not an "AI CMS". Agreed by Petr Neuman and Marek Pillár.
2. It is not urgent and not part of the current Listing MVP. It is a candidate add-on for a next-year "Listing 2.0" initiative. Dr. Max handles the current environmental-claims waves internally.

## Action Items

- [ ] **Petr Neuman**: Ask his Claude chat for a shareable executive summary of the environmental-claims work (method, rules, batches, checks) and send it to Marek — from 2026-10-05-listing-neuman-environmental-claims-bulk-edit-listing-2-0
- [ ] **Marek Pillár**: Discuss with the developers (Filip Černý) whether catalogue-wide rule-based find / replace / edit can be accounted for conceptually in the Listing foundation now — from 2026-10-05-listing-neuman-environmental-claims-bulk-edit-listing-2-0
- [ ] **Marek Pillár**: Follow up with Petr Neuman this week on the external scraping-service cost breakdown; remind him of the legal check — due 2026-10-09 — from 2026-10-05-listing-neuman-environmental-claims-bulk-edit-listing-2-0
- [ ] **Marek Pillár**: Meet Petr Neuman within the month (November at the latest) on further Listing initiatives, with the bulk-edit idea sized and a very rough estimate, to prepare a plan for Tomáš Dudaško — due 2026-11-30 — from 2026-10-05-listing-neuman-environmental-claims-bulk-edit-listing-2-0

## Open Questions

- Can the Listing foundation (data model, batch processing) support catalogue-wide rule-based operations later without rework? To be checked with the developers.
- How would rules be defined and owned (by the business team vs. BigHub), and how are results reviewed (diff view, sampling, audit)?
- What is the ROI case? How often do such regulatory changes come, and what do they cost by hand vs. fines and bureaucracy?
- Could Dr. Max IT allow API-based Claude use or internal hosting, given that GitHub and publishing are blocked?

## Sentiment & Tone

Warm, open and forward-looking. Petr Neuman came to share a need, not to escalate. He was explicit that nothing is urgent, and he was clearly proud of his PoC while modest about its rigour. He thinks like a product owner, aligned quickly with Marek's "automation, not CMS" framing, and voiced the same view on AI adoption. Marek praised his range ("I wish every business owner had your overlap" [translated from Slovak]). The relationship looks strong; he is a natural internal champion for AI work at Dr. Max.

## Routing Log

Confirmed by PM on 2026-10-05 (confirm all).

- **project-assumptions**: ASM-244 (Decided), ASM-245 (Open), ASM-246 (Decided) added
- **project-knowledge**: new "EU environmental claims (greenwashing) regulation" entry; AI Listing Tool updated with Neuman's Claude PoC
- **project-stakeholders**: STK-023 updated
- **client-overview**: Ways of Working — business users can't ship their own AI tools
- **product-requirements**: REQ-001 added (Listing 2.0 rule-based bulk edits)
- **project-daily**: 2 PM-owned action items added; scraping-research item updated (due 2026-10-09). Neuman's executive summary stays in this note.
- **project-lessons**: LL-81
