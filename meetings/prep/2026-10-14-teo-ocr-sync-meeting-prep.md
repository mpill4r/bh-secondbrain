---
last_updated: 2026-10-12
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-14
attendees: [Alana Sihelská, Jura Brázdil, Radim Švarc, Michaela Albrechtová, Marek Pillár]
---

# Príprava na stretnutie — TEO/OCR sync

## Prehľad stretnutia

**Ciele** (odvodené z harnessu, pred stretnutím uprav):
1. Skontrolovať akčné body z 2026-10-01 (dávky, polia, JSON, Excel).
2. Preniesť výstup z utorkového stretnutia s Burdom (BQ čísla, jar 2027).
3. Stav infra (test, produkcia, BDC).

**Typ**: externé (pravidelný sync)
**Dátum**: streda 2026-10-14, 13:00 (pozvánku mala poslať Alana; over, že platí)
**Účastníci**: Alana Sihelská (STK-004), Jura Brázdil, Radim Švarc (STK-041), Michaela Albrechtová (STK-042), Marek Pillár
**Predchádzajúce stretnutie**: [2026-10-01](../external/2026-10-01-teo-ocr-sync-autumn-batches-costs-next-vendors.md)

## Otvorené body z 2026-10-01

| Kto | Čo | Stav |
|---|---|---|
| Jura | JSON k dávke z 09-30 | `-tbd-` |
| Míša | Spedos jeseň, menší dodávateľ, klimatizácie (~100 PDF do konca týždňa 10-09) | `-tbd-` |
| Míša | Zoznam názvov zariadení a revízií pre import (klimatizácie) | `-tbd-` |
| Jura | Spracovanie dávok best-effort; skúsiť príznak vyhovuje áno/nie pred 10-14 | `-tbd-` |
| Radim | Excel z JSON k dávke z 09-30 | `-tbd-` |
| Marek | Návrh na jar 2027 Radimovi, review s ním, potom Burda | Poslané 10-02; review s Radimom `-tbd-`; Burda 10-13 |

## Výstup od Burdu (2026-10-13), doplnené

- **OCR je pre TEO priorita č. 1** a Burda ho chce **čo najskôr**, nie „počas celého budúceho roka“ ([[ASM-273]]).
- **BQ riadok k OCR** berie ako dohodnutý; Marek ho preniesol do master trackeru (čakanie na potvrdenie je uzavreté).
- **Nové kandidáty na 2027**: notifikácie o výpadkoch elektriny na lekárňach ([[ASM-271]]) a kniha jázd ([[ASM-272]]). BigHub pripraví riadky, Burda ich doplní e-mailom.
- **Kocián** (Praha, prehliadky) sa pridá do OCR projektu so svojimi prehliadkami (STK-068).
- K návrhu na jar 2027 sa Burda nevyjadril.

## Kontext z harnessu

- Náklady ~1 Kč/strana priemer, Spedos ~2 Kč ([[ASM-220]]). Platforma pridáva sledovanie nákladov a limity.
- Číselník sa rieši napojením na API lekární ([[ASM-218]]).
- Test prostredie ~2 týždne od 10-01 (pod VPN), produkcia závisí od BDC.
- Protokoly bez adresy, od jari 2027 tlak na ID/adresu ([[ASM-222]]); ďalšie polia čakajú na Míšin zoznam ([[ASM-221]]).
- Otvorený rozpor: TEO nechce viac kandidátov pri disambiguácii ([[ASM-128]] vs. ASM-119).

## Navrhovaný program (30 min)

1. Stav dávok a výsledky (Jura, Míša) (10 min)
2. Nové polia: vyhovuje áno/nie, zariadenia (5 min)
3. Infra: test beží? produkcia/BDC (5 min)
4. Marek: výstup od Burdu (BQ, jar 2027) (5 min)
5. Ďalší sync (5 min)

## Otázky, ktoré treba zodpovedať

- Beží test prostredie automaticky? Kedy produkcia?
- Prišli dávky Spedos a klimatizácie? Aká bola cena za stranu pri Spedos?
- Pomohol príznak vyhovuje áno/nie?
- Radim: čo hovorí na návrh na jar 2027?

## Na čo si dať pozor

- Ak Burda v utorok niečo zmenil (čísla, smer), povedz to tu ako prvé, aby Radim nebol prekvapený.
- Tlač technikov na ID/adresu je na strane TEO. Netlač to ako požiadavku BigHubu.
