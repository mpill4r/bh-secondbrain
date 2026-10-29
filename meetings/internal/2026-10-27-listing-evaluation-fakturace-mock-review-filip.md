---
last_updated: 2026-10-29
type: internal
attendees: [Marek Pillár, Filip Černý]
recording_link:
---

# Listing Evaluation & Fakturace Mock Review with Filip — 80–85 % Match on Messy Reference Data, Excel Export, Stamps as the Weak Spot

**Date**: 2026-10-27 (Tuesday, ~40 min)
**Attendees**: Marek Pillár (BigHub, PM), Filip Černý (BigHub, developer)
**Type**: internal
**Recording**: N/A
**Previous session**: [2026-10-26 Listing with Filip — supplements batch, new demo & export plan](2026-10-26-listing-filip-supplements-batch-demo-export-plan.md)

## TL;DR

Filip delivered everything promised on 10-26. The Listing demo now holds Dr. Max's 500 supplements, saves per-product versions and exports the latest state to Dr. Max's own Excel format. He also re-generated the parameters for the ~200 "validated" products: exact match is ~80–85 %, but the reference data has many errors, so the number understates quality. In logistics, Reklamace login works and the Fakturace mock demo is live. It only runs on Filip's ~10 prepared routes, because real documents still lack AR numbers and Axapta has no route lookup yet. Stamp counting is the weakest part. Marek presents both on Thursday 10-29 without a live demo; Filip sends his materials to Marek only.

## Key Discussion Points

### Listing — the demo

- The demo holds one category, food supplements: the **500 products** Dr. Max wants to process next. The other file (~200 products Dr. Max calls checked and complete) was used for the evaluation, not loaded.
- Opening a product works as before. "Generate parameters" typically finds a few more parameters from the instructions Michaela sent.
- **Versioning per product**: every save creates a new version with a timestamp. The status moves from *Import* to *Rozpracováno* (in progress), and the user can switch between versions and generate from either one. It is per product, not per listing.
- **Export Excel**: one button exports the whole category in the same format Dr. Max delivered, always with the latest version (checked live on "Zerex Classic", new parameter "bez alkoholu"). Filip: Dr. Max can't import it yet, so it is "a demo that we can export fast and in any format" [translated from Czech]. The target is still a Magento write-back with no BigHub database.
- Only the 500 new products are loaded. Adding the ~200 "good" ones would mix old and new (some proteins are also supplements). Filip can add them, e.g. separated by status, if wanted.
- The listing score is shown. Some products Dr. Max marked as not good come out good in Filip's evaluator, but the evaluator isn't tuned.

### Supplier source formats ≠ export formats

The formats in Neuman's spec comments (SPL/SPC, XML, PDF, XLSX, content-manager XLSX) are **supplier source files that Dr. Max wants to import as inputs for generation**. They are not export formats. Marek had mixed them up. Filip: he has asked Dr. Max to sort out supplier files "at about three meetings".

### Listing — the evaluation

- Method: took the ~200 reference products, removed all parameters, and regenerated them from the remaining information. He used the same module as the live app.
- Deliverables:
  - a **report** describing the method; it points to the two key files
  - **pairwise comparison** Excel: for each parameter, the reference value next to the generated one
  - **reference-data audit** Excel: all errors found in Dr. Max's data
  - a **full evaluation report** with many script-generated statistics, sent via Teams
- **Accuracy**: exact 1:1 match ~**80–85 %**. Filip: "a huge but" — shit in, shit out. The reference data is "pretty sloppy", so the measurement is strongly biased.
- Error causes (from spot-checking 5–10 cases):
  1. Less common: the information exists only in the parameters, not in the text, so the agent has nothing to extract it from.
  2. More common: the reference data contradicts itself, e.g. "vegan" set while the composition lists gelatine; the agent refuses to set it.
- Filip believes BigHub's output is already **closer to the truth than the reference**, with exceptions. Weak spot: "suitable for newborns" is mostly missed. That needs prompt tuning, e.g. a rule like "suitable for under-3s → suitable for newborns".
- The audit isn't meant as "haha, you're idiots". It explains why 85 % on bad data understates quality. Filip worried it may read as passive-aggressive.
- Marek: Dr. Max may have someone check manually before the Magento upload, which would raise their side's quality. Unlikely with ~60,000 rows, but possible.
- Marek's read of the input Excels: likely Claude-generated ("Neuman is quite AI-heavy"). The second file, the parameter catalogue, adds nothing. Dr. Max may have made up the categorisation itself.
- Value story (Filip): the user doesn't have to keep the whole catalogue in mind ("could it also be vegan, gluten-free?"). They only confirm suggestions. Marek: "we can say: look, we corrected your data, 85 %" [translated from Slovak].

### Who sends what

Filip had written a cover e-mail to all of Dr. Max. Marek asked to present it himself on Thursday instead: Neuman "couldn't get round to something for three weeks", so mailing it cold won't land. Agreed: **Filip sends everything only to Marek** (Excel ×2, report, mail draft, full evaluation). Marek uses it as input and walks Dr. Max through it.

### Logistics — Reklamace login live

- Login works through Microsoft Entra. Jana Egrmaierová, Petr Sláma and others are set up; Marek has platform admin rights.
- Marek's own account showed "not a member of the platform user group" when entering via the platform. Still to resolve.
- Filip: Juraj makes many changes, so things can look broken while they actually work.
- Label photo flow: enter a label, upload any photo, it lands in the test exports (slow). Already tested by logistics over the past ~two weeks, incl. Egrmaierová standing in for Axapta.

### Logistics — Fakturace mock demo live

- Mock deployed, connected only to **Filip's own mock Axapta proxy**, which returns answers for his prepared routes.
- **No BigHub database**:
  1. Read the AR number of the route.
  2. Ask Axapta: "Do you know this route?"
  3. Axapta returns the expected documents (and which are already in).
  4. BigHub assigns pages, assembles documents and returns clean, structured documents plus the extracted data.
- **Two blockers for real use**:
  1. Real documents still don't carry the AR number or barcode that ViaPharma promised at the start. Filip printed AR "stamps" onto his ~10 test routes (e.g. the old ZOPV type) by hand. ViaPharma still has no sample documents of the new version.
  2. The route lookup isn't implemented in ViaPharma's real Axapta, perhaps only just started. "Not something that will be there tomorrow" [translated from Czech].
- **Flow**: choosing a file simulates one scanner page. Pages process asynchronously, ~5–10 s each. Re-uploading the same page shows it as updated (overwritten). Each page is placed as "page x of y" of a document. Filip sees this as the strength: "take any page, throw it in, and it falls to the right route and the right page".
- One page per file stays. Marek: in reality the scanner produces one file per sheet, pages may be shuffled, and a 20-page PDF never happens. Folder upload isn't needed. Filip: one-at-a-time also helps the user follow what happens.
- **Stamps are the biggest limitation**. In the demo a stamp was counted twice, but flagged low-confidence with "zkontrolujte" (please check). Filip: an LLM will never count stamps reliably. With his research background in vision models, a custom detector would take **~1 working week**. He expects **95 %+ accuracy** and cheap inference. He only needs to know what the stamp type(s) look like and would build synthetic data. First ask logistics whether "check it yourself" in about half the cases is acceptable. Marek: the client's own value estimate is undercounted. Today's manual process is slow and error-prone.
- Unrelated document (e.g. a BigHub invoice) → "Dokument se nepodařilo přiřadit k trase" (couldn't be assigned to a route), which is correct. Known bug: a non-route document with a printed AR number may be classed as ZOPV.
- Filip's claim: in ~98 % of cases the page is either read correctly or read with an explicit "not sure, check" flag.
- Small visual glitch Filip knows about and parked.

### Thursday plan

- Logistics sync (Thu): Marek doesn't demo live. He clicks through himself and reports status, then agrees next steps. Filip asks for Marek's UX feedback; nobody but Filip has used the app. Filip also sends Marek the test-route bundle and a cover message (to Marek only).
- Žižka liked the UI and document processing long ago. The internals are the same; the UI changed, the old login was removed, and storage was reworked.
- Marek may leave a note for Jindřich in the chat.

## Decisions Made

- Evaluation results and materials go to Marek only; Marek presents them to Dr. Max on Thursday 10-29 rather than Filip mailing everyone.
- The Listing demo keeps only the 500 new supplements (no ~200 reference products for now).
- Fakturace keeps one-page-per-file upload (mirrors the real scanner); no folder/bulk upload.
- Stamp-counting improvement (custom vision model) is not started until logistics says whether "please check" flags are acceptable.
- No live Fakturace demo at Thursday's logistics sync; Marek reports status.

## Action Items

- [ ] **Filip Černý**: Send Marek the Fakturace test-route bundle and a cover message (to Marek only) — from 2026-10-27-listing-evaluation-fakturace-mock-review-filip
- [ ] **Marek Pillár**: Click through the Listing demo + evaluation materials; walk Neuman (+ Jindřich) through them on Thursday: export, 80–85 % on biased data, audit framed constructively, source formats = inputs — due 2026-10-29 — from 2026-10-27-listing-evaluation-fakturace-mock-review-filip
- [ ] **Marek Pillár**: Click through the Fakturace mock (test routes, unrelated document), report status at Thursday's logistics sync without a live demo, send Filip UX feedback — due 2026-10-29 — from 2026-10-27-listing-evaluation-fakturace-mock-review-filip
- [ ] **Marek Pillár**: Ask logistics whether "please check" stamp flags are acceptable or worth ~1 week for a vision model; if so, get examples of the stamp type(s) — from 2026-10-27-listing-evaluation-fakturace-mock-review-filip
- [ ] **Marek Pillár**: Chase ViaPharma for sample documents of the new version with the AR number, and Sláma for when Axapta's route lookup will exist — from 2026-10-27-listing-evaluation-fakturace-mock-review-filip
- [ ] **Marek Pillár**: Get his account added to the platform user group (Jura) — from 2026-10-27-listing-evaluation-fakturace-mock-review-filip

## Open Questions

- Is ~1 week for a stamp vision model worth it to logistics, and what do the stamps look like?
- When will real route documents carry AR numbers, and when will Axapta answer route lookups?
- Can Dr. Max import any export at all, or does Listing stay export-only until Magento?
- Does Dr. Max hand-check data before the Magento upload (affects how the 85 % is read)?
- Should the ~200 reference products also go into the demo?

## Sentiment & Tone

Productive and aligned. Filip is proud of the evaluation and eager for outside feedback ("nobody but me has ever touched it"). Marek is reassured on Listing quality ("that's what I wanted to hear") and protective of how results reach Dr. Max, given Neuman's slow engagement. Shared frustration with ViaPharma's unmet AR-number promise and Axapta's missing lookup, but both see the Fakturace core as strong.

## Routing Log

Confirmed by PM (2026-10-29, "confirm all"):

- **project-assumptions**: added ASM-355–ASM-359; updated ASM-318, ASM-350.
- **product-requirements**: added REQ-016.
- **project-knowledge**: Fakturace doprav document flow; AI Listing Tool.
- **project-stakeholders**: STK-006, STK-023 updated.
- **project-daily**: 6 action items added; 5 closed; 2 annotated.
- **project-lessons**: LL-111.
