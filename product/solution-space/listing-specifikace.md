---
last_updated: 2026-09-15
last_updated_by: manual — conversational
---

# Listing — Specifikace pro vývoj

Standardizace a automatizace produktového listingu — Dr. Max / BigHub AI Iniciativa

---

## Management summary

Listing je interní e-commerce PIM (Product Information Management) a AI platforma pro obohacování produktového katalogu, určená content manažerům lékárenského/zdravotnického e-commerce. Dnes probíhá tvorba a údržba produktového obsahu ručně, produkt po produktu, nad daty rozptýlenými napříč Excel exporty od dodavatelů — bez jednotného systému a s ručním přepisem do Magento. Cílem nástroje je tento proces nahradit centralizovaným vstupem, AI-asistovaným generováním obsahu a automatickým propisem do e-shopu.

Nástroj dnes reálně běží nad testovacími daty v jedné pilotní kategorii (Proteiny / Doplňky stravy, 72 produktů) a demonstrovatelně funguje — viz Fáze MVP níže. Produkční nasazení nad celým katalogem klienta (cca 45 000 řádků × 1 200 sloupců) ještě neproběhlo; hlavním blokátorem je nedodaný kategorický/parametrický systém na straně Dr. Max (viz Závislosti).

### MVP

| Položka | Stav |
|---------|------|
| Vstup produktových dat | Hotovo |
| Generování produktového obsahu | Hotovo |
| Struktura a parametry | Hotovo |
| Dohledání chybějících dat | Hotovo |
| Kontrola listingovým týmem | Hotovo |
| Nasazení prototypu | Hotovo |
| Propis do Magento | Backlog |
| Produkční nasazení | Plánováno |

### Plná verze

| Položka | Stav |
|---------|------|
| Dohledání v externích zdrojích (scraping) | Blokováno |
| Import z externích zdrojů (soubor od dodavatele) | Backlog |
| Tvorba popisů pro nové produkty | Hotovo (pokryto stávajícím flow) |
| Vrstvené/složené listovací standardy (hierarchie kategorií) | Backlog — potřeba vyspecifikovat |
| Update systému variant | Blokováno |

### Nice to Have / Backlog

| Položka | Stav |
|---------|------|
| Multi-kategoriální podpora (rozsah 500–2 000+) | Backlog |
| Samoobslužný import dat (bez programátora) | Backlog |

---

## Byznys hodnota

**Hlavní cíl**: vyšší konverze — kvalitní a jednotný listing prodává.

**Proč na tom záleží**: nekonzistentní a neúplný obsah dnes ztěžuje zavádění nových produktů a nechává nevyužitý konverzní potenciál. Pokud se tento stav neřeší, roste s velikostí katalogu (45 000+ řádků) i náročnost ruční správy — problém se škáluje horší, ne lépe.

**Vedlejší cíle**: spokojenější zákazníci, přehlednější e-shop, snazší vyhledávání a filtrování, lepší SEO, zrychlení procesu listingu, snížení interní administrativy.

**Kvalitativní přínos**: eliminace ruční tvorby a údržby produktového obsahu a parametrů nad velkým a nekonzistentním datasetem; standardizace procesu napříč listingovým týmem; příprava na škálování na stovky až tisíce kategorií; snížení regulatorního rizika díky deterministickému systému právních varovných šablon (Warning Templates) — AI zde pouze vybírá variantu z předem schváleného textu, nikdy nevymýšlí vlastní právní formulaci — a blacklistu neregulérních léčebných tvrzení.

**Kvantifikovaný přínos**: interní pracovní odhad 300 000 Kč — zatím neověřený s klientem, bez podkladové baseline.

**Úspora času**: `-tbd-`

---

## KPI

Dnes se formálně nesleduje žádné KPI. Kandidátní metriky, odvozené z cíle výše (Goal → Otázka → Metrika):

| Cíl | Otázka | Kandidátní metrika |
|---|---|---|
| Zvýšit konverzi kvalitním listingem | Zlepšila se konverze na produktových stránkách? | Konverzní poměr před/po zavedení AI listingu |
| Zvýšit kompletnost/kvalitu katalogu | Kolik produktů splňuje standard kvality? | Průměrné/mediánové skóre napříč katalogem; podíl produktů nad prahovou hodnotou skóre |
| Snížit ruční administrativu | Kolik listingů se schvaluje bez ručního zásahu? | Podíl produktů s automaticky doplněnými chybějícími daty bez ručního zásahu |
| Zrychlit proces listingu | Jak dlouho trvá od vstupu dat po schválení? | Čas od vstupu dat po schválení listingovým týmem |
| Škálovat na celý katalog | Kolik z cílového rozsahu je pokryto? | Počet pokrytých kategorií vs. celkový cílový rozsah (dnes: 72 produktů v 1 pilotní kategorii) |
| Řídit tok práce | Kolik listingů čeká na schválení? | Počet produktů se schváleným/publikovaným listingem |

Přesné cílové hodnoty a formální vlastnictví KPI zůstávají otevřené — viz Otevřené otázky.

---

## 1. MVP

### Co je součástí

| ID | Položka | Stav |
|----|---------|------|
| 1 | Vstup produktových dat | Hotovo |
| 2 | Generování produktového obsahu | Hotovo |
| 3 | Struktura a parametry | Hotovo |
| 4 | Dohledání chybějících dat | Hotovo |
| 6 | Kontrola listingovým týmem | Hotovo |
| 11 | Nasazení prototypu | Hotovo |
| 7 | Propis do Magento | Backlog |
| 8 | Produkční nasazení | Plánováno |

Následující funkčnost je potvrzená jako reálně existující — vychází z živého demo walkthroughu nástroje, který předvedl Filip Černý (2026-09-11), doplněného přímým čtením kódové základny (2026-09-14), nikoli z předpokladu.

### 1.1 Vstup dat, práce s kategorií a přehled katalogu

**Vstup produktových dat (upřesněno s Jan S.)**: dnešní vstup dat do nástroje vyžaduje součinnost programátora — content manažer (netechnický uživatel) si aktuální data sám nahrát nemůže. Pro MVP a ověření funkčnosti je to dostačující. Samoobslužný import dat bez zásahu programátora je navržen jako možnost dalšího rozšíření produktu — viz Fáze Nice to Have / Backlog.

Nástroj pracuje vždy v kontextu jedné vybrané kategorie. Dnes je pokryta pouze 1 pilotní kategorie (Proteiny / Doplňky stravy, 72 produktů); rozšíření na další kategorie čeká na kategorický/parametrický systém od Dr. Max (viz Závislosti) a je scopováno jako Nice to Have (multi-kategoriální podpora).

Pro vybranou kategorii nástroj poskytuje přehled všech jejích produktů, na produkt s těmito údaji:

- **Produkt a SKU** — identifikace položky.
- **Skóre** — číselné skóre kvality/kompletnosti produktu (0–100).
- **Stav** — workflow stav produktu. **Potvrzeno v kódu** (`ProductStatus` enum, `backend/src/models/domain.py`): existuje 5 stavů, ne jen 2 pozorované v demu — *Import*, *Rozpracováno*, *Čeká na doplnění informací*, *Čeká na kontrolu*, *Hotovo*. Přechod Import → Rozpracováno je automatický (nastane na serveru při prvním uložení produktu); všechny ostatní přechody jsou čistě manuální rozhodnutí uživatele. V backendu neexistuje žádná automatická logika typu "skóre ≥ X → Hotovo."
- **Problémy** — souhrn validačních problémů podle závažnosti (chyba / upozornění / info).

Přehled je stránkovaný a filtrovatelný; v testovacích datech potvrzeno 72 produktů v jedné kategorii.

Toto je i odpověď na otázku, jak se měří kvalita/kompletnost listingu — viz Skórování a validace níže.

**Skórování a validace** (potvrzeno v kódu, `backend/src/validation/scoring.py`): každý produkt startuje na 100 bodech a ztrácí body za nalezené problémy — 12 b. (chyba) / 4 b. (upozornění/info) za chybějící povinnou/doporučenou hodnotu, neznámý parametr, neplatnou hodnotu parametru nebo nedostatek obrázků; 3 b. za zakázanou frázi; 1 b. za drobnosti (délka textu, počet odrážek, chybějící název produktu). Skóre je vždy vypočítané deterministicky z konkrétních nalezených problémů, nikdy odhadem.

**Důležitá odchylka**: jakmile má produkt stav *Hotovo*, jeho skóre je natvrdo přepsáno na 100 bez ohledu na to, co validace reálně najde. To znamená, že "Hotovo" produkt vždy vypadá bezchybně bez ohledu na skutečný obsah — riziko, že reálné problémy zůstanou skryté za kosmeticky perfektním skóre. Stojí za zvážení, zda je to žádané chování, nebo mezera k opravě.

### 1.2 Generování a správa obsahu produktu

Jako content manažer chci, aby nástroj přijal dostupná produktová data a vygeneroval strukturovaný obsah a chybějící atributy, abych nemusel psát popis a parametry ručně od nuly.

- Generování je vždy explicitně spouštěné uživatelem, ne automatické na pozadí; lze zvolit zdroj podkladového textu (původní listing / vlastní text).
- Výstupem je strukturovaný text (úvodní text, hlavní vlastnosti, složení, dávkování, upozornění, o značce) plus AI-obohacené strukturované parametry. Návrh je oddělený od původního obsahu, nepřepisuje ho.
- Chybějící data dohledatelná z dostupných zdrojů jsou automaticky doplněna a odlišena od dat zadaných manuálně. **Upřesnění (Jan S.)**: "dohledání" zde neznamená vyhledávání nových dat mimo poskytnutý vstup — nástroj chybějící data pouze reformuluje/odvozuje z dat, která už má k dispozici od dodavatele. Skutečné dohledávání z externích zdrojů (web, scraping, dodavatelské dokumenty) je samostatná funkce ve Fázi Plná verze — viz Dohledání dat z externích zdrojů.
- **Verzování**: každá úprava produktu vytvoří novou verzi. Historie verzí umožňuje návrat na starší verzi (v demu předvedeno: návrat na v2.04); návrat musí zachovat auditní stopu a neztratit aktuální validační stav.
- Workflow stav produktu lze změnit manuálně kdykoli.
- **Kontrola a schválení**: navržený obsah je vždy porovnatelný s aktuálním obsahem a podléhá schválení pracovníkem listingového týmu před finálním použitím.
- **Souběžná úprava (potvrzeno v kódu)**: každý produkt nese `row_version`; uložení, obnova verze i mazání verze používají optimistický zámek. Dva lidé upravující stejný produkt souběžně dostanou explicitní konflikt (HTTP 409), ne tiché přepsání — otevřená otázka z předchozí verze tohoto dokumentu je tímto vyřešena.
- **Vztahy mezi produkty (potvrzeno v kódu, nově zjištěno — nebylo v demu)**: datový model už obsahuje pole pro variantní produkty (`variant_product_ids`) a produkty lišící se velikostí balení (`package_size_product_ids`). Zda je na tom postavené i automatické propagování odlišností mezi variantami (viz Fáze Plná verze, "Update systému variant") nebylo v kódu potvrzeno — jen že vztah lze v datech vyjádřit.
- **Externí obohacení (potvrzeno v kódu, nově zjištěno — nebylo v demu)**: existuje funkce pro dohledání produktu na webu (vyhledání podle názvu/EAN, procházení kandidátních URL, verifikace shody, očištění obsahu LLM voláním) — reálně implementováno, ale dnes vypnuté feature flagem (`ENABLE_EXTERNAL_ENRICHMENT`, výchozí off). Odpovídá položce "Dohledání v externích zdrojích" ve Fázi Plná verze — viz tam pro aktualizovaný stav.

### 1.3 Kategoriální standardy ("Listovací minima")

Jako content manažer chci, aby nástroj navrhl parametry produktu podle pravidel definovaných pro danou kategorii, aby výsledek odpovídal standardům vyhledávání a filtrování. Generování obsahu vždy respektuje pravidla nastavená pro danou kategorii. Konfigurace sestává z pěti částí:

1. **6 polí popisu** (úvodní text, hlavní vlastnosti, složení, dávkování, upozornění, o značce) — každé s vlastním pokynem pro AI v přirozeném jazyce, minimálním a maximálním počtem znaků, a příznakem povinnosti.
2. **2 meta-popisová pole** s pevným rozsahem znaků: Krátký popis 140–180 znaků, Teaser popis 60–90 znaků.
3. **Taxonomie produktových parametrů** (28 v demované kategorii — značka, věkové rozmezí, jednotka, alergeny, živiny na porci, příchuť, cílová skupina, léková forma, minerály, vitamíny, časování/užívání, EAN aj.) — každý nezávisle přepínatelný mezi automatickým generováním (AI) a pouze ručním zadáním. **Potvrzeno v kódu**: 28 není pevné číslo — architektura (`backend/STANDARDS.md`) sestavuje sadu parametrů per kategorii z opakovaně použitelných stavebních bloků: globální katalog parametrů (`parameter_definitions`) → sady hodnot (`option_sets`) → skupiny parametrů (`parameter_groups`) → sdílené fragmenty pravidel (`listing_standard_fragments`) → konkrétní konfigurace kategorie (`listing_standard_configs`), která vše slučuje do jednoho efektivního standardu. Kategorie může použít jen parametry existující v globálním katalogu, ale počet a výběr parametrů je per kategorii plně konfigurovatelný — 28 je jen výsledek pro tuto konkrétní kategorii. **Konfigurovatelné je dnes jen na úrovni kategorie** — editor sdílených katalogů (globální parametry, sady hodnot, skupiny, fragmenty) není postavený; kořenový `README.md` repozitáře to sám označuje jako "draft only, ještě k specifikaci."
4. **Blacklist zakázaných medicínských tvrzení** pro danou kategorii (např. "léčí", "hojí", "terapeutický", "léčivý", "uzdravuje", "zmírňuje příznaky") — uložený per kategorii v databázi, editovatelný per kategorie. **Potvrzeno v kódu — oprava předchozího předpokladu**: kontrola dnes NEBLOKUJE uložení. Nalezená zakázaná fráze se vyhodnotí jako `warning`-úroveň problém ve validaci (kódový komentář výslovně říká, že jde o kontextovou věc s možnými falešnými poplachy), ne jako blokující chyba před publikací. Otázka, zda toto má zůstat jen jako upozornění nebo se má zpřísnit na blokující kontrolu, je byznys/compliance rozhodnutí k vyřešení s klientem — viz Otevřené otázky ([[ASM-064]]).
5. **Warning Templates (nově zjištěno, nebylo v demu)** — kategorie může navázat na pole popisu deterministickou právní varovnou šablonu; AI je požádána pouze o výběr varianty, přesný uložený text se vloží beze změny a vygenerovaný obsah se od něj odduplikuje. Toto je druhá (silnější) linie obrany proti nekontrolovanému právnímu textu vedle blacklistu — AI zde nikdy nevymýšlí vlastní právní formulaci.

Nástroj nabízí i funkci "Odvodit minima". **Potvrzeno v kódu — nyní zodpovězeno**: nejde o AI/LLM operaci. Je to deterministický statistický výpočet nad vybranými referenčními produkty dané kategorie — povinnost pole se odvodí jen když ji mají vyplněnou úplně všechny referenční produkty; min/max znaků a rozsah počtu odrážek se odvodí jako min()/max() napříč referenčními produkty; minimální počet obrázků je nejnižší pozorovaný počet, horní práh je 75. percentil + 2. Funkce se týká jen pravidel délky/povinnosti/obrázků/odrážek — nikdy nepřepisuje vazby na parametrový katalog ani blacklist zakázaných frází.

### 1.4 Propis do Magento a produkční nasazení

Jako content manažer chci, aby schválená data byla přenesena do Magento bez ručního přepisu, abych ušetřil čas a eliminoval chyby.

**Potvrzeno v kódu — oprava předchozího předpokladu**: tato funkčnost dnes v kódu neexistuje vůbec. Nástroj je uzavřená smyčka — čte a zapisuje pouze do vlastní PostgreSQL databáze; žádný Magento klient, export, upload ani API volání nikde v backendu není. Identita produktů a kategorií je dnes jen zástupná projekce, jednorázově naseedovaná z legacy exportu ("ours until integration" — komentář přímo v `backend/STORAGE.md` a migračních skriptech). Dřívější poznámka o "pravidelném týdenním import/exportu přes Magento" jako interim řešení se v tomto repozitáři nepotvrdila — buď se odehrává mimo tento kód, nebo šlo o zastaralý/nesprávný předpoklad. Nutno ověřit přímo s klientem, než se tato věta znovu použije v jakémkoli klientském materiálu.

- Metoda přenosu (nahrání souboru vs. přímý zápis do databáze) zůstává nespecifikována — viz Otevřené otázky.
- Po dokončení MVP funkčnosti je nástroj nasazen do produkčního prostředí a použitelný listingovým týmem nad reálnými daty klienta. Produkční nasazení nad reálnými daty ještě neproběhlo — blokátory jsou nedodaný kategorický/parametrický systém na straně Dr. Max **a** nyní potvrzeně i chybějící Magento integrace samotná.

**Kritérium produkčního nasazení (dohoda s Jan S.)**: listingový tým dokáže sám naimportovat produkt, upravit jej v nástroji a dostat výsledek zpět do Magento — i kdyby zpočátku šlo o řešení "na tupáka" (např. kopírování přes Excel) — hlavní podmínkou je, že nikdo nemusí ručně přepisovat obsah mezi systémy (ctrl-c/ctrl-v). Toto je definované jako *starting line* — minimální práh, aby šlo nástroj rozumně používat v současné verzi, ne cílová plně automatizovaná integrace.

### Otevřené otázky — Fáze MVP

- Je blacklist zakázaných medicínských tvrzení schválen Dr. Max, nebo jde o návrh BigHub čekající na review klienta?
- **Byznys/compliance rozhodnutí**: má blacklist zůstat jen upozorněním, nebo se má zpřísnit na blokující kontrolu před publikací? (dnes: warning-only, potvrzeno v kódu)
- Jakým způsobem/formátem chce Dr. Max data zpět do Magento (nahrání souboru vs. přímý zápis do databáze) — a existuje dnes vůbec nějaký propis mimo tento repozitář, nebo je propis do Magento zcela nepostavený?
- Co znamená a k čemu se používá `rich_content` příznak produktu (objeven v kódu, filtrovatelný v katalogu) — A+ / rozšířený obsah?
- Kdy a za jakých podmínek se plánuje zapnout feature flag pro externí obohacení (`ENABLE_EXTERNAL_ENRICHMENT`)?
- Kdy se plánuje editor sdílených katalogů (globální parametry, sady hodnot, skupiny, fragmenty) — dnes editovatelné jen na úrovni kategorie?

---

## 2. Plná verze

### Co je součástí

| ID | Položka | Stav |
|----|---------|------|
| 5 | Dohledání v externích zdrojích (scraping) | Implementováno, vypnuto feature flagem |
| 14 | Import z externích zdrojů (soubor od dodavatele) | Backlog |
| 9 | Tvorba popisů pro nové produkty | Hotovo (pokryto stávajícím flow) |
| 15 | Vrstvené/složené listovací standardy (hierarchie kategorií) | Backlog — potřeba vyspecifikovat |
| 12 | Update systému variant | Blokováno |

### 2.1 Dohledání dat z externích zdrojů

Jako content manažer chci, aby nástroj dohledal chybějící produktová data z externích zdrojů, abych nemusel data dohledávat ručně.

**Rozdělení na dvě samostatná témata (Jan S.)**: "dohledání z externích zdrojů" pokrývá dva odlišné mechanismy se stejným cílem (dodatečný zdroj dat k těžení) — scraping webu a ruční import souboru od dodavatele. Oba jsou popsané níže.

**a) Scraping**

**Potvrzeno v kódu — status upgradovaný oproti předchozí verzi tohoto dokumentu**: funkce je reálně implementovaná, ne jen naplánovaná. Pro produkt s chybějícími daty nástroj umí vyhledat kandidáty na webu podle názvu/EAN, projít je, ověřit shodu a očistit obsah (LLM voláním) do kontextu pro generování obsahu. Dnes je vypnutá centrálním feature flagem (`ENABLE_EXTERNAL_ENRICHMENT`, výchozí hodnota off) — zapnutí je tedy konfigurační krok, ne vývojový úkol.

- Funkce musí projít právním posouzením před širším nasazením do produkce — viz Otevřené otázky. Toto zůstává v platnosti i po potvrzení, že kód existuje.
- Musí být vyřešeno proxy řešení — požadavky z datacentrových IP rozsahů jsou dnes cca z 90 % blokované. V kódu existuje proxy konfigurace, ale řešení je popsáno jako budoucí ("later") — tedy technicky připravené, ne hotové.

**b) Import z externích zdrojů (soubor od dodavatele)**

Jako content manažer chci nahrát soubor od dodavatele (produktový leták PDF nebo XLSX) jako dodatečný zdroj dat k produktu, abych mohl obsah obohatit i bez scrapingu.

- Content manažer nahraje soubor, který mu poslal dodavatel (např. "produktový leták PDF nebo XLSX s informacemi"); jakmile je nahraný, zpracovává se stejně jako scrapovaný obsah — je to další zdroj, ze kterého lze při generování těžit.
- Na rozdíl od scrapingu zde odpadá legální blokátor i proxy problém — jde čistě o ruční upload souboru uživatelem, ne o automatizované stahování.
- **Status**: `-tbd-` — nepotvrzeno v kódu jako samostatná funkce; k vyspecifikování (formát souborů, kde v UI se nahrává, jak se liší od volby "vlastní text" v generování obsahu, viz 1.2).

### 2.2 Tvorba popisů pro nové produkty

Jako content manažer chci použít stejný generační flow i pro zcela nové produkty, ne jen pro úpravu stávajících, abych mohl listovat nové produkty stejně efektivně.

**Vyřešeno — status upgradovaný na Hotovo (dohoda s Jan S.)**: podle procesního nastavení musí být i zcela nové produkty nejdřív založeny v Magentu (klientem / dodavateli), než se dostanou do tohoto nástroje — v nástroji se tedy vždy objeví jako "stávající produkt". Stejný generační flow popsaný v 1.2 (Generování a správa obsahu produktu) proto nové produkty už dnes pokrývá beze zbytku; samostatná funkce není potřeba.

- Pro nový produkt bez existujícího listingu se použije stejný generační flow jako pro úpravu stávajících produktů (viz Generování a správa obsahu produktu).
- Ruční práce, která předchází založení produktu v Magentu (na straně Dr. Max / dodavatelů), je mimo rozsah tohoto e-commerce nástroje — bude případně řešena v rámci širšího E2E procesu listingu, ne zde.

### 2.3 Update systému variant

Jako content manažer chci, aby produktové varianty (barva/příchuť) sdílely základní popis s automaticky propagovanými odlišnostmi, abych nemusel duplicitně spravovat obsah pro každou variantu zvlášť.

- Pokud mají data o variantách od dodavatele dostatečnou kvalitu, odlišnosti mezi variantami se propagují automaticky ze sdíleného základu.
- Kvalita vstupních dat o variantách je dnes nedostatečná (duplicitní/nekonzistentní identifikace napříč variantami stejného produktu) — bez zlepšení dat na straně Dr. Max nelze funkci spolehlivě nasadit.
- **Potvrzeno v kódu (částečně)**: datový model už umí vyjádřit vztah mezi produkty — variantní produkty (`variant_product_ids`) a produkty lišící se velikostí balení (`package_size_product_ids`), volitelné přímo v detailu produktu. Zda na tomto vztahu stojí i automatická propagace odlišností popsaná výše, se z kódu nepotvrdilo — jen že vztah samotný je datově možný.

### 2.4 Vrstvené/složené listovací standardy (hierarchie kategorií)

Jako content manažer chci, aby listovací minima šla definovat na úrovni nadřazené kategorie a dědila se do podkategorií s dalším zpřesněním, aby se nemusela ručně duplikovat napříč hierarchií.

**Přesunuto z Nice to Have do Plná verze (Jan S., potvrzeno)**: v rámci "multi-kategoriální podpory" (viz Fáze Nice to Have) jde ve skutečnosti o dvě oddělená témata — samotné rozšíření na 500–2 000+ kategorií (čistě rozsahová otázka, zůstává v Nice to Have) a architektura dědičnosti listovacích minim napříč vnořenými kategoriemi (toto téma, přesunuté sem, protože je potřeba ho vyspecifikovat dřív, než dojde na plošné škálování).

- **Dnešní stav**: neexistuje žádná určená logika pro vnořené kategorie — 1 listovací minimum platí pro 1 kategorii, bez ohledu na to, jak hluboko je v hierarchii.
- **Příklad hierarchie (Jan S.)**: Pro sportovce → Sportovní výživa a diety → Proteiny → Hovězí proteiny. Návrh: obecná listovací minima na úrovni superkategorie (např. "vše v Pro sportovce musí mít alespoň 3 obrázky") se dědí do nižších úrovní, které je zpřesňují (např. "vše v Proteinech respektuje vše z vyšších kategorií a zároveň vyžaduje rozlišení BIO/neBIO produktů").
- **Otevřená hypotéza (Marek)**: velká granularita kategorií může být na škodu / skreslovat výsledky generování — zvažuje se postupné nabalování kategorií po fázích po dohodě s p. Neumanem, ne otevření celého rozsahu najednou.

### Otevřené otázky — Fáze Plná verze

- Je scraping externích zdrojů právně v pořádku, nebo bude nutné oficiální rozhraní/prostředník?
- Jak se řeší proxy problém (90 % blokovaných požadavků z datacentrových IP)?
- Jak přesně má fungovat import souboru od dodavatele (formát, umístění v UI, vztah k volbě "vlastní text" v generování obsahu — viz 1.2)?
- Jak se mají chovat vnořené/zděděné listovací minima napříč hierarchií kategorií (viz 2.4)?

---

## 3. Fáze Nice to Have / Backlog

### Co je součástí

| ID | Položka | Stav |
|----|---------|------|
| 13 | Multi-kategoriální podpora (rozsah 500–2 000+) | Backlog |
| 16 | Samoobslužný import dat (bez programátora) | Backlog |

### 3.1 Multi-kategoriální podpora

Jako listingový tým chci, aby nástroj podporoval listing napříč více kategoriemi, ne jen jednou pilotní kategorií, abychom mohli škálovat na celý katalog.

**Zúženo (Jan S.)**: architektura dědičnosti listovacích minim napříč vnořenými kategoriemi ("vrstvené/složené listovací standardy") byla vyčleněna do Fáze Plná verze — viz 2.4 — protože je potřeba ji vyspecifikovat nezávisle na tom, kdy a jak moc se rozsah rozšíří. Zde v Nice to Have zůstává čistě otázka rozsahu (kolik a kterých kategorií).

- Po definování cílového rozsahu kategorií Dr. Maxem se validace, generování, uživatelské rozhraní i databázová vrstva rozšíří na plný rozsah kategorií.
- Rollout začíná malou nefarmaceutickou sadou kategorií (potraviny, doplňky stravy, sportovní potřeby) před rozšířením na komplexnější/farmaceutické kategorie ([[ASM-032]]).

### 3.2 Samoobslužný import dat (bez programátora)

Jako content manažer chci umět sám nahrát/aktualizovat aktuální produktová data bez součinnosti programátora, abych nebyl na vstupu dat závislý na vývojovém týmu.

**Nově zjištěno (Jan S.)**: dnešní vstup dat vyžaduje programátora — viz 1.1. Pro MVP a ověření funkčnosti to je v pořádku; toto je navržené jako možnost dalšího rozšíření produktu, ne jako mezera v MVP.

### Otevřené otázky — Fáze Nice to Have

- Cílový rozsah kategorií (orientačně 500–2 000+) není definován — rozsah dopadu na validaci/generování/UI/databázi nelze dnes přesně ohraničit.

---

## Další fáze

Nad rámec aktuálně scopovaných fází:

- Plné rozšíření multi-kategoriální podpory na cílový počet kategorií dle rozhodnutí Dr. Max.
- Vendorský portál — samostatná klientská iniciativa umožňující dodavatelům zadávat listing přímo v jednotném formátu; vazba na tento projekt `-tbd-`.
- Přímá integrace s Magento — uvedena jako záměr v části interních podkladů, zatímco jiný zdroj (odhadová poznámka k propisu do Magento) uvádí, že reálná přímá integrace se v dohledné době nestaví. Rozpor k vyjasnění před zařazením do roadmapy.
- Probíhající analýza možnosti vylepšení celého procesu listingu od začátku do konce — rozsah, vlastník a výstup `-tbd-`.

---

## Mimo rozsah

- **Doporučování kategorií/struktury produktů** — Listing pracuje s kategoriemi, které Dr. Max sám definuje a dodá; návrh kategorického systému samotného závisí na vlastním řešení Dr. Max a není součástí dodávky BigHub. Jakýkoli budoucí požadavek na tuto funkčnost je nový požadavek na rozšíření, ne mezera v dodávce.

---

## Závislosti

- **Kategorický/parametrický systém od Dr. Max** — hlavní blokátor. Bez něj nelze rozšířit řešení z 1 pilotní kategorie na plný rozsah; brání i dokončení produkčního nasazení nad reálnými daty.
- **Rozhodnutí Dr. Max o metodě propisu do Magento** — nahrání souboru vs. přímý zápis do databáze; dosud nespecifikováno.
- **Zlepšení kvality dat o produktových variantách od Dr. Max** — dnešní data obsahují duplicitní/nekonzistentní identifikaci napříč variantami; bez zlepšení nelze spolehlivě nasadit update systému variant (Plná verze).
- **Právní posouzení scrapingu externích zdrojů** — podmínka pro širší nasazení dohledávání dat z externích zdrojů (Plná verze).
- **Rozhodnutí Dr. Max o cílovém rozsahu a granularitě kategorií** — orientačně 500–2 000+, zcela otevřené; ovlivňuje rozsah dopadu na validaci, generování, UI i databázovou vrstvu (Nice to Have).

---

## Technická příloha — API surface

Pro engineering audienci: skutečný stav backend API (`backend/src/api/routes`), potvrzený přímo v kódu. Toto je funkční povrch nástroje dnes, ne plán.

**Products** (`/api/v1/products`):

| Endpoint | Účel |
|---|---|
| `GET /products` | Stránkovaný/třídicí/filtrovatelný seznam produktů se skóre a počty problémů podle typu; filtry: stav, typ produktu, rich content, varianty/velikost balení, fulltext. |
| `GET /products/{id}` | Plný detail produktu (popis, parametry, obrázky, verze, zpětná vazba, externí obohacení, propojené varianty/velikosti balení). |
| `GET /products/{id}/validation` | Přepočítá validaci a vrátí skóre + problémy. |
| `POST /products/{id}/generate` | AI generování — celý listing, nebo jen popis / parametry / meta popisy; vrací i `quality_improvement` (rozdíl skóre před/po). |
| `PATCH /products/{id}` | Úprava obsahu, stavu, typu produktu, zpětné vazby, externího obohacení; optimistický zámek (`expected_row_version`), konflikt vrací 409. |
| `GET /products/{id}/versions` | Historie verzí listingu. |
| `POST /products/{id}/versions/{version_id}/restore` | Návrat na historickou verzi. |
| `DELETE /products/{id}/versions/{version_id}` | Smazání historické verze (prořezání historie). |
| `POST /products/{id}/external-enrichment/scrape` | Vyhledání a načtení externího zdroje pro produkt; vrací 503, pokud je feature flag vypnutý (dnes výchozí stav). |

**Categories** (`/api/v1/categories`):

| Endpoint | Účel |
|---|---|
| `GET /categories` | Seznam kategorií. |
| `GET /categories/{id}/listing-standard/effective` | Plně vyřešený (efektivní) standard pro danou kategorii. |
| `GET /categories/{id}/listing-standard/config` | Syrová editovatelná konfigurace kategorie. |
| `PUT /categories/{id}/listing-standard/config` | Uložení konfigurace kategorie; optimistický zámek (`revision`), konflikt vrací 409. |
| `GET /categories/{id}/listing-standard/editor-view` | Jedno volání vracející konfiguraci + vyřešený standard + všechny sdílené katalogy — pohání konfiguraci kategoriálních standardů. |
| `POST /categories/{id}/derive-standard` | "Odvodit minima" — viz Kategoriální standardy ("Listovací minima"). |

---

## Otevřené otázky (konsolidované)

Fázově specifické otevřené otázky jsou u příslušné fáze výše. Zde jen otázky, které se týkají projektu jako celku:

- Jaký je konečný počet/granularita kategorií, které Dr. Max požaduje? Orientačně 500–2 000+, zcela otevřené.
- Kdo je druhý byznysový vlastník Listingu vedle Petra Neumana?
- Jaká konkrétní KPI se budou u Listingu sledovat a jaké mají cílové hodnoty? (viz kandidátní metriky výše)
- Jaká je návratnost/kvantifikovaná byznys hodnota projektu — interní odhad 300 000 Kč není klientem potvrzen a chybí i podkladová baseline.
- Existuje rozpor mezi interním podkladem (přímá integrace s Magento jako plánovaný krok) a odhadovou poznámkou k propisu do Magento (reálná přímá integrace se pravděpodobně nestaví) — který stav platí? **Potvrzeno kódem**: žádná Magento integrace dnes neexistuje v tomto repozitáři v žádné formě — otázka se tím zužuje na to, zda se propis odehrává jinde mimo tento kód, nebo je zcela nepostavený.
- Jaký je rozsah, vlastník a výstup probíhající analýzy vylepšení listing procesu od začátku do konce?
- Co znamená a k čemu se používá `rich_content` příznak produktu?
- Je zjištěná odchylka "Hotovo = skóre natvrdo 100" žádané chování, nebo se má opravit?
