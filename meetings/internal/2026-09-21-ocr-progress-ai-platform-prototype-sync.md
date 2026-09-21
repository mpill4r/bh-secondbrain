---
last_updated: 2026-09-21
type: internal
attendees: [Marek Pillár, Jura Brázdil, Alana Sihelská]
recording_link:
---

# TEO/OCR Dev Progress, AI Platform Prototype & Max Chatbot Updates with Jura Brázdil

**Date**: 2026-09-21
**Attendees**: Marek Pillár (BigHub, AI Analyst), Jura Brázdil (Dev — TEO/OCR, MaxBuddy, Max Chatbot, AI Platform), Alana Sihelská (BigHub, outgoing PM — STK-004)
**Type**: internal
**Recording**: N/A (transcript provided directly)
**Previous session**: No direct previous instance of this attendee combination found in `meetings/index.md`; content connects to and extends `2026-09-16-teo-ocr-technical-sync-pilot-results.md` (pilot results, vendor naming, Michaela Albrechtová's bug reports) and `2026-09-21-ai-platform-vision-discovery-dudasko.md` (same-day, earlier — this session is Marek relaying that call's outcome to Jura and starting execution on it).
**Meeting prep**: N/A

> **Note on date**: no explicit date was stated in the transcript. 2026-09-21 is inferred with high confidence from direct references to "we called Dudaško again this morning" (matching today's `2026-09-21-ai-platform-vision-discovery-dudasko` call) and the Wednesday 2026-09-23 UX-brief deadline discussed there — please correct if wrong.

## TL;DR

A wide-ranging internal working session covering three threads. **TEO/OCR**: Jura walked through concrete pipeline improvements (classify-against-known-branch-list instead of forced verbatim transcription, candidate-alternative disambiguation for ambiguous dates/addresses) that roughly doubled the "clean, no review needed" rate on both spring and autumn batches; surfaced an unresolved AKS node-pool connectivity blocker with Vladislav Tvarůžek/BDC, and worked through ServiceNow export scope (BigHub hands off clean structured data via API, Radim's team owns the review UI and export — not committing to build that export). **AI Platform**: Jura had already built, unprompted, a working prototype of exactly the role-based landing/consolidation concept Dudaško described to Marek and Jindřich this morning — validates Phase 1 is technically straightforward as a first pass (consolidate existing interfaces into one shell, not a redesign). **Surfaced a real conflict** worth resolving before the Wednesday brief goes final: Marek states Dudaško wants external tools embedded *inline* within the platform, which contradicts the "deep link out, no embedding" framing captured in this morning's Dudaško meeting and already written into the Jura design brief. **Max Chatbot**: Jura also shipped unprompted UX polish (URL-aware contextual prompts, a star-rating feedback widget, an editable tone prompt) — Alana flagged budget/scope discipline given none of it was formally requested.

## Key Discussion Points

### 1. TEO/OCR — from forced transcription to candidate disambiguation

Jura's core pipeline change this week: instead of forcing all reader models to transcribe an address or date character-for-character and flagging disagreement, the system now (a) extracts what it can read (e.g. a city name), (b) looks up the known branches for that city, and (c) asks the model to classify against that list rather than transcribe freehand. Where the four-model ensemble still disagrees, instead of just flagging "needs review," the system now surfaces 2-3 ranked candidate values (e.g. two plausible dates, or two plausible branch addresses) for the human reviewer to pick from via a dropdown, rather than requiring a blind re-transcription.

- **Jura Brázdil**: "Jediný co se dá udělat, je prostě jim říct: je tady těhle těch pět poboček, vyberte si, která to je, protože já to nemám šanci zjistit." [translated from Czech]
- Root cause for the hardest cases: some source documents give only a city with no street, stamp, or center number at all (e.g. Havířov, 5 branches) — genuinely unresolvable without a human picking from candidates.
- Root cause for digit misreads: Czech handwriting crosses the digit 7, which international OCR models read as confused with 1 or unusual glyphs — Jura tried explicit prompting and reference-image examples; neither fully fixed it, so disambiguation-by-candidates is the practical mitigation instead.
- Marek endorsed the approach directly: "Mne to príde super... on sa ťa spýta a dá ti tri možnosti a úplne super podľa mňa." [translated from Slovak]
- Confidence mechanism, as it exists today: four independent model reads must fully agree (including the weakest model, GPT-5.4 mini) for a field to be marked clean/no-review-needed. **Jura Brázdil**: "Jedinej confidence rating, kterej máme, je to, že proběhnou opravdu čtyři čtení různejma modelama, a ve chvíli, kdy se všechny čtyři shodnou... tak víme, že to je určitě správně." [translated from Czech]
- Marek surfaced a compounding failure mode and a fix Jura is already implementing: when the four models disagree *and* their best-supported answer still isn't in the branch directory, that's two separate problems worth flagging distinctly — Jura's in-progress fix pre-checks the branch directory and feeds the model 2-3 real candidate addresses up front, rather than surfacing a raw disagreement.

### 2. TEO/OCR — the correction feedback loop must flow back to BigHub

Alana raised a requirement that applies globally across every OCR field, not just dates/addresses: whatever Radim's team's reviewers pick or correct in their own interface needs to be captured and sent back to BigHub via API, so accuracy can be measured over time and fed back into improving the pipeline.

- **Jura Brázdil**: agreed this is the best way to improve the system going forward and confirmed it's not a technical problem on BigHub's side — the data model (per-field flags, bounding box, alternates) already supports adding a correction field. The ask needs to be made explicitly to Radim's team as they build their review interface, since it doesn't happen automatically.

### 3. TEO/OCR — measured accuracy improvement (internal only, not yet shared with client)

Back-testing the new pipeline (informed by weekend experimentation with a paid "Astra" GPT model Jura will not use in production — too expensive — but which helped him improve the pipeline they do use) against both existing batches:
- **Spring batch**: clean/no-review-needed rows rose from 74 to 114 out of 188 (~54% improvement).
- **Autumn batch**: rose from 47 to 61 out of 140.
- One previously-reported "silent" error (a misread number flagged earlier by Michaela Albrechtová, STK-042) was found and fixed — traced to an oversized bounding-box crop; tightening the crop resolved it.
- Alana cautioned against surfacing these specific internal numbers to the client before they're externally validated. Jura agreed — plans to deliver a visibly cleaner result without quoting exact percentages, to avoid setting expectations that later need walking back.
- Separately confirmed: the duplicate-write bug in the "závady" (defects) field that Michaela Albrechtová (referred to as "paní Míša") flagged is fixed and does not reproduce in the new protocol version.
- A new pilot-vendor batch (city examples discussed: Havířov, Holice) surfaced the same address-resolution gap. Jura referred to this vendor inconsistently as "Spedos" mid-conversation — **this is a third name variant on top of the already-tracked "Racun"/"Thermetal" open item** (see Open Questions).

### 4. TEO/OCR — infra blockers: Blob storage and AKS node-pool connectivity

- **Blob storage**: Alana asked whether the TEST-environment Blob storage (to be self-provisioned per ASM-088) is ready. Jura clarified it isn't built yet — the platform manages Blob storage per use-case via its own provisioning (possibly Helm charts/manifests), and he needs to check whether he can safely provision the space ahead of a full deploy without breaking anything. Technically feasible, not yet confirmed.
- **AKS node-pool connectivity — still unresolved, now a repeated blocker**: Jura still cannot reach OpenAI/platform services from the new node pool (forbidden/timeout), while the same calls work fine from the old node pool. He sent Vladislav Tvarůžek precise reproduction steps and a specific address list last Friday; as of today, no confirmation anyone has actually tested it the way Jura described (Vladislav's earlier claim that "it works" came from someone else's report, possibly checked against the old cluster). Alana committed to chasing this with BDC before tomorrow's meeting.

### 5. TEO/OCR — ServiceNow export: BigHub will not own this

Alana raised the next product-scope gap: ServiceNow export is Phase 2 and currently undefined. Jura pushed back on BigHub committing to build it:
- His preferred model: a review interface (he already has a working left/right-comparison version he built for his own testing) where a human confirms the data is clean and correct, in exactly the shape ServiceNow expects (no flags, no metadata, just clean fields) — but **Radim's team is the one building this interface and owns that final step**, not BigHub.
- **Jura Brázdil**: "Nesliboval bych, že budeme dělat exporty... přijde mi to takové na hlavu." [translated from Czech] — reasoning: promising an export now risks BigHub ending up on the hook for a ServiceNow-side build whose shape (e.g. can ServiceNow even host image crops?) isn't yet known.
- Agreed approach: BigHub hands Radim's team everything it knows per document via API — values, confidence flags, alternates, bounding boxes — and Radim's team owns the review UI and the ServiceNow export from there. If Radim's team explicitly asks BigHub to build the export later, once the final clean-data format is confirmed, that's a separate future ask, not something to volunteer now.
- Alana separately flagged, as an open strategic question rather than a decision: once this pilot (3 vendors, automatic-door protocols only) proves out, worth identifying the next highest-leverage document/equipment category (e.g. air-conditioning) to extend into — not resolved today.

### 6. AI Platform — Jura already built the Phase 1 prototype

Marek relayed this morning's Dudaško call (see `2026-09-21-ai-platform-vision-discovery-dudasko.md`) — unified entry point, role-based landing, no selector needed. Jura had, independently and before being asked, already built a working prototype of almost exactly this:
- Login with a Microsoft/Entra-backed profile; a user with access to only Lexie lands directly in Lexie.
- A user with multiple roles (e.g. Lexie admin + Max Chatbot CC access) sees a small hub/switcher between their tools.
- A "super admin" role sees everything, plus technical/ops status info (e.g. whether pipelines are running).
- **Jura Brázdil**: "Krok číslo jedna je to funkčně dostat na jedno místo s nějakou navigací rozumnou, jednoduchoučkou a pak dopřepsat ty jednotlivý komponenty, jo, abychom nemuseli tady dělat vyloženě šílenej design přes sedm projektů." [translated from Czech] — Phase 1, as he frames it, is purely consolidating already-built interfaces into one navigable shell (tabs), with per-app visual redesign deliberately deferred to a later pass — consistent with the phasing already agreed with Dudaško (ASM-115) and with the design-authority sequencing Jura and Jindřich agreed back on 2026-09-10 (Lexie design-compromise ticket, consolidate-first).
- Hosted on Jura's personal Cloudflare account, PIN-protected. Explicitly not functionally wired to real services — a clickable, mocked prototype, sufficient for Marek to hand to Dudaško as a design deliverable, not a working build, ahead of Wednesday.
- Marek's plan: review the prototype and leave feedback notes; treat this as the Wednesday deliverable rather than building something separate from scratch.

### 7. AI Platform — open conflict: inline embedding vs. deep-link-out

Marek flagged a requirement he plans to formalize: **"on vlastne všetky tie služby chce mať inline... že by sa ti otvárali v rámci toho celého rozhrania"** [translated from Slovak] — i.e. Dudaško wants external tools to open *inline*, within the platform's own interface, not just link out to a separate URL.

**This directly conflicts with what this morning's Dudaško meeting captured and what's already written into the Jura design brief** (`documents/internal/2026-09-21-ai-platform-design-brief-jura-brazdil.md`): tools with their own separate frontend get a "deep link out... no embedding." Jura's own existing prototype design assumes the inline model for anything browser-accessible ("u těch use caseů, který jsou přístupný přes browser, tak se počítá s tím, že tam se přímo dostaneš inline... protože seš na jedný webovce s jedním URL a tam naviguješ na všechno" [translated from Czech]) — so Jura's build and Marek's stated plan already lean inline, while the design brief and ASM-113 currently say deep-link-out. **This needs explicit PM resolution before the brief is finalized** — flagged in Open Questions and the Routing Review below.

One clear exception either way: MaxBuddy has no standalone web service (it's Farmis-integrated), so it only ever gets a demo view inside the platform, regardless of which model is chosen for the rest.

### 8. Max Chatbot — unprompted UX polish

Jura demoed several small features built in the same work cycle as ongoing bug fixes:
- **URL-aware contextual prompts**: without requiring explicit user input, the chatbot infers context from the page URL and proactively offers relevant help — e.g. on a pharmacy-locator page it offers to show nearby pharmacies (using geolocation); on an orders page it offers order lookup by number; on an eRecept page it offers lookup by identifier; on a product page it offers to check stock, including resolving which single pharmacy has all items in stock for a multi-item eRecept.
- **Star-rating feedback widget**: replaced an in-chat-message rating prompt with a persistent, collapsible 1-5 star control docked at the top of the chat; rating and free-text feedback are both stored, feedback surfaces with a copyable ticket ID for the X-Manager.
- **Editable tone/character prompt**: exposed per-browser-session (not centrally persisted) so tone can be tested without a redeploy.
- **Guardrail check**: tested with an off-topic request (a pancake recipe) — the bot correctly declined and redirected to pharmacy-relevant help, confirming the existing "won't help outside pharmacy scope" guardrail still holds.

### 9. Budget and scope discipline

Alana flagged, without it being a live problem yet, that Jura should keep Jindřich looped in on budget and avoid unrequested extras. Jura's response: the additions above were incidental, bundled into an existing feedback-triage cycle rather than separately billed scope. Marek raised a related but distinct concern — more shipped features mean a larger surface for hallucination/bugs, which compounds testing and feedback-loop burden even if the build itself was cheap. Jura acknowledged this, noting the changes so far were simple ones.

## Decisions Made

1. TEO/OCR disambiguation shifts from forced verbatim transcription to classify-against-known-branch-list, surfacing 2-3 ranked candidate values to the human reviewer via API rather than requiring blind re-transcription on disagreement.
2. Correction feedback from Radim's team's review interface must flow back to BigHub via API so OCR accuracy can be tracked and the pipeline improved over time — to be explicitly requested of Radim's team, not assumed.
3. BigHub will not commit to building the ServiceNow export. It hands Radim's team complete structured data (values, confidence flags, alternates, bounding boxes) via API; Radim's team owns the review UI and the ServiceNow export, unless explicitly asked otherwise later once the clean-data format is confirmed.
4. AI Platform Phase 1 execution approach validated hands-on by Jura: consolidate already-built per-project interfaces into one navigable, role-based-landing shell (tabs) — no per-app visual redesign yet. Deliverable for Wednesday is a clickable but non-functional prototype (already built, Cloudflare-hosted), not a working build.
5. **Not decided — flagged as a conflict needing PM resolution**: whether external tools with a browsable interface should open inline within the platform shell (Marek's read of Dudaško's ask, and Jura's existing prototype assumption) or via deep link out with no embedding (this morning's Dudaško meeting notes and the current design brief). See Open Questions and Routing Review.

## Action Items

- [ ] **Alana Sihelská**: Check with Vladislav Tvarůžek/BDC before tomorrow's meeting whether anyone has actually tested the AKS node-pool connectivity issue Jura reported last Friday — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] **Jura Brázdil**: Check whether TEO/OCR's TEST-environment Blob storage can be self-provisioned on the platform ahead of a full deploy, without breaking anything — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] **Jura Brázdil**: Continue tuning OCR bounding-box/crop accuracy and complete the candidate-list disambiguation approach for dates and addresses; re-run against full spring/autumn batches — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] **Marek Pillár**: Write up and send Jura the platform requirement on external-tool access (inline vs. deep-link — pending resolution of the conflict flagged above) — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] **Marek Pillár**: Click through Jura's AI Platform prototype and leave feedback notes, aiming for tomorrow — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] **Marek Pillár / Jura Brázdil**: Explicitly ask Radim Švarc's team to persist and send back reviewer corrections via API so OCR accuracy can be measured and improved over time — from 2026-09-21-ocr-progress-ai-platform-prototype-sync
- [ ] **Marek Pillár / Alana Sihelská**: Resolve the pilot-vendor naming ambiguity — a third name variant ("Spedos") surfaced today alongside the already-tracked "Racun"/"Thermetal" open item — from 2026-09-21-ocr-progress-ai-platform-prototype-sync

## Open Questions

- **Inline embedding vs. deep-link-out for external platform tools** — Marek's stated read of Dudaško's ask (inline) conflicts with this morning's Dudaško meeting notes and the current Jura design brief (deep link, no embedding). Needs explicit PM resolution — see Routing Review.
- Whether the "Spedos" name (today's transcript) is a third variant of the already-ambiguous pilot-vendor naming ("Racun"/"Thermetal") or a genuinely separate, unrelated supplier — not resolved on this call.
- Which document/equipment category to target next after the current 3-vendor automatic-door pilot proves out (e.g. air-conditioning) — raised by Alana, not decided.
- Whether Radim's team will ask BigHub to build the ServiceNow export once their own review interface and the clean-data format are finalized — open, contingent on their build.

## Sentiment & Tone

Productive, technical, and good-humored working session with no real friction. Jura was candid and specific about both progress (measurable accuracy gains, a working AI Platform prototype built ahead of being asked) and open problems (the AKS blocker, remaining crop/bounding-box tuning, digit-misread limitations he hasn't fully solved). Alana played a light PM-oversight role — budget caution, chasing the AKS blocker, keeping ServiceNow scope bounded — without any tension with Jura. Marek was engaged throughout, synthesizing Jura's technical descriptions into product framing (the candidate-disambiguation UX, the inline/deep-link conflict) rather than just receiving updates.

## Routing Log

Routed on PM confirmation, 2026-09-21 (conflict resolved via explicit question — external tools open inline, not deep-link):

- **project-assumptions**: ASM-119 (OCR candidate-disambiguation approach), ASM-120 (correction feedback loop via API), ASM-121 (ServiceNow export stays with Radim's team); updated ASM-113 (external tools open inline, not deep-link — same-day correction to this morning's entry)
- **project-stakeholders**: STK-026 (Jura Brázdil) — OCR progress, AKS blocker, AI Platform prototype, chatbot polish; STK-004 (Alana Sihelská) — PM-oversight actions (feedback loop, ServiceNow scope, AKS chase, budget flag)
- **documents/internal**: updated `2026-09-21-ai-platform-design-brief-jura-brazdil.md` acceptance criteria and open questions to reflect inline embedding
- **project-daily (2026-09-21)**: 7 action items added
- **meetings/index.md**: entry added

