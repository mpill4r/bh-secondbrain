---
last_updated: 2026-10-01
type: external
attendees: [Alana Sihelská, Jura Brázdil, Marek Pillár, Radim Švarc, Michaela Albrechtová]
recording_link:
---

# TEO/OCR Sync — Autumn Batches Delivered, Cost per Page & Next Vendors

**Date**: 2026-10-01 (Thursday; inferred from "tomorrow is Friday")
**Attendees**: Alana Sihelská (BigHub, STK-004), Jura Brázdil (BigHub, STK-026), Marek Pillár (BigHub, STK-001) — Radim Švarc (TEO, STK-041) and Michaela "Míša" Albrechtová (TEO, STK-042), in the Brno room. Tomáš Burda (STK-025) didn't join.
**Type**: external
**Recording**: N/A (transcript, ~25 min, Czech/Slovak)
**Previous session**: [2026-09-22 TEO/OCR technical sync](2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal.md)
**Meeting prep**: N/A

> **Transcript note**: the Brno room shows up as one speaker ("CZ Brno Titanium…"), covering both Radim and Míša; they are attributed here by content. Marek's lines (email reply, platform proposals) were labelled "Alana Sihelská".

## TL;DR

The offline route agreed on 2026-09-22 is working. BigHub processed both autumn batches it received (Termetal, Rakun), with Excel and JSON output.
- **Rakun:** 84 protocols, 18 fields flagged for review, **no silent errors**, ~4 fixes.
- **Míša:** "a huge help", even before full automation.
- **Cost:** ~0.50–0.60 Kč per page for Termetal/Rakun, ~2 Kč for the harder Spedos; ~1 Kč per page on average. Everyone considers this negligible against the value.

**Next:** TEO sends Spedos autumn, a smaller vendor and, from October–November, the big air-conditioning batch. Jura processes them best-effort. Possible additions: a pass/fail flag and device/inspection names.

**Infra:** services are being deployed on the test environment, running automatically there in ~2 weeks (under VPN). Production still depends on BDC.

**Marek:** he'll send platform/initiative proposals by the end of the week to prepare for the spring cycle, then review them with Radim and consult with Burda.

**Next sync:** Wednesday 2026-10-14, 13:00.

**Continuity with 2026-09-22**:
- "Bezručova" is closed: the street had changed.
- Číselník gaps are decided: **connect to the API** rather than update the list manually.
- The offline first batch Jura owed was delivered, plus a second one.

## Key Discussion Points

### Recap and results (Alana, Jura, Míša)

Alana recapped last week:
- The Bezručova (Mělník) case was a street-name change.
- Missing addresses will be solved by **connecting to the API**, not by maintaining the číselník (branch list).
- Because infra looks bleak, TEO and BigHub exchange this autumn's protocols offline.

TEO sent two batches (last week and yesterday). Jura returned results incl. JSON; the JSON for yesterday's batch is still to come.

**Rakun batch**: 84 protocols, 18 fields flagged for review, no silent error; about 4 needed fixing (odd sevens read as twos). Míša checked everything: "when it's highlighted in colour, it's great… it was read very well" [translated from Czech]. She is converting the output into her import form for TEO's system. The "wheel" (full automation) isn't working yet, but "even this is a huge help" [translated from Czech].

**The "address outside the číselník" from last time** was actually a **wrong address written by the supplier**: a non-pharmacy address. The tool caught a real error Míša hadn't noticed. The číselník is current and stays as is.

**Radim**: built his Excel from the JSON; image filtering and sorting works (in Jura's file too). He is almost ready and needs yesterday's JSON plus the zip structure; Jura sent the zip during the call.

### Cost per page (Jura)

- Termetal ~0.50 Kč per page, Rakun ~0.60 Kč per page.
- The harder spring Spedos batch ~2 Kč per page; Jura believes it can be pushed down on the next batch.
- Across both autumn batches plus Spedos spring: **~1 Kč per page on average**. Radim and Míša: "fine for us".

### Next batches and scope

**Míša:**
- Will send **Spedos autumn**, a **smaller vendor** and the **air-conditioning** protocols (the big batch, October–November; one PDF with ~100 documents expected by the end of next week).
- Smaller vendors (a few pharmacies) she can handle "the old way". The big ones (50–100 pharmacies) help most.
- Many vendors' protocols carry **no address at all**. It's too late to change that this autumn, but for **spring** she will push technicians and vendors to write an ID number or an address on every protocol so it can be matched.

**Jura:**
- Send anything, in any format (zip, PDF); he builds for non-uniform input.
- Best-effort given heavy infra firefighting, with no promise of the same quality. A hard case like Spedos may need more time. When it's simple, "it's more or less free for us".
- Currently reads primarily **date and address**, so other device types work too.
- Could add fields such as device count or EPS systems: "think about what helps you most".
- He offered to try a **pass/fail flag** ("vyhovuje ano/ne") on current batches.

**Míša on air-conditioning protocols:**
- **Four protocols per pharmacy**, each with a different name, which could be tricky.
- She will send a guide listing the device and inspection names as they must appear for the import.
- These are TEO's own protocol templates, so names are consistent. There is a dedicated **defects (závady) field**, handwritten but in one place, which should make pass/fail easier than for automatic doors.

### Infrastructure (Jura)

- Services are being deployed on the **test environment**, alongside platform changes for reporting and **cost management**.
- Sober estimate: **~2 weeks until it runs automatically on test** (under VPN).
- **Production** is still in extensive negotiation with BDC. A call with Láďa Tvarůžek follows right after this meeting.

### Business value and platform proposals (Marek)

**BQ:** Marek replied to Radim's email. Reducing the volume from 13,000 to 10,000 items barely changed the quantified benefit. Jura answered the cost question today. The tracker for Tomáš Dudaško doesn't need every cost line, and a few hellers per page don't distort the business value.

**Platform proposals:** Marek is putting together ideas for moving the initiative forward, getting it "into nicer shape" for the spring cycle, since the process runs twice a year: "do autumn well, spring nicer" [translated from Slovak]. He'll send them **by the end of this week**, review them with Radim early next week, then consult Tomáš Burda. Radim agreed.

**Cost visibility:**
- **Burda's concern** (via Radim): he wants platform costs tracked, so TEO isn't hit by "hundreds of thousands a year" with nothing to defend itself with.
- **Jura:** the platform will have per-use-case **cost management/tracking** in one place, plus configurable **spending caps** so an automated run can't run away.
- **Radim:** at ~2 Kč per document × 10,000–12,000 documents a year, the operating cost is small.
- **Marek:** against low-hundreds-of-thousands in value, ~50k in cost is fine.

### Next meeting

The team agreed to meet again in two weeks, once there are results on the new batches: **Wednesday 2026-10-14, 13:00** (Radim is busy Tuesday afternoon). Alana sends the invite. In between, communication goes via Teams, and Míša sends protocols as they arrive.

Side notes: Jura has a physics-faculty AI conference tomorrow (Friday). He said MaxBuddy, the chatbot and Lexie are now live on the platform, apart from some certificates.

## Decisions Made

- **Offline processing continues** for the autumn 2026 cycle: TEO sends batches in any format, and BigHub returns Excel + JSON on a best-effort basis.
- **Číselník gaps are solved by connecting to the pharmacy API**, not by manual updates. The číselník stays as is (it's current).
- **Cost per page (~0.50–2 Kč, ~1 Kč on average) is acceptable** to both sides. The platform will provide per-use-case cost tracking and spending caps.
- **Extraction focus stays on date + address.** Pass/fail and device/inspection names are candidate additions, pending Míša's naming guide.
- **Next sync: 2026-10-14, 13:00**.

## Action Items

- [ ] **Jura Brázdil**: Deliver the JSON for yesterday's batch (zip sent during the call) — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Michaela Albrechtová**: Send Spedos autumn, the smaller vendor's protocols, and the air-conditioning batch (~100-document PDF, by end of next week) — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Michaela Albrechtová**: Send the guide/list of device and inspection names required for TEO's import (air-conditioning protocols) — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Jura Brázdil**: Process incoming batches best-effort; try a pass/fail (vyhovuje ano/ne) flag on current batches — due before 2026-10-14 — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Radim Švarc**: Finish the Excel build from JSON on yesterday's batch — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Marek Pillár**: Send Radim platform/initiative proposals for the spring cycle — due 2026-10-02 (end of week); review with Radim early next week, then consult Tomáš Burda — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Alana Sihelská**: Send the invite for the next sync, 2026-10-14 13:00 — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors
- [ ] **Michaela Albrechtová**: For spring 2027, push technicians/vendors to put an ID number or address on every protocol — due spring 2027 — from 2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors

## Open Questions

- Which extra fields (pass/fail, device count, EPS systems, inspection names) help TEO most?
- When will production run, given the BDC negotiation? Test is ~2 weeks out.
- Can the Spedos cost (~2 Kč per page) be brought down on the autumn batch?
- Tomáš Burda's view on the costs and on Marek's spring proposals (he didn't attend).

## Sentiment & Tone

Warm, practical and noticeably positive, the best tone of the TEO series so far. Míša was openly grateful ("a huge help", "every bit of help is welcome"), and Radim was engaged and self-driven on his Excel. Both treated BigHub's work as real value even without full automation. Jura was relaxed but candid about his infra load and set expectations honestly (best-effort, no quality promise on new vendors). The cost topic was defused quickly: Burda's worry about runaway costs came up, and Jura's answer (cost tracking + caps) was accepted. Marek positioned the next step (spring proposals via Radim, then Burda) in line with the Radim-first path ([[ASM-166]]).

## Routing Log

Confirmed by PM on 2026-10-01 (confirm all).

- **project-assumptions**: ASM-218–ASM-222; update notes on ASM-129, ASM-165, ASM-130, ASM-120, ASM-127
- **project-knowledge**: TEO/OCR entry
- **project-stakeholders**: STK-041, STK-042, STK-026, STK-025
- **project-daily**: 1 PM-owned item added; Blob-storage reconcile resolved; others' items stay in this note
