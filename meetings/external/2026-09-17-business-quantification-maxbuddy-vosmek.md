---
last_updated: 2026-09-17
type: external
attendees: [Marek Pillár, Luboš Vosmek]
tldv_link:
---

# Business Quantification Call with Luboš Vosmek — MaxBuddy

**Date**: 2026-09-17
**Attendees**: Marek Pillár (BigHub, running the interview), Luboš Vosmek (Dr. Max — Regional Director, MaxBuddy business owner)
**Type**: external
**Recording**: N/A (Marek recorded the call himself; transcript export only)
**Previous session**: N/A — first direct 1:1 Business Quantification interview for MaxBuddy. Related prior context: [2026-09-03-maxbuddy-chatbot-ocr-project-handoff](../internal/2026-09-03-maxbuddy-chatbot-ocr-project-handoff.md) (Jura Brázdil's handoff, incl. MaxBuddy's regulatory history)
**Meeting prep**: N/A

## TL;DR

Second Business Quantification interview of the day (after Mertová on Max/Maxie/Lexie), this time on MaxBuddy — due to Marek tomorrow (2026-09-18) for Tomáš Dudaško. Vosmek confirmed he's business owner without budget (IT/Dudaško holds it), gave a well-grounded JTBD origin story explaining why MaxBuddy started with a since-abandoned dosage-checking feature, and produced real (if partially estimated) revenue and satisfaction figures. He committed to sending three concrete missing numbers tomorrow morning. He also surfaced a real operational pain point — a ~14-day silent data-feed outage that took 4 days to diagnose — driving a concrete "coverage dashboard" wishlist item for the future, separate from this quantification.

## Key Discussion Points

### Housekeeping and ownership

Brief audio issues at the start (Vosmek joined from his car). Marek explained the same process used with Mertová earlier: a recorded interview, pre-filled Excel sent immediately after, Vosmek reviews/edits/confirms by tomorrow (Friday) for Marek to forward to Dudaško.

Vosmek confirmed he's the **business owner of MaxBuddy**, but was explicit about a nuance: **"I'm business owner without budget. IT — Tomáš Dudaško — holds the budget"** `[translated from Czech]`.

On domain expert, Vosmek named two people with different roles — a distinction he corrected Marek on mid-call:
- **Lukáš Sýč** — his IT liaison, "builds the bridges" between BigHub, Farmy (the pharmacy POS system), BDC, and Vosmek. This is the go-to contact for anything non-functional or blocked.
- **Jiří Trajer** — data warehouse/Power BI, feeds MaxBuddy its underlying data. Marek initially assumed Trajer would be the fallback contact for roadmap/feature questions; Vosmek corrected this directly: **"if something's non-functional, Lukáš Sýč is the one who handles it... Trajer just feeds it"** `[translated from Czech]` — Trajer is not involved in any feature/functionality decisions.

### Objective (JTBD) — origin story

Vosmek gave a clean two-layer answer, explicitly distinguishing "how the project started" from "why, in business terms."

**How it started**: Dr. Max's ownership/IT ran an internal competition inviting every business team to propose an AI use case. Dr. Max won with a proposal to computer-check syrup dosing (**"kontrola dávkování"**, specifically cough-syrup dosing) — which was later found legislatively unworkable (the same medical-device certification block already on record for MaxBuddy's history).

**The real "why" behind starting there anyway**: dosage-checking itself carries **no direct business value** — Vosmek was candid about this. The actual reason to start there was psychological: the moment "AI" is mentioned inside a pharmacy, **staff panic — distrust, a sense of being professionally replaced, "this isn't right in healthcare"** `[translated from Czech]`. Dosage-checking was chosen deliberately as a way to "get inside their heads" with something that visibly helps and reads as expert, not threatening. Complex care / upselling (**"komplexní péče" / "příprodeje"**) was always the intended step two — legislative blockage of step one simply forced Dr. Max to skip straight to step two, "even though it isn't AI" `[translated from Czech]`.

**Notable nuance**: Vosmek stated plainly that the live upsell/cross-sell feature today is **not actually LLM/AI-driven** — it's rule-and-data-based ("**it's all tied together with data**" `[translated from Czech]`). Worth confirming how this affects MaxBuddy's classification in an "AI initiatives" portfolio tracker.

### Business value

**Original hypothesis (company-wide, not MaxBuddy-specific)**: each 1 percentage-point increase in "komplexní péče" conversion ≈ **~400 million CZK/year** in revenue across the whole Dr. Max network — Vosmek called this explicitly a **"vzdušný zámek"** (a castle in the air / unverified back-of-envelope figure), not a MaxBuddy-attributed number.

**Real, MaxBuddy-attributed uplift**: roughly **~1–1.2%**, but Vosmek was upfront he doesn't have the exact case-count denominator on hand: **"I won't lie to you about the numbers... I'll calculate it and can have it tomorrow morning"** `[translated from Czech]`.

**Per-item economics**: each additional complementary product ("krabička") sold via complex care yields on average **+150 CZK revenue**, ideally on Dr. Max's own private-label brand where margin is higher.

**Coverage**: MaxBuddy today only covers dispensing cases within one therapeutic pilot area ("bolest"/pain, ~20 target molecules) out of many hundreds of molecules dispensed overall. Coverage was at 26 molecules, expanded again last week (exact new count not confirmed on the call) — Vosmek estimated **~40%** of all dispensing cases are currently covered. Full theoretical potential across all therapeutic areas is far higher than what's realized today.

**Secondary value — customer satisfaction (measured, not estimated)**: Dr. Max sends **~40,000 customer surveys/month**; when complex care is offered, satisfaction runs **~31% higher**.

**Explicitly excluded**: employee satisfaction. Vosmek was firm this should not be listed as a value driver — he expects real pushback from pharmacy staff, since it reads to them as extra work and an implicit challenge to their professional judgment ("**you already showed me this, why didn't you do it**" `[translated from Czech]`), not as something staff will welcome.

### KPI

**Primary/headline KPI (tracked by Dr. Max's corporate "Holding")**: the share of **single-item dispensing events** ("jednopoložkové expedice" — a dispensing case where no complementary/supporting product was added) out of all dispensing cases. Currently roughly **50%** of all dispensing is single-item. Target: **reduce this by 1.5 percentage points every year**. Vosmek deliberately chose to frame and track this as a *declining* metric (rather than the equivalent rising "multi-item %") because that's how Holding already watches it — despite noting wryly that everyone prefers charts that go up. **Exact current baseline % and the formal 1.5pp/year target on paper are due from Vosmek tomorrow morning (2026-09-18).**

**Secondary/internal reports** (tracked on Dr. Max's own side via Power BI/Jiří Trajer, reading pharmacy POS receipt data — BigHub only needs to keep supplying underlying data, not build or run these reports): breakdown by therapeutic group/molecule (e.g. pain+magnesium, pain patches, roll-ons); and a conversion-rate report by upsell "reason"/benefit (e.g. antibiotic → probiotic suggestion), already commissioned internally as report #3, to identify which upsell logic converts best and prioritize expanding it.

**Third KPI candidate — per-expedient (per-pharmacist) engagement**: MaxBuddy's decision-tree logic ("stromy") sometimes needs the pharmacist to answer a follow-up question rather than inferring purely from the dispensed item — e.g. an antibiotic case branches by ailment (sore throat vs. urinary tract infection) into different complementary suggestions. Vosmek wants per-pharmacist click-through counts on these branches as his only real proxy for actual engagement ("**I can't watch their eyes, but I can count what they click**" `[translated from Czech]`) — this was already requested from BigHub (Marek initially misattributed this to "Juraj," corrected on the call to **Jura Brázdil**) but **is not built/working yet**.

### Future wishlist (not part of this quantification — flagged separately, "don't forget")

Two concrete, actionable items surfaced that are operational/roadmap requests rather than business-quantification inputs:

1. **Molecule/group coverage visibility dashboard**: Vosmek is currently "blind" to how many therapeutic groups/molecules are configured in MaxBuddy and their status. He wants a simple color-coded tracker (red = no data flowing in; blue = data flowing but no upsell "benefit" rule configured yet; yellow = benefit approved and live) so he can see the full picture at a glance. Motivated by being put on the spot by Tomáš Dudaško that same day ("how many groups do you have, is Buddy working?" — Vosmek could only guess "46") and by a real incident: a fiber ("vláknina") data feed **silently broke for as long as 14 days** before anyone noticed, then took **4 days to diagnose** once flagged — with no live overview, this kind of gap can recur invisibly.
2. **Broader MaxBuddy scope-expansion wishlist**: Vosmek has additional ideas beyond the above, to be sent separately; Marek proposed a dedicated follow-up discovery/prioritization call, with Tomáš Dudaško involved as the decision-maker on priority and resourcing.

### Closing

Marek asked for any final input beyond MaxBuddy or a "magic wand" wish for Dr. Max more broadly; Vosmek had nothing further on the spot but flagged (half-joking) that if pressed for more time he and colleagues would inevitably think of something. Marek confirmed all future work will route through Tomáš Dudaško as decision-maker. Vosmek was given full edit access to the shared Excel and confirmed he'd fill in the outstanding numbers tomorrow (Friday) morning.

## Decisions Made

- MaxBuddy's KPI will track **single-item dispensing rate declining** (not multi-item rate rising) — Vosmek's explicit choice, matching how Holding already monitors it.
- Employee satisfaction will **not** be included as a claimed business-value driver for MaxBuddy — Vosmek's explicit request, anticipating staff resistance.
- Domain-expert responsibilities are split: **Lukáš Sýč** for functionality/decisions/escalation, **Jiří Trajer** for data-feed only — corrects an initial (reversed) assumption from earlier in the call.
- The molecule/group coverage-visibility dashboard and the broader scope wishlist are treated as **separate future roadmap items**, not part of this quantification exercise.

## Action Items

- [ ] **Marek Pillár**: Fill in the Business Quantification/KPI Excel for MaxBuddy from this call and send to Vosmek for review — **done, filled directly in `Max Buddy BQ`** — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **Luboš Vosmek**: Send the exact revenue-uplift % attributable to MaxBuddy and the case-count basis it's calculated on — due 2026-09-18 morning — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **Luboš Vosmek**: Send the current baseline % of single-item dispensing and the formal 1.5pp/year reduction target in writing — due 2026-09-18 morning — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **Luboš Vosmek**: Review, edit, and confirm the completed MaxBuddy BQ sheet — due 2026-09-18, ahead of Marek's sync with Tomáš Dudaško — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **Luboš Vosmek**: Send his broader MaxBuddy scope-expansion wishlist separately — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **Marek Pillár**: Schedule a follow-up discovery/prioritization call on Vosmek's wishlist, with Tomáš Dudaško involved on priority/resourcing — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **Jura Brázdil**: Build per-expedient click-through tracking on MaxBuddy's decision-tree ("stromy") branches — previously requested, still not delivered — from 2026-09-17-business-quantification-maxbuddy-vosmek
- [ ] **BigHub (owner TBD)**: Scope and build a molecule/group coverage-visibility dashboard for Vosmek (red/blue/yellow status per group) — motivated by the undetected ~14-day fiber data-feed outage — from 2026-09-17-business-quantification-maxbuddy-vosmek

## Open Questions

- Exact current MaxBuddy molecule coverage count (was 26, expanded again last week — new total unconfirmed) and resulting % of dispensing cases covered (Vosmek estimated ~40%).
- Whether/how to classify MaxBuddy's current live feature as "AI" for portfolio-tracking purposes, given Vosmek's own characterization that it's rule/data-driven, not LLM-based.
- Owner for the molecule/group coverage-visibility dashboard build — not yet assigned (raised for Lukáš Sýč, but Vosmek is routing it through this channel since it concerns Tomáš Dudaško).
- Whether Jindřich Tůma still intends to join a MaxBuddy domain-expert session in person (per his 2026-09-09 stated intent) — did not join this one.

## Sentiment & Tone

Warm, relaxed, and unusually candid throughout — Vosmek handled the rocky audio start with easy humor ("at least I can say hi from the car") and stayed forthcoming even while driving. He was consistently precise about drawing lines Marek hadn't asked for: correcting the domain-expert assumption unprompted, refusing to overstate the revenue number rather than round it up ("I won't lie to you about the numbers"), and proactively vetoing the employee-satisfaction framing before Marek could even propose it as a value driver — a clear signal of someone protecting his team's trust rather than inflating the business case. He was refreshingly transparent about MaxBuddy's origin being partly political/psychological (a trust-building trojan horse) rather than a clean ROI story, and about the current feature not really being "AI." The fiber-outage anecdote, told without prompting, reads as a genuine and still-live frustration — a concrete, credible ask rather than a vague complaint. No friction with Marek at any point; closed cooperatively with full Excel edit access and a same-day commitment to follow up with numbers.

## Routing Log

- **project-stakeholders**: Enriched STK-011 (Luboš Vosmek — owner-without-budget nuance, JTBD origin story, sentiment, Last interaction → 2026-09-17). Flagged possible identity overlap on STK-031 (Lukáš Síč) against this call's "Lukáš Sýč" — not merged, pending verification. Added STK-049 (Jiří Trajer — data-feed-only contact).
- **project-assumptions**: Added ASM-097 (MaxBuddy's live feature is data/rule-based, not LLM/AI — portfolio-classification question), ASM-098 (revenue/coverage figures provisional pending Vosmek), ASM-099 (all three KPI targets pending quantification from Vosmek).
- **project-daily**: 7 action items added to 2026-09-17's daily (Excel fill itself already done, not tracked as a pending item).
- **meetings/index**: Entry added.
- **Related**: `Max Buddy BQ` sheet in `~/Library/CloudStorage/OneDrive-BigHubs.r.o/2. Business Quantification/businessQuantificationWorskop.xlsx` filled and subsequently revised directly with this call's content, per PM request.
- **project-lessons**: Triggered autonomously — see project-lessons.md for any captured entries.
