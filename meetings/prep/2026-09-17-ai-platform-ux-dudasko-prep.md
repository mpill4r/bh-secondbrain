---
last_updated: 2026-09-17
last_updated_by: manual — conversational
---

# Meeting Prep — AI Platform UI/UX, Tomáš Dudaško (STK-010)

**Meeting**: 2026-09-17, with Tomáš Dudaško (Head of IT, Dr. Max — holds BigHub budget, primary approver)
**Duration**: 30 min
**Purpose**: Diagnose the "does not like UX" pain point on the AI Platform (Lexie/Max/Maxie/MaxBuddy) with enough specificity to scope a real fix, reconcile it against his written requirements Excel, and get his input on phasing — what belongs in phase 1, and what a successful end-of-phase looks like to him.

---

## Context going in

- **Sentiment**: "A bit frosty" per stakeholder record — paying for months without enough visible delivered value; expects results now that streams are nearing production. Open with acknowledgment, not straight into questions.
- **The wishlist Excel** (`Copy of DrMax_Expectations_with_BigHub_status.xlsx`) is **not a UX document**. All 48 tracked capabilities are governance/compliance-framed (identity, audit trail, NIS2/AI Act, DLP, EU residency) — zero UI/UX items. This matches the existing stakeholder note that both Marek and Jan Sovka independently assessed it as "~70% governance-framed, not addressing actual use cases." His verbal ask (unified test/prod environments, visual polish, consolidation onto the platform) diverges sharply from what he put in writing — worth surfacing directly rather than assuming the Excel is his real UX brief.
- **Open blocker**: "Sync with Ján Kabát before further platform conversations with Dudaško" (Jan Sovka, 2026-09-08) is still unresolved as of today. Kabát shaped how Dudaško currently frames the ask — stay in discovery mode today, avoid committing to a specific redesign direction.
- **Technical reality check** (Jura Brázdil, 2026-09-08): the platform today is essentially one RAG/document-retrieval product; MaxBuddy isn't migrated in yet; shared DB with no isolation between use cases; single shared admin account. Don't let a UX promise outrun what's actually buildable near-term.
- **One real proof point**: a Lexie visual-polish ticket is already open (Jindřich/Jura, 2026-09-10) — usable as evidence of momentum if needed.

---

## Script (Slovak, word-for-word)

**0:00–3:00 — Otvorenie**

> "Tomáš, ďakujem, že si si na toto stretnutie našiel čas. Mám vyhradených tridsať minút a chcem ich využiť na jednu konkrétnu vec — ako AI platforma pôsobí z pohľadu používateľského zážitku, teda UI/UX. Viem, že to je téma, ktorá ťa dlhšie trápi, a namiesto toho, aby som ti niečo navrhoval naslepo, chcem najprv poriadne pochopiť, čo presne ti na tom nesedí."

**3:00–9:00 — Diagnostika pain pointu** (jadro stretnutia — must-ask aj pri skrátení času)

1. "Keď hovoríš, že sa ti UX platformy nepáči — vieš uviesť konkrétny príklad? Ktorá obrazovka alebo ktorý moment ťa naposledy najviac zarazil?"
2. "Je to skôr o tom, ako to vyzerá vizuálne, alebo skôr o tom, ako je to poskladané — teda ako sa to používa a či to dáva logiku?"
3. "Týka sa to všetkých nástrojov — Lexie, Max, Maxie, MaxBuddy — alebo najmä jedného konkrétneho?"
4. "Máš pocit, že tieto nástroje pôsobia ako jeden konzistentný produkt, alebo skôr ako viacero samostatných vecí poskladaných vedľa seba?"
5. "Dostávaš k tomu spätnú väzbu aj od ľudí, ktorí s tým reálne pracujú — Simona a jej tím napríklad — alebo je to primárne tvoj vlastný dojem?"
6. "Napadá ti nejaký produkt — interný alebo externý — ktorý podľa teba robí UX dobre, a k tomu by sme sa mali aspoň priblížiť?"

**9:00–13:00 — Zosúladenie s dokumentom (Excel) a priority**

7. "Prešli sme si dokument, ktorý si pripravil k platforme. Je z veľkej časti o governance a compliance — identita, audit, riadenie prístupov. UX tam prakticky nefiguruje. Bol to zámer, alebo to bol skôr východiskový bod a UX je téma, ktorá je pre teba dôležitá popri tom?"
8. "Ak by sme si mali vybrať, čo rieši prvé — aby platforma bola bezpečnejšia a auditovateľná, alebo aby lepšie vyzerala a používala sa — čo z toho pre teba v tejto chvíli váži viac?"
9. "Keď hovoríš o zjednotenom testovacom a produkčnom prostredí a o vizuálnom doladení — je to pre teba jedna téma, alebo dve oddelené veci s inou prioritou?"

**13:00–17:00 — Definícia "dobrého UX"**

10. "Keby sme sa o tri mesiace stretli znova a ty by si povedal 'toto teraz vyzerá a funguje tak, ako malo od začiatku' — čo presne by si vtedy videl na obrazovke?"
11. "Existuje nejaká úplne minimálna zmena, bez ktorej by si toto stretnutie považoval za stratu času?"
12. "Máš pocit, že súčasný stav UX priamo ovplyvňuje, ako vieš platformu obhájiť pred vedením ako niečo, do čoho sa oplatilo investovať?"

**17:00–25:00 — Fázovanie** (druhé ťažisko stretnutia — explicitne požadovaný fokus)

13. "Ako si predstavuješ ďalší postup — má to byť jeden väčší krok, alebo by dávalo zmysel rozdeliť to na viac fáz?"
14. "Keby sme to rozdelili na fázy, čo by podľa teba malo byť v tej úplne prvej — a čo môže bez problémov počkať na neskôr?"
15. "Ako by pre teba konkrétne vyzeral úspešný koniec prvej fázy? Čo presne by si musel vidieť — na obrazovke, v číslach, alebo v spätnej väzbe od ľudí — aby si povedal, že fáza je hotová a môžeme ísť ďalej?"
16. "Je pre teba dôležitejšie, aby prvá fáza bola rýchla, aj keby pokryla menej vecí, alebo aby pokryla viac naraz, aj keby to trvalo dlhšie?"
17. "Ako často by si chcel počas jednotlivých fáz vidieť priebežný pokrok — pravidelne v čase, alebo až vtedy, keď bude fáza reálne hotová?"

**25:00–29:00 — Ďalšie kroky**

18. "Ak ti do ďalšieho stretnutia pripravíme konkrétny vizuálny návrh, mockup — ako by si ho chcel dostať? Naživo na stretnutí, alebo radšej dokument, ktorý si prejdeš sám vopred?"
19. "Kedy by pre teba dávalo zmysel sa znova stretnúť a pozrieť sa na prvý konkrétny návrh?"

**Closing**

> "Zhrniem si, čo som si dnes zapísal, a pošlem ti to na potvrdenie, nech mám istotu, že sme sa pochopili správne. Ďakujem za čas."

**If time is short**: protect questions 1–6, 13–17, and 18–19 — they deliver the diagnosis, the phasing structure, and a concrete next step even if the Excel-reconciliation and "definícia dobrého UX" sections get compressed.

---

**Sources**: `project-stakeholders.md` (STK-010 Tomáš Dudaško, STK-002 Jan Sovka, STK-026 Jura Brázdil), `Copy of DrMax_Expectations_with_BigHub_status.xlsx` (Overview/Capabilities/Roadmap sheets — full governance/compliance register, no UX content), project-daily 2026-09-17 (open action items re: Kabát sync, Lexie design-compromise ticket).
