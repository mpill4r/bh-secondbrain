---
last_updated: 2026-10-05
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-05
attendees: [Rudolf Žůrek, Tomáš Dudaško, Petr Spilka, Tereza Foltová, Marek Pillár, Jindřich Tůma]
---

# Príprava na stretnutie — Reklamační proces: další kroky

## Prehľad stretnutia

**Názov**: Reklamační proces — další kroky (organizuje Tereza Foltová)
**Ciele** (ako ich zadal PM):
1. **Zrekapitulovať, kde stream stojí a aká je teraz nálada**: Excel s dátovou mapou z minulého týždňa, špecifikácia Reklamácií a čo je dohodnuté.
2. **Upokojiť tému nezodpovedaných komentárov Petra Slámu v špecifikácii.**
3. **Voliteľne otvoriť AI use casy z marcového e-mailu logistiky (2026)** (Doprava / Vratky / Cenařky / Sklad).

**Typ**: klientske (manažérska úroveň)
**Dátum**: 2026-10-05, 10:00, osobne
**Účastníci**:
- Rudolf Žůrek: šéf logistiky, najvyšší v miestnosti, rozhoduje.
- Tomáš Dudaško: sponzor AI iniciatív a rozpočet.
- Petr Spilka: šéf skladov ViaPharma, business vlastník Reklamácií.
- Tereza Foltová: logistika, organizátorka.
- Marek Pillár: BigHub, vlastník špecifikácie Reklamácií, jediný kontakt pre logistiku.
- Jindřich Tůma: koordinácia BigHub/Dr. Max.

Nezúčastnia sa: Jan Sovka (zámerne, [[ASM-241]]) a Petr Sláma (na 09-24 žiadal, aby bol prizvaný; nič nenasvedčuje, že je pozvaný).

## Ciele a otázky PM

- Ukázať, že stream je **späť na správnej ceste**: patová situácia z minulého týždňa sa vyriešila 10-01 a existuje jasná cesta k rozhodnutej špecifikácii do 10-09.
- **Zneškodniť príbeh o Slámových komentároch** skôr, než sa z neho stane „BigHub ignoroval klienta".
- Ak bude priestor, **posunúť debatu od „stoja Reklamácie za to?" k „čo chce logistika ďalej?"** pomocou ich vlastného marcového zoznamu.
- Kontext poruke: všetky nedávne stretnutia s logistikou a vstupy od Terezy.

## Kontext z harnessu

### Prečo sa stretnutie pravdepodobne koná ([[ASM-242]], nepotvrdené)

- **Reklamácie sú aktívna iniciatíva s najnižšou hodnotou.**
  - V trackeri majú hodnotu ~425 tis. Kč (fáza 1) až ~700 tis. Kč/rok, oproti ~34 mil. pri Listingu a ~81 mil. pri MaxBuddy.
  - Hodnota stojí na Terezinom hrubom (Fermiho) odhade 4 ľudia × 2 h/deň ≈ 8 h/deň ≈ 1 FTE, ktorý sa naplní až keď sa dodajú **všetky** fázy (09-15).
  - Na 10-02 Spilka nazval 8 h/deň „sľubom nepodloženým dátami" a „pre mňa malou úsporou", v porovnaní s cenařkami a ich „stovkami hodín mesačne".
- **Od 09-22 sú preformulované ako digitalizácia, nie AI.** Jindřich povedal Dudaškovi, že reálny prínos je digitalizácia a konsolidácia dát, a rozhodnutie pokračovať alebo ukončiť sa presunulo na manažérske stretnutie (Dudaško, Žůrek, Spilka, Žižka). **Toto je veľmi pravdepodobne to stretnutie.**
- **Dudaškov vyslovený postoj (09-23)**:
  - Chce Axaptu vypnúť približne do 6 mesiacov.
  - Akceptoval by vyššie náklady na vývoj teraz za riešenie, ktoré sa prenesie na to, čo Axaptu nahradí.
  - Na 09-24 povedal Slámovi, že logika patrí do „AI aplikácie", nie do Axapty.
- **Tereza** sa bojí, že Reklamácie zastavia. V septembri bola zdrojom príbehu „BigHub nechce dodať", ktorý Jindřich na 09-23 uviedol na pravú mieru s ňou a so Spilkom.

### Téma 1: kde stream stojí (fakty)

#### Stav fáz v skratke

Zdroj: tabuľka roadmapy v `3. Reklamace v5.docx`. Vo v5 sú stále sledované zmeny, ktoré si ešte neprijal.

**✅ Hotové**

- **Fáza 0: Príprava (Příprava)**
  - API Axapta ✅ (#15)
  - API Boomi ✅ (#16)
- **Fáza 1: Príjmové reklamácie, poškodený tovar (väčšina).** Mobilná aplikácia (PWA) je postavená a v klientskom testovaní:
  - Príjem s výhradou (příjem s výhradou) ✅ (#1)
  - Identifikácia reklamovaného tovaru ✅ (#2)
  - Čítanie čiarového kódu ✅ (#21)
  - Fotodokumentácia poškodenia ✅ (#3)
  - Automatické založenie reklamácie v Axapte ✅ (#4)
  - Prepojenie príjmu s výhradou a reklamácie ✅ (#5)
  - Chybové stavy ✅ (#11)
  - Integrácia Axapta ✅ (#12)
- **Proof of concept e-mailového agenta** (základ pre fázu 1.1b): postavený zo 7 reálnych vlákien a predvedený 10-01. Sláma: „veľký krok vpred". Zatiaľ to nie je produkčná práca.

**🔧 Rozpracované (dokončiť fázu 1 → UAT)**

| Položka | Stav | Blokér / závislosť |
|---|---|---|
| Produkčné nasadenie (#13, fáza 0) | Vo vývoji | Infra Maxu (eskalácia AKS) |
| Dokumenty k reklamácii: rozvozový list a návratka dodávateľovi (#7) | Vo vývoji | Rozvozový list spúšťa `claim_case_closed`; v kontrakte chýba len dátum vystavenia |
| Draft e-mailu dodávateľovi (#8) | Vo vývoji | Prístup ku Graph API a mailboxu (Tvarůžek, očakávané v týždni od 10-05) |
| Údaje o dodávateľoch / znalostná báza (#6) | **Blokované** | **Rozhodnutie**: jeden SharePoint List kľúčovaný číslom dodávateľa. Čaká sa na Slámov stĺpec J a menovaného vlastníka na strane Dr. Max ([[ASM-228]]) |
| Fáza 1.1a, auditná stopa: e-mailové vlákno s dodávateľom ako PDF na reklamácii v Axapte (#9) | Backlog → **súčasť UAT** | Dohodnuté 10-01; Graph API |
| Testovanie fázy 1 | Predĺžené o **+1 týždeň** (10-01) | Zdieľaný testovací telefón (bez termínu); prihlásenie per používateľ tento týždeň |
| Okamžité avízo (voliteľné, per dodávateľ) | Špecifikované, nenaplánované | Ktorí dodávatelia, aká lehota, ktorá fáza ([[ASM-240]]). Neblokuje testovanie. |
| **Plné UAT** | Plánované na **15.–16. 10.** ([[ASM-056]]) | Posúva ho predĺženie testovania o +1 týždeň? **Potvrdiť.** |

**⏭️ Nasleduje: po UAT fázy 1**

| Fáza | Čo dodá | Pripravenosť |
|---|---|---|
| **1.1b: Navazující e-mailový sled** (e-mailový agent v produkcii) | Agent klasifikuje odpovede dodávateľa a pripraví draft ďalšieho e-mailu správnemu adresátovi: odoslanie na sklad, vlastný zvoz, likvidácia, čakanie, nesprávny adresát. Toto je Slámov májový smer „Zentiva", teraz prijatý. | Dohodnutý smer; **odhad MD -tbd-**, nacenený ako samostatná časť (change request, [[ASM-186]]). Potrebuje kontakty podľa roly (API dnes nesie jeden kontakt), spísané postupy per dodávateľ a testovací O365 účet. |
| **2: Skladové reklamácie** (kvalitatívne vady po vybalení, vratky expirácií a sezónne vratky, sklad RV) | Rovnaký flow ako fáza 1, začína od palety alebo skladovej lokácie; čítanie ručne písaných štítkov cez OCR (#34); čistenie testovacích dát (#35) | Backlog. Veľká časť aplikácie už existuje z fázy 1. Otvorené: tlačené vs. ručne písané štítky. |

**🔍 Neskôr: pred akýmkoľvek záväzkom treba discovery** (špecifikácia výslovne hovorí „východiskový bod pre discovery, nie finálne zadanie")

| Fáza | Čo pokrýva | Poznámka |
|---|---|---|
| **3: Príjmové reklamácie, nedodaný tovar** | Viditeľný manko (zistený pri vybaľovaní) a neviditeľný manko (rozdiel medzi dodacím listom a naskladnením, zistený v Axapte) | Rozhranie Axapty už pozná zdroj a typ „nedodané". Odtiaľto prichádzajú aj ostatné typy problémov z Axapty (cca 19) (fázovanie z 10-01). |
| **4: Reklamácie z lekární** | Tovar poslaný dodávateľovi na posúdenie (30-dňová lehota, nezaúčtuje sa hneď); párovanie duplicít | Rozhranie Axapty už pozná zdroj „lekáreň". Zodpovedá marcovej položke o zákazníckych reklamáciách privátnej značky Dr. Max, ktorá potrebuje schválenie kvalifikovanou osobou (SDP). |
| **5: Reklamácie z e-shopu** | Rovnaký flow ako fáza 4 | Rozhranie Axapty už pozná zdroj „e-shop" |

**Ako to povedať v miestnosti:** Fáza 0 je hotová a fáza 1 je z väčšej časti postavená a v testovaní. Pred UAT zostávajú dokumenty, draft e-mailu a rozhodnutie o dátach dodávateľov; to posledné je na strane logistiky, nie BigHubu. Fáza 1.1b (e-mailový agent) je ďalší krok s hodnotou a dostane vlastnú cenu. Fázy 2–5 potrebujú krátke discovery so Spilkom, ktoré definujú, čo každá dodá, skôr než sa BigHub zaviaže ich stavať. Podľa 09-15 prichádza plná úspora ~1 FTE až keď sú živé všetky fázy.

#### Detail

| Oblasť | Stav |
|---|---|
| **Sync 10-01** | Patová situácia odblokovaná. Sláma: „veľký krok vpred oproti minulému týždňu". Vzťahy s Terezou, Slámom a Egrmaierovou sa obnovili (Marek Janovi, 10-02). |
| **E-mailový agent (skutočná AI časť)** | Filipov proof of concept bol prijatý dobre. Pripraví prvý e-mail, pracovník ho schváli, agent klasifikuje odpovede (konečný stav / čakanie / odovzdať človeku) a vždy má únikovú cestu k človeku. Dohodnuté doplnky: ViaPharma v kópii (CC), vlákno archivované ako PDF na reklamácii v Axapte a alternatívne drafty, keď má dodávateľ viac možných adresátov. |
| **Údaje o dodávateľoch („znalostná báza")** | Smerujeme k minimu v Axapte (číslo dodávateľa plus polia prípadu, ktoré má len Axapta), všetko ostatné v **jednom SharePoint Liste kľúčovanom číslom dodávateľa**. Excel je von („posledná voľba", Sláma) ([[ASM-228]]). **Otvorené:** Slámova spätná väzba v stĺpci J, termín začiatkom tohto týždňa ([[ASM-229]]), a **menovaný vlastník Listu na strane Dr. Max** (nikto sa neprihlásil). |
| **Špecifikácia** | `3. Reklamace v5.docx` (interná, sledované zmeny). Obsahuje výstupy z 10-01, fakty z nových API kontraktov (Axapta v0.9.10, inbound v0.4.0) a okamžité avízo podľa Jana. Položky z dátovej mapy sú označené fialovo ako otvorené. **Logistike ešte neodoslaná.** Rekapitulácia so špecifikáciou mali ísť 10-02, teraz sú plánované na začiatok tohto týždňa. |
| **Testovanie** | Fáza 1 predĺžená o +1 týždeň na žiadosť Terezy. Prihlásenie per používateľ sa tento týždeň stavia cez platformu. Zdieľaný testovací telefón nemá termín. Graph API a prístup k mailboxu sú blokované na infra Maxu (eskalácia AKS). |
| **Typy problémov** | Dohodnuté fázovanie: poškodené na príjme → poškodené v sklade → ostatné typy problémov z Axapty (číselník v aplikácii). Tereza a Jana posielajú zoznam typov. |
| **Okamžité avízo** | Voliteľné nočné automatické upozornenie per dodávateľ po príjme s výhradou. Neblokuje testovanie ([[ASM-240]]). Ešte treba: ktorí dodávatelia, aká lehota, ktorá fáza. |
| **Neskoršie fázy** | Fázy 2–4 nie sú poriadne špecifikované („nie je popísaná ani polovica procesu", Tereza 09-25). Každá potrebuje v discovery definovať hlavný ťahúň hodnoty („system seller") ([[ASM-190]]). |
| **Pracovné dohody** | Špecifikácia je kontrakt: logické zmeny idú cez change request s cenou v MD a písomným schválením ([[ASM-186]]). UX spätná väzba sa rieši operatívne. Rozhodnutia sa potvrdzujú písomne ([[ASM-185]]). Marek je vlastník špecifikácie a jediný kontakt pre logistiku. |

### Téma 2: Slámove komentáre (fakty, ktoré treba mať v poriadku)

- **Čo sa stalo**:
  - **2026-05-20** napísal Sláma do špecifikácie komentáre, že e-maily majú odchádzať automaticky, s príkladom „Zentiva" (viacero adresátov postupne).
  - Na strane BigHubu sa komentáre riešili za predchádzajúceho tímu (zapojený Honza Sovka), ale **k Slámovi sa nikdy nedostala odpoveď**.
  - Na 09-24 to uviedol ako dôkaz, že BigHub to vedel; schválená špecifikácia fázy 1.1 hovorí „vyjednávání s dodavatelem probíhá ručně".
- **Ako sa to uzavrelo 10-01**:
  - Jindřich to prijal ako **spoločné zlyhanie**: BigHub mal uzavrieť slučku a ViaPharma to mohla skontrolovať.
  - **Prijal komentár ako smer** („pôjdeme cestou vášho komentára").
  - E-mailový agent je teraz dohodnutá cesta, nie sporný doplnok ([[ASM-181]], Rozhodnuté).
  - Akýkoľvek dopad na rozpočet bol uznaný len v princípe a stále sa riadi [[ASM-186]].
- **Čo sa odvtedy zmenilo**:
  - Marek je menovaný vlastník špecifikácie a otvorený kanál pre zmeny.
  - Všetky otvorené komentáre sa zodpovedajú písomne.
  - v4/v5 už obsahujú májový smer ako sledované zmeny.
- **Čo je stále otvorené a je to riziko**:
  - **Písomné odpovede na Slámove májové komentáre ešte treba finálne skontrolovať** pred odoslaním.
  - Rekapitulačný e-mail **mešká 3 dni** (termín 10-02).
  - Ak sa Žůrek alebo Dudaško spýtajú „má už Sláma odpovede?", poctivá odpoveď je: „dohodnuté v miestnosti 10-01, písomne tento týždeň". **Povedz konkrétny dátum.**
- **Užitočný kontext**: Sláma je pod tlakom vlastného manažéra, aby ukázal viditeľné úspory. Sám povedal, že skutočná úspora je v **automatizácii e-mailového workflow**, nie vo vytváraní protokolu. Presne to teraz dodáva e-mailový agent, takže jeho komentár a príbeh o hodnote smerujú rovnakým smerom.

### Téma 3: marcové AI use casy logistiky (z Janovho preposlaného e-mailu)

Namapované na to, čo dnes beží alebo je známe:

| Oblasť | Marcový use case | Stav dnes |
|---|---|---|
| **Doprava** | Skenovanie dokladov od vodičov (zošívané papiere, lístky z dataloggerov vo formáte „účtenky", potvrdenia o prevzatí OPL) | **= Fakturace doprav** kiosk (pozastavené; čaká sa na Slámovo posúdenie návrhu API) |
| Doprava | Modul fakturácie: AI dopĺňa km, poznámky a teploty z dataloggerov a vytlačených papierikov, plus validácia | **= Fakturace doprav** (medzera v OCR teplotných záznamov je jeden z rozporov kód vs. špecifikácia, ASM-134) |
| **Vratky** | Sťahovanie certifikátov od dodávateľov (atest potrebný, keď sme prví v EÚ, kto tovar prijme; prichádza e-mailom alebo zo stránok dodávateľa) | Nezačaté |
| Vratky | **Reklamácie dodávateľom**: formulár reklamácie v AX; AI číta Teams, pracovník odfotí identifikátor príjmu, napíše „reklamace…", spraví X fotiek, AI vyplní formulár a pošle e-mail dodávateľovi podľa naučeného štýlu a podmienok | **= dnešné Reklamácie**: aplikácia plus e-mailový agent. Toto je pôvodná vízia, na ktorú sa Sláma odvoláva. |
| Vratky | Vratky od odberateľov: dorobiť rozhranie Farmis ↔ Axapta a automaticky vypĺňať formuláre v AX | Nezačaté; integrácia, nie AI |
| Vratky | Zákaznícke reklamácie privátnej značky Dr. Max (90 % zamietnutých z centrály a odpísaných): automatizovať toky v AX a odstrániť dokumentáciu (tonometre, teplomery). Potrebuje schválenie kvalifikovanou osobou (SDP) v koordinácii s nákupom a ekonomikou. | Nezačaté; zmena procesu s compliance bránou |
| Vratky | Automatické ukladanie fotiek poškodeného tovaru (napr. pre ekonomiku) | **Čiastočne pokryté Reklamáciami** (fotky plus PDF archív na reklamácii v AX) |
| **Cenařky** | Načítať a validovať cenníky dodávateľov v AX/EDI; AI naskenuje faktúry a ocení položky podľa identifikátora | **= Cenařky** (Spilkova top voľba, 10-02; potrebuje analýzu na mieste, nov–dec alebo marec, [[ASM-232]]) |
| Cenařky | Zapisovanie faktúr: AI naskenuje doklad a zapíše ho do príslušného záznamu v AX (EDI/AI) | = Cenařky (tých 5–10 %, ktoré analyzovala konzultantská firma) |
| Cenařky | Prevody medzi menami, rozpočítavanie recyklačných poplatkov, rozpočítavanie dopravy (EDI/faktúra/AI) | = Cenařky |
| **Sklad** | Výstupná kontrola: vysypať obsah bedne na stôl, kamera plus AI vyhodnotí obsah (dáta z BPI / AI kamery, AF) | V starých riadkoch trackera; nezačaté |
| Sklad | Riadenie spúšťania beden do linky: AI rozhoduje, ktorá bedna kedy ide, podľa naplnenosti linky, zastávok, dennej doby a aktívnych čítačiek | Nezačaté (optimalizácia a predikcia) |
| Sklad | Dvojdňové doručovanie: spúšťanie beden podľa naplnenosti áut a trás; návrh presunov na iné trasy alebo na ďalší deň; e-mail dopravcovi s potvrdzovacím tlačidlom | Nezačaté |
| Sklad | Stratégia tvorby beden: naplnenosť podľa dennej doby, veľkosti, vyskladňovacej technológie, typu položky (cytostatiká nemiešame), času odjazdu; napr. dve malé bedne namiesto jednej veľkej kvôli lead time | Nezačaté |
| Sklad | Prideľovanie práce na vyskladnenie kartónov a beden z VOS: optimálny vyskladňovací „had" podľa odjazdov a prechodu skladom | Nezačaté |
| Sklad | Naskladňovacia stratégia na príjme (obsadenosť technológií, predajnosť, akcie, nákupné objednávky, sezónnosť, nastavenie položiek) plus chatbot o dostupnosti položiek a prečo sa položka nepredáva | Nezačaté; prekrýva sa s prácou na predikcii objednávok |
| Sklad | OPL stôl: AI kamera spáruje fotky s výdajkou a uloží ich do AX | Nezačaté; blízke vzoru Reklamácií foto → AX |

Screenshoty používajú olivové, tyrkysové a zelené zvýraznenie. Ich význam nie je známy, takže sa spýtaj, ak je to dôležité.

**Čítanie**:
- **Reklamácie sú jednou z pôvodných marcových požiadaviek samotnej logistiky**, nie niečo, čo vymyslel BigHub. „Automatizovať reklamáciu dodávateľovi end-to-end vrátane e-mailov" je marcové znenie. Zostáva pipeline foto → AX → e-mail, a táto pipeline je znovupoužiteľná: certifikáty, fotky poškodeného tovaru pre ekonomiku, OPL stôl.
- **Cenařky aj Fakturace doprav sú tiež na marcovom zozname.** Nový zoznam „na zelenej lúke" by teda mal hlavne prepriorizovať tieto položky, nie vymýšľať nové.
- **Skladové položky sú kandidáti s najväčšou hodnotou** (priepustnosť a lead time), ale najmenej špecifikované. Sú prirodzenými témami na discovery v okt–nov ([[ASM-190]]).

### Najnovšie vstupy od Terezy (09-25 → 10-02)

- **09-25**:
  - Marek vlastní dokumentáciu Reklamácií približne 2 týždne, pred Fakturace doprav, a je jej jediným kontaktom.
  - Nové iniciatívy validuje najprv so Spilkom, potom so Žůrkom.
  - Jej pohľad: rozsah „sa stále nafukuje"; prechod na „agile" „sa nám vypomstil".
- **10-02**:
  - Master tracker od riadku 13 nižšie bol vyhlásený za historický.
  - Logistika stavia zoznam od nuly („zelená lúka"), s krátkym prínosom ku každej položke, vo svojej kópii na SharePointe; Marek prenáša dohodnuté riadky do mastera. Ďalšia revízia je na stredajšom stretnutí, ak bude pripravené.
  - Spilka presadzoval cenařky.
  - **„Duo"** (pravdepodobne LLM platforma Deloitte, [[ASM-187]]) sa už používa na logistické témy mimo trackera.
- **Otvorené na strane BigHubu**:
  - Jindřich sa mal spýtať Dudaška, či sa dá z AI rozpočtu financovať aj automatizácia bez AI ([[ASM-233]], termín 10-02). **Over si odpoveď s Jindřichom pred 10:00.**

## Otvorené body na vyriešenie

Z 09-24 → 10-01 → 10-02:

| Položka | Vlastník | Stav |
|---|---|---|
| Rekapitulačný e-mail rozhodnutí z 10-01 + špecifikácia logistike | Marek | **Mešká** (termín 10-02); plánované na začiatok tohto týždňa |
| Písomné odpovede na Slámove májové komentáre | Marek | Vo v5; čaká na finálnu kontrolu |
| Spätná väzba v stĺpci J k dátovej mape | Sláma | Termín začiatkom tohto týždňa |
| Vlastník SharePoint Listu dodávateľov na strane Dr. Max | Sláma / Tereza | **Nikto nemenovaný** |
| Zoznam typov problémov z Axapty | Tereza / Jana | Neprišiel |
| Okamžité avízo: ktorí dodávatelia, lehota, fáza | Marek sa spýta logistiky | Otvorené ([[ASM-240]]) |
| Harmonogram aktualizovaný o +1 týždeň testovania; dopad na plné UAT 10-15/16 ([[ASM-056]]) | Jindřich | Nepotvrdené |
| Graph API + prístup k mailboxu | Filip → infra Maxu | Blokované (eskalácia AKS) |
| Zdieľaný testovací telefón | Dušan / Tereza | Bez termínu |
| Automatizácia bez AI v rámci AI rozpočtu? | Jindřich → Dudaško | Odpoveď neznáma |
| Časový plán celého projektu pre Terezu | Jindřich | Sľúbená high-level verzia |

## Navrhovaná agenda

Predpokladá ~60 min. Pozvánku vlastní Tereza, takže to ponúkni ako časť za BigHub.

1. **(5 min) Úvod, vedie Jindřich.** Predstaviť BigHub tím na plný úväzok: „úvodná fáza je za nami; Marek a ja sme na tom na plný úväzok." Spýtať sa Žůrka a Dudaška, s čím chcú odísť. **Nech oni pomenujú otázku.**
2. **(15 min) Kde Reklamácie stoja: Marek, téma 1.** Jeden slide alebo ústne: čo je dohodnuté, čo je otvorené, termíny. Zdôrazniť e-mailového agenta ako AI časť a časť s úsporou, a dizajn s minimom v Axapte, prenositeľný, ako chcel Dudaško.
3. **(5–10 min) Slámove komentáre: Jindřich, Marek podporuje, téma 2.** Len ak to niekto otvorí, alebo stručne, ak už príbeh koluje. Prevziať zodpovednosť a povedať dátum.
4. **(15 min) Hodnota a pokračovanie.** Hodnota fázy 1 je skromná; plná hodnota potrebuje všetky fázy a neskoršie fázy potrebujú definovaný ťahúň hodnoty. Ponúknuť krátke discovery pre každú neskoršiu fázu pred ďalším záväzkom na vývoj. Rozhodnutie o pokračovaní je na nich.
5. **(10 min) Širší backlog logistiky: marcový zoznam, téma 3.** Reklamácie boli ich vlastná marcová požiadavka. Kam zapadajú cenařky a skladové položky; zoznam „na zelenej lúke" ako nástroj; stredajšie stretnutia ako fórum.
6. **(5 min) Záver.** Rozhodnutia, vlastníci, termíny. Marek pošle písomnú rekapituláciu v ten istý deň.

## Hlavné body a na čo si dať pozor

**Hlavné body**
- **„Reklamácie boli marcová požiadavka samotnej logistiky."** Je to v ich e-maile takmer doslova: odfotiť identifikátor príjmu, AI vyplní formulár a pošle e-mail dodávateľovi. BigHub túto víziu dokončuje. Neodchyľuje sa.
- **AI časť je e-mailový agent.** Tam podľa Slámu leží skutočná úspora. Je postavený ako PoC a 10-01 bol prijatý dobre. Aplikácia, protokol a rozvozový list sú digitalizácia a základ, na ktorom agent stojí.
- **Dizajn zapadá do Dudaškovho odchodu z Axapty**: minimum v Axapte, údaje o dodávateľoch v SharePoint Liste kľúčovanom číslom dodávateľa, logika v aplikácii/platforme. Prenesie sa, keď sa nahradí WMS časť Axapty. Sláma potvrdil, že ERP časť, register dodávateľov a doklady reklamácií zostávajú.
- **Špecifikácia je odteraz kontrakt.** Jeden vlastník (Marek), každý klientsky komentár zodpovedaný písomne, zmeny ako change requesty s cenou v MD a písomným schválením. Toto je náprava medzery s májovými komentármi.
- **Pri hodnote buď úprimný.** Fáza 1 ≈ 425 tis. Kč, plné ≈ 1 FTE len so všetkými fázami, a číslo je odhad, nie meranie. KPI je end-to-end čas procesu, ktorý potrebuje baseline pred spustením. Ponúkni, že ho zmeriame.
- **Rámec kapacity (Marekova rola)**: BigHub prioritizuje naprieč ~50 iniciatívami, čoskoro približne šesťkrát viac naprieč celým Maxom. Poradie určujú prínosy a priority stanovuje business.

**Na čo si dať pozor**
- **Rudolf Žůrek** je priamy („to je blbosť" je možné), ale férový a otvorený argumentom. Neber priamosť osobne; odpovedaj číslami a dátumami (Jan, 10-02).
- **Petr Spilka** môže pred Žůrkom a Dudaškom pózovať ako ten, kto rozhoduje, a reálne má menšiu moc, než ukazuje. Už nazval úsporu Reklamácií malou a tlačí cenařky. **Nedovoľ, aby sa „BigHub urobí analýzu cenařiek" stalo bezpodmienečným.** Závisí to od toho, či cenařky skončia na vrchole s kvantifikovanými prínosmi, od realistického štartu v januári a od pozorovania v nov–dec alebo v marci.
- **Tereza** je v strese a už predtým posunula informácie nepresne. Drž ju blízko a všetko povedané dnes potvrď písomne v ten istý deň ([[ASM-185]]).
- **Tomáš Dudaško** je podľa Marekovho čítania 50/50. Trochu sa ohradil voči rámcu „nie AI" (09-22). Začni e-mailovým agentom a platformou, nie „je to len digitalizácia".
- **Nehovor zle o predchodcoch** (Honza Sovka, Alana). Rámec je „úvodná fáza, teraz na plný úväzok".
- **Deloitte / „Duo"** je už v logistike prítomný. Ak budú Reklamácie vyzerať slabo, otázka pokračovania môže byť v skutočnosti o tom, kto robí AI pre logistiku. Neotváraj to; buď pripravený, ak to príde.
- **Nezaväzuj sa v miestnosti k zmene MD ani rozpočtu** za rozsah z májových komentárov. Podľa [[ASM-186]] to ide cez change request.
- **Nástroj pre údaje o dodávateľoch**: Jindřich nadhodil X-Manager ([[ASM-243]]). Zosúlaď sa s ním pred 10:00, aby BigHub pred klientom neprotirečil smeru so SharePoint Listom.
- **Sláma nie je v miestnosti.** Nedohaduj detaily dátovej mapy bez neho; povedz „čaká sa na Slámov stĺpec J".

## Otázky, na ktoré treba získať odpoveď

1. **Aké rozhodnutie má toto stretnutie priniesť?** Pokračovať s Reklamáciami podľa plánu, pokračovať v užšom rozsahu, pozastaviť po fáze 1, alebo prepriorizovať voči iným logistickým iniciatívam?
2. Ak sa pokračuje: **kto na strane Dr. Max vlastní SharePoint List s údajmi o dodávateľoch** a kto podpisuje finálnu špecifikáciu (len Sláma, alebo Spilka ako business vlastník)?
3. **Je prijateľné discovery pre každú fázu** (ťahúň hodnoty pre fázy 2–4) pred ďalším záväzkom na vývoj?
4. **Kto zmeria baseline KPI** (end-to-end čas procesu) pred spustením?
5. **Okamžité avízo**: ktorí dodávatelia, aká lehota, ktorá fáza? Je automatické odoslanie prijateľné?
6. **Rozpočet**: dá sa automatizácia bez AI (napr. cenařky cez Power Automate) financovať z rozpočtu AI iniciatív? (Dudaško je v miestnosti.)
7. **Priorita naprieč logistikou**: kde stoja Reklamácie, Fakturace doprav a cenařky voči sebe, a akceptuje Žůrek zoznam „na zelenej lúke" ako jediný nástroj?
8. **Časový plán**: je +1 týždeň testovania akceptovaný a posúva plné UAT (10-15/16)?

## Pred 10:00 (s Jindřichom)

- [ ] Zisti Dudaškovu odpoveď na rozpočet pre automatizáciu bez AI ([[ASM-233]]) a nápad s „manager" nástrojom ([[ASM-243]]).
- [ ] Dohodnite, kto otvára (Jindřich) a kto rieši tému Slámu (Jindřich ju preberá; Marek povie dátum).
- [ ] Vyber dátum odoslania rekapitulácie + špecifikácie a povedz ho v miestnosti.
- [ ] Prines vytlačenú alebo otvorenú dátovú mapu (Excel) a deck e-mailového agenta (Filipov, v priečinku na Teams).
