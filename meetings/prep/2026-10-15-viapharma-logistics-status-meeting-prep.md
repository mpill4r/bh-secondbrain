---
last_updated: 2026-10-12
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-15
attendees: [Tereza Foltová, Petr Sláma, Petr Spilka, Jana Egrmaierová, Jindřich Tůma, Marek Pillár]
---

# Príprava na stretnutie — ViaPharma logistika: štvrtkový status

## Prehľad stretnutia

**Ciele** (odvodené z harnessu, pred stretnutím uprav):
1. Uzavrieť mapu dát (odpovede p. Slámu na riadky 17 a 21) a potvrdiť, že špecifikácia prvých fáz odišla.
2. Stav po testovaní: UX zmeny, login, zariadenie (Zebra vs. telefón).
3. Výstup zo stredajšieho stretnutia o fakturácii dopráv a ďalší krok (dokument + Swagger).
4. Roadmapa a ďalšie fázy.

**Typ**: externé (pravidelný status)
**Dátum**: štvrtok 2026-10-15, 10:00
**Účastníci**: Tereza Foltová, Petr Sláma, Petr Spilka, Jana Egrmaierová (ak príde), Jindřich Tůma, Marek Pillár. **Filip má dovolenku** (štvrtok a piatok); technické otázky si zapíš pre neho.
**Predchádzajúce stretnutie**: [2026-10-08](../external/2026-10-08-viapharma-reklamace-sync-data-map-slip-all-phases-slama-capacity.md) · [wrap-up 2026-10-12](../external/2026-10-12-reklamace-phase-1-testing-wrap-up-login-zebra-fakturace-state.md)

## Stav sľubov (doplň pred stretnutím)

| Kto | Čo | Termín | Stav |
|---|---|---|---|
| Marek | Komentáre do mapy dát (stĺpce K, L) + e-mail Slámovi | 10-12 | `-tbd-` |
| Marek | Aktualizovaná špecifikácia prvých fáz | 10-13 | `-tbd-` |
| Sláma | Odpovede na riadky 17 (spôsob vybavenia) a 21 (adresa skladu) | — | `-tbd-` |
| Filip | UX zmeny z testovania, chybové hlášky (návrh na Teams) | — | `-tbd-` |
| Filip / Sláma | Identita používateľa v API | — | `-tbd-` |
| Tereza | Call s IT (Dušan) + Spilka o zariadení | ASAP | `-tbd-` |
| Tereza | Testovací telefón do Brna | — | `-tbd-` |
| Jana | Podklady k fázam 3–5 | ~10-26 | v procese |
| Jindřich | Roadmapa Reklamácií s dátumami | — | `-tbd-` |
| Tereza | Call so Žižkom + Canon o skeneri | — | `-tbd-` |

## Kontext z harnessu

- **Mapa dát**: Sláma súhlasil so smerom; údaje mimo AX budú vo znalostnej báze ([[ASM-228]]), externý zdroj veľmi pravdepodobne X-Manager ([[ASM-243]], rieši Jindřich). Otvorené: [[ASM-262]] (riadok 17), [[ASM-263]] (riadok 21).
- **Testovanie fázy 1**: hotové ([[ASM-227]]); UX zmeny ([[ASM-267]]); login cez Microsoft ([[ASM-266]]); zariadenie otvorené ([[ASM-265]]).
- **Fakturácia dopráv**: výstup zo stredy 8:30 ([[ASM-053]], [[ASM-269]]).
- **Všetkých 5 fáz sa dokončí** ([[ASM-255]]); kapacita BigHubu na fázy 2–5 je menšia ([[ASM-256]]). Sláma robí jednu vec naraz ([[ASM-257]]).
- **Roadmapa** s dátumami je povinná, posuny sú OK ([[ASM-248]]).

## Navrhovaný program (45–60 min)

1. Mapa dát: uzavrieť riadky 17 a 21 (10 min)
2. Špecifikácia: čo sa zmenilo, kedy pripomienky od Slámu (5 min)
3. Testovanie: UX zmeny, login, zariadenie (10 min)
4. Fakturácia dopráv: výstup zo stredy, ďalší krok (10 min)
5. Roadmapa a fázy 3–5 (Jindřich) (10 min)
6. Rekap (5 min)

## Otázky, ktoré treba zodpovedať

- Sláma: dokedy pošle pripomienky ku špecifikácii?
- Tereza: padlo rozhodnutie o zariadení? Ak nie, kedy bude call s IT?
- Kedy prišiel / príde testovací telefón?
- Kedy ďalšia testovacia vlna (po UX zmenách a logine)?
- Platí plný UAT, alebo sa posúva?

## Na čo si dať pozor

- Pri kapacite vždy začni tým, že **dokončíme všetkých 5 fáz**, inak to znie ako odchod.
- Ak Filip chýba, technické detaily (API, Swagger) si len zapíš a nič neprisľubuj.
- Pošli recap po stretnutí (logistika ho víta, bez odpovede, ak nie sú námietky).
