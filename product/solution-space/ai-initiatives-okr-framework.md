---
last_updated: 2026-09-11
last_updated_by: manual — conversational
---

# AI Initiatives — Objective / Key Results Framework

A single reusable structure for every tracked AI initiative: what business objective it serves, what measurable Key Results prove it worked, and what the initiative itself actually contains. Paired with a facilitator script for eliciting this from each business owner in a discovery interview.

## Framework

Built on **OKRs (Objectives and Key Results)** — the standard product-management framework for separating a qualitative business goal from the measurable evidence that it was reached, with the actual build work sitting one level below both ([Atlassian](https://www.atlassian.com/agile/agile-at-scale/okr), [Product School](https://productschool.com/resources/glossary/okr), [Wikipedia](https://en.wikipedia.org/wiki/Objectives_and_key_results)):

- **Objective** — the qualitative outcome. Answers *"what value are we driving for the business?"* One sentence, no numbers.
- **Key Results** — 2–3 quantitative metrics that prove the Objective was reached. Each has a **baseline** (today) and a **target** (by when). Answers *"how do we know we got there?"*
- **Initiative** — the actual project/build. In the OKR hierarchy, initiatives are the work that moves a Key Result — this is "what's going into it."

This directly matches what every tracked project in this account is missing today: a roadmap Excel full of initiative *names* and effort estimates, with almost no Objective or Key Result attached to any of them.

## The card (one structure, every initiative)

```
INITIATIVE — {name}
Owner: {business owner}                    Status: {idea / scoping / in progress / live}

OBJECTIVE
{one qualitative sentence — why this matters to the business}

KEY RESULTS
KR1: {metric} — baseline {X} → target {Y}, by {date}
KR2: ...
KR3: ...

WHAT'S GOING INTO IT
{what the initiative actually builds/contains}

CONFIDENCE: 🟢 confirmed by owner · 🟡 estimate · 🔴 unknown

OPEN QUESTIONS
{what to ask the owner directly}
```

## Interview guide — how to lead these conversations

Grounded in standard OKR-workshop facilitation ([Caroli.org](https://caroli.org/en/objectives-and-key-results-workshop-session/), [Asana](https://asana.com/resources/okr-meaning)), sequenced for a 1:1 or small-group session with a business owner. Run in this order — each question only makes sense once the previous one is answered.

1. **Context** — "What's the current state of {initiative}, in your own words?" (grounds the conversation in their reality before asking anything abstract)
2. **Objective** — "Where do we want this to go? What does success look like for the business, not for the software?" → this becomes the Objective. Push past "it should work well" — ask "and what would that let you or your team do that you can't do today?"
3. **Key Results** — "How would you know, without me telling you, that we got there?" → brainstorm 2–3 candidate metrics. If they only offer qualitative answers, ask "if you had to put a number on that, even a rough one, what would it be?"
4. **Baseline** — "What's true today, before any of this exists?" — this is usually the hardest part to get and the most valuable; don't let it stay vague ("it takes a while") — push for a number, even an estimate range.
5. **Target** — "What number would make this a clear win? What number would be a stretch?" — capture both.
6. **Measurement method** — "How and when will we actually check this?" — a Key Result nobody measures isn't one.
7. **Confidence check** — reflect the Objective/KRs back and ask the owner to color-code them themselves: confirmed / estimate / unknown. This transfers ownership of the number to them, not to you.
8. **Open questions** — anything that came up but couldn't be resolved live goes into the parking lot, explicitly assigned to someone with a next step.

---

## Scope of this document

Applied to the **17 named initiatives** that exist as their own tracked entity (a Portfolio row and/or its own detail sheet in `product-roadmap-portfolio-full.xlsx`). Excluded: the **40+ bare one-line "idea" rows** in the Portfolio sheet (warehouse/pharmacy/HR/marketing wishlist items with no owner, no objective, nothing to interview about yet) — those need a lighter-weight intake pass first, not a full OKR interview. Happy to run that as a separate exercise if useful.

---

## MaxBuddy

**Owner**: Tomáš Dudaško (domain expert: Lubos Vosmek) · **Status**: Live, MVP 100% complete, deployed on 21 pobočky

**Objective**
Help pharmacists give better dosage guidance and surface relevant upsell during checkout, without slowing down service.

**Key Results**
- KR1: Live on 21 branches — 🟢 confirmed (Produkční nasazení: Hotovo)
- KR2: Internal benefit estimate 150 000 Kč — 🟡 not confirmed with business
- KR3: (unset) — 🔴 ask owner directly what "success" looks like now that it's live

**What's going into it**
Dosage-check + upsell recommendation engine integrated into Farmis; core flow (integration, complex-care recommendation, product suggestion, reasoning, OTC scenario, stock availability, product data) all Done. A second batch (dosage calculation, dosage verification, medication-quantity check, dosage traffic-light) is technically built but deactivated pending medical-device certification. "Analytika" (usage analytics) is blocked on missing data — flagged as low-stakes, already handed to the Farmis team, no BigHub action needed.

**Confidence**: 🟡 — build status is solid, business value is not yet owner-confirmed

**Open questions**: Now that it's live on 21 branches, what's the actual observed impact (sales lift, time saved per pharmacist)? Is there a rollout plan beyond 21 branches?

---

## Max Chatbot

**Owner / domain expert**: Simona Mertová · **Status**: In Development, 40% complete

**Objective**
Let Dr. Max customers self-serve common queries (order status, pharmacy locator, e-recepty, stock) via chat, reducing load on human channels.

**Key Results**
- 🔴 None set — Portfolio benefit/score fields are empty

**What's going into it**
LLM-backed customer-facing chatbot on drmax.cz, with a medical-advice guardrail. Demoed live to strong client praise.

**Confidence**: 🔴 — no business quantification exists anywhere for this initiative

**Open questions**: What volume of queries would need to shift from human channels to call this a win? Simona Mertová was asked (2026-09-03) for business-case/time-savings metrics — still outstanding.

---

## Lexie

**Owner**: Tomáš Dudaško (domain expert: Simona Mertová) · **Status**: In Testing, 40% complete

**Objective**
Give the Dr. Max CC (call center) team an internal RAG assistant so they answer faster and more consistently.

**Key Results**
- 🔴 None set

**What's going into it**
Internal AI agent (RAG over CC knowledge base), role-based access built for 4 CC sub-departments; test-account mechanics for multi-role testing still being worked out.

**Confidence**: 🔴

**Open questions**: Same outstanding ask as Max Chatbot — lightweight time-savings metrics per CC sub-department, never delivered.

---

## Maxie

**Owner / domain expert**: Simona Mertová · **Status**: In Development, 40% complete

**Objective**
Extend Max Chatbot's self-service coverage to the voice/IVR channel, replacing manual phone handling for the same query types.

**Key Results**
- 🔴 None set (only build-effort estimates exist — MVP 30 MD / Full Version 25 MD / Nice to Have 22 MD — that's cost, not value)

**What's going into it**
Voice/IVR channel reusing Max Chatbot's backend; MVP estimate may land under 30 MD since core LLM/prompting is shared with Max Chatbot.

**Confidence**: 🔴

**Open questions**: What's the current IVR call volume/cost this is meant to reduce?

---

## Listing

**Owner**: Petr Neuman · **Status**: In Testing, 15% complete

**Objective**
Higher conversion — a quality, consistent product listing sells better than today's manual, inconsistent one.

**Key Results**
- KR1: Catalog health score (already computed per-product by the tool) — no baseline/target set yet — 🟡
- KR2: Conversion rate on listed products — 🔴 not tracked
- KR3: Internal benefit estimate 300 000 Kč — 🟡 unconfirmed, previously flagged by Alana Sihelská as unconvincing

**What's going into it**
Full detail already captured in `product/solution-space/listing-specifikace.md` — content generation, category-standards config ("Listovací minima"), compliance guardrail, currently 1 pilot category (72 products).

**Confidence**: 🟡

**Open questions**: See that document's Open Questions section — KPI targets specifically are still open.

---

## Řízení poptávky (Order/Demand Prediction)

**Owner / domain expert**: Marek Šimoník / Petr Ondráček · **Status**: In Testing, 30% complete

**Objective**
Forecast order volume and revenue so the business can react faster to market shifts (both strategic planning and shift-level logistics).

**Key Results**
- KR1: Internal benefit estimate 220 000 Kč — 🟡 unconfirmed
- KR2: (unset) — 🔴 forecast accuracy target never defined

**What's going into it**
Live dashboard (v1 done), covering daily/weekly strategic forecasting and 6–12h shift-level logistics forecasting from largely the same model.

**Confidence**: 🟡

**Open questions**: What forecast-accuracy threshold counts as "good enough" for the business to act on it?

---

## Reklamace

**Owner**: Rudolf Žůrek (domain expert: Petr Sláma) · **Status**: In Testing, 20% complete

**Objective**
Automate manual complaint processing, currently consuming ~8h/day across the quality team.

**Key Results**
- KR1: Time saved — baseline 8h/day (4 staff × 2h/day) → 45% reduction on intake claims (largest phase); 5–30% across other phases — 🟢 already documented in the dev spec
- KR2: Internal benefit estimate 90 000 Kč — 🟡 unconfirmed

**What's going into it**
MVP mostly Done (intake, SP-label ID via Axapta, auto case creation, error handling); photo documentation and supplier knowledge-base still Blocked; document generation + email draft In Development.

**Confidence**: 🟢 — the strongest-documented initiative in the whole portfolio

**Open questions**: Do the phase-level savings percentages still hold given today's staffing?

---

## Fakturace od dodavatelů

**Owner**: Rudolf Žůrek (domain expert: Jan Žižka) · **Status**: In Development, 10% complete, described internally as "still in diapers"

**Objective**
🔴 Unset beyond "automate manual entry of supplier invoices into Axapta" — never articulated as a business outcome

**Key Results**
- KR1: Internal benefit estimate 450 000 Kč — 🟡 highest of any Žůrek-owned initiative, entirely unconfirmed
- KR2: (unset) — 🔴 no baseline for today's manual effort exists anywhere

**What's going into it**
OCR processing of supplier invoices at line-item level. Feature checklist exists (13 items: requirements → Swagger → Axapta API → OCR pipeline → UAT → production) with zero status filled in.

**Confidence**: 🔴

**Open questions**: Is this the same initiative as Fakturace doprav (below), or genuinely distinct? Flagged since 2026-09-02, never resolved (see [[ASM-006]]).

---

## Fakturace doprav (freight invoicing)

**Owner**: Jan Žižka / Petr Sláma · **Status**: MVP mostly Done — not in the Portfolio sheet at all, tracked separately through meetings

**Objective**
Digitize and automate processing of driver/carrier route documentation for freight invoicing and Axapta records.

**Key Results**
- 🔴 None set — no Kč/time business value figure documented anywhere for this initiative, despite being one of the most mature in the account

**What's going into it**
Kiosk-based document scanning (ZOPV, delivery confirmations, temperature logs, narcotics-transport confirmations); digitization, document processing, completeness check, and data validation all Done. UAT targeted for mid-October.

**Confidence**: 🔴 — mature build, zero business quantification

**Open questions**: This is arguably the single best candidate to quantify first — build is nearly done, so time/Kč baseline should be the easiest of all 17 to establish. Worth asking Jan Žižka directly rather than waiting for the Terka session.

---

## TEO_OCR

**Owner / domain expert**: Radim Švarc · **Status**: Prioritized, 10% complete

**Objective**
🔴 Unset beyond "OCR extraction of technical-department revision/repair protocol documents for ServiceNow"

**Key Results**: 🔴 None set

**What's going into it**: OCR pipeline for TEO documents, feeding ServiceNow.

**Confidence**: 🔴

**Open questions**: What manual process does this replace, and how much of it?

---

## TD revize

**Owner**: Tomáš Burda · **Status**: Prioritized / Not Started

**Objective**
🔴 Unset beyond "automation and elimination of manual document processing from revisions"

**Key Results**
- KR1: Internal benefit estimate 330 000 Kč — 🟡 unconfirmed, and inconsistent with the Portfolio's own priority-score field (shows 0)

**What's going into it**: 🔴 Nothing scoped — this stream has never appeared in a single meeting transcript.

**Confidence**: 🔴

**Open questions**: Who is Tomáš Burda, and has anyone actually spoken with him about this?

---

## Kontrola beden

**Owner**: Rudolf Žůrek (named contact: Jan Maroušek — never actioned) · **Status**: Idea

**Objective**: 🔴 Unset

**Key Results**: 🔴 None set

**What's going into it**: Automated crate/box content control via camera, compared against WMS. Feature sheet is completely empty.

**Confidence**: 🔴

**Open questions**: Is Jan Maroušek still the right contact? Possible overlap with "Kamera na lince" in the idea backlog below.

---

## Certifikáty dodavatelů

**Owner**: 🔴 Unknown — no Portfolio row exists, only an Excel tab

**Objective**
🔴 Unset beyond "electronic tracking of supplier certificate validity (SÚKL, BIO) incl. AI check at goods receipt"

**Key Results**: 🔴 None set

**What's going into it**: 🔴 Nothing scoped — empty feature sheet.

**Confidence**: 🔴

**Open questions**: Who owns this? It has no business or domain-expert contact anywhere in the harness.

---

## Optimalizace tras

**Owner**: 🔴 Unknown — no Portfolio row exists, only an Excel tab

**Objective**
🔴 Unset beyond "daily route optimization and reallocation based on capacity and constraints"

**Key Results**: 🔴 None set

**What's going into it**: 🔴 Nothing scoped.

**Confidence**: 🔴

**Open questions**: Same as above — no owner anywhere.

---

## Core Call Centrum

**Owner**: 🔴 Unknown — no Portfolio row exists, only an Excel tab

**Objective**
🔴 Unset beyond "backup project for Core Call Centrum after the AI platform rollout — synergy with the Maxie voice assistant"

**Key Results**: 🔴 None set

**What's going into it**: 🔴 Nothing scoped — reads as a placeholder for future Maxie-adjacent work rather than an active initiative.

**Confidence**: 🔴

**Open questions**: Is this real yet, or should it just be folded into Maxie's own roadmap?

---

## Poradna - Zeptejte se lékárníka

**Owner / domain expert**: Petr Neuman · **Status**: Idea

**Objective**
🔴 Unset beyond "speeding up patient consultation solutions"

**Key Results**: 🔴 None set

**What's going into it**: 🔴 Nothing scoped.

**Confidence**: 🔴

**Open questions**: Same owner as Listing (Petr Neuman) — worth asking about both in the same conversation.

---

## Warehouse/Logistics idea backlog (8 items)

**Owner**: 🔴 None — pure brainstorm list, no individual scoping

**Objective**: 🔴 Unset for any of the 8

**What's in it**: Automatické objednávky dle sezónnosti a počasí · Alokace zboží mezi sklady · Kamera na lince – kontrola obsahu bedny (possible overlap with Kontrola beden above) · Inteligentní rádce pro vedoucího skladu · Konsolidace/rozdělování balíčků · Balancování skladových zásob vč. lékáren · Supply chain – komplexní AI/Copilot strategie · Sklad – vychystávací strategie (AI decision engine)

**Confidence**: 🔴 — title-only, not yet real initiatives

**Open questions**: Which of these 8 are worth turning into real initiatives at all? This needs a lighter triage pass before any of them earn a full OKR card.

---

## Rollup

| Confidence | Count | Initiatives |
|---|---|---|
| 🟢 Objective + Key Results both real | 1 | Reklamace |
| 🟡 Partial (benefit estimate only, unconfirmed) | 4 | MaxBuddy, Listing, Řízení poptávky, Fakturace od dodavatelů |
| 🔴 Nothing quantified | 9 | Max Chatbot, Lexie, Maxie, Fakturace doprav, TEO_OCR, TD revize, Kontrola beden, Certifikáty dodavatelů, Optimalizace tras |
| 🔴 No owner at all | 3 | Certifikáty dodavatelů, Optimalizace tras, Core Call Centrum |

**Sources**: `product-roadmap-portfolio-full.xlsx` (Portfolio + all individual sheets), `project-stakeholders.md`, `project-knowledge.md`, `project-assumptions.md` ([[ASM-006]]), `product/solution-space/listing-specifikace.md`, and prior meeting notes across this account.
