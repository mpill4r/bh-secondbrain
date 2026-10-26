---
last_updated: 2026-10-26
type: internal
attendees: [Marek Pillár, Filip Černý]
recording_link:
---

# Listing with Filip — Food-Supplements Batch, New Demo & Export Plan

**Date**: 2026-10-26 (Monday, ~22 min)
**Attendees**: Marek Pillár (BigHub, PM), Filip Černý (BigHub, developer)
**Type**: internal
**Recording**: N/A
**Previous session**: [2026-09-30 Listing reset with Neuman and Michaela](../external/2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy.md); risk raised at the [2026-10-21 BigHub weekly](2026-10-21-bighub-weekly-sync-reklamace-fakturace-listing-aks-rollout.md)
**Meeting prep**: [2026-10-26-listing-filip-doplnky-stravy-meeting-prep](../prep/2026-10-26-listing-filip-doplnky-stravy-meeting-prep.md)

## TL;DR

Michaela Vdovicynová finally sent the food-supplements material: a filled-in example file and 500 unfilled supplements. The 500 are spread across many main categories (protein, magnesium, collagen, vitamin C…), not one complete category. They also came without the per-category listing instructions BigHub expected. Agreed: run the whole batch at the attribute-set level ("doplněk stravy"). Parameters should work well as-is; texts will be more generic. BigHub won't invent per-category rules Dr. Max hasn't defined.

Filip builds a new demo today:
- the old protein data is hidden and the new data imported
- the allergen duplicates are fixed (his own import mistake)
- export = the same Excel filled in, with the added values highlighted

Marek and Filip review it Tuesday at 16:00, ahead of Thursday's call with Neuman (Filip is on holiday Thursday–Friday).

## Key Discussion Points

### What Dr. Max sent

- Marek: the spec comments from Dr. Max came in too; no big changes expected. He felt the data was thin.
- Filip: "a bit odd" — he expected the listing minima / instructions per supplement type. He can mock instructions from the protein work. The idea is that Dr. Max later edits the LLM instructions and deterministic checks themselves.
- Parameter names are mostly self-explanatory (e.g. "příchuť" → strawberry/raspberry). Special cases (e.g. "stopy" of allergens ≠ allergens) can be added gradually.
- The 500 products are all in one attribute set (doplněk stravy) but span many main categories, e.g. ~20 here, ~30 collagen. So BigHub doesn't get one complete new category like proteins.

### Attribute-set level vs. main-category rules

- Filip: the target is layered rules — all products → attribute set (Dr. Max wants ~14) → main category ([[ASM-068]]). But Dr. Max still hasn't defined its main categories ("we've been at this since April").
- At the attribute-set level the model only knows "write for a food supplement" (plus legal elements such as the supplement warning). It can't add category-specific content like "mention the protein benefits", as the protein demo did.
- **Parameters**: Filip is confident they work as-is. They're one-of-n choices, independent of whether it's protein or vitamin C. **Texts** will be more generic.
- Agreed: treat all supplements as one group for now. A filter by main category could help Dr. Max's team work through them. Don't invent per-category instructions — "it's not our fault or our job; being proactive here may be wasted" (Marek) [translated from Slovak].
- Framing for Dr. Max: present the layered structure as the outlook, and remind them it depends on defining main categories. Show that the product is valuable even at attribute-set granularity. Marek's user angle: shoppers decide by purpose (magnesium for sleep vs. energy), which favours the finer layer later.
- Marek may draw the hierarchy for Dr. Max. Today it's flat: one box (all products) → one arrow (doplněk stravy). The Listing repo now lives in Dr. Max's Azure DevOps (it used to be Filip's own).

### Allergen duplicates

Not a real bug. Filip imported two different parameter sets from the ~10 Excels Dr. Max has sent, so some values appear twice (same meaning, slightly different names, e.g. with brackets). Fix: import the new catalogue Dr. Max sent on Friday, ~20–30 minutes, today. Filip doesn't need to defend it: "our mistake, fixed immediately" [translated from Czech]. Marek replies to Dr. Max: thanks, we're on it, more on Thursday.

### Demo and export

- New demo: Filip hides (doesn't delete) the old protein products and imports only the new products and parameters, so nothing is confusing.
- **Export**: the same Excel Dr. Max sent, filled in. Changed or added cells are highlighted so it's clear what's new. Marek dropped the idea of accept-per-change in Excel (500 rows of clicking). Highlighting mirrors the app, which shows old vs. new and lets the user approve or edit. The format is still unconfirmed with Dr. Max; Filip is fine asking first.
- Filip expects all of it **today**.

### Timing

- Filip is on holiday **Thursday–Friday (10-29, 10-30)**, so he can't join Marek's Thursday call with Neuman (with Jindřich).
- Sync **Tuesday 10-27 at 16:00** (30 min): walk through the demo; if it isn't ready, Filip says so, no pressure. On Thursday Marek can click through the demo with Dr. Max.
- For Thursday, Filip suggests a ~2-minute summary of the decisions and compromises from the last meeting rather than re-asking the same open questions; "they simply don't know" [translated from Czech].

### Filip's blockers elsewhere

- Logistics: waiting for Machata (back 10-27; per Jindřich realistically Thursday). Fakturace mock demo blocked because BDC infra misconfigured something. "Completely outside our control and frustrating" [translated from Czech]. He has small Fakturace backlog items to fill time.
- Marek: the Reklamace roadmap Excel was outdated the morning after he finished it (ViaPharma shifted).
- Listing outlook: Marek finds it the most interesting project with real money potential and Neuman cooperative. Filip fears it will die on integrations and stay a PoC.

## Decisions Made

- The supplements batch (500 SKUs) runs at the attribute-set level (one rule set for all food supplements); no invented per-main-category instructions. Parameters first, generic texts accepted.
- Old protein demo data hidden (not deleted); the new demo shows only the new products and parameters.
- Allergen duplicates fixed by importing Dr. Max's latest parameter catalogue.
- Export = Dr. Max's own Excel filled in, with changed cells highlighted (to confirm with Dr. Max).
- For Thursday: summarise the decisions and compromises instead of re-asking open questions.

## Action Items

- [ ] **Filip Černý**: Import the new supplements data + latest parameter catalogue (fixes allergen duplicates), hide the protein demo, run enrichment, build the Excel export with highlighted changes — due 2026-10-27 — from 2026-10-26-listing-filip-supplements-batch-demo-export-plan
- [ ] **Marek Pillár / Filip Černý**: Demo review sync — due 2026-10-27 16:00 — from 2026-10-26-listing-filip-supplements-batch-demo-export-plan
- [ ] **Marek Pillár**: Reply to Dr. Max: thanks for the material, allergen issue being fixed, more on Thursday — due 2026-10-26 — from 2026-10-26-listing-filip-supplements-batch-demo-export-plan
- [ ] **Marek Pillár**: Prepare the Thursday call with Neuman (+ Jindřich): 2-min summary of decisions/compromises, demo walkthrough, export format, 500 vs. ~2,000 SKUs, main-category definition as the outlook — due 2026-10-29 — from 2026-10-26-listing-filip-supplements-batch-demo-export-plan
- [ ] **Marek Pillár**: Optionally draw the current vs. target rule hierarchy (all products → attribute set → main category) for Dr. Max — from 2026-10-26-listing-filip-supplements-batch-demo-export-plan

## Open Questions

- Is 500 the first tranche of the ~2,000 SKUs agreed on 09-30, or the whole scope?
- Will Dr. Max define main categories and per-category listing instructions, and when?
- Is the highlighted-Excel export what the parameter specialist needs?
- Any route into Magento at all, or does Listing stay an export tool / PoC?

## Sentiment & Tone

Easy and collegial. Both are frustrated with Dr. Max's slow, partial inputs (the "thin" data, main categories undefined since April) but agree not to over-invest in guessing. Filip is visibly frustrated by logistics and BDC blockers outside BigHub's control, and wanted it on record that he isn't neglecting that work. Shared worry that Listing dies on integrations despite the product's potential.

## Routing Log

Confirmed by PM (2026-10-26, "confirm all"; sender = Michaela Vdovicynová):

- **project-assumptions**: added ASM-349, ASM-350; updated ASM-068, ASM-207, ASM-208 (500 received, ~2,000 open), ASM-318.
- **product-requirements**: added REQ-014.
- **project-stakeholders**: STK-006, STK-023, STK-048 updated.
- **project-knowledge**: AI Listing Tool — rule hierarchy and repo.
- **project-daily**: 5 action items added; 2 annotated.
- **project-lessons**: LL-110.
