---
last_updated: 2026-10-26
type: prep
meeting_date: 2026-10-26
attendees: [Marek Pillár, Filip Černý]
---

# Príprava — Listing: doplnky stravy s Filipom (to-do bod po bode)

## Prehľad stretnutia

**Názov**: Listing — podklady pre doplnky stravy, to-do pre Filipa
**Cieľ**: Prejsť s Filipom to-do bod po bode, ku každému dohodnúť vlastníka, termín a čo treba od Dr. Max.
**Typ**: interné
**Dátum**: 2026-10-26
**Účastníci**: Marek Pillár (PM), Filip Černý (vývoj)

## Kontext

**Nový stav (e-mail z Dr. Max, 2026-10-26)**: konečne prišli podklady:
- **DS -vyplněné parametry-vzor.xlsm** = hotové doplnky stravy ako vzor
- **DS parametry k vyplnění.xlsx** = 500 neupravených doplnkov stravy, všetky parametre treba skontrolovať

Dr. Max si zároveň v deme všimol bug: v alergénoch sa niektoré hodnoty zobrazujú 2x (vždy tie so zátvorkou).

**Dohoda z 30. 9. (Neuman, Michaela)**:
- **Magento je mimo MVP.** Import berie jeden zmenený stĺpec na import, takže ~20 stĺpcov = ~20 importov. Global sa Magentom nezaoberá a čaká na globálny PIM.
- **Ideme po skupinách produktov.** Teraz celá legislatívna skupina doplnky stravy ako jedna kategória. Delenie na podskupiny (vitamíny, minerály, deti, bylinné) až neskôr.
- **Prioritou sú parametre** (cieľ ~10 na produkt, dnes 2–3), texty až potom.
- **Každý SKU validuje človek.** Automaticky doplnené hodnoty majú stav „neskontrolované“. Lieky sú mimo.
- **Výstupom je export** vo formáte pre parametrovú špecialistku (Filip: tlačidlo ~2 h).
- **Scraping** je vedľajší cieľ a čaká na právnikov.

**Riziko**: Listing je podľa sync 10-21 vo vysokom riziku (Magento zablokované, tím Neumana nereagoval). Jindřich ide tento týždeň s Neumanom na obed. Tieto podklady sú prvý reálny posun, preto chceme rýchlo ukázať výsledok.

## Agenda (bod po bode)

### 1. Rozbor tabuliek
- Aké parametre sú v batchi a aké vo vzore? Sedia na seba?
- Je tam kompletný číselník povolených hodnôt (pôvodných ~14 + ~6 nových parametrov)?
- Ak niečo chýba, čo presne vyžiadame od Dr. Max?
- **Dohodnúť**: kto, do kedy, zoznam chýbajúcich vecí

### 2. Setup v nástroji
- Doplnky stravy ako jedna kategória (primárna = legislatívna skupina)
- Základný štandard + pravidlá pre skupinu, vzorové produkty ako príklady
- Ide to v súčasnom nástroji bez úprav, alebo treba vývoj?
- **Dohodnúť**: náročnosť, termín

### 3. Bug: duplicitné alergény
- Hodnoty so zátvorkou sa zobrazujú 2x. Príčina?
- Treba skontrolovať aj ostatné viachodnotové parametre
- **Dohodnúť**: termín opravy (pred vzorkou pre Dr. Max)

### 4. Enrichment: vzorka → celý batch
- Najprv vzorka (cca 20–50 SKU) na kontrolu s Dr. Max, potom 500
- Parametre prioritou, texty potom; stav „neskontrolované“; lieky mimo
- Koľko parametrov na produkt reálne doplníme? (cieľ ~10)
- **Dohodnúť**: kedy je vzorka pripravená pre Dr. Max

### 5. Export
- Tlačidlo na stiahnutie; formát ideálne pripravený na import po stĺpcoch
- Formát od Dr. Max stále nemáme (otvorené od 30. 9.). Navrhneme my, alebo počkáme?
- **Dohodnúť**: návrh formátu a kto ho pošle Dr. Max na potvrdenie

### 6. Odhad a termíny
- Celková náročnosť (rozbor → setup → bug → vzorka → 500 SKU → export)
- Kedy môže Dr. Max začať validovať vzorku a kedy celý batch
- **Dohodnúť**: dátumy do roadmapy a pre odpoveď Dr. Max

### Mimo rozsahu (len pripomenúť)
Import do Magenta, scraping (čaká na právnikov), automatická synchronizácia číselníka (až po globálnom PIM).

## Otázky na vyjasnenie

- **500 vs. ~2 000 SKU**: 30. 9. sa hovorilo o ~2 000 SKU (20 % doplnkov, ktoré robia 80 % tržieb). Je 500 prvá dávka, alebo sa rozsah zmenšil? → spýtať sa Dr. Max
- **Export**: aký presný formát potrebuje parametrová špecialistka?
- **Validácia**: kto z Dr. Max bude kontrolovať vzorku a koľko na to má kapacity?

## Po stretnutí

- Odpovedať Dr. Max: poďakovať za podklady, potvrdiť bug v alergénoch, poslať termín vzorky, opýtať sa na 500 vs. 2 000 a na formát exportu
- Termíny zapísať do roadmapy Listingu (prepis špecifikácie: Magento mimo MVP, enrichment first)
