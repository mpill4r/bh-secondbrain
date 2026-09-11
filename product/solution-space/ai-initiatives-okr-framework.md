---
last_updated: 2026-09-11
last_updated_by: manual — conversational
---

# AI Initiatives — Objective / Key Results Framework

A single, strict structure for every tracked AI initiative, and the exact questions to ask on the call to fill it in.

## Framework

Built on **OKRs (Objectives and Key Results)** — the standard product-management framework for separating a qualitative business goal from the measurable evidence that it was reached ([Atlassian](https://www.atlassian.com/agile/agile-at-scale/okr), [Product School](https://productschool.com/resources/glossary/okr), [Wikipedia](https://en.wikipedia.org/wiki/Objectives_and_key_results)).

## The card — 6 fields, always in this order

| Field | Question to ask |
|---|---|
| **Vlastník (Owner)** | Prefilled if a record exists — confirm it's still accurate. |
| **Domain expert** | Left blank on every card — determined together, live, on the call. |
| **Objective** | Jaký je byznys cíl? Proč na tom záleží? |
| **Business hodnota / OKR** | Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| **Klíčové KPI / měření** | Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| **Poznámky / otevřené otázky** | Co zůstává nejasné? |

Only **Reklamace** and **Fakturace od dodavatelů** are prefilled below, with whatever brief already exists for them — every other field on every other card is the literal question, left blank on purpose. Nothing is guessed.

## Interview guide — how to lead these conversations

Each field uses a different technique, because "what's the objective" and "what's the number" are different kinds of question and fail differently when asked the wrong way.

### Opening (say this before field 1, once, per initiative)

> "Pro {initiative} chci s tebou projít 6 věcí — kdo to vlastní, kdo je odborný kontakt, proč to děláme, jaká je hodnota, jak to změříme, a co zůstává otevřené. Není problém říct 'nevím' — pak to prostě odhadneme společně a označíme jako odhad, ne jako fakt."

This sets the "nevím je v pořádku" norm up front — it's the single biggest thing that keeps people from just guessing to look competent, which produces fake-precise numbers you can't trust later.

### Time budget for the 11 cards

- **Reklamace** (5 min) — confirm, don't discover. This one's already documented; spend the time on the 2 blank fields only (Klíčové KPI/měření, Domain expert).
- **Fakturace od dodavatelů** (10 min) — the ASM-006 overlap question (is this the same as Fakturace doprav?) needs answering *before* anything else on this card, or you'll quantify the wrong thing.
- **Kontrola beden** (10 min) — starts from zero.
- **The 8 ideas** (10 min total, not 10 min each) — triage first, don't interview all 8 in depth. Ask one question across all 8: *"Which of these, if any, would you actually put a person on in the next 6 months?"* Only the survivors get the full 6-field treatment; the rest stay as titles.

### Field 1 — Vlastník (Owner)

**Ask**: "Je Rudolf Žůrek pořád ten, kdo za tohle formálně odpovídá?"
**If no**: "Kdo tedy?" — update immediately, don't leave the old name standing.

### Field 2 — Domain expert

**Ask**: "Kdo je člověk, který nám dnes dokáže dát nejlepší odpověď na zbytek téhle karty?"
**Technique — single-threaded owner**: insist on one name, not a team or department. "Sklad/logistika" is not an answer here; a person is. If they name two people, ask which one is accountable if the number turns out wrong.

### Field 3 — Objective

**Technique — Jobs-to-be-Done interviewing**: ask *what* and *how*, never *why* — "why" questions make people rationalize after the fact and hand you a plausible-sounding story instead of the real reason ([LinkedIn — JTBD question framework](https://www.linkedin.com/pulse/framework-questions-jobs-done-interviews-michael-boysen), [Dscout — JTBD interviewing style](https://dscout.com/people-nerds/the-jobs-to-be-done-interviewing-style-understanding-who-users-are-trying-to-become)).

**Ask, in order**:
1. "Co se dnes děje, co byste chtěli, aby fungovalo jinak?" (not "why do you want this")
2. "Co je na tom dnes nejvíc zdržující nebo frustrující?"
3. "Byl moment, kdy jste si řekl/a — takhle to dál nejde?"

**If the answer stays vague** ("chceme to zlepšit"): "Kdyby to fungovalo dokonale, co byste zítra ráno dělal/a jinak, co dnes dělat nejde?" — forces a concrete before/after instead of a mission statement.

### Field 4 — Business hodnota / OKR

**Technique — Fermi estimation**: when there's no baseline (true for 10 of these 11 cards), don't ask for a remembered fact — build the number live, out loud, from smaller pieces. Structure it as: scope → assumptions → central estimate → range, and sanity-check with a second calculation path ([Anderson — Fermi estimation for business problems](https://gwern.net/doc/statistics/prediction/2010-anderson.pdf)).

**Ask, in order**:
1. "Kolik lidí / hodin / případů týdně se toho dnes týká?" (get a volume first, not a value)
2. "Kdybyste musel/a hádat, i nepřesně — kolik by to bylo v Kč, čase, nebo FTE?"
3. "Jaký je rozsah — od kolika do kolika, ne jedno přesné číslo?"
4. Cross-check: "Sedí to i spočítáno jinak — třeba počet případů × čas na jeden × sazba?" If the two paths disagree by more than ~2×, the number isn't ready to write down yet — mark it 🟡 and flag which assumption is shaky, in Poznámky.

### Field 5 — Klíčové KPI / měření

**Technique — SMART specificity check**: a Key Result only counts if it's specific and measurable, not just directionally true ([JTBD/Fermi search synthesis](https://valchanova.me/customer-development-jobs-to-be-done/)).

**Ask, in order**:
1. "Jak konkrétně to změříme — jaký systém, report, nebo čí je práce to zapsat?"
2. "Jak často se na to bude koukat — týdně, měsíčně?"
3. "Kdo to uvidí, když to nevyjde?" (if nobody's named, nobody will look)

### Field 6 — Poznámky / otevřené otázky

Not a question — a capture step. Every open item gets a name and a next step, not just a note: *"kdo to zjistí, do kdy."* An open question with no owner just reappears at the next meeting unchanged.

### Rescue script — when someone says "nevím"

This will happen on most of the 9 blank cards. Don't let it end the conversation:

> "To je v pořádku — pojďme to nahrubo odhadnout společně teď, přesnost doladíme příště. Radši hrubý odhad označený jako odhad, než prázdné pole."

Then go straight into the Fermi sequence above (Field 4) even for the Objective/KPI fields — a rough, owned guess beats a blank field every time, as long as it's honestly labeled 🟡 estimate rather than passed off as 🟢 confirmed.

---

## Scope of this document

The **11 Žůrek / logistics initiatives** relevant to the 2026-09-14 session with Tereza Foltýnová: the 3 initiatives Rudolf Žůrek directly owns, plus each of the 8 Sklad/Logistika-domain ideas as its own card. The other 6 named portfolio initiatives (MaxBuddy, Max Chatbot, Lexie, Maxie, Listing, Řízení poptávky, Fakturace doprav, TEO_OCR, TD revize, Certifikáty dodavatelů, Optimalizace tras, Core Call Centrum, Poradna) were covered in an earlier pass and can be restored on request.

---

## 1. Reklamace — prefilled

| Field | Content |
|---|---|
| Vlastník | Rudolf Žůrek — confirm |
| Domain expert | _____ (candidate: Petr Sláma) — confirm on call |
| Objective | Automatizovat zpracování dodavatelských reklamací — dnes 8 h/den u 4 pracovníků kvality. |
| Business hodnota / OKR | Časová úspora: baseline 8 h/den (4 × 2 h) → 45 % úspora na příjmových reklamacích (největší fáze), 5–30 % v dalších fázích. Interní odhad přínosu 90 000 Kč — nepotvrzeno. |
| Klíčové KPI / měření | _____ — doplnit na hovoru (jak se bude % úspora reálně sledovat) |
| Poznámky / otevřené otázky | Platí fázové % úspory ještě dnes, nebo se změnil štáb? MVP většinou hotovo; fotodokumentace a znalostní báze dodavatelů zůstávají Blocked. |

---

## 2. Fakturace od dodavatelů — prefilled (thin brief)

| Field | Content |
|---|---|
| Vlastník | Rudolf Žůrek — confirm |
| Domain expert | _____ (candidate: Jan Žižka) — confirm on call |
| Objective | _____ — doplnit na hovoru. Dnes jen popsáno jako "automatizace zpracování dodavatelských faktur," nikdy neformulováno jako byznys cíl. |
| Business hodnota / OKR | Interní odhad přínosu 450 000 Kč — nejvyšší ze všech tří, zcela nepotvrzeno. Žádná baseline dnešní ruční zátěže neexistuje. |
| Klíčové KPI / měření | _____ — doplnit na hovoru |
| Poznámky / otevřené otázky | Je to totéž co Fakturace doprav, nebo samostatná iniciativa? Nevyřešeno od 2026-09-02 ([[ASM-006]]). Interně popisováno jako "ještě v plenkách." |

---

## 3. Kontrola beden — to fulfill on the call

| Field | Content |
|---|---|
| Vlastník | Rudolf Žůrek — confirm |
| Domain expert | _____ — doplnit na hovoru (dříve zmíněn Jan Maroušek, nikdy nekontaktován — ověřit, jestli je pořád správná osoba) |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | Možný překryv s "Kamera na lince — kontrola obsahu bedny" (#6 níže) — ověřit, ať se nepočítá dvakrát. |

---

## 4–11. Sklad / Logistika — 8 samostatných karet, všechny to fulfill on the call

Žádná z nich nemá vlastníka ani objective — jen název. Každá dostává stejnou strukturu.

### 4. Automatické objednávky dle sezónnosti a počasí

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | _____ |

### 5. Alokace zboží mezi sklady

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | _____ |

### 6. Kamera na lince — kontrola obsahu bedny

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | Možný překryv s Kontrola beden (#3) — ověřit, jestli je to totéž. |

### 7. Inteligentní rádce pro vedoucího skladu

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | _____ |

### 8. Konsolidace / rozdělování balíčků (master data)

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | _____ |

### 9. Balancování skladových zásob vč. lékáren

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | _____ |

### 10. Supply chain — komplexní AI/Copilot strategie

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | Nejširší/nejvágnější položka ze všech 8 — možná spíš zastřešující téma než samostatná iniciativa. |

### 11. Sklad — vychystávací strategie (AI decision engine)

| Field | Content |
|---|---|
| Vlastník | — žádný záznam |
| Domain expert | _____ — doplnit na hovoru |
| Objective | _____ — Jaký je byznys cíl? Proč na tom záleží? |
| Business hodnota / OKR | _____ — Jakou hodnotu (Kč / čas / FTE) to přinese? Jaký je cílový Key Result? |
| Klíčové KPI / měření | _____ — Jak přesně poznáme a změříme, že jsme cíle dosáhli? |
| Poznámky / otevřené otázky | _____ |

---

## Rollup

| Field completed | Count |
|---|---|
| Objective + Business hodnota prefilled | 1 — Reklamace |
| Business hodnota only (thin) prefilled | 1 — Fakturace od dodavatelů |
| Fully blank, to fulfill live | 9 — Kontrola beden + 8 idea cards |
| Vlastník known | 3 (all Rudolf Žůrek) |
| Vlastník unknown | 8 |
| Domain expert known on any card | 0 — by design, every card confirms this live |

**Sources**: `product-roadmap-portfolio-full.xlsx` (Portfolio + individual sheets), `project-stakeholders.md`, `project-knowledge.md`, `project-assumptions.md` ([[ASM-006]]), and prior meeting notes across this account.
