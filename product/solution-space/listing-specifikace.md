---
last_updated: 2026-09-11
last_updated_by: manual — conversational
type: byznysová specifikace (custom — nekopíruje šablonu /product-scope)
---

> **Poznámka k formátu**: Tento dokument vznikl na přání PM podle struktury `Logistika - 2026-06_Reklamace_Specifikace_3.5.docx`, ale na byznysové (nikoli vývojářské) úrovni — bez krok-za-krokem technických flow, systémových diagramů a rozhraní, protože ty pro Listing zatím nejsou nikde zdokumentované. Pole bez spolehlivého zdroje jsou označena `-tbd-`. Řada otevřených bodů je vázána na plánované 1:1 s Petrem Neumanem.

<br>

# Listing
## Standardizace a automatizace produktového listingu
### Specifikace — byznysový přehled

<br>

Dr. Max — AI Iniciativa

---

## Management Summary

Listing má za cíl automatizovat tvorbu a správu produktového listingu u Dr. Max — návrh obsahu, struktury a doplnění chybějících dat s minimem manuální práce nad dnes extrémně nepřehlednými daty (cca 45 000 řádků × 1 200 sloupců pokrývajících vlastnosti jako příchuť, cena, benefitové karty, viditelnost na e-shopu, SEO parametry). Základní generování obsahu, struktury a parametrů je hotové a funguje na testovacích datech; produkční nasazení nad reálnými daty klienta zatím neproběhlo.

**Aktuální stav** (dle portfolio trackeru): fáze *In Testing*, dokončenost **15 %**. Cílové datum dokončení v trackeru je zastaralé a je již po termínu — `-tbd-`, potřeba nový odhad/rozhodnutí.

Hlavní blokátor není na straně BigHub, ale na straně klienta: Dr. Max dosud nedodal fungující systém kategorií/parametrů produktů. Bez něj nelze rozšířit řešení z jedné pilotní kategorie na plný rozsah. Proto byla navržena a odsouhlasena formální Discovery fáze s klientem (viz [[ASM-011]]) — tento dokument je prvním krokem k tomu, aby Listing měl konečně jednu ucelenou specifikaci.

| Fáze | Co se dodá | Stav | Odhad realizace (BigHub) |
|------|------------|------|---------------------------|
| MVP | Vstup dat, generování obsahu, struktura/parametry, dohledání chybějících dat, kontrola listingovým týmem, propis do Magento, produkční nasazení | 6 z 8 položek hotovo, 2 zbývají (propis do Magento, produkční nasazení) | 1–2 MD (zbývající práce) |
| Full Version | Dohledání dat z externích zdrojů (scraping), tvorba popisů pro nové produkty, update systému variant | Vše blokováno nebo v backlogu — viz Otevřené body | 2,75–5,5 MD |
| Nice to Have / Backlog | Multi-kategoriální podpora (rozsah zcela otevřený, řádově 500–2 000+ kategorií) | Backlog | 3–6 MD |
| **Celkem** | | | **6,75–13,5 MD** |

> Odhady pocházejí od Filipa Černého a jsou dle standardní konvence tohoto projektu (viz `project-knowledge` — Effort estimate convention) zadány jako pesimistická hodnota s optimistickou dopočtenou na 50 %.

---

## Listing na e-commerce dnes — slabiny a dopady

> Zdroj: interní prezentace "Listing na e-commerce dnes" (dodáno PM).

**Největší slabiny aktuálního systému**:
- **Neúplné podklady** — dodavatelé neposílají kompletní informace o produktech.
- **Ruční úprava pracovníky listingu** — vylepšení dle listovacích minim / SEO parametrů, produkt po produktu.
- **Excel exporty namísto jednoho systému** — data o produktech jsou rozptýlená v několika tabulkách.
- **Copy-paste do Magenta** — ruční přenos s minimální integrací.

**Důsledky**:
- **Nekonzistentní kvalita** — manuální práce vnáší variabilitu výsledku, interpretace vstupu od dodavatelů se liší produkt od produktu.
- **Náročné zavádění nových produktů** — rychlost ručního zpracování limituje množství produktů, které lze listovat najednou.
- **Nevyužitý potenciál konverze** — kvalitnější obsah by přinesl vyšší traffic i zákaznickou konverzi (SEO / filtry).

---

## Byznys hodnota

**Kvalitativní přínos**: eliminace ruční tvorby a údržby produktového obsahu a parametrů nad extrémně velkým a nekonzistentním datasetem; standardizace procesu napříč listingovým týmem; příprava na budoucí škálování na stovky až tisíce kategorií; snížení regulatorního rizika díky vestavěnému blacklistu neregulérních léčebných tvrzení (viz demo, Krok 4) — relevantní vzhledem k tomu, že jde o lékárenský e-commerce.

**Hlavní cíl** (dle interní prezentace "Další kroky"): **Vyšší konverze** — kvalitní a jednotný listing prodává.

**Sekundární cíle**:
- Spokojenější zákazníci
- Přehlednější e-shop
- Snazší vyhledávání a filtrování
- Lepší SEO
- Zrychlení procesu listingu
- Snížení interní administrativy

> Toto jsou pojmenované kvalitativní cíle ze zdrojové prezentace, ne měřitelná KPI s konkrétní cílovou hodnotou — viz sekce KPI níže pro stav jejich kvantifikace.

**Kvantifikovaný přínos**: `-tbd- (neověřeno s klientem)`

Interní hrubý odhad v portfolio trackeru: **300 000 Kč** odhadovaný přínos (prioritizační skóre 450 000 Kč = Priorita × Přínos ÷ Effort). Tato hodnota **nebyla formálně kvantifikována ani potvrzena s klientem** — jde o pracovní číslo z plánování roadmapy, ne o byznysem podepsaný business case. Jindřich Tůma explicitně požádal o dodání konkrétních byznysových čísel per iniciativa, počínaje CC; pro Listing to zatím neproběhlo. Alana Sihelská už dříve flagovala, že prezentovaná byznys hodnota Listingu "nebyla úplně přesvědčivá" — stojí za dovyjasnění.

**Úspora času**: na rozdíl od Reklamace (kde je baseline 8 h/den u 4 zaměstnanců kvality) nemá Listing zatím žádnou zdokumentovanou baseline ruční práce ani měřenou úsporu. `-tbd-`

---

## KPI

**V portfolio trackeru není u Listingu vyplněno žádné KPI** (pole "Key KPI" je prázdné) — formálně se dnes nic nesleduje.

Zdrojová prezentace pojmenovává hlavní a sekundární cíle (viz sekce Byznys hodnota — vyšší konverze, spokojenost zákazníků, přehlednost e-shopu, SEO, rychlost listingu, nižší administrativa), ale **žádný z nich nemá přiřazenou konkrétní metriku ani cílovou hodnotu** — jde o kvalitativní směřování, ne měřitelné KPI.

Vyplnění sloupců Value + KPI ve Strategy tabu je otevřená úloha (carry-forward akční položka, PM).

> **Návrh, ne rozhodnutí**: Seznam níže je pracovní návrh sestavený při přípravě tohoto dokumentu — nevzešel od klienta ani nebyl odsouhlasen PM. Nepovažovat za závazná KPI, dokud neprojdou rozhodnutím na 1:1 s Petrem Neumanem.

Kandidátní metriky k projednání s Petrem Neumanem, navržené jako možný způsob, jak zmíněné cíle změřit — `-tbd-, potřeba rozhodnutí`:
- **Průměrné/mediánové SKÓRE napříč katalogem** a **podíl produktů nad prahovou hodnotou skóre** — nástroj toto skóre už dnes počítá per produkt (viz demo, Krok 2–3), nejpřirozenější kandidát na formální KPI, protože se nemusí nic nově měřit.
- Konverzní poměr na produktových stránkách před/po (přímo k hlavnímu cíli "vyšší konverze")
- Počet produktů se schváleným/publikovaným listingem
- Podíl produktů s automaticky doplněnými chybějícími daty (bez ručního zásahu)
- Čas od vstupu dat po schválení listingovým týmem
- Počet pokrytých kategorií vs. celkový cílový rozsah (dnes: 72 produktů v 1 pilotní kategorii, viz demo)

---

## Fázování

- **MVP** — generování obsahu, struktury a parametrů pro existující produkty; kontrola listingovým týmem; propis do Magento; produkční nasazení
- **Full Version** — externí zdroje dat (scraping), tvorba popisů pro nové produkty (ne jen úprava stávajících), update systému variant
- **Nice to Have / Backlog** — multi-kategoriální podpora nad rámec pilotní kategorie

---

## Fáze MVP — Detail

| ID | Položka | Popis | Stav |
|----|---------|-------|------|
| 1 | Vstup produktových dat | Přijmout základní dostupná data o produktu jako vstup pro vytvoření nebo doplnění listingu. | Done |
| 2 | Generování produktového obsahu | Na základě vstupních informací navrhnout obsah pro konkrétní produkt/položku. | Done |
| 3 | Struktura a parametry | Doporučit odpovídající parametry produktu potřebné pro vyhledávání a filtrování. | Done |
| 4 | Dohledání chybějících dat | Identifikovat chybějící produktová data (externí zdroje jsou až ve Full Version). | Done |
| 6 | Kontrola listingovým týmem | Umožnit pracovníkovi listingového týmu výsledek zkontrolovat a schválit před finálním použitím. | Done |
| 7 | Propis do Magento | Po schválení předat/propsat připravená produktová data do Magento bez ručního kopírování. | Backlog — viz Otevřené body |
| 8 | Produkční nasazení | Řešení nasazeno v produkčním prostředí a použitelné listingovým týmem pro reálné produkty. | Planned |
| 11 | Nasazení prototypu | — | Done |

> Položky 1, 2, 3, 4, 6, 11 jsou níže doloženy konkrétním demem nástroje (Filip Černý) — viz sekce **Jak nástroj funguje dnes**.

---

## Jak nástroj funguje dnes (demo Filipa Černého)

> Zdroj: `documents/internal/2026-09-11-ai-listing-tool-demo-walkthrough.md`, walkthrough dema AI Listing Tool, prezentoval Filip Černý.

### Přehled nástroje

Demoovaný nástroj je **Dr. Max AI Listing Tool** — interní e-commerce PIM (Product Information Management) a AI platforma pro obohacování katalogu, určená content manažerům lékárenského/zdravotnického e-commerce ke třem věcem:

1. **Audit a validace zdraví katalogu** — skórování produktových listingů proti regulatorním a kategorizačním kritériím.
2. **Automatizace tvorby obsahu** — GenAI generuje strukturované produktové popisy, meta texty a standardizované taxonomické atributy.
3. **Konfigurace kategoriálních standardů ("Listovací minima")** — granulární pravidla, pokyny pro AI prompty, znakové limity, povolené hodnoty atributů a blacklist zakázaných medicínských tvrzení.

### Krok za krokem

**Krok 1 — Výběr kategorie (úvodní obrazovka)**
Minimalistická landing page: logo Dr. Max a výběr jazyka v horní liště, titulek "AI Listing Tool" / podtitulek "Výběr kategorie", vyhledávací pole ("Hledat kategorie..."), chipy nedávných kategorií (např. "Proteiny / Doplňky stravy") a tlačítko "Procházet všechny kategorie". Uživatel zvolí kategorii kliknutím na chip.

**Krok 2 — Přehled produktů**
Dashboard s levým sidebarem (breadcrumb kategorie, sub-navigace *Listovací minima* / *Přehled produktů* / *Úprava produktu*, přepínač jazyka) a centrální tabulkou se sloupci: PRODUKT, SKU, **SKÓRE** (progress bar zdraví/kompletnosti listingu — červená = nízké, zelená = vysoké), **STAV** (workflow badge: *Import*, *Rozpracováno*) a **PROBLÉMY** (badge: červená = chyba, oranžová = upozornění, modrá = info). Stránkování v demu ukázalo **72 produktů celkem** v kategorii *Proteiny / Doplňky stravy* — konkrétní potvrzení rozsahu dnešního pilotu (v souladu s "natvrdo na 1 kategorii" z Otevřených bodů).

**Krok 3 — Detail produktu a AI generování ("Úprava produktu")**
Dvoupanelový diff editor: aktuální listing vlevo, AI návrh vpravo. Hlavička nese název/SKU, editovatelný stav workflow, **historii verzí s možností rollbacku** (např. v2.04) a CTA tlačítko **"Generovat"**. Validační karta ukazuje skóre (v demu 23) a rozklad problémů (červené = chybí povinná pole, žluté = např. krátký popis nezačíná názvem značky). Uživatel může zvolit zdroj pro AI (*Použít původní listing* / *Použít vlastní text*). Po kliknutí na "Generovat" se vpravo vyrenderuje strukturovaný text (úvod, Hlavní vlastnosti, Složení, Dávkování, Upozornění) a obohacené parametry zvýrazněné zeleně (např. *Zdroj proteinu: Vegan*, *Forma: Prášek*, *Vlastnosti: Bez lepku, BIO, Vegan*), plus meta texty (Krátký popis, Teaser popis).

**Krok 4 — Kategoriální standardy ("Listovací minima")**
Konfigurační obrazovka pravidel a promptů per kategorie, čtyři sekce:
- **Pole popisu (6 polí)** — Úvodní text, Hlavní vlastnosti, Složení, Dávkování, Upozornění, O značce; každé s POKYNY PRO AI (promptem v přirozeném jazyce), min./max. počtem znaků a příznakem POVINNÉ.
- **Meta popisy (2)** — Krátký popis (140–180 znaků), Teaser popis (60–90 znaků).
- **Parametry produktu (28 atributů)** — např. značka, věkové rozmezí, jednotka, alergeny, živiny na porci, příchuť, cílová skupina, léková forma, minerály, vitamíny, časování/užívání, EAN; každý s přepínačem *Generovat automaticky* (AI) vs. *Pouze ručně*.
- **Zakázané fráze (compliance guardrail)** — blacklist neregulérních léčebných tvrzení pro doplňky stravy, např. *léčí, hojí, terapeutický, léčivý, uzdravuje, zmírňuje příznaky*.

**Krok 5 — Návrat na Přehled produktů**
Uživatel se vrací do tabulky katalogu pro kontrolu dalších položek.

### UX/UI — designový systém

| Vrstva | Implementace |
|--------|--------------|
| Barvy a brand identita | Dr. Max zelená pro primární CTA, aktivní navigaci a validní/AI-generované položky; sémantické stavové barvy (červená = chyba/nízké skóre, oranžová = upozornění, zelená = úspěch). |
| Layout pattern | Split/Diff screen — porovnání aktuálního a AI-navrženého obsahu vedle sebe před potvrzením změny. |
| Hustota informací | Vysoká — kompaktní tabulky, tag cloudy, data pills, optimalizováno pro zpracování vysokého objemu SKU. |
| AI integrace UX | Explicitní řízení uživatelem (ruční spuštění "Generovat"), vizuální diffing generovaných atributů, transparentní atribuce zdroje, editovatelná governance pravidla (prompty + blacklist). |

> **Poznámka**: STAV v tabulce produktů (*Import*, *Rozpracováno*) je workflow stav jednotlivého produktu/SKU — nezaměňovat se stavem dodávky feature v Excelu roadmapy (*Done/Backlog/Planned/Blocked* výše). V demu byly pozorovány jen 2 hodnoty stavu; existence dalších stavů (např. *Schváleno*/publikováno) není potvrzena — `-tbd-`.

---

## Fáze Full Version — Detail

| ID | Položka | Popis | Stav | Blokace |
|----|---------|-------|------|---------|
| 5 | Dohledání v externích zdrojích | Dohledání relevantních informací v definovaných externích zdrojích (např. Notino). | Blocked | Technicky téměř hotovo, nepublikováno kvůli právní nejistotě scrapingu; při schválení bude navíc potřeba řešit proxy (Azure IP rozsahy jsou cca z 90 % blokované). |
| 9 | Tvorba popisů pro nové produkty | Přepoužít flow nejen na zlepšení již zalistovaných produktů, ale i na listování zcela nových produktů. | Backlog | Není součástí MVP (MVP řeší jen stávající produkty). |
| 12 | Update systému variant | Zlepšit kvalitu dat o produktových variantách od dodavatele. | Blocked | Systém variant je hotový, ale data o variantách od Dr. Max jsou aktuálně velmi špatná kvalita — čeká se na klienta, není to práce na straně BigHub. Jakmile se odblokuje, práce na naší straně je triviální. |

---

## Fáze Nice to Have / Backlog — Detail

| ID | Položka | Popis | Stav | Poznámka |
|----|---------|-------|------|----------|
| 13 | Multi-kategoriální podpora | Podpořit listing napříč více kategoriemi (aktuální demo je natvrdo na 1 kategorii). | Backlog | Zdaleka největší položka celého Listingu — dotýká se validace, generování, UI i databáze. Reálný rozsah cca 500–2 000+ kategorií dle granularity pravidel, kterou zvolí Dr. Max — zcela otevřené. Součástí je samostatně odhadovaný (~3 MD) vrstvený/kompozitní systém listingových standardů. |

---

## Další fáze (Next Phases / budoucí rozšíření)

**Hlavní fáze dalšího vývoje** (dle interní prezentace "Další kroky"):
- **Externí datové zdroje** — data z internetu, specializovaných stránek či dalších e-shopů. Odpovídá položce 5 (Dohledání v externích zdrojích) ve Full Version — technicky téměř hotovo, čeká na vyřešení právní otázky scrapingu.
- **Podpora listingu nových produktů** — listing i zcela nových produktů, ne jen kontrola/vylepšení stávajících. Odpovídá položce 9 ve Full Version.
- **Přímá integrace s Magentem** — bez ručních exportů a importů, po schválení se změny uloží přímo do Magenta.
- **+ aktuálně probíhající analýza** možnosti vylepšení celého procesu listingu od úplného začátku až do konce — rozsah, vlastník a výstup této analýzy nejsou jinde zdokumentované. `-tbd-, potřeba doplnit`

> ⚠️ **Rozpor k vyjasnění**: Prezentace uvádí "přímou integraci s Magentem" jako jeden z hlavních kroků dalšího vývoje. To je v napětí s poznámkou k položce 7 v Excelu roadmapy (Filip Černý), která popisuje odhad propisu do Magenta jako export/import na základě klientem zaslaného souboru a dodává, že "reálná přímá integrace je něco, co se pravděpodobně nikdy nestane a aktuálně se na tom vůbec nepracuje." Potřeba ujasnit, zda prezentace popisuje jiný/pozdější záměr, nebo zda je Excelová poznámka zastaralá.

Další, dosud jen okrajově zmíněné směry — žádný z nich není odsouhlasený rozsah, jen otevřené možnosti:

- **Plné rozšíření multi-kategoriální podpory** na cílový počet kategorií (dle rozhodnutí Dr. Max) — navržený start s malou sadou mimo léky (potraviny, doplňky stravy, sportovní potřeby), viz [[ASM-032]].
- **Doporučování kategorií/struktury** — explicitně **mimo scope** (viz [[ASM-031]]); jakýkoli budoucí požadavek se řeší jako nový feature/change request, ne jako mezera v dodávce.
- **Vendorský portál** — samostatná, ne zcela překrývající se klientská iniciativa (dodavatelé by mohli zadávat listing přímo v jednotném formátu); zatím pravděpodobně nikým nestavěná, scope se částečně kryje s validací/labelingem Listingu. `-tbd-, potřeba ujasnit vazbu na tento projekt`

---

## Otevřené body

| Bod | Popis | Vlastník |
|-----|-------|----------|
| Kategorie/parametrický systém | Hlavní blokátor celého projektu — Dr. Max dosud nedodal systém kategorií/parametrů (např. jak kategorizovat "balenou vodu"). Bez něj nelze rozšířit z 1 pilotní kategorie. | Dr. Max (Petr Neuman) |
| Způsob propisu do Magento | Nespecifikováno klientem — Excel upload, nebo přímý zápis do DB? Odhad cca 0,5 dne práce jakmile bude metoda zvolena. | Dr. Max |
| Kvalita dat o variantách | Data o produktových variantách od Dr. Max jsou špatná, blokují update systému variant. Práce na straně BigHub je hotová/triviální, čeká se na klienta. | Dr. Max |
| Právní status scrapingu (Notino apod.) | Nevyjasněno, může vyžadovat oficiální API nebo prostředníka místo scrapingu. | -tbd- (právní review) |
| Druhý byznysový vlastník Listingu | Vedle Petra Neumana existuje dle Jindřicha Tůmy ještě druhý byznysový vlastník na straně klienta — jméno stále neznámé. | Dr. Max |
| Formální kvantifikace KPI a byznys hodnoty | Sloupce Value/KPI ve Strategy tabu nejsou vyplněné; interní odhad 300 000 Kč není klientem potvrzen; kandidátní KPI seznam v tomto dokumentu je jen návrh, ne rozhodnutí — viz sekce KPI. | Marek Pillár (plánované 1:1 s Petrem Neumanem) |
| Cílový rozsah kategorií | 500–2 000+ kategorií je čistě orientační rozpětí, konečné číslo zcela otevřené, závisí na Dr. Max. | Dr. Max |
| Rozpor: přímá integrace s Magentem | Interní prezentace ji uvádí jako plánovaný další krok; poznámka v roadmap Excelu (Filip Černý) říká, že reálná přímá integrace se pravděpodobně nikdy nepostaví. Potřeba sjednotit. | Marek Pillár |
| Probíhající end-to-end analýza listing procesu | Zmíněna v prezentaci ("+ aktuálně probíhající analýza možnosti vylepšení celého procesu listingu od úplného začátku až do konce"), rozsah/vlastník/výstup nejinde nezdokumentovány. | -tbd- |

---

## FAQ

**Co Listing řeší?**
Automatizaci tvorby a doplňování produktového obsahu, struktury a parametrů pro potřeby vyhledávání/filtrování na e-shopu, nad dnes ručně a nekonzistentně vedenými daty.

**Běží už Listing nad reálnými daty klienta?**
Ne. Aktuálně běží nad testovacími daty zvolenými klientským týmem. Import/export reálných dat řeší dočasně pravidelný (týdenní, ~10 min) proces přes Magento; produkční nasazení nad reálnými daty je ve stavu Planned, ještě nedokončené.

**Bude Listing doporučovat kategorie produktů?**
Ne — to je explicitně mimo scope (viz [[ASM-031]]). Listing pracuje s kategoriemi, které Dr. Max sám definuje a dodá.

**Funguje Listing napříč všemi kategoriemi produktů?**
Ne, zatím jen pro 1 pilotní kategorii natvrdo. Rozšíření na více kategorií je položka Nice to Have / Backlog, čeká na rozhodnutí Dr. Max o rozsahu a granularitě.

**Co brání dokončení produkčního nasazení?**
Primárně nedodaný kategorický/parametrický systém na straně Dr. Max — viz Otevřené body.

**Jaká je návratnost/byznys hodnota projektu?**
Zatím formálně nekvantifikováno a klientem nepotvrzeno — viz sekce Byznys hodnota a KPI.

**Jak konkrétně AI generuje obsah listingu?**
Content manažer otevře produkt, zvolí zdroj (původní listing nebo vlastní text) a klikne na "Generovat" — nástroj vygeneruje strukturovaný popis (úvod, hlavní vlastnosti, složení, dávkování, upozornění) a obohacené parametry vedle původního obsahu, k ručnímu schválení. Viz demo, Krok 3.

**Jak se hlídá, aby AI nevygenerovala nepovolené léčebné tvrzení?**
Per kategorie existuje konfigurovatelný blacklist zakázaných frází (např. "léčí", "terapeutický", "uzdravuje") jako součást "Listovacích minim" — viz demo, Krok 4.

**Jak se měří kvalita/kompletnost listingu?**
Nástroj počítá per produkt číselné SKÓRE (zobrazené i jako progress bar v tabulce produktů) plus rozklad konkrétních validačních problémů. Toto skóre je zatím jediný objektivně měřený ukazatel kvality, který v nástroji existuje — viz sekce KPI.

---

## Q&A — otázky vznesené na schůzkách

| # | Otázka | Odpověď | Stav | Zdroj |
|---|--------|---------|------|-------|
| 1 | Zredukuje klient kategorický požadavek na ~10 klíčových kategorií, nebo zůstane u granulárnějšího výčtu? | Částečně: dohodnut fázovaný start s malou nefarmaceutickou sadou (potraviny, doplňky, sportovní potřeby), ale konečný počet/granularita zůstává zcela otevřená. | Částečně zodpovězeno | 2026-09-01-dr-max-listing-introduction, 2026-09-07-ai-portfolio-roadmap-scope-review |
| 2 | Je doporučování kategorií/struktury v rozsahu dodávky? | Ne — potvrzeno mimo scope, jakýkoli budoucí požadavek je nový feature request. | Zodpovězeno | 2026-09-07-ai-portfolio-roadmap-scope-review, [[ASM-031]] |
| 3 | Existuje už někde kompletní spec Listingu od začátku do konce? | Ne, žádná neexistovala — tento dokument je první pokus takovou specifikaci sepsat. | Zodpovězeno (řešeno tímto dokumentem) | 2026-09-01-dr-max-listing-introduction |
| 4 | Kdo je druhý byznysový vlastník Listingu vedle Petra Neumana? | Neznámo — jméno se dosud nepodařilo zjistit. | Nezodpovězeno | 2026-09-02-roadmap-tracking-and-listing-onboarding-sync |
| 5 | Jaký je reálný cílový rozsah multi-kategoriální podpory (počet kategorií)? | Zcela otevřené, orientačně 500–2 000+, závisí na rozhodnutí Dr. Max. | Nezodpovězeno | 2026-09-07-ai-portfolio-roadmap-scope-review |
| 6 | Je scraping externích zdrojů (např. Notino) právně v pořádku? | Ne, nejasné — potřeba právní review, možná bude nutné oficiální API/prostředník. | Nezodpovězeno | 2026-09-07-ai-portfolio-roadmap-scope-review, [[ASM-033]] |
| 7 | Jakým způsobem/formátem chce Dr. Max data zpět do Magento? | Nespecifikováno. | Nezodpovězeno | 2026-09-07-ai-portfolio-roadmap-scope-review |
| 8 | Je prezentovaná byznys hodnota Listingu dostatečně přesvědčivá/podložená? | Ne dle Alany Sihelské — stálo by za dovyjasnění a přepočet. | Nezodpovězeno | 2026-09-02-logistics-listing-team-sync |
| 9 | Jaké konkrétní KPI se budou u Listingu sledovat? | Žádné zatím formálně nejsou definované. | Nezodpovězeno | Portfolio tracker (Key KPI prázdné), carry-forward akční položka |

---

**Zdroje**: 2026-09-01-dr-max-listing-introduction, 2026-09-02-logistics-listing-team-sync, 2026-09-02-roadmap-tracking-and-listing-onboarding-sync, 2026-09-07-ai-portfolio-roadmap-scope-review, `project-management/project-assumptions.md` (ASM-011, ASM-031, ASM-032, ASM-033), `product-roadmap-portfolio-full.xlsx` (listy Portfolio, Listing), interní prezentace "Listing na e-commerce dnes" / "Další kroky" (dodáno PM), `documents/internal/2026-09-11-ai-listing-tool-demo-walkthrough.md` (demo AI Listing Tool — Filip Černý).
