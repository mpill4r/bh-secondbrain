---
last_updated: 2026-09-11
last_updated_by: manual — conversational
---

# Listing — Specifikace

Standardizace a automatizace produktového listingu — Dr. Max AI Iniciativa

---

## Přehled produktu

Listing je interní e-commerce PIM (Product Information Management) a AI platforma pro obohacování produktového katalogu, určená content manažerům lékárenského/zdravotnického e-commerce. Řeší tři věci: audit a validaci zdraví katalogu (skórování listingů proti regulatorním a kategorizačním kritériím), automatizaci tvorby obsahu (GenAI generuje strukturované popisy, meta texty a taxonomické atributy) a konfiguraci kategoriálních standardů ("Listovací minima" — pravidla, AI pokyny, znakové limity, povolené hodnoty atributů, blacklist zakázaných medicínských tvrzení).

**Problém, který řeší**: produktová data od dodavatelů jsou dnes neúplná, ruční úprava listingu probíhá produkt po produktu, data jsou rozptýlená napříč Excel exporty místo jednoho systému a propis do Magenta je ruční přepis s minimální integrací. Důsledky: nekonzistentní kvalita obsahu, náročné zavádění nových produktů a nevyužitý potenciál konverze.

**Rozsah dat**: produktový katalog klienta čítá cca 45 000 řádků × 1 200 sloupců (příchuť, cena, benefitové karty, viditelnost na e-shopu, SEO parametry apod.). Nástroj dnes pracuje nad testovacími daty v jedné pilotní kategorii (Proteiny / Doplňky stravy, 72 produktů); produkční nasazení nad reálnými daty klienta ještě neproběhlo.

**Hlavní blokátor**: Dr. Max dosud nedodal fungující systém kategorií/parametrů produktů (např. jak kategorizovat "balenou vodu"). Bez něj nelze rozšířit řešení z jedné pilotní kategorie na plný rozsah.

---

## Byznys hodnota

**Hlavní cíl**: vyšší konverze — kvalitní a jednotný listing prodává.

**Vedlejší cíle**: spokojenější zákazníci, přehlednější e-shop, snazší vyhledávání a filtrování, lepší SEO, zrychlení procesu listingu, snížení interní administrativy.

**Kvalitativní přínos**: eliminace ruční tvorby a údržby produktového obsahu a parametrů nad velkým a nekonzistentním datasetem; standardizace procesu napříč listingovým týmem; příprava na škálování na stovky až tisíce kategorií; snížení regulatorního rizika díky vestavěnému blacklistu neregulérních léčebných tvrzení.

**Kvantifikovaný přínos**: interní pracovní odhad 300 000 Kč, zatím neověřený s klientem.

**Úspora času**: `-tbd-`.

---

## KPI

Dnes se formálně nesleduje žádné KPI. Kandidátní metriky:

- Průměrné/mediánové skóre napříč katalogem a podíl produktů nad prahovou hodnotou skóre
- Konverzní poměr na produktových stránkách před/po
- Počet produktů se schváleným/publikovaným listingem
- Podíl produktů s automaticky doplněnými chybějícími daty bez ručního zásahu
- Čas od vstupu dat po schválení listingovým týmem
- Počet pokrytých kategorií vs. celkový cílový rozsah (dnes: 72 produktů v 1 pilotní kategorii)

---

## Fázování

- **MVP** — vstup dat, generování obsahu a parametrů pro existující produkty, kontrola listingovým týmem, propis do Magento, produkční nasazení.
- **Plná verze** — dohledání dat z externích zdrojů, tvorba popisů pro nové produkty, update systému variant.
- **Nice to Have / Backlog** — multi-kategoriální podpora nad rámec pilotní kategorie.

---

## Mimo rozsah

- Doporučování kategorií/struktury produktů — závisí na vlastním kategorickém systému Dr. Max, není součástí dodávky BigHub ([[ASM-031]]). Jakýkoli budoucí požadavek je nový požadavek na rozšíření, ne mezera v dodávce.

---

## Závislosti

- Kategorický/parametrický systém od Dr. Max — blokuje rozšíření z 1 pilotní kategorie na plný rozsah.
- Rozhodnutí Dr. Max o metodě propisu do Magento.
- Zlepšení kvality dat o produktových variantách od Dr. Max.
- Právní posouzení scrapingu externích zdrojů.
- Rozhodnutí Dr. Max o cílovém rozsahu a granularitě kategorií.

---

## Fáze MVP

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

### Uživatelské scénáře a akceptační kritéria

**Vstup dat, generování obsahu a doplnění chybějících dat**

Jako content manažer chci, aby nástroj přijal dostupná produktová data a vygeneroval strukturovaný obsah a chybějící atributy, abych nemusel psát popis a parametry ručně od nuly.

- Pokud má produkt dostupná vstupní data, content manažer zvolí zdroj (původní listing / vlastní text) a spustí generování tlačítkem "Generovat".
- Během generování se zobrazí stav načítání.
- Po dokončení se zobrazí strukturovaný text — úvodní text, hlavní vlastnosti, složení, dávkování, upozornění — vedle původního obsahu, bez jeho přepsání.
- Chybějící data dohledatelná z dostupných zdrojů jsou automaticky doplněna a vizuálně odlišena jako AI-doplněná.
- Dokud není žádný popis vygenerován, zobrazí se prázdný stav ("Zatím nebyl vygenerován žádný popis").

**Struktura, parametry a kategoriální standardy ("Listovací minima")**

Jako content manažer chci, aby nástroj navrhl parametry produktu podle pravidel definovaných pro danou kategorii, aby výsledek odpovídal standardům vyhledávání a filtrování.

- Generování obsahu pro produkt v dané kategorii vždy respektuje pravidla nastavená v "Listovacích minimech" pro tuto kategorii.
- Každé z polí popisu (úvodní text, hlavní vlastnosti, složení, dávkování, upozornění, o značce) má definovaný pokyn pro AI, minimální a maximální počet znaků a příznak povinnosti.
- Krátký popis respektuje rozsah 140–180 znaků, Teaser popis rozsah 60–90 znaků.
- Každý z parametrů produktové taxonomie (značka, věkové rozmezí, jednotka, alergeny, živiny na porci, příchuť, cílová skupina, léková forma, minerály, vitamíny, časování/užívání, EAN aj.) je nezávisle přepínatelný mezi automatickým generováním a pouze ručním zadáním.
- Vygenerovaný text nesmí obsahovat žádnou frázi ze seznamu zakázaných frází pro danou kategorii (např. "léčí", "hojí", "terapeutický", "léčivý", "uzdravuje", "zmírňuje příznaky").
- AI-obohacené hodnoty parametrů jsou vizuálně odlišeny od původních.

**Kontrola a schválení listingovým týmem**

Jako pracovník listingového týmu chci zkontrolovat a schválit navržený obsah před jeho finálním použitím, abych měl kontrolu nad výslednou kvalitou.

- Navržený obsah je vždy zobrazen v porovnání vedle aktuálního obsahu.
- Produkt nese číselné skóre a rozklad validačních problémů podle závažnosti (chyba / upozornění / info).
- Každá úprava produktu vytvoří novou verzi, předchozí verze zůstává dostupná pro návrat.
- Workflow stav produktu je editovatelný v hlavičce detailu produktu (pozorované hodnoty: Import, Rozpracováno — úplný seznam stavů viz Otevřené otázky).
- Katalogová tabulka zobrazuje u každého produktu sloupce Produkt, SKU, Skóre, Stav a Problémy, se stránkováním a filtry.

**Propis do Magento**

Jako content manažer chci, aby schválená data byla přenesena do Magento bez ručního přepisu, abych ušetřil čas a eliminoval chyby.

- Schválený produktový listing je po propisu přenesen do Magento bez ručního zásahu.
- Metoda přenosu (nahrání souboru vs. přímý zápis do databáze) není dnes specifikována — viz Otevřené otázky.

**Produkční nasazení**

- Po dokončení MVP funkčnosti je nástroj nasazen do produkčního prostředí a použitelný listingovým týmem nad reálnými daty klienta.
- Testovací data jsou nahrazena reálným datovým tokem (dnešní interim: pravidelný týdenní import/export přes Magento).

### Hraniční případy a chybové scénáře

- Produkt bez dostupných vstupních dat — generování nelze spustit, nástroj musí uživatele informovat o chybějícím vstupu.
- Generovaný text obsahuje zakázanou frázi — musí být zablokován před uložením, ne až po publikaci.
- Krátký popis nezačíná názvem značky jako první slovo — vyhodnoceno jako upozornění.
- Chybí povinné pole dle "Listovacích minim" — vyhodnoceno jako chyba, produkt nelze schválit se skóre pod definovaným prahem (hraniční hodnota — viz Otevřené otázky).
- Souběžná úprava stejného produktu více uživateli — chování při konfliktu není definováno, viz Otevřené otázky.
- Kategorie nemá definovaná "Listovací minima" — chování (blokace, nebo výchozí pravidla) není definováno, viz Otevřené otázky.
- Návrat na starší verzi produktu musí zachovat auditní stopu a neztratit aktuální validační stav.

---

## Fáze Plná verze

### Co je součástí

| ID | Položka | Stav |
|----|---------|------|
| 5 | Dohledání v externích zdrojích | Blokováno |
| 9 | Tvorba popisů pro nové produkty | Backlog |
| 12 | Update systému variant | Blokováno |

### Uživatelské scénáře a akceptační kritéria

**Dohledání dat z externích zdrojů**

Jako content manažer chci, aby nástroj dohledal chybějící produktová data z externích zdrojů, abych nemusel data dohledávat ručně.

- Pro produkt s chybějícími daty a povolenými externími zdroji nástroj dohledá relevantní informace a nabídne je k doplnění.
- Funkce musí projít právním posouzením před širším nasazením do produkce — viz Otevřené otázky.
- Musí být vyřešeno proxy řešení — požadavky z datacentrových IP rozsahů jsou dnes cca z 90 % blokované.

**Tvorba popisů pro nové produkty**

Jako content manažer chci použít stejný generační flow i pro zcela nové produkty, ne jen pro úpravu stávajících, abych mohl listovat nové produkty stejně efektivně.

- Pro nový produkt bez existujícího listingu se použije stejný generační flow jako pro úpravu stávajících produktů.

**Update systému variant**

Jako content manažer chci, aby produktové varianty (barva/příchuť) sdílely základní popis s automaticky propagovanými odlišnostmi, abych nemusel duplicitně spravovat obsah pro každou variantu zvlášť.

- Pokud mají data o variantách od dodavatele dostatečnou kvalitu, odlišnosti mezi variantami se propagují automaticky ze sdíleného základu.
- Kvalita vstupních dat o variantách je dnes nedostatečná (duplicitní/nekonzistentní identifikace napříč variantami stejného produktu) — bez zlepšení dat na straně Dr. Max nelze funkci spolehlivě nasadit.

### Hraniční případy a chybové scénáře

- Externí zdroj dat je nedostupný nebo blokovaný — dohledání dat musí selhat bez pádu a nabídnout ruční doplnění.
- Data o variantách obsahují duplicitní nebo nekonzistentní identifikaci — update systému variant musí tento stav rozpoznat a nepropagovat chybná data napříč variantami.

---

## Fáze Nice to Have / Backlog

### Co je součástí

| ID | Položka | Stav |
|----|---------|------|
| 13 | Multi-kategoriální podpora | Backlog |

### Uživatelské scénáře a akceptační kritéria

**Multi-kategoriální podpora**

Jako listingový tým chci, aby nástroj podporoval listing napříč více kategoriemi, ne jen jednou pilotní kategorií, abychom mohli škálovat na celý katalog.

- Po definování cílového rozsahu kategorií Dr. Maxem se validace, generování, uživatelské rozhraní i databázová vrstva rozšíří o vrstvený/kompozitní systém listingových standardů.
- Rollout začíná malou nefarmaceutickou sadou kategorií (potraviny, doplňky stravy, sportovní potřeby) před rozšířením na komplexnější/farmaceutické kategorie ([[ASM-032]]).

### Hraniční případy a chybové scénáře

- Cílový rozsah kategorií (orientačně 500–2 000+) není definován — rozsah dopadu na validaci/generování/UI/databázi nelze dnes přesně ohraničit.

---

## Další fáze

Nad rámec aktuálně scopovaných fází:

- Plné rozšíření multi-kategoriální podpory na cílový počet kategorií dle rozhodnutí Dr. Max.
- Vendorský portál — samostatná klientská iniciativa umožňující dodavatelům zadávat listing přímo v jednotném formátu; vazba na tento projekt `-tbd-`.
- Přímá integrace s Magento — uvedena jako záměr v části interních podkladů, zatímco jiný zdroj (odhadová poznámka k propisu do Magento) uvádí, že reálná přímá integrace se v dohledné době nestaví. Rozpor k vyjasnění před zařazením do roadmapy.
- Probíhající analýza možnosti vylepšení celého procesu listingu od začátku do konce — rozsah, vlastník a výstup `-tbd-`.

---

## Časté otázky

**Co Listing řeší?**
Automatizaci tvorby a doplňování produktového obsahu, struktury a parametrů pro vyhledávání/filtrování na e-shopu, nad dnes ručně a nekonzistentně vedenými daty.

**Běží už Listing nad reálnými daty klienta?**
Ne. Aktuálně běží nad testovacími daty v 1 pilotní kategorii. Produkční nasazení nad reálnými daty je plánováno.

**Bude Listing doporučovat kategorie produktů?**
Ne — mimo rozsah. Listing pracuje s kategoriemi, které Dr. Max sám definuje a dodá.

**Funguje Listing napříč všemi kategoriemi produktů?**
Ne, zatím jen pro 1 pilotní kategorii. Rozšíření je položka Nice to Have / Backlog.

**Co brání dokončení produkčního nasazení?**
Primárně nedodaný kategorický/parametrický systém na straně Dr. Max.

**Jak konkrétně AI generuje obsah listingu?**
Content manažer zvolí zdroj (původní listing nebo vlastní text) a spustí generování — nástroj vygeneruje strukturovaný popis a obohacené parametry vedle původního obsahu, k ručnímu schválení.

**Jak se hlídá, aby AI nevygenerovala nepovolené léčebné tvrzení?**
Per kategorie existuje konfigurovatelný blacklist zakázaných frází jako součást "Listovacích minim".

**Jak se měří kvalita/kompletnost listingu?**
Nástroj počítá per produkt číselné skóre plus rozklad konkrétních validačních problémů.

---

## Otevřené otázky

- Jaký je konečný počet/granularita kategorií, které Dr. Max požaduje? Orientačně 500–2 000+, zcela otevřené.
- Kdo je druhý byznysový vlastník Listingu vedle Petra Neumana?
- Je scraping externích zdrojů právně v pořádku, nebo bude nutné oficiální rozhraní/prostředník?
- Jakým způsobem/formátem chce Dr. Max data zpět do Magento?
- Jaká konkrétní KPI se budou u Listingu sledovat a jaké mají cílové hodnoty?
- Jaká je návratnost/kvantifikovaná byznys hodnota projektu — interní odhad 300 000 Kč není klientem potvrzen.
- Existuje rozpor mezi interním podkladem (přímá integrace s Magento jako plánovaný krok) a odhadovou poznámkou k propisu do Magento (reálná přímá integrace se pravděpodobně nestaví) — který stav platí?
- Jaký je rozsah, vlastník a výstup probíhající analýzy vylepšení listing procesu od začátku do konce?
- Existuje kompletní seznam workflow stavů produktu nad rámec pozorovaných (Import, Rozpracováno)?
- Jaká je přesná funkce tlačítka "Odvodit minima" na obrazovce kategoriálních standardů?
- Je taxonomie parametrů fixní napříč celou platformou, nebo konfigurovatelná per kategorie?
- Je blacklist zakázaných medicínských tvrzení schválen Dr. Max, nebo jde o návrh čekající na review klienta?
- Jaké je chování při souběžné úpravě stejného produktu více uživateli?
- Jaké je chování generování pro kategorii bez definovaných "Listovacích minim"?
