---
last_updated: 2026-10-29
last_updated_by: manual — conversational
type: meeting-prep
meeting_date: 2026-10-29
attendees: [Marek Pillár, Jindřich Tůma, Petr Neuman]
sources: [2026-10-27-listing-evaluation-fakturace-mock-review-filip, report.pdf, parove_porovnani.xlsx, audit_referencnich_dat.xlsx]
---

# Prep — Listing call s Petrom Neumanom (+ Jindřich), 2026-10-29

**Cieľ**: ukázať, že na doplnkoch stravy to funguje (demo → export → čísla → audit), a odísť s odpoveďami na 4–5 otázok. Filip je na dovolenke, prezentuješ ty. Podklady od Filipa máš len ty — **pošli ich až po calle**, s krátkym sprievodným mailom (Filipov draft ako základ).

**Poradie a čas (~30 min)**: 1. Úvod (2 min) → 2. Demo (8 min) → 3. Evaluácia (8 min) → 4. Audit (5 min) → 5. Otázky (7 min).

Otvorené pred callom (`~/Desktop/listing/`): demo v prehliadači, `report.pdf`, `parove_porovnani.xlsx`, `audit_referencnich_dat.xlsx`.

---

## 1. Úvod — čo sme sa dohodli (2 min, neotvárať znova)

- Magento je mimo MVP. Najprv obohatenie dát + export pre parametrového špecialistu.
- Dodali ste **500 doplnkov stravy** (pôvodný cieľ bol ~2 000) a **~200 hotových** ako referenciu.
- 500 produktov je naprieč mnohými hlavnými kategóriami a bez inštrukcií pre jednotlivé kategórie. Preto ideme na úrovni **attribute setu „doplněk stravy"**: parametre fungujú dobre, texty sú zatiaľ generickejšie. Pravidlá pre kategórie nevymýšľame — to je vaše rozhodnutie.
- Duplicity alergénov boli naša chyba pri importe, **opravené** (nový katalóg parametrov).

> Hovor: „Nebudeme znova otvárať otvorené otázky. Ukážem, čo sme za týždeň spravili, a na konci potrebujem pár rozhodnutí."

## 2. Demo (8 min, klikáš ty)

V deme je len **500 nových doplnkov** (referenčných 200 tam zámerne nie je, aby sa nemiešali staré a nové).

1. **Otvor produkt** → klikni **Generovať parametre** → zvyčajne doplní niekoľko parametrov navyše (podľa inštrukcií od Michaely).
   - Hovor: „Používateľ nemusí mať v hlave celý katalóg — či to môže byť aj vegan, bez lepku… Len potvrdzuje návrhy."
2. **Ulož** → vznikne **nová verzia** s časom. Stav sa zmení *Import → Rozpracováno*. Ukáž prepínanie medzi verziami (verzie sú pre každý produkt zvlášť).
3. **Export Excel** → celá kategória v **ich vlastnom formáte**, vždy posledná verzia, zmenené bunky zvýraznené.
   - Overený príklad: **„Zerex Classic"** → nový parameter **„bez alkoholu"**.
   - Hovor: „Export vieme spraviť rýchlo a v akomkoľvek formáte. Cieľ je stále zápis rovno do Magenta — ak viete takýto Excel naimportovať, môžeme to používať hneď."
4. **Listing score** — ak sa spýtajú: evaluátor ešte nie je vyladený, neber ho ako metriku.

## 3. Evaluácia — čísla (8 min, `report.pdf`)

**Ako sme to testovali** (jednou vetou): Vzali sme vašich **202 „hotových" produktov** (198 SKU, 14 parametrov), parametre sme zmazali a nechali nástroj vyplniť ich znova len z textov produktov — výsledok nevidel. Rovnaký modul, aký beží v appke. Dokončil všetky produkty.

| Číslo | Čo to znamená po ľudsky |
|---|---|
| **86,6 %** | v priemere toľko informácií z vašich dát náš výstup obsahuje |
| **83,8 %** | v toľkých poliach sme trafili všetko, čo ste tam mali |
| **80,0 %** | toľko jednotlivých hodnôt sme trafili pri viacnásobnom výbere (napr. „bez lepku, bez laktózy, vegan") |

> Hovor: „Po vašom tíme vyplníme zhruba 80–87 %. Ale je jedno veľké ALE — meriame zhodu s vašimi dátami, nie či sú pravdivé. A vaše dáta majú chyby."

- **Silné**: cieľová skupina (deti / muži / ženy), forma produktu (kapsle, prášok…).
- **Slabšie** (priznať, opravíme): vlastnosti produktu, kombinované príchute, kedy užívať, vekové hranice (napr. „vhodné pre novorodencov" sa často nedoplní → doladíme inštrukcie).
- Ukáž `parove_porovnani.xlsx` — pre každý parameter vaša hodnota vedľa našej, všetkých 202 riadkov, čísla riadkov z vášho Excelu. Príklad: **riadok 82 Dr. Max Energy Sticks** — ich vlastná značka, 10 parametrov 1:1 (viac v ťaháku nižšie).

## 4. Audit referenčných dát (5 min, `audit_referencnich_dat.xlsx`)

**Tón: bonus, nie výčitka.** Filip sa bál, že to vyznie pasívne-agresívne.

> Hovor: „Pri vyhodnocovaní sme narazili na veci vo vašich dátach, ktoré by vám aj tak niekto musel opraviť. Spísali sme ich aj s dôkazmi. Keď je náš nástroj správne a referencia zle, ráta sa to proti nám — takže reálna kvalita je vyššia než tých 85 %."

**86 nálezov v 63 produktoch**, každý s citáciou zo zdroja. Ukáž 2–3 najsilnejšie:

1. **Vegan, ktorý nie je vegan** (5 produktov, overený rozpor):
   - **NatureVia OptiVizin Blue** (audit r. 44 / porovnanie r. 165) — u vás „Vegan", v zložení **rybí olej**. My sme vegan správne nedali → zhoda klesla.
   - podobne **Nordbo Omega 3** (audit r. 46, 47, 51), **Pangamin Bifi** (audit r. 86 — srvátka).
   - Toto je najsilnejší argument — je to aj legislatívne / reklamačné riziko.
2. **Skladovanie** (8 produktov): všetkých 202 má „izbová teplota", ale napr. **Mollers Omega 3** (audit r. 36–39) píše „po otvorení 2–8 °C", Optibac For Woman (audit r. 83, 85) „po otvorení v chladničke". Váš číselník nerozlišuje pred / po otvorení.
3. **Hodnoty mimo vášho číselníka** (63 polí v 48 produktoch): referencia obsahuje hodnotu, ktorú váš vlastný katalóg parametrov neponúka (napr. audit r. 8 Beggs Methylfolate: u vás „Vitamin B9", číselník má len „Vitamin B"). Toto nie je chyba modelu — treba doplniť číselník.

Menšie: forma vstrebávania (4× — napr. Beggs bisglycinát je chelátová forma, u vás „bežné uvoľňovanie"), 4× len iné poradie / veľké písmená príchutí, 1× vegan + želatínová kapsula (MAXXWIN, audit r. 24 — treba overiť).

Férovo povedať: **nie všetkých 86 sú potvrdené chyby**, časť potrebuje posúdenie odborníkom.

## ★ Ťahák — presné riadky v Exceloch

Súbory: `~/Desktop/listing/`. **Riadok = číslo riadku v Exceli (vľavo).** V `parove_porovnani.xlsx` sedí s číslom produktu (stĺpec A); v `audit_referencnich_dat.xlsx` nie — tam používaj čísla nižšie.

Stĺpce v `parove_porovnani.xlsx` (vždy pár *referencia / naša hodnota*): D/E min. vek · F/G max. vek · **H/I vlastnosti** · J/K cieľová skupina · L/M príchuť · N/O forma · R/S vitamíny · T/U kedy užívať · **V/W alergény** · **AB/AC forma vstrebávania** · **AD/AE skladovanie**.

### A) `parove_porovnani.xlsx` — „funguje to" (sekcia 3)

| Riadok | Produkt | Čo ukázať |
|---|---|---|
| **82** | Dr. Max Energy Sticks 30 sáčků | **ich vlastná značka, 10 parametrov, všetko 1:1** — najlepší úvodný príklad |
| 19 | Barny´s Klokan limitovaná edice | 9 parametrov, všetko 1:1 |
| 63 | Cemio Kamzík XXL 365 kapslí | 9 parametrov, všetko 1:1 |
| 100 | LifeCode by Dr. Max Liposomal Vitamin D | vlastná značka, 8 parametrov 1:1 |

(Celkovo 26 produktov s ≥ 7 vyplnenými parametrami úplne bez rozdielu.)

### B) `parove_porovnani.xlsx` — „sme lepší ako referencia"

| Riadok | Produkt | Bunky | Referencia → my |
|---|---|---|---|
| **165** | NatureVia OptiVizin Blue | H/I | „…Vegan" → bez Vegan (v zložení **rybí olej**) |
| **200** | Pangamin Bifi s inulinem | H/I + V/W | „Vegan" → bez Vegan; alergény: doplnili sme **Mléko** (obsahuje srvátku) |
| 169 | Nordbo Omega-3 Trout Oil 120 kapslí | H/I | „Vegan" → bez Vegan (rybí olej, rybia želatína) |
| **26** | Beggs Iron bisglycinate | AB/AC | „Běžné uvolňování" → „Vyšší vstřebatelnost – chelátová forma" |
| 71 | Clinical Magnesium chelát + B6 | AB/AC | „Běžné uvolňování" → „Vysoká vstřebatelnost – bisglycinát" |

### C) `audit_referencnich_dat.xlsx` — audit (sekcia 4)

Stĺpce: C produkt · D parameter · E typ nálezu · F miera overenia · G referencia · H naša hodnota · **I dôkaz zo zdroja** · J vysvetlenie. **Vždy ukáž stĺpec I** — citácia z ich vlastného textu.

| Riadok | Produkt | Nález |
|---|---|---|
| **44** | NatureVia OptiVizin Blue | Vegan vs. rybí olej — **začni týmto** |
| 46, 47, 51 | Nordbo Omega 3 (3 produkty) | Vegan vs. rybí olej / rybia želatína |
| 86 | Pangamin Bifi | Vegan vs. srvátka |
| **36–39** | Mollers Omega 3 (4 produkty) | izbová teplota vs. „po otvorení 2–8 °C" |
| 83, 85 | Optibac For Woman 30 / 90 | izbová teplota vs. „po otvorení v chladničke" |
| **8** | Beggs Methylfolate | „Vitamin B9" — číselník má len „Vitamin B" → treba doplniť číselník |
| 6, 17 | Beggs Iron, Clinical Magnesium | chelátová forma vs. „bežné uvoľňovanie" |
| 24 | MAXXWIN Arginine | Vegan + želatínová kapsula — „treba overiť" (férový príklad, že nie všetko je istá chyba) |
| 15 | Centrum Kids Gummies | len iné poradie / veľké písmená príchutí — nejde o chybu |

### ⚠ Neotvárať (naše slabé miesta — keby sa pýtali, priznať a povedať „doladíme")

| Riadok (`parove_porovnani`) | Produkt | Problém |
|---|---|---|
| 143, 144 | Mollers Omega 3 Citron / D+ | **nedoplnili sme alergén „Ryby"** (V/W) pri rybom oleji |
| 15, 66 | Arctic Blue Kids, Centrum Kids Gummies | detský produkt, my pridali „Pro muže, Pro ženy" (J/K) |
| 142, 144 | Mollers | chýbajú vlastnosti (H/I) a min. vek (D/E) |
| 5 | ADVANCE Calmin | „Denně" → „Podle potřeby" (T/U) |

## 5. Ďalší krok + otázky (7 min)

**Návrh (z reportu)**:
1. Spolu prejsť sporné prípady → opraviť referenciu a doplniť číselník.
2. My doladíme slabé miesta (vlastnosti, príchute, vek).
3. Váš tím si v deme otestuje ďalšie produkty a posúdi použiteľnosť → potom meriame znova na overených dátach.

**Otázky, na ktoré potrebujeme odpoveď**:
1. **Export** — vyhovuje formát (váš Excel + zvýraznenie)? Viete ho reálne **naimportovať do Magenta**?
2. **Kto u vás prejde audit** a v deme otestuje produkty? Dokedy?
3. **Zvyšok do ~2 000 SKU** — kedy a od koho (Michaela / Týblová)?
4. **Hlavné kategórie + inštrukcie** — kto a dokedy ich zadefinuje? Bez nich zostanú texty generické. (Outlook: všetky produkty → attribute set (~14) → hlavná kategória.)
5. **Kontrolujete dáta ručne pred uploadom do Magenta?** (mení to, ako čítať 85 %)
6. **Zdrojové súbory od dodávateľov** (SPL/SPC, XML, PDF, XLSX) — chápeme ich ako **vstup** pre generovanie, nie export. Pošlete vzorky? Filip o ne žiada už ~3 stretnutia.
7. **Technický owner** za Listing na strane Dr. Max — stále chýba.
8. Chcete do dema aj tých ~200 referenčných (oddelených stavom)?

Spec v2 (tracked changes + odpovede na všetkých 14 komentárov) — spomenúť, že príde.

## Nehovoriť / pozor

- Nehovoriť, že ich Excely vyzerajú vygenerované AI, ani že katalóg parametrov nič nepridáva.
- Nesľubovať zápis do Magenta ani termín pre hlavné kategórie — závisí od nich.
- Listing score nepredávať ako metriku kvality.

## Po calle

- Poslať: `report.pdf` + 2× Excel (+ spec v2 po review), sprievodný mail podľa Filipovho draftu.
- Dať Filipovi spätnú väzbu (je na Teams).
- Spracovať cez `/project-meeting-upload`.
