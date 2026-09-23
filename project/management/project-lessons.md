---
last_updated: 2026-09-24
last_updated_by: auto — project-meeting routing (2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers, 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting)
owner: Marek Pillár
---

# Lessons Learned

---

### LL-056

| Field | Value |
|-------|-------|
| ID | LL-056 |
| Created | 2026-09-24 |
| Category | relationship-management |
| Source | 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers |

**Lesson**
When a client-side contact starts attributing a scope or delivery change to "the vendor doesn't want to do X," calibrate the narrative directly and explicitly with them as soon as it's noticed, rather than letting it propagate informally through the team's various contacts — and ask the team to flag it centrally rather than each person quietly correcting it their own way.

**Context**
Tereza Foltýnová had been telling multiple Reklamace stakeholders that BigHub didn't want to deliver certain functionality, when the real cause was a scope reframe (AI to digitization). Jindřich ran a direct calibration meeting with her and Petr Spilka to correct it, and asked the whole team to route any future instances through him rather than resolve them individually.

**Cross-reference**
[[ASM-122]], STK-013 (Tereza Foltýnová)

---

### LL-055

| Field | Value |
|-------|-------|
| ID | LL-055 |
| Created | 2026-09-24 |
| Category | client-management |
| Source | 2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting |

**Lesson**
When demoing a system with more capability than what's being shown, show less now and let more come later rather than surfacing everything up front — revealing too much too early (e.g. a fully autonomous agent) can invite the client to demand it immediately, derailing a deliberately staged rollout.

**Context**
Jura independently proposed building a cross-platform RAG "ask anything" agent into the AI Platform prototype. Both he and Marek agreed to keep it in reserve rather than demo it to Dudaško now, given only ~3 projects are currently active — offering it only if Dudaško asks for more than the navigation-based approach already shown.

**Cross-reference**
[[ASM-146]]

---

### LL-054

| Field | Value |
|-------|-------|
| ID | LL-054 |
| Created | 2026-09-23 |
| Category | delivery-process |
| Source | Fakturace doprav redline review, this session |

**Lesson**
Before finalizing or presenting a client-facing spec for an initiative with an existing codebase, run a direct code audit against every "promised," "planned," or "confirmed decision" claim in the spec — not just against the roadmap tracker. Stakeholder-reported status (even from the developer) can lag or contradict what's actually deployed in both directions: things marked "still missing" can already be built, and things marked "decided" (like an architectural ownership split) can be quietly not what the code does. The gap is invisible from meeting notes and the spec text alone.

**Context**
A single code audit on Fakturace doprav's `transport_invoicing_api`/`_web` found 5 real contradictions: the kiosk requires login despite being told to the client as open-access; document versioning is fully local despite a recent "Axapta owns it" conclusion; the AR pairing key already works for document types marked as still missing it; a document type marked "confirmed in code" is actually unreachable from OCR; and multi-vehicle routes silently overwrite data instead of being rejected or flagged. Several of these directly affect what's already been communicated to the client.

**Cross-reference**
[[ASM-131]], [[ASM-132]], [[ASM-133]], [[ASM-134]], [[ASM-135]]

---

### LL-053

| Field | Value |
|-------|-------|
| ID | LL-053 |
| Created | 2026-09-23 |
| Category | harness |
| Source | 2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal |

**Lesson**
When new meeting notes appear to contradict a very recent, well-documented decision, record the contradiction as an open item needing direct reconciliation with the original decision-maker — don't silently overwrite the old decision, and don't ignore the new note either. A single secondhand data point (especially from condensed notes rather than a full transcript) isn't strong enough evidence to flip a decision on its own.

**Context**
Two apparent reversals surfaced in the same TEO/OCR sync: a rejection of multi-candidate disambiguation output seemed to contradict ASM-119 (decided one day earlier), and a Blob storage/BDC dependency note seemed to contradict ASM-088 (decided a week earlier). Both were logged as new, open assumptions flagging the conflict rather than treated as automatic supersessions.

**Cross-reference**
[[ASM-128]], [[ASM-129]]

---

### LL-052

| Field | Value |
|-------|-------|
| ID | LL-052 |
| Created | 2026-09-22 |
| Category | discovery-methodology |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |

**Lesson**
When a stakeholder gives an illustrative business-value estimate but explicitly refuses to have it treated as a formal, accepted business case (often to protect their own team's headcount or interests), don't push them to accept the number as official — instead add a separate, harder KPI that doesn't depend on their cooperation with the original framing.

**Context**
Simona Mertová (Dr. Max CC) gave FTE-avoidance figures for Max chatbot/Maxie/Lexie but explicitly refused to let them be used as an accepted business case, worried it could justify cutting her operators' headcount. Rather than negotiate her past that objection, Jindřich added a second, measured KPI (actual request-handling volume × a reduction target) that stands independently of her FTE framing.

**Cross-reference**
[[ASM-124]]

---

### LL-051

| Field | Value |
|-------|-------|
| ID | LL-051 |
| Created | 2026-09-22 |
| Category | project-management |
| Source | 2026-09-22-ai-portfolio-business-value-review-reklamace-reframe |

**Lesson**
A bottom-up dollar-value model can understate the priority of an initiative whose real leverage comes from scale/compounding effects (e.g. a small per-unit gain applied across a very large item count) — cross-check any dollar-ranked priority order against direct stakeholder consensus before treating the model's ranking as final.

**Context**
A quarter's modeled dollar figure ranked Listing (~34M Kč/year) below MaxBuddy and Max/Maxie in this session's portfolio priority review, but the PM and multiple client-side stakeholders (Honza Sovka, Alana Sihelská, Petr Neuman) consistently maintain Listing should be the top priority, arguing the model doesn't capture the compounding value of even small per-item gains at Dr. Max's ~10,000-SKU scale.

**Cross-reference**
[[ASM-125]]

---

### LL-050

| Field | Value |
|-------|-------|
| ID | LL-050 |
| Created | 2026-09-21 |
| Category | AI/ML review-interface design |
| Source | 2026-09-21-ocr-progress-ai-platform-prototype-sync |

**Lesson**
When an AI extraction system can't resolve a field with full confidence, surfacing 2-3 ranked, validated candidate answers for a human to pick from beats either forcing a blind verbatim re-transcription or just flagging "needs review" with no guidance — it's faster for the reviewer and more accurate than an open-ended re-guess.

**Context**
TEO/OCR's date and branch-address fields were often ambiguous from source documents (crossed digit 7s misread across models, cities with multiple branches and no other identifying detail). Switching from "transcribe exactly, flag on disagreement" to "classify against a known candidate list, offer alternatives" measurably improved clean/no-review rates (~54% on the spring batch) without requiring better source documents or a better base model.

**Cross-reference**
[[ASM-119]]

---

### LL-049

| Field | Value |
|-------|-------|
| ID | LL-049 |
| Created | 2026-09-21 |
| Category | Cross-team collaboration |
| Source | 2026-09-21-ocr-progress-ai-platform-prototype-sync |

**Lesson**
A correction/feedback loop between two teams' systems doesn't happen automatically just because the technical capability (e.g. an API) exists — it requires an explicit, named ask to the other team, made before they build their own side of the interface, or the loop quietly never gets built.

**Context**
BigHub's TEO/OCR system can accept reviewer corrections back via API and use them to measure/improve accuracy over time, but Radim Švarc's team building their own review interface wouldn't send that data back unless BigHub explicitly asks for it as a requirement — raised proactively by Alana Sihelská before Radim's build was finalized, not after.

**Cross-reference**
[[ASM-120]]

---

### LL-048

| Field | Value |
|-------|-------|
| ID | LL-048 |
| Created | 2026-09-21 |
| Category | relationship-management |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |

**Lesson**
A stakeholder who has been burned by past unmet promises values fast, partial, visible progress over a delayed polished deliverable — bias toward shipping something concrete, open questions and all, on a short explicit cadence rather than waiting until it's "ready."

**Context**
Jindřich's read of Tomáš Dudaško immediately after this call: right vision, but visibly worn down by predecessors over-promising and under-delivering. His explicit ask was UX mockup variants by Wednesday — even incomplete — rather than a complete result later in the week.

**Cross-reference**
STK-010 (Tomáš Dudaško), ASM-115

---

### LL-047

| Field | Value |
|-------|-------|
| ID | LL-047 |
| Created | 2026-09-21 |
| Category | scoping |
| Source | 2026-09-21-ai-platform-vision-discovery-dudasko |

**Lesson**
When a stakeholder's concern sounds like it requires expanding your team's ownership, test it against one concrete incident before agreeing to take on more — it often surfaces an existing internal channel already responsible for that piece, narrowing the actual commitment rather than expanding it.

**Context**
Jindřich raised a general worry (are pharmacists actually adopting MaxBuddy?) that could have implied BigHub needed end-to-end rollout ownership. Citing one specific incident (a confused pilot pharmacist) got a precise answer from Dudaško: that's the job of Dr. Max's own training center and expert-group leads ("osmec"), not BigHub — capping the adoption campaign's real scope to awareness/comms.

**Cross-reference**
ASM-117, project-knowledge (Expertní skupiny, Osmec, Tréninkové centrum)

---

### LL-046

| Field | Value |
|-------|-------|
| ID | LL-046 |
| Created | 2026-09-18 |
| Category | Data quality / stakeholder review |
| Source | PM (BQ_Final.xlsx OCR/TEO row) |

**Lesson**
When two figures meant to describe the same quantity in a source document don't reconcile (e.g. a stated total-effort baseline vs. a volume × per-unit-time calculation that implies a very different total), don't silently pick one and present a clean number — surface both readings, the size of the gap, and the plausible reasons for the mismatch, and let the PM decide which basis to use (or whether to hold for confirmation from the source stakeholders).

**Context**
The OCR/TEO business-quantification row gave both "~40 hours/month total manual effort" and "~250 docs/week at ~10 min/doc" as inputs to the same savings calculation — the second implies ~180h/month, roughly 4.5× the first. Rather than picking one, the discrepancy was flagged with reasoning options (current vs. future-scope volume, non-uniform per-document time, stale estimate) and put to the PM, who resolved it as a current-state-vs-future-target distinction rather than a data error — preserving the ~273,000 Kč/year figure with an explanatory note instead of a silently wrong number or an unexplained flag.

**Cross-reference**
`BQ_Final.xlsx` (All Products (Updated), row 8)

---

### LL-045

| Field | Value |
|-------|-------|
| ID | LL-045 |
| Created | 2026-09-17 |
| Category | Client negotiation |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |

**Lesson**
When a client holds firm on a launch/delivery date for risk-management reasons, resist countering with your own preferred date. Instead, split the commitment into an internal milestone you control (which you can push to be as early as reasonably possible) and the client-facing date they asked for (which you accept as-is) — then earn the option to pull the public date in through demonstrated quality, rather than negotiating for it upfront.

**Context**
Jura pushed for an end-of-September public launch; Mertová held firm on end of October, citing thin test coverage (only 4 sample e-recepty tested) and an explicit "we'd rather launch late than lose trust" framing. Jindřich didn't contest this — he reframed BigHub's commitment as hitting its own 3 internal deployment phases by end of September, with the public date staying October unless Mertová herself chose to move earlier. This resolved a real point of friction cleanly, with no forced agreement, and preserved the client's ownership of risk tolerance on a decision (public website launch) where a bad outcome would be highly visible.

**Cross-reference**
[[ASM-100]]

---

### LL-044

| Field | Value |
|-------|-------|
| ID | LL-044 |
| Created | 2026-09-17 |
| Category | Client coaching / feedback elicitation |
| Source | 2026-09-17-lexie-max-maxie-weekly-sync |

**Lesson**
When asking a non-technical/non-design client for input on a UX or design change, explicitly ask for the *problem* (what's broken, missing, or frustrating — ideally with a screenshot or recording) rather than the *solution*. Framing it this way prevents the client from prescribing an implementation that may conflict with existing design standards, and gives the delivery team room to solve it properly.

**Context**
Jindřich reopened the long-deferred Lexie design-refresh ask by requesting Dr. Max articulate concrete pain points rather than proposed changes. Marek reinforced this explicitly on the call: *"my nepotrebujeme vedieť riešenie od vás, my potrebujeme zistiť, čo je váš problém... iba definujte ten problém, maximálne s nejakým screenshotom, možno screen recordingom."* Accepted without pushback, and gave the team (Kadlecová) a concrete, bounded next step (a "vibe check" exercise) instead of an open-ended design conversation.

**Cross-reference**
Meeting: 2026-09-17-lexie-max-maxie-weekly-sync (Lexie design/UX refresh)

---

### LL-043

| Field | Value |
|-------|-------|
| ID | LL-043 |
| Created | 2026-09-17 |
| Category | business-quantification interviewing |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |

**Lesson**
When a business owner proposes an ambitious KPI target for an untested first version, surfacing the downside of overpromising (what happens if real performance lands well short of it) prompts more calibrated self-correction than directly arguing the number is unrealistic.

**Context**
Mertová first proposed a 90%-contained / 10%-escalated target for Maxie's voicebot. Rather than pushing back on the number itself, Marek pointed out that publicly committing to only 10% escalation risks looking bad if actual performance lands closer to 30%. Mertová immediately and voluntarily revised down to a 50/50 placeholder, explicitly flagging it as provisional — no further debate was needed.

**Cross-reference**
2026-09-17-business-quantification-cc-max-maxie-lexie; ASM-094

---

### LL-042

| Field | Value |
|-------|-------|
| ID | LL-042 |
| Created | 2026-09-17 |
| Category | stakeholder sentiment |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie, 2026-09-17-business-quantification-maxbuddy-vosmek |

**Lesson**
When a stakeholder proactively vetoes a value-framing before it's even proposed to them (e.g., rejecting "time saved therefore fewer people needed," or an employee-satisfaction claim), treat it as a protective/ownership signal worth capturing directly — not noise to filter out of the deliverable. It usually means the stakeholder anticipates internal resistance and is shielding their team.

**Context**
In two back-to-back interviews the same day, both business owners independently and unprompted rejected a framing the interviewer hadn't yet suggested: Mertová refused to let Lexie's ~30 min/day time-savings estimate be read as grounds for headcount cuts, and Vosmek explicitly excluded employee satisfaction as a MaxBuddy value driver, anticipating real staff pushback. Both were noted in Sentiment & Tone rather than smoothed over in the business-value fields.

**Cross-reference**
2026-09-17-business-quantification-cc-max-maxie-lexie; 2026-09-17-business-quantification-maxbuddy-vosmek; ASM-095

---

### LL-041

| Field | Value |
|-------|-------|
| ID | LL-041 |
| Created | 2026-09-17 |
| Category | business-quantification framing |
| Source | 2026-09-17-business-quantification-cc-max-maxie-lexie |

**Lesson**
For a channel serving fixed-size, largely inelastic demand (e.g., a call center covering a fixed customer base), adding a new self-service channel does not reduce total volume — the value is capacity/coverage increase and reduced staff cognitive load, not FTE/cost savings. Forcing an FTE-savings framing onto a fixed-volume system produces a business case the owner will rightly reject.

**Context**
Mertová was explicit, for both Max chatbot and Maxie, that Dr. Max's call center handles a roughly constant volume of calls regardless of which self-service channels exist — when one topic is deflected, another fills the gap, since the center serves the whole pharmacy network. She and Marek agreed the honest framing is "serves more customers at the same headcount, with lower cognitive load on staff," not "needs fewer agents."

**Cross-reference**
2026-09-17-business-quantification-cc-max-maxie-lexie; ASM-092

---

### LL-040

| Field | Value |
|-------|-------|
| ID | LL-040 |
| Created | 2026-09-16 |
| Category | harness |
| Source | project-daily-2026-09-16 (Fakturace doprav spec rebuild) |

**Lesson**
When a deliverable's whole point is faithful coverage of a source (every comment on a document, every item on a roadmap), verifying "all of X incorporated" by spot-checking a representative sample is not sufficient — real gaps hide in exactly the items not sampled. Default to a systematic, enumerated pass (check item 1, item 2, ... item N against the output) rather than a plausible-looking subset, whenever fidelity-to-source is the deliverable's core requirement.

**Context**
While rebuilding `2. Fakturace doprav.docx`, an initial claim of "all screenshots/comments reviewed and incorporated" held up under a PM spot-check of one specific comment, but a full systematic re-check of all 20 original Word comments (only prompted by that spot-check) found one genuine gap (comment #17, a Q1/Axapta dependency note) that sampling-based review had missed. The same pattern repeated one step later at the roadmap-table level: a claim the doc "matched the roadmap" wasn't wrong on the sampled items the PM had checked before, but a full comparison found 8 of 13 Plná verze/Nice to Have items missing entirely.

**Cross-reference**
project-daily-2026-09-16; ASM-090; [[LL-025]]

**Recurrence (2026-09-17, Listing client-doc rebuild)**: A third instance, different mechanism. A regex-based removal of Word comment-reference XML (stripping `commentRangeStart`/`commentReference` runs before building a client-facing copy) silently over-matched near dense comment clusters and deleted real paragraph/table content — including an entire section (heading, intro text, two API-endpoint tables, 16 rows) — with no error, no visible symptom, and a document that still opened and "looked right." Went undetected through several further rounds of edits until the PM asked for a full diff-check against the original, which used a systematic sequence-alignment comparison (Python's `difflib`) rather than a spot-check and immediately surfaced four separate missing spans. Reinforces the lesson at the mechanism level too: any regex or pattern-based bulk edit on structured/XML content should be verified with a full structural diff against the pre-edit original immediately after running it, not deferred until a symptom appears or a spot-check happens to hit the damaged area.

**Cross-reference**
project-daily-2026-09-17; [[LL-025]]

---

### LL-039

| Field | Value |
|-------|-------|
| ID | LL-039 |
| Created | 2026-09-16 |
| Category | transcript reliability |
| Source | 2026-09-16-devops-kanban-rollout-status-sync |

**Lesson**
Automated speaker diarization can silently collapse multiple real speakers into one label — often the first/loudest voice detected — especially when several attendees share one room or microphone channel. A transcript that looks cleanly attributed can still be substantively wrong; when a speaker's attributed content doesn't match their known role (e.g. deep technical commitments attributed to a PM in handover), that mismatch is a signal worth checking against context before writing anything into the record, not dismissing as an oddity.

**Context**
In this meeting's transcript, nearly all substantive content across three different topics (Fakturace doprav/Reklamace technical work, an order-prediction status update, a Listing update) was labeled "Alana Sihelská" — despite her tracked role being an outgoing PM in handover, not a developer. Content-matching against each topic's established owner (Filip Černý, Juraj Kmec, Marek Pillár respectively) and direct PM confirmation reassigned all three. Alana's actual presence/role in the meeting was left unconfirmed rather than guessed further.

**Cross-reference**
See `meetings/internal/2026-09-16-devops-kanban-rollout-status-sync.md` and the earlier same-day TEO/OCR technical sync, which had a separate (lower-stakes) speaker-identity ambiguity.

---

### LL-038

| Field | Value |
|-------|-------|
| ID | LL-038 |
| Created | 2026-09-16 |
| Category | validation methodology |
| Source | 2026-09-16-teo-ocr-technical-sync-pilot-results |

**Lesson**
Running a blind test against real, unmodified historical data — rather than only a curated benchmark/test set — surfaces bugs and edge cases that controlled test sets miss, precisely because nobody has had a chance to tune around them yet.

**Context**
BigHub ran TEO/OCR's extraction pipeline, untouched, against a real 2025 dataset spanning the 2 pilot vendors. This surfaced 2 concrete bugs the curated test set hadn't caught — a duplicated defects-text field, and a protocol with a genuine error that should have been, but wasn't, flagged for review — alongside confirmation that overall accuracy held up (in fact ran a few points higher, though possibly partly luck).

**Cross-reference**
See the "TEO / OCR" entry in `project-knowledge.md` and [[ASM-088]].

---

### LL-037

| Field | Value |
|-------|-------|
| ID | LL-037 |
| Created | 2026-09-16 |
| Category | knowledge-base staleness |
| Source | 2026-09-16-teo-ocr-solution-proposal-variants, 2026-09-16-teo-ocr-accuracy-validation-cost-analysis, 2026-09-16-teo-ocr-production-spec-v1-1 (routing session) |

**Lesson**
Internal engineering/delivery progress can significantly outpace a PM's own knowledge-base entry when the work happens on a parallel technical track without an explicit sync-back step. A status recorded as current at the time of writing can go stale within days if nobody flags "this changed" back to the PM — don't assume a status untouched for ~1-2 weeks is still accurate on a fast-moving workstream; proactively ask engineering-adjacent contacts for a progress check before treating a knowledge-base status as ground truth.

**Context**
`project-knowledge.md`'s TEO/OCR entry described the pipeline as "still a local feasibility prototype ... not deployed anywhere" per the 2026-09-07 portfolio review. Four internal BigHub documents dated July-August 2026 (surfaced 2026-09-16) showed the pipeline had already reached validated, production-grade accuracy (91%/94% across all 7 document categories, 0 fabricated values across 500+ pages) with an agreed v1.1 architecture dated 2026-08-07 — predating the "still a prototype" status by about a month. The gap likely existed because this engineering work wasn't discussed in any processed meeting between 2026-09-07 and 2026-09-16.

**Cross-reference**
See [[ASM-076]], [[ASM-077]], [[ASM-078]] and the "TEO / OCR" entry in `project-knowledge.md`.

---

### LL-036

| Field | Value |
|-------|-------|
| ID | LL-036 |
| Created | 2026-09-16 |
| Category | tooling / harness reliability |
| Source | 2026-09-16-business-quantification-listing-petr-neuman (routing session) |

**Lesson**
Writing directly to a cloud-synced Office file (OneDrive/SharePoint) with a scripting library while that same file is open live in the desktop app is unreliable — the app's own AutoSave can silently re-sync its in-memory state over the on-disk change shortly after, discarding the edit with no error. Always verify the write by re-reading the file back immediately after saving, and if it didn't stick, ask the user to avoid touching/saving the file for a short window (or close it) before retrying — don't assume a successful `save()` call means the change persisted.

**Context**
A first attempt to fill the Listing row in `businessQuantificationWorskop.xlsx` (OneDrive-synced, open live in Excel with AutoSave on) appeared to succeed via openpyxl, but a screenshot moments later showed the old content still there. Re-reading the file confirmed the write had been silently reverted. The fix was a second write followed by an explicit ask to the PM not to interact with the file for ~30-60 seconds, which was then confirmed to persist.

**Cross-reference**
2026-09-16-business-quantification-listing-petr-neuman

---

### LL-035

| Field | Value |
|-------|-------|
| ID | LL-035 |
| Created | 2026-09-16 |
| Category | interviewing technique |
| Source | 2026-09-16-business-quantification-listing-petr-neuman |

**Lesson**
The problem that originally motivated a stakeholder to request an initiative is not always the problem they most urgently want solved by the time you interview them for business quantification. Always ask explicitly whether the original framing still holds ("is that still the main driver, or has something changed since?") rather than assuming the initiative's origin story is still its current priority.

**Context**
Listing was originally framed (2026-09-01, via Filip Černý's handoff) as a supplier-data-quality problem — enriching thin product data from suppliers. In the first direct interview with the actual business owner (Petr Neuman, 2026-09-16), that framing turned out to be secondary: his real, currently-most-urgent driver is Magento's growing instability at scale, which surfaced only in the last month or two — after the project had already started. Without directly probing for this shift, the quantification would have anchored on the wrong problem.

**Cross-reference**
project-assumptions ASM-073; project-stakeholders STK-023; 2026-09-01-dr-max-listing-introduction

---

### LL-034

| Field | Value |
|-------|-------|
| ID | LL-034 |
| Created | 2026-09-15 |
| Category | interviewing technique |
| Source | 2026-09-15-business-quantification-teo-ocr |

**Lesson**
In a business-quantification or scoping interview, don't take the interviewee's first "yes, that's me" on the Owner field at face value — explicitly reflect the Owner/Domain-Expert distinction back to them ("so X is the owner and you're my daily contact?") before writing it down. People default to saying yes to the person asking, then self-correct once the actual decision-making implication is spelled out.

**Context**
In the TEO/OCR quantification call, Radim Švarc initially confirmed he was the business owner ("Můžete si to tam napsat"), but immediately qualified it once Marek probed further — major decisions actually need Tomáš Burda's sign-off. Marek caught this by explicitly reflecting the corrected roles back ("takže business owner tohoto byl pan Burda a vy budete ten můj daily contact?"), which Radim then confirmed. Without that reflect-back step, Radim would likely have stayed recorded as owner.

**Cross-reference**
project-stakeholders STK-025, STK-041; product/solution-space/ai-initiatives-okr-framework.md (Pole 1 — Vlastník)

---

### LL-033

| Field | Value |
|-------|-------|
| ID | LL-033 |
| Created | 2026-09-15 |
| Category | workshop planning |
| Source | 2026-09-15-business-quantification-reklamace-fakturace-doprav |

**Lesson**
A per-item interview script's stated time budget (e.g. "~10-15 min per initiative") is a floor for a focused, uninterrupted exchange — real calls with a client stakeholder run longer per item once genuine back-and-forth, self-correction, and tangents happen, so a session prepped to cover many items in one sitting should expect to cover far fewer and plan an explicit follow-up rather than treating partial coverage as a shortfall.

**Context**
The Business Quantification workshop was prepped for 11 initiatives using a 6-field, ~10-15-min-per-item script. The first live execution covered only 2 (Reklamace, Fakturace doprav) in the available time before the client stakeholder had to leave for another call — each item ran meaningfully longer than the script's estimate once real discussion, self-correction on numbers, and tangential clarifications (naming, phasing) were included.

**Cross-reference**
product/solution-space/ai-initiatives-okr-framework.md; meetings/prep/2026-09-14-ai-initiatives-business-quantification-prep.md

---

### LL-032

| Field | Value |
|-------|-------|
| ID | LL-032 |
| Created | 2026-09-15 |
| Category | stakeholder tracking |
| Source | 2026-09-15-order-prediction-dashboard-follow-up |

**Lesson**
When processing a recurring meeting, actively cross-check any newly-named person against existing *low-confidence* stakeholder entries (not just full duplicates) — a name and role profile that loosely matched an old "unclear identity" record is a stronger signal than it looks, and flagging the possible match (without merging) keeps the record honest while surfacing it for PM confirmation.

**Context**
The 2026-09-15 order-prediction dashboard follow-up repeatedly referenced "Honza/Jan Maroušek," a warehouse-staffing planner needing a per-warehouse reservation breakdown. This closely matched two existing low-confidence entries created from earlier, thinner mentions: STK-036 ("Honza," flagged 2026-09-03 as wanting a month-ahead logistics view) and STK-021 (Jan Maroušek, the Kontrola beden contact). Rather than creating a third entry or silently merging, both existing records were annotated with the possible match and left for PM verification.

**Cross-reference**
project-stakeholders STK-021, STK-036; 2026-09-03-order-prediction-dashboard-live-demo

---

### LL-031

| Field | Value |
|-------|-------|
| ID | LL-031 |
| Created | 2026-09-11 |
| Category | working method |
| Source | project-daily-2026-09-11 |

**Lesson**
A workshop-prep artifact's field set and scope (how strict, how many entities, prefilled vs. blank) is a design decision the requester usually only discovers by seeing a first draft — expect at least one full restructure after showing initial work, and treat that as normal iteration rather than a sign the first attempt was wrong.

**Context**
The Žůrek/logistics Business Quantification prep went through three real restructures in one session: scope narrowed from 17 portfolio initiatives to 11, then the field set tightened from a loose OKR/confidence structure to a strict 6-field card with prefill rules, then an interview script was layered on top per field. Each pass was fast because the underlying research (OKR framework, JTBD, Fermi estimation) stayed valid across all three — only the presentation and scope changed.

**Cross-reference**
product/solution-space/ai-initiatives-okr-framework.md

---

### LL-030

| Field | Value |
|-------|-------|
| ID | LL-030 |
| Created | 2026-09-11 |
| Category | working method |
| Source | project-daily-2026-09-11 |

**Lesson**
An existing skill's internal structure can be borrowed for a deliverable that doesn't fit that skill's formal mechanics — apply its rigor (e.g. User Story / Acceptance Criteria discipline) without invoking its file-registration or ID-tracking machinery, when the underlying tracking system (FEAT-NNN, product-scope) doesn't actually apply to the content being produced.

**Context**
Drafting a first-ever Listing project spec, the PM asked to "leverage" the `/product-feature` skill's structure. This harness's `product-scope`/`FEAT-NNN` system is scoped to the Second Brain meta-tool, not Dr. Max's products, so the spec was written using `product-feature`'s section shape and AC rigor directly in `product/solution-space/listing-specifikace.md`, without registering a `feat_id` or linking to a `product-scope` file — kept the quality bar, skipped the mismatched mechanics.

**Cross-reference**
product/solution-space/listing-specifikace.md

---

### LL-029

| Field | Value |
|-------|-------|
| ID | LL-029 |
| Created | 2026-09-11 |
| Category | discovery method |
| Source | 2026-09-11-ai-listing-tool-demo-walkthrough |

**Lesson**
A live product demo/walkthrough can surface built capabilities that status meetings and roadmap trackers never mention — status updates report *progress against a plan*, while a demo reveals *what actually exists*, including features nobody thought to report because they weren't asked about.

**Context**
A structured walkthrough of the AI Listing Tool (presented by Filip Černý) surfaced several capabilities — a per-product catalog health score, version history/rollback, a granular per-field AI prompt configuration system, and a regulatory compliance blacklist for medical claims — none of which appeared anywhere in prior Listing meeting notes or the roadmap Excel, despite the underlying features being marked "Done."

**Cross-reference**
2026-09-11-ai-listing-tool-demo-walkthrough, `project-knowledge` (AI Listing Tool entry)

---

### LL-028

| Field | Value |
|-------|-------|
| ID | LL-028 |
| Created | 2026-09-10 |
| Category | requirements-gathering / access & permissions |
| Source | 2026-09-10-lexie-max-maxie-weekly-sync |

**Lesson**
A client request that sounds like a single simple ask (e.g. "we need a test account") can conceal several orthogonal technical requirements that only surface once you ask concretely how it will actually be used — who, how many people at once, and what exactly must and must not be visible to each. Treating the original request's brevity as evidence of simplicity, rather than as a sign the real requirement was never spelled out, wastes a cycle chasing the wrong ticket.

**Context**
A months-old ticket simply said "create a test account for AI," with no group/role detail — which nobody downstream had been able to act on. Only when the client (Mertová) was asked directly how testing would actually happen did it surface that 4 distinct role-scoped identities were needed simultaneously, that a single shared account in every permission group wouldn't actually test real role-restriction behavior, and that concurrent multi-tester use of one account might itself cause conflicts — three separate technical problems hiding inside what had been logged as one generic access request.

**Cross-reference**
2026-09-10-lexie-max-maxie-weekly-sync, ASM-063

---

### LL-027

| Field | Value |
|-------|-------|
| ID | LL-027 |
| Created | 2026-09-10 |
| Category | architecture / client communication |
| Source | 2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo |

**Lesson**
A confusing implementation detail (e.g. "why doesn't this count match?") can be a visible symptom of a much bigger unstated assumption (e.g. "who actually owns this system's state?") rather than a bug worth patching in isolation. When a data-contract question keeps not quite making sense despite incremental fixes, it's worth asking the client a blunt, higher-level ownership question directly — the answer can retire several smaller confusions at once.

**Context**
Filip Černý built the Fakturace doprav kiosk assuming the app needed to track its own route-completion state (deciding when a route was ready for manual review or invoicing) and had separately convinced himself Axapta returned per-document page counts to validate completeness — a claim that turned out, live in an internal demo, to be a hardcoded/faked value. Both confusions dissolved at once when the client (Jan Žižka) clarified directly, in the very next meeting, that Axapta is the sole owner of route/document state and the app should hold none at all. The page-count question had never been the real problem — it was a downstream symptom of an unstated architecture assumption nobody had asked the client to confirm.

**Cross-reference**
2026-09-10-fakturace-doprav-kiosk-portal-demo, 2026-09-10-viapharma-reklamace-uat-fakturace-doprav-demo, ASM-053

---

### LL-026

| Field | Value |
|-------|-------|
| ID | LL-026 |
| Created | 2026-09-09 |
| Category | stakeholder communication |
| Source | 2026-09-09-logistics-cc-roadmap-presentation-prep |

**Lesson**
Effort estimates alone (e.g. man-days) don't communicate delivery timing to non-technical business stakeholders — a unit like "one man-day" has no fixed meaning in wall-clock time without a calendar attached, and can be misread as "one day away." Pairing any effort-based roadmap with a simple calendar/timeline view (what happens when: testing, fixes, rollout) closes that gap.

**Context**
Reviewing the roadmap board ahead of presenting it to Logistika and CC, Jindřich Tůma pointed out that a phase estimate like "MVP in one man-day" would mean nothing to Tereza Foltová — she needs to see concretely when testing starts, how long it runs, and when rollout lands, not an abstract effort unit. The fix didn't require new data, just a second, simpler view (item + filled time-axis cells) built from the same information already collected.

**Cross-reference**
2026-09-09-logistics-cc-roadmap-presentation-prep, ASM-050

---

### LL-025

| Field | Value |
|-------|-------|
| ID | LL-025 |
| Created | 2026-09-09 |
| Category | harness |
| Source | project-daily-2026-09-09 |

**Lesson**
When a client-facing board/deck is built by distilling a source-of-truth data file, check that per-item annotations (comments, caveats, rationale notes) carried over along with the headline numbers — a derived view can transfer the numeric totals correctly while silently dropping or misplacing the supporting detail attached to individual rows, and that gap isn't visible unless someone spot-checks the rendered artifact against its source.

**Context**
The PM noticed Honza Zelený's effort estimates appeared in the v3 roadmap board without any supporting comments, and initially thought they'd been misattributed to Lexie. Checking the live Excel confirmed the numbers were correctly Maxie's, and Maxie's sheet actually has 6 rich supporting comments (including a reuse note from Jura Brázdil) — none of which had made it into the board. The board's numeric totals were right; the per-box narrative context wasn't carried over during the board build.

**Recurrence (2026-09-16, Fakturace doprav spec)**: A more severe instance of the same failure mode. Rebuilding `2. Fakturace doprav.docx`'s MVP/Plná verze/Nice to Have tables as an abstracted "capability summary" (paraphrased and merged from the spec's own narrative) rather than a literal copy of the roadmap Excel silently dropped entire items — 3 of 7 Plná verze items and 5 of 6 Nice to Have items were missing, not just annotations. Only surfaced when the PM visually compared a screenshot of the roadmap Artifact against the doc's table side by side. Fix: rebuilt the tables as a direct 1:1 mirror (same IDs, names, statuses) with an added source-citation column, rather than a paraphrase — the more useful general rule this points to is that *paraphrasing/summarizing a source list is inherently lossy in a way that isn't self-evident from reading the output alone*; when two artifacts need to stay comparable item-by-item, mirror the source verbatim with a source column instead of re-authoring a "cleaner" version of it.

**Cross-reference**
project-daily-2026-09-09; project-daily-2026-09-16; ASM-090

---

### LL-024

| Field | Value |
|-------|-------|
| ID | LL-024 |
| Created | 2026-09-09 |
| Category | tooling-collaboration |
| Source | project-daily-2026-09-09 |

**Lesson**
Never script-write to a file the user has open live in Excel/Office with AutoSave on. It's not just a race condition (see LL-023) — Excel's cloud co-authoring session actively breaks: it detects the file changed outside its own sync protocol and cannot reconcile that with its in-memory change history, so it locks all further saves ("Upload Blocked... can't save any new changes"). The fix isn't a longer delay before re-checking — it's confirming the file is closed before writing at all.

**Context**
While routing Filip Černý's estimates into the live roadmap Excel, Marek had the file open with AutoSave and was actively editing (mid-keystroke in a cell) when the script overwrote the file on disk. Excel Online surfaced a hard "Upload Blocked" error and would not save further changes; Marek had to close the file and discard his in-progress edit before a clean re-run of the same script succeeded. This explains an earlier silent-revert incident (LL-023) too — likely the same root cause, just resolved by Excel's autosave overwriting the script's change instead of blocking outright.

**Cross-reference**
LL-023, project-daily-2026-09-09

**Recurrence (2026-09-17, Listing client-doc annotation work)**: Same root cause, different tool and file format — python-docx writes to a `.docx` open live in Word were silently reverted mid-session (a section-move/renumber edit reverted all the way back to its pre-move state). Confirmed via `lsof` that Word held the file open; asking the PM to close it, then re-verifying via `lsof` before every subsequent write, resolved it. Generalizes this lesson beyond Excel/openpyxl to any Office format (Word/docx included) and any scripting library (python-docx included) — the fix (`lsof`-style open-file check before writing, not just a delay-and-recheck) is now the default habit before any script-write to a user-facing Office file.

**Cross-reference**
project-daily-2026-09-17

### LL-023

| Field | Value |
|-------|-------|
| ID | LL-023 |
| Created | 2026-09-08 |
| Category | tooling-collaboration |
| Source | project-daily-2026-09-08 |

**Lesson**
A programmatic write to a live cloud-synced file (OneDrive, Google Drive, etc.) can appear to succeed — and even verify correctly if re-read immediately — but still get silently reverted moments later by a sync conflict, most likely if the file is open elsewhere. Immediate post-write verification is not sufficient proof of persistence for actively-synced files; re-check after a short delay (several seconds) before reporting success, and if a write is found reverted, flag to the user that the file may be open elsewhere and ask them to close it before retrying.

**Context**
A batch of Excel comment/estimate writes to the live `product-roadmap-portfolio-full.xlsx` (OneDrive) verified correctly right after saving, but had reverted to the pre-write state by the next turn. Re-running the same write and checking again after a 10-second delay confirmed it held that time. The file had also spontaneously renamed itself mid-session earlier (dropping a version-number suffix), independently confirming OneDrive was actively manipulating the file outside of direct control.

**Cross-reference**
project-daily-2026-09-08

### LL-022

| Field | Value |
|-------|-------|
| ID | LL-022 |
| Created | 2026-09-08 |
| Category | discovery-methodology |
| Source | 2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil |

**Lesson**
When scoping new work on top of an existing internal system, a manager's or account owner's strategic/historical account and the actual builder's technical account can diverge significantly even when both are told in good faith — the strategic account explains *why* and *what was intended*, but only the person who currently maintains the code can say *what's actually built*. Get both, in that order, before committing to a delivery plan.

**Context**
Jan Sovka's account of BigHub's AI platform (deployed for ~2 years, role-based permissions live across the client base) was accurate as far as intent and history go, but Jura Brázdil's technical deep-dive the same day revealed a materially different present-day reality: the platform in practice is just one RAG product, MaxBuddy still isn't migrated into it, the permission system Jan described is Lexie-specific rather than platform-wide, and there's a shared database with zero isolation between use cases. Scoping the near-term delivery plan only became reliable once Jura's account was folded in — holding both meetings back-to-back the same day, rather than relying on the manager's account alone, is what surfaced the gap before commitments were made to the client.

**Cross-reference**
2026-09-08-ai-platform-strategy-history-with-jan-sovka, 2026-09-08-ai-platform-technical-deepdive-jura-brazdil, ASM-038, ASM-039

---

### LL-021

| Field | Value |
|-------|-------|
| ID | LL-021 |
| Created | 2026-09-07 |
| Category | tooling-collaboration |
| Source | project-daily-2026-09-07 |

**Lesson**
When a stakeholder is actively hand-editing a shared deliverable in parallel with AI-assisted generation, treat their live edits as the source of truth and layer additions on top rather than regenerating from scratch — a fresh regeneration silently overwrites judgment calls (manual status assignments, row splits, renumbering, owner attributions) that took real thought to make.

**Context**
While building `product-roadmap-portfolio-full.xlsx`, Marek began hand-editing the workbook directly (Status values, Owner names, deliberate row splits distinguishing MVP-done vs. Full-Version-continuation work) between generation passes. Continuing to regenerate the file from the original script would have destroyed that work. Switching to load-and-append edits on his live copy instead preserved everything and let new additions (new rows, Portfolio entries, comments) sit alongside his own changes without conflict.

**Cross-reference**
project-daily-2026-09-07

---

### LL-020

| Field | Value |
|-------|-------|
| ID | LL-020 |
| Created | 2026-09-07 |
| Category | discovery-methodology |
| Source | 2026-09-07-ai-portfolio-roadmap-scope-review |

**Lesson**
Cross-referencing a shared tracker against every independent source that fed it (exports, specs, meeting transcripts, live stakeholder edits) before treating it as final surfaces real conflicts that no single source alone would reveal — disputed ownership, duplicate/stale entries, and quietly-changed decisions all hide in the gaps between sources.

**Context**
Reconciling the AI portfolio/roadmap workbook against v8.xlsx, the BigHub Notion export, the MVP Scope & Acceptance doc, and the 2026-09-07 review meeting surfaced several real discrepancies that a single-source build would have missed: disputed Reklamace dev ownership (two independent people each named as owner), the Maxie/Voicebot naming collision (same initiative tracked under two names), and a claim in the meeting note (Campaign Recommendation Model "confirmed Full Version") that turned out to overstate what was actually decided once checked against the PM's own live-edited Excel.

**Cross-reference**
2026-09-07-ai-portfolio-roadmap-scope-review, project-daily-2026-09-07

---

### LL-019

| Field | Value |
|-------|-------|
| ID | LL-019 |
| Created | 2026-09-04 |
| Category | discovery-methodology |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

**Lesson**
When onboarding onto a client-facing AI product, explicitly ask whether the underlying platform/infrastructure is dedicated to this client or shared across others. Don't assume a component is client-exclusive just because that's the only context you've seen it deployed in — shared internal platforms are common, and the assumption gets baked into scope, ownership, and design decisions before anyone corrects it.

**Context**
Several days into the Dr. Max account, a routine internal stand-up revealed the AI/chatbot platform (Max, Maxie, Lexie) is actually shared BigHub infrastructure also deployed for other clients (Brněnská komunikace, Kooperativa, Unica) — not built exclusively for Dr. Max. This reframed an open question about who owns the platform's product roadmap (a single client-scoped PM, or someone owning it across all clients) and how design/theming decisions should be made (centralized template vs. per-client customization) — questions that hadn't been asked earlier because the Dr. Max-exclusive framing had gone unchallenged.

**Cross-reference**
2026-09-04-ai-platform-standup-xmanager-lexi-demo, ASM-025, ASM-026

---

### LL-018

| Field | Value |
|-------|-------|
| ID | LL-018 |
| Created | 2026-09-04 |
| Category | client-management |
| Source | 2026-09-04-ai-platform-standup-xmanager-lexi-demo |

**Lesson**
When a client is eager for visual polish but technical validation isn't done yet, offer a zero-engineering-cost placeholder — a single AI-generated image of what the redesign could look like — rather than either building real mockups or ignoring the request. It manages expectations and gives the client something concrete to react to, without pulling engineering time away from the actual priority.

**Context**
Dr. Max's CC team casually mentioned wanting Lexie to look as polished as the newly-demoed Max chatbot. Rather than scoping a real design pass (which would compete with fixing 3 blocking bugs) or dismissing the comment, the BigHub team's plan was to generate a single representative image via an AI tool — no mockup, no frame, no code — just something to show "this is the direction," while keeping actual engineering focused on technical fixes.

**Cross-reference**
2026-09-04-ai-platform-standup-xmanager-lexi-demo, ASM-024

---

### LL-017

| Field | Value |
|-------|-------|
| ID | LL-017 |
| Created | 2026-09-03 |
| Category | harness |
| Source | project-daily-2026-09-03 |

**Lesson**
When generating Office file formatting programmatically (fill colors especially), a structurally valid, error-free file can still render as blank/invisible if a color is written with a transparent alpha channel. Don't stop verification at "did it save without error" or "does the XML parse" — check the actual color/format values themselves (e.g. that an RGB fill starts with `FF` alpha, not `00`) before declaring a formatting change done.

**Context**
Applying conditional-formatting row colors to a client roadmap spreadsheet, a fill color built from a bare 6-character hex string (e.g. `"C8E6C9"`) saved successfully, passed zip/XML integrity checks, and correctly referenced the right cells and formulas — but rendered with 0% opacity because the alpha channel defaulted to `00` instead of `FF`. The PM reported "not working" with a screenshot; the fix was supplying an explicit 8-character ARGB string (`"FFC8E6C9"`). Root cause was only found by reading the raw dxf XML values, not by re-running the generation script and re-checking structural validity.

**Cross-reference**
project-daily-2026-09-03

| Field | Value |
|-------|-------|
| ID | LL-016 |
| Created | 2026-09-03 |
| Category | domain-specific |
| Source | 2026-09-03-maxbuddy-chatbot-ocr-project-handoff |

**Lesson**
On a regulated-industry AI feature (healthcare, finance, etc.), get a compliance/regulatory review early — as soon as the feature's data flow is defined — rather than after significant development investment. A feature that looks clearly compliant in early prototyping can turn out to require formal certification once its actual data-handling pattern is examined.

**Context**
MaxBuddy's original core feature — flagging outdated drug dosages against updated SPC guidance — was developed for roughly six months before Dr. Max discovered it made the product a regulated medical device requiring certification: any pipeline where patient data goes in and an LLM-derived recommendation comes out is prohibited without it. The feature is now frozen rather than shipped, and development pivoted to an expert-panel-reviewed upsell/cross-sell recommendation feature instead, which doesn't trigger the same certification requirement.

**Cross-reference**
2026-09-03-maxbuddy-chatbot-ocr-project-handoff, [[project-knowledge]] (MaxBuddy entry)

---

### LL-015

| Field | Value |
|-------|-------|
| ID | LL-015 |
| Created | 2026-09-03 |
| Category | design |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |

**Lesson**
When designing an in-product feedback mechanism, default to a lightweight rating widget (stars, emoji, a color-ordered scale) over a free-text form — and if the client already has UX data from prior deployments about what actually gets used, defer to it rather than re-litigating the design from scratch.

**Context**
Dr. Max's CC team pushed back on a free-text feedback form for the Max chatbot, citing their own prior chatbot data: free-text fields see low completion, and a green→red color-ordered rating scale outperformed the reverse order in their testing. The team adopted stars/emoji-only, no free text. Logged as ASM-017 (Decided).

**Cross-reference**
ASM-017, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync

---

### LL-014

| Field | Value |
|-------|-------|
| ID | LL-014 |
| Created | 2026-09-03 |
| Category | project-management |
| Source | 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync |

**Lesson**
Route all client feature/change requests for a given product through a single named point of contact rather than accepting them individually from every user who touches it. Aggregate requests from many individual testers tend to drown out what the actual business owner needs, creating noise and duplicate or conflicting asks.

**Context**
Jindřich Tůma requested this explicitly for Max/Lexie/Maxie X-Manager tickets, routing everything through Simona Mertová, based on prior experience where requests from ten-plus individual users didn't reflect what the business owner actually wanted in the end. Logged as ASM-018 (Decided).

**Cross-reference**
ASM-018, 2026-09-03-max-chatbot-demo-lexi-maxi-status-sync

---

### LL-013

| Field | Value |
|-------|-------|
| ID | LL-013 |
| Created | 2026-09-03 |
| Category | stakeholder-management |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |

**Lesson**
When first-demoing a predictive or analytics dashboard to its real business owner, proactively point out a moment where the live data correctly reflects a known real-world event (an outage, a campaign, an anomaly the stakeholder already knows happened). This is a far more persuasive trust-building signal than any amount of explaining the model's methodology, because the stakeholder can verify it themselves against something they already know is true.

**Context**
An 8-minute site outage on 2026-08-24 showed up as a visible dip in the order-prediction dashboard's live chart during the demo. Marek Šimoník (Dr. Max, Head of E-commerce) immediately recognized and confirmed it, unprompted, calling it "an extremely good indicator" — this single moment did more to establish confidence in the tool than the rest of the walkthrough combined.

**Cross-reference**
2026-09-03-order-prediction-dashboard-live-demo

---

### LL-012

| Field | Value |
|-------|-------|
| ID | LL-012 |
| Created | 2026-09-03 |
| Category | delivery-process |
| Source | 2026-09-03-order-prediction-dashboard-live-demo |

**Lesson**
When rolling a predictive/forecasting tool out to a business stakeholder for testing, set an explicit review order upfront: verify the underlying data/numbers are correct first, then gather display/UX feedback, and only then evaluate and tune the model's forecasting accuracy. Skipping this order lets an engaged, technical stakeholder pull the conversation into premature model-accuracy debates before the more basic, more easily verified layers are settled.

**Context**
Jan Sovka set this three-layer order (data accuracy → UX → model accuracy) proactively during the order-prediction dashboard's first live demo, reasoning that today's model accuracy was "good enough" and that arguing over forecasting precision too early would distract from the data/UX issues that are actually blocking the client from trusting the tool. Logged as ASM-014 (Decided).

**Cross-reference**
ASM-014, 2026-09-03-order-prediction-dashboard-live-demo

---

### LL-011

| Field | Value |
|-------|-------|
| ID | LL-011 |
| Created | 2026-09-03 |
| Category | delivery-process |
| Source | 2026-09-03-viapharma-logistics-status-reklamace-demo |

**Lesson**
When rolling out a new feature or app to client testers, don't let a proper production auth system (SSO, OAuth, Entra ID, etc.) block the start of testing — ship the simplest workable stand-in (e.g. hardcoded per-user logins) and build the real auth in parallel. Confirm what the requester actually needs first: sometimes a request that sounds like a security requirement ("I need to see who's logged in") is really about traceability/audit logging, which a much simpler mechanism satisfies.

**Context**
For the Dr. Max reklamace mobile app, Entra ID/OAuth was flagged as a likely integration friction point. Rather than wait for it, the team issued hardcoded per-tester logins so ViaPharma's testers (Tereza Foltová, then Jana) could start immediately, while Entra ID work continued in parallel. The client's stated interest in per-user login was clarified as wanting traceability in Axapta's logs (who performed which action), not concern about credential misuse — confirming a simple mechanism was sufficient. Logged as ASM-012 (Decided).

**Cross-reference**
ASM-012, 2026-09-03-viapharma-logistics-status-reklamace-demo

---

### LL-010

| Field | Value |
|-------|-------|
| ID | LL-010 |
| Created | 2026-09-02 |
| Category | project-management |
| Source | project-daily-2026-09-02 |

**Lesson**
When deriving task priority algorithmically (e.g. from milestone proximity, activity type, or "strategic vs. housekeeping" framing), explicitly weight requests from people with direct reporting-line authority as heavily as external stakeholder asks — and don't let a task's housekeeping surface appearance discount it, since the person requesting it may see it as a real delivery blocker even though it doesn't look that way from the outside.

**Context**
The daily's derived priority ranking treated a tooling migration (moving a tracking artifact into Notion) and setting up an internal sync cadence with the new PM as low-priority process/housekeeping. Both had in fact been directly requested by direct-authority figures (Jindřich Tůma as PM, Honza Sovka as line manager) during today's meetings, and the PM flagged that such requests should outrank the algorithmic ranking.

**Cross-reference**
project-daily-2026-09-02, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync

---

### LL-009

| Field | Value |
|-------|-------|
| ID | LL-009 |
| Created | 2026-09-02 |
| Category | delivery-process |
| Source | 2026-09-02-aks-atlantis-infra-sync |

**Lesson**
Before planning any redeployment, migration, or significant change to an existing system, confirm whether it was provisioned via infrastructure-as-code or set up manually (ad hoc clicking) — manually-configured infrastructure has no reliable reproduction path, and that risk stays invisible until someone actually needs to touch it again.

**Context**
A question about redeploying legacy MaxBuddy infrastructure (PTU/model provisioning) surfaced that it had been configured manually rather than via Terraform, and that the people most familiar with the original setup were no longer easily reachable — nobody in the room could confidently reconstruct how it was built. The team's practical response was to leave it untouched while it keeps working rather than risk a change with no clean rollback path.

**Cross-reference**
2026-09-02-aks-atlantis-infra-sync

---

### LL-008

| Field | Value |
|-------|-------|
| ID | LL-008 |
| Created | 2026-09-02 |
| Category | trust-building |
| Source | 2026-09-02-logistics-listing-team-sync |

**Lesson**
When automating a client-facing communication channel for the first time, default to producing a human-reviewed draft rather than an automatic send — even once the underlying logic is trusted, the send action itself is where an error becomes visible and costly to the client relationship.

**Context**
Designing the reklamace email-automation workflow, Jindřich Tůma set the rule explicitly the moment it was raised: the system pre-fills a draft from the applicable supplier procedure, a human reviews and edits it, then sends — never an automatic send. Logged as ASM-010 (Decided).

**Cross-reference**
ASM-010, 2026-09-02-logistics-listing-team-sync

---

### LL-007

| Field | Value |
|-------|-------|
| ID | LL-007 |
| Created | 2026-09-02 |
| Category | scope-protection |
| Source | 2026-09-02-logistics-listing-team-sync |

**Lesson**
When a project is blocked on an undefined client-side dependency (data model, category system, taxonomy), stop further development rather than continuing to build speculatively against a moving target — the cost of rework outweighs the appearance of progress, and framing the pause as "we need X from you before we continue" protects both budget and the relationship.

**Context**
Filip Černý refused to continue Listing development until Dr. Max delivers a category/parameter system, explicitly reasoning that further coding would "burn money for nothing." Jindřich Tůma validated this rather than pushing for visible progress, and the team agreed to a Discovery-first path instead (ASM-011) — explicitly framed as not a billing play, but as the only productive way forward.

**Cross-reference**
ASM-011, 2026-09-02-logistics-listing-team-sync

---

### LL-006

| Field | Value |
|-------|-------|
| ID | LL-006 |
| Created | 2026-09-02 |
| Category | scope-protection |
| Source | 2026-09-02-roadmap-tracking-and-listing-onboarding-sync |

**Lesson**
Protect delivery against scope creep by requiring every spec to carry an explicit, business-signed hypothesis + acceptance-criteria section before build starts — a short "what we're solving, what we'll build, how we'll know it's done" framing gives both sides a clear reference point when disputes arise later, without needing a heavyweight spec process.

**Context**
Jindřich Tůma introduced this as a direct response to requirement creep observed on the Dr. Max account ("the requests never stop") — the specific failure mode being a business owner claiming after delivery that an unstated expectation wasn't met (his example: "the button should have been pink"). Logged as ASM-009 (Decided).

**Cross-reference**
ASM-009, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync

---

### LL-005

| Field | Value |
|-------|-------|
| ID | LL-005 |
| Created | 2026-09-02 |
| Category | data-quality |
| Source | 2026-09-02-order-prediction-dashboard-walkthrough |

**Lesson**
When two independent team members separately name different individuals as owning the same workstream, treat both attributions as provisional and record both rather than silently picking one — single-source ownership claims on an account with fragmented documentation are a recurring failure mode, not a one-off.

**Context**
Filip Černý (2026-09-01) named "Kuba Turner" as the main builder of the reklamace stream; Juraj Kmec (2026-09-02), speaking independently, instead attributed both reklamace and freight invoicing to "Jura Brázdil." Neither source expressed full confidence. This is the third such conflict surfaced on the account in two days (see also ASM-005, ASM-006), suggesting the underlying documentation/reporting gap Jindřich was hired to fix is still actively producing inconsistent records.

**Update (2026-09-03)**: The "resolved" version of this conflict (ASM-007, Decided 2026-09-02 — Turner=MaxBuddy only, Brázdil=reklamace) turned out to be incomplete rather than either side being wrong: a follow-up meeting showed Turner is *also* active on the reklamace backend. Lesson refined — when reconciling two conflicting ownership claims, don't assume the resolution must be exclusive (one right, one wrong); check whether both can be true at once (shared/overlapping ownership) before closing the conflict as Decided.

**Cross-reference**
ASM-007, ASM-005, ASM-006, 2026-09-02-order-prediction-dashboard-walkthrough

---

### LL-004

| Field | Value |
|-------|-------|
| ID | LL-004 |
| Created | 2026-09-01 |
| Category | delivery-process |
| Source | 2026-09-01-dr-max-x-bighub-project-status-sync |

**Lesson**
When a deliverable is blocked by an unrelated internal process the client is running on their own timeline (e.g. a company-wide tender or approval), ship using what's currently available and explicitly plan a follow-up wave once the client-side process resolves — rather than waiting for it and blocking delivery.

**Context**
A chatbot's design/logo was blocked because Dr. Max's Brno headquarters was running its own company-wide tender for design/logo work. Resolved by shipping now with the existing design (following a prior Slovak precedent) and agreeing to apply the new branding in a later wave once the tender concludes — explained directly to the affected stakeholder, who agreed not to block the release on it.

**Cross-reference**
2026-09-01-dr-max-x-bighub-project-status-sync

---

### LL-003

| Field | Value |
|-------|-------|
| ID | LL-003 |
| Created | 2026-09-01 |
| Category | stakeholder-management |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |

**Lesson**
Passive delivery of a finished feature (one announcement email, then silence) rarely drives adoption — sustained, active promotion (workshops, demos, reminders) is usually required even when the feature clearly solves a stated problem.

**Context**
An early call-center automation feature was released for UAT with a single announcement; after 14 days, zero users had engaged with it. By contrast, presenting the listing automation work live on the client's board (with a short demo video and deck, ~6 hours of prep) produced strong visible buy-in.

**Cross-reference**
2026-08-25-marek-onboarding-with-jan-sovka

---

### LL-002

| Field | Value |
|-------|-------|
| ID | LL-002 |
| Created | 2026-09-01 |
| Category | discovery |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |

**Lesson**
When learning an unfamiliar account or process, gather input from both directions before proposing changes: management's stated priorities/KPIs, and separately, the reality reported by the people actually doing the work day to day. The two often diverge, and the gap is where the real risk hides.

**Context**
A warehouse claims-automation project was speced based on the Prague warehouse's process; two months before go-live it emerged that three other warehouses (including Brno) ran a materially different, paper-based process the process owner hadn't accounted for.

**Cross-reference**
2026-08-25-marek-onboarding-with-jan-sovka, [[project-knowledge]] ("old wise man" discovery approach)

---

### LL-001

| Field | Value |
|-------|-------|
| ID | LL-001 |
| Created | 2026-09-01 |
| Category | specification |
| Source | 2026-08-25-marek-onboarding-with-jan-sovka |

**Lesson**
Showing business stakeholders a clickable/prototype mockup before or alongside writing a spec surfaces edge cases and gets substantially better engagement than a text brief alone — stakeholders who won't react to a two-paragraph description will spot and raise issues when they can click through a flow.

**Context**
Prototype-first specs became the default approach across the Dr. Max streams (e.g. MaxBuddy, logistics/claims) after repeatedly producing better-informed specs and stronger stakeholder buy-in than text-only briefs.

**Cross-reference**
2026-08-25-marek-onboarding-with-jan-sovka

---

## Entry Format

```markdown
---

### LL-{NNN}

| Field | Value |
|-------|-------|
| ID | LL-{NNN} |
| Created | {YYYY-MM-DD} |
| Category | {open-ended label} |
| Source | {meeting-slug, daily-slug, document-slug, or "PM"} |

**Lesson**
{Generalized insight — 1-3 sentences, understandable without project context}

**Context**
{What specifically happened — project-specific details}

**Cross-reference**
{Links to related artifacts: assumptions, meetings, dailies — when applicable}
```
