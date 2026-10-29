---
last_updated: 2026-10-29
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-29
attendees: [Tereza Foltová, Petr Spilka, Jana Egrmaierová, Jan Žižka, Jindřich Tůma, Marek Pillár]
---

# Príprava — ViaPharma logistika: štvrtkový status (demo Reklamácií, demo Fakturácie dopráv, nová roadmapa)

## Prehľad stretnutia

**Ciele** (podľa zadania PM):
1. **Menšie demo Reklamácií**: login cez firemný účet funguje, krátke preklikanie.
2. **Demo Fakturácie dopráv**: prvé živé demo; čo vie, kde sú limity a čo potrebujeme od nich.
3. **Nová roadmapa (v2)**: ukázať ju a vysvetliť, **prečo** sme ju zmenili a **ako** je postavená.

**Typ**: externé (pravidelný status)
**Dátum**: štvrtok 2026-10-29, čas -tbd- (či sync vôbec bude, mali potvrdiť Jindřich / Tereza)
**Účastníci**: Tereza Foltová, Petr Spilka, Jana Egrmaierová, Jan Žižka (k fakturácii, ak príde), Jindřich Tůma, Marek Pillár.
- **Filip má dovolenku** (štvrtok a piatok). Je na Teams, ale bez notebooku, takže technické otázky si len zapíš.
- **P. Sláma je tento týždeň mimo** (WMS).

**Predchádzajúce stretnutie**: [2026-10-22](../external/2026-10-22-viapharma-reklamace-sync-slama-out-email-test-setup-fakturace-excel.md)
**Podklady**:
- `Reklamace-roadmapa v2.xlsx` (OneDrive, 3. Reklamace/Final)
- Filipove správy z 10-27
- zip `testovací_trasy`
- [interná porada s Filipom 10-27](../internal/2026-10-27-listing-evaluation-fakturace-mock-review-filip.md)

## Stav sľubov z 10-22

| Kto | Čo | Stav |
|---|---|---|
| Tereza / Sláma | Termín, dokedy ViaPharma dodá vstupy ([[ASM-330]]) | otvorené: **hlavná otázka dňa** |
| Tereza / Jana | ~3 testovací dodávatelia pre e-mailový test ([[ASM-331]]) | otvorené |
| Tereza | Finálny popis používateľského pohľadu (Jana) | otvorené |
| Tereza | Technický vlastník za logistiku ([[ASM-332]]) | otvorené |
| Filip | Login Reklamácií | **hotovo** |
| Filip | Mock Fakturácie pre logistiku | **hotovo** (len testovacie trasy) |
| Machata | Prístup k X-Manageru | **hotovo**: API overené, napojenie od 2. 11. |
| Filip → Kopecký | Zmeny Swaggeru | **odovzdané** J. Kopeckému (Boomi) |

## 1. Menšie demo Reklamácií (5 min)

- Login cez firemný Microsoft účet (Entra) funguje na tej istej adrese. Prístup majú všetci, čo chodia na statusy, cez svoj e-mail.
- Ukáž: prihlásenie → štítok → fotka → odoslanie. Tento tok si už 2 týždne testovali (aj p. Egrmaierová namiesto AX), takže stačí rýchlo.
- **X-Manager**: API funguje, Filip od pondelka napája znalostnú bázu.
- **Pozor**: J. Kopecký môže nasadiť zmeny Swaggeru skôr, ako sa Filip vráti. Aplikácia potom môže chvíľu nefungovať. Povedz to vopred; oficiálne UAT nebeží, takže to nevadí.
- Ak by niečo vyzeralo divne: Juraj robí veľa zmien na platforme a niekedy to vyzerá nefunkčne, aj keď to funguje.

## 2. Demo Fakturácie dopráv (15 min)

**Odporúčanie z 10-27**: neukazuj naživo, len popíš stav. Ak predsa demo:
- **pred stretnutím** si preklikaj zip `testovací_trasy`
- aplikácia ide len cez **VPN**

**Čo ukázať (scenár)**:
1. Nahrať jednu stranu z testovacej trasy: zaradí sa k trase a k dokumentu ako „strana 2 zo 6". **Toto je silná stránka**: ľubovoľná strana, poradie nehrá rolu.
2. Nahrať ďalšiu stranu toho istého dokumentu. Stránky sa spracúvajú paralelne, ~5–10 s na stranu.
3. Nahrať tú istú stranu znova: ukáže sa ako aktualizovaná (prepíše sa).
4. Nahrať úplne iný dokument: „Dokument se nepodařilo přiřadit k trase". Tak je to správne.
5. Ukázať počítanie pečiatok s nízkou istotou a hláškou „zkontrolujte".

**Ako to funguje (jednou vetou)**: BigHub nemá vlastnú databázu. Prečíta AR číslo, opýta sa Axapty, aké dokumenty k trase čaká, a vráti jej čisté, poskladané dokumenty aj s vyčítanými údajmi.

**Prečo po jednej strane**: tak to robí aj skutočný skener (jeden súbor = jeden list, strany môžu byť pomiešané). Používateľ zároveň vidí, čo sa s každou stranou stalo.

**Limity, otvorene** (Filip: ~98 % strán je prečítaných buď správne, alebo s príznakom „neistý, skontrolujte"):
- Testovať sa dá **len na testovacích trasách**. Filip na ne ručne dotlačil AR číslo a jeho **mock Axapta** zatiaľ zastupuje skutočnú.
- **Blokér 1**: skutočné dokumenty stále nemajú AR číslo ani čiarový kód, hoci to ViaPharma na začiatku sľúbila. Nemáme ani vzorky novej verzie dokumentov.
- **Blokér 2**: Axapta zatiaľ nevie vyhľadať trasu („poznáš túto trasu, aké dokumenty čakáš?"). Bez toho to na reálnych trasách nepôjde.
- **Pečiatky** sú najslabšie miesto. LLM ich spoľahlivo počítať nebude.
- **Rukou písaný text** je druhá oblasť na zlepšenie. Platí: čo je jednoduché pre človeka, je jednoduché aj pre AI.
- Známa chyba: dokument s vytlačeným AR číslom, ktorý nepatrí k trase, sa môže zaradiť ako ZOPV.

**Otázky na nich**:
- Pečiatky: stačí vám, že pri časti prípadov systém povie „skontrolujte"? Ak nie, navrhujeme vlastný vision model ([[ASM-358]]):
  - odhad **±5 MD**, presnosť 95 %+, lacná prevádzka
  - podmienka: **všetky tvary pečiatok** vopred (vzorky)
- Rukopis: je pravda, že v nových verziách dokumentov bude rukou písaného menej? (Filip si to pamätá od p. Žižku.)
- Kedy budú vzorky dokumentov s AR číslom a kedy bude v Axapte vyhľadanie trasy (Sláma)?
- Kto si demo preklikne a dá spätnú väzbu? Filip o ňu výslovne stojí: okrem neho ho ešte nikto nepoužíval.

## 3. Nová roadmapa — prečo a ako (15 min)

**Prečo sme ju zmenili**:
- Pôvodné dodanie **4. 11.** a testovanie **4.–6. 11.** už neplatia:
  - P. Sláma je tento týždeň mimo (WMS) a od 16. 11. bude na BrightPick
  - termín vstupov od ViaPharma ešte nie je potvrdený ([[ASM-330]])
  - Filip má 29.–30. 10. dovolenku
- Nechceme ďalšie pevné dátumy, ktoré sa po týždni rozpadnú. Prvá verzia bola neaktuálna hneď na druhý deň.

**Ako je postavená**:
- **Dodanie BigHub = 5–7 pracovných dní po dodaní vstupov od ViaPharma.** Dátumy v Exceli sú orientačné. Predpoklad: vstupy a schválenia do **4. 11.**
- Orientačne:

  | | Dodanie | Testovanie |
  |---|---|---|
  | Fáza 1 | 10. 11. | 11.–18. 11. |
  | Fáza 1.1a | 19. 11. | 2 týždne |
  | Fáza 2 | 4. 12. | — |
  | Avízo | 21. 12. | — |

- Práca v AX pre Fázu 1 a 1.1a musí byť hotová **pred 16. 11.** (Sláma potom na BrightPick). Fáza 2 v AX je len okno; termín určí ViaPharma.
- **Nový stĺpec „Stav"**: hneď vidno, čo je hotové, čo čaká a čo je po termíne. Hárok **„Podle osob"** je zároveň krátky zoznam najhorúcejších blokérov, ktorý Tereza chcela 10-22.
- Hotové: login, prístup k X-Manageru. Odovzdané: zmeny Swaggeru J. Kopeckému.
- Po termíne: popis Fáz 3 a 4–5 (Jana, Tereza, Spilka; termín bol 26. 10.).

**Čo potrebujeme do 4. 11.**:
- Rezervovať testovacie okno (orientačne **11.–18. 11.**)
- Schválenie zmien API (Sláma, Kopecký)
- Chybové hlášky: prípady a texty (Sláma, Jana)
- Testovanie e-mailov: vybrať ~3 dodávateľov (Tereza)
- **Rozhodnutie, kedy posielať otisk e-mailovej komunikácie do AX**: na vyžiadanie, alebo pri uzavretí; prílohy zvlášť, alebo v PDF ([[ASM-360]]).
  - Je to rozhodnutie pre business, preto Tereza a Spilka, nie len Sláma.
  - Chceme ho čo najskôr, aby išlo do tej istej sady zmien API, ktorú robí J. Kopecký (Boomi).
- Zebra: potvrdiť model a požičať jeden kus (do 30. 10.)

## Navrhovaný program (40–45 min)

1. Stav sľubov z 10-22 (5 min)
2. Menšie demo Reklamácií + X-Manager + upozornenie na nasadenie Kopeckého (5 min)
3. Fakturácia dopráv: stav, limity, pečiatky, rukopis (15 min)
4. Roadmapa v2: prečo, ako, čo potrebujeme do 4. 11. (15 min)
5. Rekap: kto čo dokedy (5 min)

## Otázky, ktoré musia zaznieť

- **Dokedy ViaPharma dodá vstupy?** Od toho sa odvíja celá roadmapa.
- Kedy sa posiela otisk e-mailovej komunikácie do AX ([[ASM-360]])?
- Pečiatky: „skontrolujte" stačí, alebo ±5 MD na vision model?
- Vzorky dokumentov s AR číslom + vyhľadanie trasy v Axapte: kedy?
- Rezervujú testovacie okno 11.–18. 11.?

## Na čo si dať pozor

- Roadmapu podávaj ako **„termíny sa odvíjajú od vašich vstupov"**, nie ako náš sklz. Fakty: 4. 11. padol pre neprítomnosť Slámu a nepotvrdené vstupy.
- Pri limitoch Fakturácie nezabudni, že prínos je väčší, než si sami vyčíslili: ručná práca je dnes pomalá a chybová.
- Technické veci (Swagger, Boomi, Axapta lookup) len zapíš a nič nesľubuj za Filipa.
- Tereza: všetko dôležité potom **písomne** (recap e-mail).
