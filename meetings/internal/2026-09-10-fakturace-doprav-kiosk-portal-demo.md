---
last_updated: 2026-09-10
type: internal
attendees: [Filip Černý, Jan Sovka, Jindřich Tůma, Jakub Turner, Alana Sihelská]
tldv_link:
---

# Fakturace Doprav Kiosk Portal Demo & Review

**Date**: 2026-09-10
**Attendees**: Filip Černý (Dev, demoing), Jan Sovka (Escalation/account), Jindřich Tůma (PM/coordination lead), Jakub Turner (Dev), Alana Sihelská (Outgoing PM). Marek Pillár and a "Lukáš" (surname unstated — likely Lukáš Szücs or Lukáš Starenko) were excused/absent.
**Type**: internal
**Recording**: N/A (transcript provided as text, no tldv link)
**Previous session**: N/A — new thread (relevant prior context: ASM-036, Fakturace doprav's 2026-09-07/08 roadmap review)
**Meeting prep**: N/A

## TL;DR

Filip Černý demoed the Fakturace doprav (freight invoicing) document-scanning kiosk portal end-to-end — automatic classification by AR number/barcode, confidence-flagged OCR extraction, versioning, and route status transitions — to strong reception from Jan Sovka. The team surfaced two real gaps: the portal currently has zero authentication (anyone can walk up and upload anything straight to the LLM, with no injection/security review), and Filip's demo used a faked page-count value he'd wrongly assumed came from Axapta — it doesn't, only document counts do, so expected-page-count validation needs a real solution. Filip closed with a running list of open business questions for the client (stamp-validation scope, kiosk touchscreen vs. keyboard, cross-document-context OCR, an unexplained document type) still to be sent.

## Key Discussion Points

### Portal demo — upload, classification, OCR (Filip Černý)

Walked through the live portal: intro screen, a mocked login (no real auth behind it), and the main upload screen (UI designed by "Honza Skubou" `[name uncertain in transcript]`). Demoed uploading a "záznam o provozu vozidla" (ZOPV, vehicle-operation record) — the app auto-extracts driver name, plate, delivery date, etc. Documents are classified by AR number; currently hand-stamped for testing since real barcodes aren't live yet, with a further testing round expected once barcodes land (not seen as a risk). Barcode reads happen almost instantly; if no barcode is present (e.g. "noční závoz"/night-delivery documents), the app falls back to reading the printed AR number. Filip's hard line: every document must carry at least a computer-printed AR number — a handwritten-only AR number would be unacceptable. Jan Sovka confirmed, per Petr Sláma's latest input, that barcodes won't always be present but a printed AR number always will be.

Processing is fully asynchronous — pages can arrive out of order (e.g. page 5 before page 3) and the app correctly reassembles the right document. A key feature is confidence-flagging on OCR reads, especially handwriting: uncertain reads are explicitly marked "zkontrolujte" (please verify) for human review. Filip's accuracy philosophy: "read it right, or clearly flag that you're not sure" — never silently guess, particularly on stamps and handwriting, the hardest part `[translated from Czech]`. He noted one license plate he still can't decipher himself and plans to warn the client that if a human can't read it, the app won't either.

Once a route's documents are uploaded, it moves to either manual review (on uncertainty, or a page/stamp-count mismatch) or "připravena fakturace" (ready for invoicing), which can proceed without human review. The driver reviews an on-screen confirmation table of everything uploaded/extracted, can add an optional note to the route, and submits — intended to eventually trigger an email confirmation to the carrier.

### Confirmation-screen scope question (Jan Sovka)

Jan Sovka liked the demo overall — "nekopíruje se původní design a tohle přijde ještě funkčnější" ("it's not just copying the original design, and this comes across as even more functional") `[translated from Czech]` — but flagged that the full confirmation table, notes field, and review-before-send flow go beyond what was actually specified with Jan Žižka; Žižka's side had indicated a bare "we received documents from the carrier" confirmation would likely be enough, no extra input. He asked Filip to demo it as-is to the client but explicitly ask whether they want to keep the richer version, rather than assume it's wanted. Filip agreed to raise it.

### Open-access / authentication gap (Alana Sihelská, Jakub Turner, Jindřich Tůma, Jan Sovka)

Alana asked about the "Jan Novák" placeholder shown on the login screen — Filip clarified there's no real login, it was mocked; he wasn't sure one was needed. Jan Sovka confirmed the intended model: anyone can walk up to the kiosk and start uploading documents, mirroring today's physical process. Jakub Turner and Jindřich Tůma both pushed back that fully open access can't be right — uploads go straight to the LLM with no validation that the content is even a real document, a genuine risk surface since "it's on the infra directly, on the LLM — literally anything can get through" `[translated from Czech, Jakub Turner]`. Jan Sovka's fallback: a large disclaimer, plus an assumption that someone will be supervising the kiosk in person, at least initially — he conceded it was a fair point. Alana pushed further: could drivers at least enter something like a license plate so it isn't fully anonymous? Jan Sovka said the client's posture so far has been indifferent to driver identification. Left unresolved.

### Axapta page-count assumption error (Alana Sihelská, Jakub Turner, Jan Sovka, Filip Černý)

Alana asked Filip to confirm his earlier claim that per-document page counts come from Axapta. Live in the demo, Filip realized he'd actually been showing a hardcoded/faked count ("4 z 5") rather than a real Axapta value — Jan Sovka called it out directly: "to je cheating" ("that's cheating") `[translated from Czech]`. Correcting the record: Axapta only returns document *counts* per type (how many night-delivery, OPIATY, ZOPV documents are expected per route), not page counts. Jan Sovka explained the actual plan: Axapta holds each route's original unfilled document templates; BigHub would need to derive expected page counts from those originals directly — or, better, have Dr. Max supply page counts themselves going forward. Jakub Turner questioned whether page-count is even the right completeness signal at all versus just confirming the right document *types* were submitted, since printing/handling could shift page counts without anything actually being wrong. Filip's rationale for tracking pages: so a reviewer can tell if, say, page 3 of a multi-page document is specifically missing. No resolution — flagged as a direct question for the client, alongside a fifth, still-unexplained document type: "POPLSOL," a bulk/collective document Filip hasn't figured out how to process yet.

### Document-type validation vs. security (Jakub Turner, Filip Černý, Alana Sihelská, Jindřich Tůma)

Filip confirmed the app already classifies document type and rejects/flags anything that doesn't match an expected type ("nerozpoznáno") — the kiosk can reject, discard, or lock in response. Jakub Turner argued this solves "don't accept garbage" but does *not* address prompt-injection risk (adversarial text embedded in an uploaded image, aimed at the LLM) — that remains unaddressed. Consensus: type-validation ≠ security review of the LLM-facing surface; Jindřich flagged the latter as something to explore separately. Filip volunteered to actually try uploading something inappropriate during testing rather than assume the outcome.

### Kiosk hardware and workflow design (Jan Sovka, Filip Černý, Jakub Turner)

Kiosk hardware (scanner + PC) is expected to be Dr. Max's own procurement responsibility — likely repurposing whatever the person currently processing this manually already uses — a position BigHub has pushed hard to keep on the client's side. Filip's own open business question: touchscreen vs. keyboard/mouse for the kiosk UI, which materially affects design and is still unanswered (Alana noted Tereza Foltová previously said she'd raise this with "pan Kim"/"keem" `[name uncertain in transcript]`).

Jan Sovka pushed for a more automated scan→save flow — ideally the scanner pushes pages directly into shared storage without a manual "scan next document" click. Filip clarified current behavior: each scan uploads to storage *and* triggers processing simultaneously (not pulled back from storage). Storage design: raw individual pages are stored separately per scan session; on driver confirmation, pages are assembled and named as a complete document (e.g. "Scan session 10.9 v 9 hodin, trasa AR154, ZOPV" / "...rozvozový list") — effectively split into "raw" and "complete" groupings alongside the generated confirmation record. Jakub Turner raised a reliability concern (drawing an analogy to phone-scanning apps mis-ordering pages) about whether scans should sit in-memory for review before committing to storage, since committed pages are harder to clean up later if something goes wrong mid-batch (e.g. 50 pages at once). Filip's counter: the physical scanner is hardware-constrained to one A4 page per pass, which limits how messy input can get compared to phone-camera scanning.

### Error handling / versioning (Jindřich Tůma, Filip Černý, Jan Sovka)

Jindřich asked: if a driver scans 20 documents and realizes the 5th was scanned wrong, what happens? Filip: depends on the failure mode. If the page just has unwanted content, versioning kicks in — rescanning the same page creates a new version, both are retained, but the new one is marked authoritative. If the scan is fundamentally unusable (unclear what document it even is), it's rejected as invalid outright. A third case: a document scanned against a route already "ready for invoicing" or already invoiced gets flagged/rejected as belonging to a closed route. Jan Sovka confirmed this matches the original spec — rescanning is allowed while the original version is preserved. Filip flagged that thorough testing of these edge cases and versioning is still in the backlog, given how fast the build has moved.

### Filip's open business questions for the client (Filip Černý)

A running list, not yet sent to Dr. Max:
1. Stamps on documents aren't always pharmacy-confirmation stamps (example: a stamp just noting "fridge was between -2°C and 7°C") — hard to tell programmatically which stamps matter; wants to ask whether validating every stamp type is actually necessary or if scope can narrow.
2. Whether it's acceptable to use cross-document context to improve OCR accuracy — driver name and plate are often barely legible on the ZOPV record itself but appear cleanly printed elsewhere in the same document set, so cross-referencing could meaningfully cut handwriting error rates even though the exact format isn't standardized. Alana flagged a wrinkle: per spec, drivers can still manually change route/plate assignments for edge cases, so a hard cross-reference match can't be absolute — Filip's plan is a fuzzy/approximate match rather than exact, specifically because of this.
3. What "POPLSOL" is and how it should be processed (see above).
4. The confirmation-screen scope question (see above).

## Decisions Made

- OCR confidence-flagging philosophy is fixed: read a field correctly, or explicitly flag it as uncertain for human review — never silently guess.
- Documents without a barcode always fall back to a computer-printed AR number as the minimum machine-readable identifier; handwritten-only AR numbers are unacceptable.
- Route status model confirmed: routes move to manual review (on uncertainty or page/stamp mismatch) or "ready for invoicing" (can proceed without human review) once documents are uploaded.
- Re-scanning a page creates a new version while preserving the original; documents belonging to an already-invoiced route are rejected — matches the original spec agreed with Jan Žižka.
- Kiosk hardware (scanner + PC) stays Dr. Max's procurement responsibility, continuing the position already pushed to the client.
- Filip's earlier claim that Axapta returns per-document page counts was incorrect — confirmed live during the demo to have been hardcoded/faked. Axapta only returns document counts per type; expected page counts still need a real solution (deriving them from Axapta's stored unfilled originals, or asking Dr. Max to supply them directly).

## Action Items

- [ ] **Jindřich Tůma**: Set and hold to a 2-4 week delivery timeline for this project — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Jan Sovka**: Push forward the disclaimer/access-control approach for the fully open kiosk (no login) with the client — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Jan Sovka**: Firm up and close the data-contract question with Axapta on document counts vs. page counts — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Filip Černý**: Test uploading unrelated/inappropriate documents to see how the app behaves — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Filip Černý**: Continue hardening document versioning and error-state handling (in backlog) — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Filip Černý**: Compile and send the running list of open business questions to the client (stamp-validation necessity, kiosk touchscreen vs. keyboard, cross-document-context OCR assist, POPLSOL document type, confirmation-screen scope vs. original Žižka spec) — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Jakub Turner / Jindřich Tůma**: Assess the LLM prompt-injection risk on uploaded documents, separate from the document-type validation already in place — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Alana Sihelská / Jan Sovka**: Resolve whether minimal driver identification (e.g. license-plate entry) is needed at the kiosk, given the open-access concern — from 2026-09-10-fakturace-doprav-kiosk-portal-demo
- [ ] **Alana Sihelská**: Follow up on the touchscreen-vs-keyboard kiosk question with "pan Kim" per Tereza Foltová's earlier comment — from 2026-09-10-fakturace-doprav-kiosk-portal-demo

## Open Questions

- Whether the richer confirmation-screen/notes feature is something Dr. Max actually wants, or exceeds the original Žižka spec — unconfirmed with the client.
- Whether page-count tracking is the right completeness signal at all, vs. just document-type presence (Jakub Turner's concern) — unresolved.
- What "POPLSOL" is and how it should be processed — Filip doesn't yet understand it.
- Whether any driver identification will be required at the kiosk, or whether open access + disclaimer is acceptable to the client.
- "Pan Kim"/"keem" — name uncertain in the transcript; likely a Dr. Max IT/kiosk-hardware contact, needs verification.
- "Honza Skubou" (credited with the portal UI design) — name uncertain in the transcript, doesn't clearly match any known stakeholder; needs verification.

## Sentiment & Tone

Internal, technical, high-energy working session — genuine enthusiasm for the demo ("Pěkný, super, super" from Jan Sovka) balanced by direct, unfiltered peer critique (Jakub Turner repeatedly pressing on security/architecture gaps; Jan Sovka calling out the faked page-count data live: "to je cheating"). Filip took the pushback well throughout, conceding points readily ("chápu, úplně chápu", "to je moja chyba"). Casual, informal register (heavy slang) throughout reinforces this was a low-stakes internal build review, not a client-facing meeting.

## Routing Log

Confirmed 2026-09-10 (all items, reconciled jointly with the same-day external ViaPharma demo — see that meeting note for the corrected Axapta state-ownership finding, which retired this note's page-count-vs-document-count concern). Written:
- **project-assumptions**: ASM-051 (OCR/AR-number design confirmed), ASM-052 (kiosk open-access risk), ASM-055 (kiosk hardware ownership) — jointly sourced with the external demo
- **project-stakeholders**: enriched STK-006 (Filip Černý)
- **project-daily** (2026-09-10): 6 action items added
