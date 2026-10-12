---
last_updated: 2026-10-12
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-14
attendees: [Peter Šišo, Marek Pillár]
---

# Príprava na stretnutie — Peter Šišo (Akvizičné oddelenie): Lexie + iniciatívy 2027

## Prehľad stretnutia

**Ciele** (odvodené z harnessu, pred stretnutím uprav):
1. Upresniť dva use casy Lexie pre akvizície (zmluvy z TAS, stav akvizičného procesu).
2. Pozbierať prípadné ďalšie iniciatívy 2027.
3. Dohodnúť ďalší krok: vzorky dokumentov, prístupy, vlastník.

**Typ**: externé (prvé stretnutie)
**Dátum**: streda 2026-10-14 (čas `-tbd-`; v ten istý deň je o 8:30 fakturácia dopráv a o 13:00 TEO sync)
**Účastníci**: Peter Šišo (STK-061, business vlastník Lexie pre akvizície), Marek Pillár

## Kontext z harnessu

- **Odkiaľ prišiel**: Lukáš Szücs (STK-012), 2026-10-05. Jindřich odpovedal 10-06, že BigHub ho kontaktuje. Szücs je proxy.
- **Use case 1 (hlavný)**: porovnávanie **nájomných zmlúv** a extrakcia údajov z nich. Zmluvy sú v **TAS**.
- **Use case 2**: sledovanie **stavu akvizičného procesu** a notifikácie kľúčovým používateľom.
- **Outreach**: e-mail iba o Lexie odišiel 2026-10-09, odpovedal.
- **Lexie**: vlastníci Simona Mertová (produkt), Tomáš Dudaško (IT/rozpočet). Back-office agent na vlastnom SharePointe je možný, ale nie self-service ([[ASM-238]]).
- **Podobná práca**: extrakcia z dokumentov už beží pri TEO/OCR (servisné protokoly, ~1 Kč/strana, [[ASM-220]]), dá sa použiť ako referencia.

## Navrhovaný program (~30–45 min)

1. Predstavenie, čo BigHub robí pre Dr. Max (Lexie, extrakcia dokumentov) (5 min)
2. Akvizičný proces end-to-end: kroky, ľudia, systémy (10 min)
3. Use case 1: nájomné zmluvy (10–15 min)
4. Use case 2: stav procesu a notifikácie (5–10 min)
5. Ďalšie nápady na 2027 a ďalší krok (5 min)

## Otázky, ktoré treba zodpovedať

**Nájomné zmluvy (TAS)**
- Čo je TAS a ako sa z neho dostávajú dokumenty (export, API, len UI)? Kto ho spravuje?
- Koľko zmlúv (stovky, tisíce)? PDF so skenmi alebo text? Rôzne šablóny?
- Čo presne porovnávate (nájomné, doba, výpovedné lehoty, indexácia, opcie)? Proti čomu (štandard, iná zmluva, nová verzia)?
- Kto to dnes robí a koľko času to trvá na jednu zmluvu?
- Chcete odpovede v chate (Lexie), alebo tabuľku s vyťaženými údajmi?

**Stav akvizičného procesu**
- Kde sa dnes sleduje (Excel, SharePoint, TAS)? Aké sú kroky a kto ich vlastní?
- Kto má dostať notifikáciu a kedy (termíny, zmena stavu)?
- Je to skôr AI, alebo čistá automatizácia (Power Automate)?

**Všeobecne**
- Citlivosť dát (zmluvy, ceny), kto schvaľuje prístupy?
- Môžete poslať 3–5 vzorových zmlúv (anonymizovaných)?
- Kto je business vlastník a kto rozhoduje o priorite?

## Talking points a na čo si dať pozor

- Extrakcia zo zmlúv je skôr **automatizácia/OCR + LLM** ako chat. Lexie môže byť rozhranie, ale jadro je extrakcia. Pomenuj to, aby očakávania sedeli.
- Use case 2 môže byť čistá automatizácia: nie je isté, či ju pokryje AI rozpočet ([[ASM-233]]).
- Neprisľubuj termín bez kapacity od Jindřicha ([[ASM-190]]).
- Výstup zapíš do formátu trackeru 2027 (prínos + KPI + spôsob merania).
