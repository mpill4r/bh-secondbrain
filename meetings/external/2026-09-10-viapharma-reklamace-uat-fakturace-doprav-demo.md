---
last_updated: 2026-09-10
type: external
attendees: [Jindřich Tůma, Jakub Turner, Jan Sovka, Filip Černý, Tereza Foltová, Jana Egrmaierová, Petr Sláma, Jan Žižka]
tldv_link:
---

# ViaPharma Sync — Reklamace UAT Timeline & Fakturace Doprav Client Demo

**Date**: 2026-09-10
**Attendees**: Jindřich Tůma (PM/coordination lead), Jakub Turner (Dev), Jan Sovka (Escalation/account), Filip Černý (Dev, demoing) — BigHub. Tereza Foltová, Jana Egrmaierová, Petr Sláma (Reklamace half), Jan Žižka (Fakturace doprav half, joined ~30 min in) — ViaPharma CZE. Jan Kopecký was expected but did not attend.
**Type**: external
**Recording**: N/A (transcript provided as text, no tldv link)
**Previous session**: [2026-09-03-viapharma-logistics-status-reklamace-demo](2026-09-03-viapharma-logistics-status-reklamace-demo.md)
**Meeting prep**: N/A

## TL;DR

Two-part recurring ViaPharma sync, extended to a full hour. The Reklamace half got genuinely tense — Petr Sláma pushed back hard on BigHub's proposed short testing windows, clarifying his team needs to validate downstream Axapta financial/logistics effects, not just app UX, and has limited September capacity due to two unrelated GoLive projects; landed on starting full-scope UAT October 15–16 through October 2. The Fakturace doprav half was Filip's first live demo of the kiosk portal to Jan Žižka, who gave concrete, largely positive feedback and delivered a major architecture clarification that resolves earlier internal confusion: **Axapta — not the BigHub app — is the sole source of truth for route/document state**, so the app doesn't need to hold or reconcile any status of its own.

## Key Discussion Points

### Part 1: Reklamace

#### Excel data consolidation status (Tereza Foltová, Jana Egrmaierová)
Tereza and Jana continue consolidating ~3–4 source tables into one; data doesn't fully reconcile yet. They plan to eventually socialize the cleaned table with more carriers, but that step won't block deployment — they'll launch with whatever version they land on and treat further cleanup as an internal follow-up. Aiming to show progress to Filip next Tuesday; wants a short (~10–30 min) working session with Filip specifically, since he knows the reklamace domain best, rather than a broader team walkthrough.

#### Test access & certificate (Jakub Turner, Jindřich Tůma)
Waiting on an "EGRES" certificate from Dr. Max's infra side (Vladislav Tvarůžek) before BigHub can share test access — targeting this Friday, though Tvarůžek is stretched across AKS and other projects. Tereza requested a short (~10 min) live walkthrough call once access is shared, rather than just an access email, so the ViaPharma side isn't stuck on basic login questions.

#### UAT timeline negotiation — the core tension (Petr Sláma, Jindřich Tůma, Jakub Turner, Jana Egrmaierová)
Jindřich presented a draft 2–4 week rolling timeline (explicitly framed as adjustable, not final) for phase 1/1.1. Petr Sláma pushed back hard: he'd understood testing to mean validating the *entire* reklamace flow end-to-end including downstream Axapta financial/logistics effects — not just clicking through the app UI — and said 2 days is nowhere near enough; he estimated 14+ days needed given ~18 process variants recently surfaced in a separate internal VMS meeting, plus a need to involve Finance (constrained by their own close-out schedules) to verify financial impacts. He's also personally capacity-constrained in September due to two unrelated GoLive projects.

Jakub Turner clarified BigHub's model: testing is split per released feature — last week's scan-only demo is what should be tested now (document scanning + Axapta write, already confirmed correct with Jan Kopecký over the past two weeks); document-generation and email-generation are separate, later UAT rounds, still in development. He pushed back that Sláma's "2 days" framing was about the *first* narrow feature slice, not the full flow, and that a longer window is fine and can run in parallel with continued development.

Jan Sovka reframed to reduce anxiety: each numbered timeline row maps to a specific feature scope, not "everything" — row 7 won't include document generation yet, that arrives ~5 days later at row 11, etc. — so Sláma should read each row's scope literally rather than assume full functionality at every stage.

Sláma maintained that full-flow UAT (through email generation) and the narrower scan-only UAT can't run fully in parallel for his team, given no extra testing headcount (just him and Jana) — full testing should start only once scan-only testing concludes. Jindřich acknowledged this is genuinely the client's call: parallel testing shortens the overall project timeline, sequential lengthens it, and either is fine — BigHub just needs an actual dated timeline to plan around.

**Landed date**: full-functionality UAT to start October 15–16 (pending final dev completion), targeting completion by October 2, with an implicit buffer already built in. Sláma committed to reporting blockers to BigHub continuously during testing rather than batching them.

#### Reklamace–Axapta API detail gap (Petr Sláma, Jan Sovka)
Sláma flagged that current documentation doesn't cover API sequencing/behavior between the reklamace app and Axapta in enough operational detail to safely start backend development against it. Jan Sovka believed Sláma's written feedback had already been incorporated into the doc; Sláma clarified he'd only received acknowledgment of his comments, not an actual doc update. Resolved by scheduling a dedicated walkthrough session next week (Jindřich/Jakub with Sláma) before backend work proceeds further.

### Part 2: Fakturace doprav — live client demo

#### Portal demo to Jan Žižka (Filip Černý)
Filip re-ran essentially the same portal demo already reviewed internally (see the 2026-09-10 internal Fakturace Doprav Kiosk Portal Demo note) directly for Jan Žižka — upload/classification by AR number, asynchronous multi-document scanning, page-count tracking, OCR of ZOPV driver records, route status transitions, document versioning on rescans, and the end-of-session confirmation table with attached scans.

#### Open-access kiosk confirmed acceptable (Jan Žižka, Jakub Turner)
Žižka's first reaction: no driver login is correct — anyone should be able to walk up and start uploading documents. Jakub Turner still flagged the same security caveat raised internally (fully open access means BigHub can't be responsible for what gets uploaded directly to their infra/LLM) and suggested capturing a minimal identifier (e.g. license plate) per scan session for post-incident traceability. Žižka was skeptical any driver would attempt anything malicious but said he'd raise it internally.

#### Driver-confirmation email — mailbox overload risk (Jan Žižka, Jakub Turner)
Žižka's real concern: if every scan session emails a confirmation with attached scans to a carrier contact, that could mean 20+ emails/day with attachments, risking mailbox limits over time. Jakub Turner confirmed images are already compressed client-side (kilobyte-range, not large files) and considers one consolidated email per session preferable to a storage-link approach, which Žižka rejected outright (carriers shouldn't get storage access). Considered low-risk once compression is confirmed; Žižka asked BigHub to keep attachments as small as technically possible.

#### Confirmation detail: page numbers, not just counts (Jan Žižka)
Žižka pushed back on the confirmation table only showing e.g. "2 of 7" pages submitted — he wants specific missing page numbers (e.g. "pages 4–5 missing") so a dispatcher facing a driver dispute can point to exactly what's missing. Filip agreed this is a reasonable, low-effort change.

#### Standardized field formats (Jan Žižka)
Žižka asked that extracted fields (date format, plate format, etc.) be normalized across document types before landing in ViaPharma's downstream Excel — inconsistent formats currently cost his team cleanup time. Filip agreed this is straightforward and simply hadn't been a stated requirement before now.

#### Major architecture clarification: Axapta owns all state (Jan Žižka, Filip Černý, Jakub Turner, Jan Sovka)
A significant misunderstanding surfaced and got resolved live. Filip had believed the app needed to track its own internal route-completion state and push a manual-review / ready-for-invoicing status to Axapta. Žižka clarified this is backwards: **Axapta is the sole source of truth for route/document state** — his team needs a row to appear in Axapta the moment the *first* document for a route arrives (so they have reaction time to chase a slow-to-report carrier before month-end close), and the app should simply forward whatever gets scanned, whenever it gets scanned, without holding or reconciling status itself. If a driver scans a route's documents across multiple sessions, Axapta handles pairing them — not the app. This resolves Filip's earlier confusion (he'd read the spec/Swagger as requiring the app to send a manual-review/ready-for-invoicing status) and, per Filip, genuinely simplifies the app's design since it no longer needs to hold state at all.

One follow-on requirement: Žižka wants the driver-facing UI to show a running history of what's been scanned for a route so far (a completeness indicator, not full previews) — which now requires the app to query Axapta for that history on demand, since it holds no state itself. Filip flagged this needs validation against what Axapta's API can actually return, and likely implies a Swagger change.

#### Kiosk hardware (Jan Žižka, Filip Černý, Jakub Turner)
Hardware sourcing (scanner + PC) is confirmed as ViaPharma's IT responsibility, though Žižka has no personal visibility into it and will loop in his own IT colleague and Petr Sláma — flagging an internal "who owns the kiosk" gap on their side. Filip will send a same-day written hardware proposal/minimum-spec recommendation (touchscreen preferred, screen large enough for document review, no keyboard needed — see below) so ViaPharma's IT has something concrete to act on. In the meantime, testing will happen without real hardware — ViaPharma will use their own local scanner and upload files manually, skipping the physical-scan step. Three warehouse locations exist; not expected to require different technical handling, just correct per-site configuration.

#### Driver notes feature — rejected (Jan Žižka)
Explicitly rejected an optional driver-note field floated earlier: drivers would use it inconsistently, creating manual-review noise with no clear payoff — a driver with a real problem should call ViaPharma directly. Confirms no keyboard is needed on the kiosk, only touchscreen.

#### Language support — deprioritized (Jan Žižka)
Czech-only is fine for now; demand for other languages could arise only if the concept expanded to other countries, not a near-term need.

#### POPLSOL document type clarified (Jan Žižka)
Confirmed: POPLSOL is a warehouse-transfer document ("pendl mezi skladovejnou"); the only requirement is matching it to the correct route and confirming it's the right document type — no further data extraction needed. Resolves Filip's open question from the internal demo.

#### Temperature logs & future GPS integration (Jan Žižka, Jan Sovka)
Žižka will send sample temperature-log slips for testing. Confirmed the longer-term vision (already discussed) is fully electronic temperature data pulled via GPS-tracker APIs, but that transition is a 2–3 year process even with budget already allocated — paper temperature slips need to be supported in parallel indefinitely, not replaced outright.

#### Driver override of AI reads — rejected (Jan Žižka)
Asked whether a driver should be able to manually flag a document for review if they disagree with a read. Žižka: no — leave it to the system's own confidence flagging; ViaPharma resolves any resulting manual-review cases on their end.

#### Cross-document-context OCR — substantially resolved via a new ZOPV form (Jan Žižka)
Filip's open question from the internal demo (using cleanly-printed name/plate elsewhere in a document set to disambiguate illegible ZOPV handwriting) was largely superseded: Žižka revealed ViaPharma is independently building a new standardized ZOPV form (with Petr Sláma's team) that will print pre-filled data and attach to the rozvozový list — leaving only kilometers driven as a manual field (drivers are paid by distance, and actual mileage can vary from the fixed route distance). Žižka expects this to cover 80%+ of cases cleanly, eliminating most of the illegible-handwriting problem at the source.

## Decisions Made

- Full-functionality reklamace UAT (through email generation) starts October 15–16, targeting completion by October 2 — sequential-vs-parallel testing was explicitly left to Petr Sláma's judgment.
- Reklamace–Axapta API sequencing needs a dedicated walkthrough session before further backend development — current documentation is insufficiently detailed.
- **Axapta is the sole source of truth for Fakturace doprav route/document state** — the BigHub app holds no state of its own and simply forwards scanned documents as they arrive; Axapta reconciles multi-session submissions. Specification/Swagger to be updated accordingly.
- Kiosk stays fully open-access (no driver login) — confirmed acceptable by the client.
- Driver-note field rejected — out of scope.
- Confirmation table will show specific missing page numbers, not just fractional counts.
- Extracted field formats (dates, plates) will be standardized across document types.
- Kiosk UI: touchscreen only, no keyboard.
- Language support stays Czech-only for now.
- POPLSOL confirmed as a warehouse-transfer document requiring only route-matching, no further extraction.

## Action Items

- [ ] **Filip Černý**: Hold a short working session with Tereza Foltová on the reklamace Excel consolidation, targeting next Tuesday — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Vladislav Tvarůžek**: Deliver the EGRES certificate so reklamace test access can be shared — due this Friday — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Jindřich Tůma**: Hold a short live walkthrough call with Tereza Foltová/Jana Egrmaierová once test access is shared — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Jindřich Tůma / Jakub Turner**: Schedule and run a dedicated Reklamace–Axapta API walkthrough session with Petr Sláma next week — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Petr Sláma**: Report testing blockers to BigHub continuously during UAT rather than batching them — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Filip Černý**: Update the Fakturace doprav spec/Swagger to reflect that Axapta (not the app) owns all route/document state — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Filip Černý**: Validate with Axapta's API what history/status data it can return, to support the driver-facing "what's been scanned so far" view — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Filip Černý**: Send a same-day kiosk hardware proposal/minimum-spec recommendation to Jan Žižka — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Jan Žižka**: Identify an internal kiosk-hardware owner (with Petr Sláma) and act on Filip's spec recommendation — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Jan Žižka**: Send sample temperature-log slips for testing — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Filip Černý**: Standardize extracted field formats (dates, plates) across document types — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo
- [ ] **Filip Černý**: Update the confirmation table to show specific missing page numbers instead of fractional counts — from 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo

## Open Questions

- Whether a minimal driver identifier (e.g. license plate) will actually be implemented for kiosk traceability, or the kiosk stays fully anonymous — Žižka non-committal, taking it internally.
- Exact kiosk hardware spec and who owns procurement at ViaPharma — unresolved, action item pending.
- Whether the driver-facing "scan history" feature is technically feasible against Axapta's actual API — needs validation, may require a Swagger change.
- The earlier internal-demo open question about Axapta page-count vs. document-count validation is likely superseded now that Axapta is confirmed to own all state — worth reconciling explicitly when routing.

## Sentiment & Tone

Two distinct tones in one call. The Reklamace half ran genuinely tense at points — Petr Sláma pushed back firmly and repeatedly on being asked to commit to a testing timeline he felt was unrealistic and under-communicated, invoking real capacity constraints and a note of frustration with shifting expectations ("teď najednou chcete ze mě rozhodnutí, že teď rychle udělat plán" — "now you suddenly want a decision from me, to make a plan quickly" `[translated from Czech]`). Jindřich de-escalated well, repeatedly clarifying BigHub wasn't pressuring a specific answer and handing the timing decision back to the client — the exchange ended constructively with a landed date and Sláma's own commitment to continuous blocker reporting.

The Fakturace doprav demo to Jan Žižka, by contrast, was warm, low-friction, and highly productive — Žižka engaged substantively with every question Filip raised, gave clear opinionated answers, and proactively surfaced useful context BigHub didn't have (the new standardized ZOPV form, the Axapta state-ownership model) that meaningfully de-risked the build. A genuinely collaborative first client demo.

## Routing Log

Confirmed 2026-09-10 (all items, reconciled jointly with the same-day internal Fakturace Doprav Kiosk Portal Demo note). Written:
- **project-assumptions**: ASM-051 (OCR/AR-number design, joint source), ASM-052 (kiosk open-access risk, joint source), ASM-053 (Axapta owns all state — retires the internal note's page-count concern), ASM-054 (confirmation-screen scope), ASM-055 (kiosk hardware ownership, joint source), ASM-056 (reklamace UAT timeline), ASM-057 (reklamace-Axapta API gap)
- **project-stakeholders**: enriched STK-002 (Jan Sovka), STK-003 (Jindřich Tůma), STK-006 (Filip Černý, joint source), STK-007 (Jakub Turner), STK-013 (Tereza Foltová), STK-015 (Jan Žižka), STK-034 (Petr Sláma); resolved STK-044 name uncertainty to "Jana Egrmaierová"
- **project-knowledge**: updated Axapta entry (state-ownership clarification); added Fakturace doprav document-types entry
- **project-daily** (2026-09-10): 12 action items added
