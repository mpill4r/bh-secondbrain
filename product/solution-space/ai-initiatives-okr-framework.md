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

Narrowed to the **11 Žůrek / logistics initiatives** relevant to the 2026-09-14 Business Quantification session with Tereza Foltýnová: the 3 initiatives Rudolf Žůrek directly owns, plus the 8 unassigned Sklad/Logistika-domain ideas. The other 6 named portfolio initiatives (MaxBuddy, Max Chatbot, Lexie, Maxie, Listing, Řízení poptávky, Fakturace doprav, TEO_OCR, TD revize, Certifikáty dodavatelů, Optimalizace tras, Core Call Centrum, Poradna) were covered in an earlier pass of this document and can be restored on request — dropped here to keep this version focused on what's actually on Monday's agenda.

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

## Kontrola beden

**Owner**: Rudolf Žůrek (named contact: Jan Maroušek — never actioned) · **Status**: Idea

**Objective**: 🔴 Unset

**Key Results**: 🔴 None set

**What's going into it**: Automated crate/box content control via camera, compared against WMS. Feature sheet is completely empty.

**Confidence**: 🔴

**Open questions**: Is Jan Maroušek still the right contact? Possible overlap with "Kamera na lince" in the idea backlog below.

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
| 🟡 Partial (benefit estimate only, unconfirmed) | 1 | Fakturace od dodavatelů |
| 🔴 Nothing quantified | 1 | Kontrola beden |
| 🔴 Not yet real initiatives (title only, no owner) | 8 | The warehouse/logistics idea backlog |

**Sources**: `product-roadmap-portfolio-full.xlsx` (Portfolio + all individual sheets), `project-stakeholders.md`, `project-knowledge.md`, `project-assumptions.md` ([[ASM-006]]), `product/solution-space/listing-specifikace.md`, and prior meeting notes across this account.
