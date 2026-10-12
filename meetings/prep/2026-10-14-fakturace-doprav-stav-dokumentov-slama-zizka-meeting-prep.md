---
last_updated: 2026-10-12
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-14
attendees: [Petr Sláma, Jan Žižka, Tereza Foltová, Filip Černý, Marek Pillár]
---

# Príprava na stretnutie — Fakturácia dopráv: kde sa drží stav dokumentov (Sláma + Žižka)

## Prehľad stretnutia

**Cieľ**: odísť s **jedným modelom**, na ktorom sa zhodnú Sláma aj Žižka. Kedy a čo BigHub posiela do Axapty a kto drží neúplné dokumenty. Potom BigHub aktualizuje dokument procesu a Swagger.

**Typ**: externé
**Dátum**: streda 2026-10-14, 8:30 (pozvánku posiela Tereza; Žižkova účasť zatiaľ nepotvrdená)
**Účastníci**: Petr Sláma (STK-034, Axapta), Jan Žižka (STK-015, business vlastník fakturácie dopráv), Tereza Foltová (STK-013), Filip Černý (STK-006), Marek Pillár. Filip je od štvrtka na dovolenke.

## Dva modely na stole

| | **Žižka (2026-09-10, [[ASM-053]])** | **Sláma (2026-10-12, [[ASM-269]])** |
|---|---|---|
| Čo ide do AX | Každý sken hneď, aj jedna strana trasy | Iba **kompletný dokument** (všetky strany), hneď ako je kompletný, aj keď trasa nie je |
| Neúplné dokumenty | V AX | U BigHubu, do AX až na pokyn (koniec mesiaca alebo jednotlivo z AI aplikácie) |
| Verzie | AX dostáva priebežne | **Bez verzovania v AX**; inak by AX len prepisovala dokument |
| Prečo | Logistika hneď vidí, čo chýba, a má čas urgovať pomalého dopravcu pred uzávierkou | AX nemá mechanizmus na verzie; návrh postavený na Žižkovom modeli zamietol Tomáš Hraško (príliš veľa vývoja v AX) |
| Dopad na BigHub | App nedrží stav (dnešný stav, [[ASM-053]]) | BigHub potrebuje vlastnú databázu dokumentov („ľahké rozšírenie“, Filip) |

## Kontext z harnessu

- **Swagger v0.9.11** (zjednodušený): Sláma ho schválil („viac by som to nezjednodušoval“). Chce aktualizovaný dokument procesu aj Swagger po tomto stretnutí.
- **Dnešný Swagger**: BigHub posiela autoritatívne najnovšiu verziu dokumentu (AX nič neporovnáva).
- **Súvisiace**: trasy sa posielajú do AX priebežne a AX rozhoduje o uzávierke sama, mesačný cron zrušený ([[ASM-084]]); km porovnanie robí AX ([[ASM-082]]); viac vozidiel na trase sa prepisuje ([[ASM-135]]); verzovanie je v kóde lokálne ([[ASM-132]]); párovanie cez AR ([[ASM-133]]).
- **Sláma** je kapacitne limitovaný, robí jednu vec naraz ([[ASM-257]]).
- **Lekcia** ([[LL-89]]): rozpor nevytýkať, len ich dať dokopy a spýtať sa „tak ako to bude?“.

## Navrhovaný program (30 min)

1. Marek: prečo sme tu, dva modely v jednej vete každý (3 min)
2. Žižka: čo potrebuje vidieť v AX počas mesiaca a prečo (7 min)
3. Sláma: čo AX vie a nevie (verzie, stav per trasa/dokument) (7 min)
4. Hľadanie zhody (10 min)
5. Rekap a ďalší krok: BigHub aktualizuje dokument + Swagger (3 min)

## Možný kompromis (ak sa zasekne)

- Do AX ide **kompletný dokument hneď**. Pre neúplné posiela BigHub do AX **iba stav/metadáta** (napr. „trasa X: chýba strana 2 z ROZV“), nie dokument a nie verzie. Žižka vidí, čo chýba, Sláma nemusí verzovať.
- Koniec mesiaca: tlačidlo „pošli všetky neúplné za mesiac“, prípadne jednotlivo.
- Over s Filipom pred stretnutím, či je to v API realistické.

## Otázky, ktoré treba zodpovedať

- Potrebuje Žižka v AX počas mesiaca **dokument**, alebo mu stačí **informácia**, že niečo chýba?
- Kto a kde urguje dopravcu, keď chýba dokument (AX, AI aplikácia, e-mail)?
- Na úrovni čoho sa sleduje kompletnosť: dokument alebo trasa?
- Kto dáva pokyn „pošli neúplné“ a kde (AI aplikácia, AX)?
- Do kedy BigHub dodá aktualizovaný dokument procesu a Swagger?

## Na čo si dať pozor

- Sláma sa stavia s BigHubom ako „implementátori“ proti Žižkovi. **Nestav sa na stranu**, BigHub sa prispôsobí.
- Ak Žižka nepríde, nerozhodujte bez neho. Dohodnite len návrh, ktorý mu Tereza vysvetlí.
- Ak vyhrá Slámov model: nový vývoj na strane BigHubu (DB dokumentov). Neprisľubuj termín bez Filipa a Jindřicha.
