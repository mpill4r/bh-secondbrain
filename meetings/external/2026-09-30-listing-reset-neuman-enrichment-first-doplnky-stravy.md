---
last_updated: 2026-09-30
type: external
attendees: [Marek Pillár, Petr Neuman, Michaela Vdovicynová, Filip Černý]
recording_link:
---

# Listing Reset with Petr Neuman — Magento Blocker, Enrichment-First Scope & Food Supplements Batch

**Date**: 2026-09-30
**Attendees**: Marek Pillár (AI Analyst / PM, BigHub), Petr Neuman (Listing business owner, Dr. Max, STK-023), Michaela "Míša" Vdovicynová (Listing domain expert / testing, Dr. Max, STK-048), Filip Černý (Developer, BigHub, STK-006, online)
**Type**: external
**Recording**: N/A (transcript, ~63 min, Czech/Slovak)
**Previous session**: [2026-09-16 Business Quantification call with Petr Neuman](2026-09-16-business-quantification-listing-petr-neuman.md)
**Meeting prep**: [2026-09-30-listing-neuman-discovery-kickoff-meeting-prep](../prep/2026-09-30-listing-neuman-discovery-kickoff-meeting-prep.md)

> **Transcript note**: the transcription tool labeled almost all in-room speech as "Marek Pillár". Speakers are attributed here from content: the Czech-speaking business owner is Petr Neuman, the parameter/data answers come from Michaela Vdovicynová, and Marek speaks Slovak. Attribution between Neuman and Míša is best-effort.

## TL;DR

The Listing plan was reset around two blockers.
- **Magento write-back isn't feasible now.** Magento imports accept only one changed column per import (no "leave unchanged" value), so 20 columns means 20 imports. Nobody on the global side will integrate with Magento, which is being replaced by a global PIM that is ~9 months away and slipping.
- **Suppliers never send enough data.** Parameters, about 10 per product, are the real driver of findability and conversion.

Agreed direction: **enrichment first, Magento out of the MVP**. The next batch is the **food supplements (doplňky stravy) legislative group, ~2,000 SKUs**: the top 20 % that make 80 % of the revenue. BigHub gets the parameter catalogue, the SKU batch and already-finished examples, and delivers an export in whatever format the parameter specialist needs. Every SKU stays human-validated.

Scraping external sources is the secondary goal. Neuman takes it to Dr. Max legal once BigHub describes the variant; BigHub researches third-party services and cost.

**Continuity with 2026-09-16**: Neuman's "get the team out of Magento" driver ([[ASM-073]]) is now blocked by the import limitation and gives way to a parameter-enrichment driver. The import/export person he promised is effectively the parameter specialist ("Maruška"), not yet met directly. KPIs weren't revisited (already committed, [[ASM-123]]).

## Key Discussion Points

### Status and budget

Marek opened by aiming to set a roadmap and timeline despite the blockers. He confirmed that Marek Šimoník has moved the e-commerce budget onto Listing; the order-prediction dashboard only has small tweaks left this year and a 2027 roadmap later.

The team used the protein POC for a week and saw how it works. The Magento merchant-tools save failures were fixed about 1.5 months ago: saves now go through first time, but work is still slow and will get harder once attribute groups are removed.

Neuman's staging:
- **First milestone**: get the new listing flow working, including preparing brand-new products (~6,000 products per half-year).
- **Big scope**: "at minimum step two". A smaller scope of ~200–250 SKUs per week is the right size to tune the process.

### Real data and Magento

Filip: BigHub **already works on real data**, but it was imported once and is neither live nor writable back to Magento.

Neuman, on why live Magento integration should wait:
- Nobody at Dr. Max global will engage, because global is moving away from Magento.
- CZ should move to a new global PIM, "a question of three quarters of a year". The original date was about now, so it keeps slipping.
- "It should be a live platform only much later; for now I'd be happy if we found a way to get data in and out" [translated from Czech].
- He is still waiting for the parameter specialist's code lists (číselníky) per attribute set and category.

**Import limitation, discovered ~2 weeks ago.** A Magento import changes one attribute across all included SKUs, and there is no "null / don't import" value. Two products with different changed fields therefore can't share an import, because the unchanged fields would be overwritten with empty values. With ~5 text fields (description, meta description, teaser, composition, properties) and ~15 parameters, that is ~20 columns and so ~20 imports. Neuman: this "took the wind out of my sails", and he isn't sure what sensible next steps are.

**Vendor portal** (formerly "promotu") is coming online. Suppliers will eventually enter data there instead of emailing Excel. Longer term, BigHub's tool should integrate with it; Neuman thinks this is likelier to happen before any Magento integration.

### What really matters: parameters

The only thing suppliers reliably send is **product name, EAN, SKU and descriptions (texts)**. Parameters are missing in effectively "10 out of 10" cases, and ten years of pushing suppliers hasn't changed it.

Neuman's target is **~10 parameters per product**, against 2–3 today, which are often not user-facing (brand, product line). Parameters drive findability, filtering and bot discoverability, and so the conversion KPI. He wants to start fixing web filters next, but "parameters first". Texts the team can write or adapt themselves.

Constraints from Neuman:
- Any auto-filled value must carry a status saying no human has reviewed it yet.
- Liability matters: if an inspection (SZPI/SÚKL) comes, "the supplier gave it to us" is defensible, "we pulled it from somewhere" is not. Medicines are out of scope ("we don't have pharmacists for that"); the target is the broad non-drug portfolio.
- He can accept auto-filling ~70 % and asking the supplier for the rest, which is still far better than today.

Marek added the ideas of an LLM confidence status and a human-assisted variant, where the person pastes a competitor URL and the tool reads it.

### Scraping external sources

Filip: about 3 months ago BigHub demoed an agent tool that searches the EAN online and reuses information from other listings (Notino, small specialist e-shops). It worked "very nicely" but was deliberately left out of the user demo because of legal doubts. A legal check was requested at the time via Alana (and possibly Lukáš Szücs); its outcome is unknown.

Filip on alternatives: third-party scraping services exist, take on responsibility and aren't expensive. BigHub's own approach runs into anti-bot defences and datacentre-IP blocking.

Marek flagged it as a grey zone (Google vs. Reddit). Neuman will take it to Dr. Max legal once BigHub describes the variant precisely ("describe the variant so I know what I'm talking about"). Legal answers within a month.

Neuman also wants the third-party options and their cost ("is it viable for hundreds or tens of thousands of SKUs?"). Scraping is a **secondary** goal, not a blocker.

### Next scope: food supplements (doplňky stravy)

Neuman proposed the next step: instead of the team fixing each SKU by hand, run the batch they're currently working on through the tool, as was done with proteins. Inputs:
1. the **new parameter set** from the parameter specialist;
2. the **SKU batch** being worked on;
3. **already-finished SKUs** as good examples.

Then define an **export in exactly the format the specialist needs**, e.g. per column, so she doesn't spend a week splitting it into imports. He says this may help more than the new-listing flow ("these are hundreds of hours of manual work"). Cosmetics comes after.

- **Scale**: ~2,000 SKUs, the 20 % of supplements that make 80 % of revenue. Already Pareto-prioritised, so no per-SKU prioritisation is needed.
- **Export**: Filip says it's no problem, about 2 hours for a download button, in any agreed format.

**Category model (Filip's question).** Filip needs each product to belong to exactly one identifiable category.
- **Legislative group** is the anchor: ~6–7 groups, each product in exactly one, so each SKU gets a fixed primary category.
- The protein POC was a small category spanning two groups (foods and supplements).
- Neuman proposed splitting supplements into main subgroups (vitamins, minerals, for children, herbal, other) with rules per subgroup, so generated text can say protein-specific things only for protein.
- Filip endorsed **layered standards**: a base standard for all products, then attribute-set rules, then subcategory rules ([[ASM-068]]). He flagged the risk of contradictory rules. Children's products that are also vitamins need a primary/secondary rule.
- Míša: the existing "main category" in the e-shop export isn't always usable (e.g. "zdravé žíly", "healthy veins").
- **Agreed**: start with the whole legislative group as one unit and consider sub-splitting along the way, so it doesn't become another roadblock.

**Parameter catalogue.** The girls hold the catalogue for the group. The protein-era supplement parameters were probably complete, but the ~6 new parameters now being added are missing. The current export may also lack the existing ~14 values, so both are needed. Míša will coordinate with the parameter specialist.

### Human review and AI Act

Every SKU stays human-validated in the app "for now, definitely". Neuman gave two reasons:
- the AI Act would otherwise require labelling content as AI-generated;
- "we need to build credibility; I don't want to lose it".

He can imagine relaxing this only after ~2 years of proven use.

### Magento and global PIM next steps

Neuman will find out the global PIM migration timeline for CZ. In early November he visits Slovakia, which already uses the new tool, for insight into how the workflow differs. Direct integration needs someone from the global team, who will likely refuse, so it's parked.

Marek will rewrite the spec and roadmap: **Magento out of the MVP, the MVP comes later, and the focus is data enrichment**. He asked Neuman and Míša to answer the yellow comments in the Listing spec (mostly UX points decided by Filip and Marek) and will send an email recap.

**Parameter catalogue drift (Filip, future).** Ideally the app pulls the parameter catalogue automatically so it doesn't drift from Dr. Max's source. Neuman: yes, but only after the global PIM standardises parameters across markets. Filip: no need to prepare anything now.

## Decisions Made

- **Magento integration is out of the MVP.** No live or automated write-back for now. The MVP comes later and the focus shifts to data enrichment plus a usable export.
- **Next scope: the food-supplements legislative group, ~2,000 SKUs**, the top 20 % that make 80 % of revenue. Inputs: parameter catalogue (new + existing), the SKU batch, finished examples.
- **Output: an export in the format the parameter specialist needs** (e.g. per column / import-ready).
- **Category model**: each SKU has one primary category = its legislative group (~6–7 groups). Sub-splitting (vitamins, minerals, children, herbal, other) with layered rules comes later, not now.
- **Parameters (~10 per product) are the primary value driver** for findability, filtering and conversion. Texts are secondary.
- **Human validation of every SKU stays.** Auto-filled values carry an "unreviewed" status; medicines are excluded.
- **Scraping is a secondary goal.** Legal check via Neuman once BigHub describes the variant; BigHub researches third-party services and cost, including a human-assisted variant.
- **Parameter-catalogue auto-sync is deferred** until after the global PIM standardisation.

## Action Items

- [ ] **Michaela Vdovicynová**: Coordinate with the parameter specialist ("Maruška") to send BigHub the food-supplements data: full parameter catalogue (existing ~14 + ~6 new), the ~2,000-SKU batch, and already-finished SKUs as examples, plus the export format she needs — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Petr Neuman**: Find out the global PIM migration timeline for CZ — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Petr Neuman**: Take the scraping variant to Dr. Max legal once BigHub describes it (answer within ~1 month) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Petr Neuman / Michaela Vdovicynová**: Answer the yellow comments in the Listing spec — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Marek Pillár / Filip Černý**: Describe the scraping variant precisely for Dr. Max legal (process, sources, how the team uses it) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Marek Pillár / Filip Černý**: Research third-party scraping/extraction services and a cost breakdown (hundreds vs. tens of thousands of SKUs), including a human-assisted URL variant — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Marek Pillár / Filip Černý**: Find out what happened to the earlier scraping legal check (via Alana Sihelská / Lukáš Szücs) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Marek Pillár**: Rewrite the Listing spec and roadmap (Magento out of the MVP, enrichment first, supplements batch, export) — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Marek Pillár**: Send the email recap to Petr Neuman and Michaela Vdovicynová — due 2026-09-30 — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy
- [ ] **Filip Černý**: Build the export (download button, agreed columns, ~2 h) once the format is known — from 2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy

## Open Questions

- What exact export format does the parameter specialist need? Is a one-column-per-file, import-ready output possible?
- Is the protein-era supplement parameter catalogue complete, and does the current export include the existing ~14 parameter values?
- Primary vs. secondary category rules for overlapping subgroups (e.g. a children's vitamin), and whether to sub-split supplements at all.
- The legal verdict on scraping, and which third-party service and at what cost.
- When does CZ move to the global PIM, and what changes in the workflow (Slovakia visit, early November)?
- How and when will the vendor portal integrate with the tool?
- Not discussed from the prep: blacklist approval and warning vs. blocking ([[ASM-064]]); the "head of listing" gap.

## Sentiment & Tone

Constructive and candid. Neuman was open that the Magento import finding "took the wind out of his sails" and that he didn't know the sensible next step. He then drove the solution himself (the supplements batch through the tool, an export shaped for the specialist) and was clearly energised by it. He was firm on liability and credibility (human review, no medicines, supplier-sourced facts). Filip was engaged and aligned, validating Neuman's layered-category idea as "a really great idea". Marek steered toward concrete action items and accepted the scope change pragmatically ("I'd rather move forward with something that makes sense"). The relationship signal is good: Neuman treats BigHub as a partner in finding a path, not a vendor behind schedule. The meeting overran by ~10 minutes with no friction.

## Routing Log

Confirmed by PM on 2026-09-30 (confirm all).

- **project-assumptions**: ASM-207–ASM-212 added; ASM-065, ASM-067, ASM-032 superseded; update notes on ASM-073, ASM-033, ASM-068
- **project-knowledge**: AI Listing Tool entry, Listing reset
- **project-stakeholders**: STK-023, STK-048, STK-006 updated; STK-058 "Maruška" added (low confidence)
- **project-daily**: 5 PM-owned action items; others' items stay in this note
