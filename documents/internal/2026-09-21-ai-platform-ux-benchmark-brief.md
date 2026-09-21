---
last_updated: 2026-09-21
last_updated_by: manual — conversational
type: internal
---

# AI platforma — UX/UI benchmark brief (Glean, Databricks Genie One/Databricks One)

## Účel tohoto dokumentu

Doplňkový podklad k `2026-09-21-ai-platform-design-brief-jura-brazdil.md` (Fáze 1 zadání pro Juru). Tento dokument shrnuje, jak tři existující produkty nejblíže odpovídající Dudaškově vizi (Glean, Databricks Genie One / Databricks One) skutečně řeší UX/UI, a převádí to na konkrétní doporučení pro Dr.Max AI Platform. Zdrojem jsou přímo scrapnuté marketingové/produktové stránky (ne jen popisy z paměti) — konkrétní UI vzory jsou vidět na reálných screenshotech těchto produktů.

Čtvrtý zdroj (Cloudera, "The Great AI Re-Architecture") je gated research report bez viditelného UI — nepřidává vizuální vzory, ale potvrzuje strategický kontext: enterprise firmy napříč obory pod tlakem řeší přesně to, co Dudaško pojmenoval — bilancování AI nákladů/governance s reálným byznys dopadem, tlak na hybridní/škálovatelné datové základy pro AI. Používáme ho jen jako podpůrné zdůvodnění pro Fázi 2 (FinOps/governance), ne jako zdroj UI vzorů.

---

## 1. Glean — co jsme zjistili

**Zdroj:** glean.com (homepage), glean.com/ai-assistant

### Domovská obrazovka / vstupní bod
Jeden centrální vyhledávací/promptovací řádek s ikonou "+" (přiložit), přepínačem filtru a mikrofonem, a pod ním řádkem **štítků připojených zdrojů** (Slack, Google Drive, Jira, Confluence, SharePoint, GitHub, Salesforce...). Uživatel vidí už na domovské obrazovce, *odkud* AI čerpá, dřív než cokoliv napíše — transparentnost zdrojů je vestavěná do samotného vstupního pole, ne schovaná v nastavení.

### Asistent jako "jeden AI kolega," ne přepínání nástrojů
Glean Assistant je explicitně "one AI coworker for all your work" — jedno rozhraní, které:
- **proaktivně navrhuje**, co potřebuje pozornost, dřív než se uživatel zeptá ("Proactively find what you need")
- umožňuje **týmovou spolupráci v jednom chatu** (multiplayer beta) — kolegové se @zmiňují navzájem i @Glean ve stejném vlákně, staví na sdíleném kontextu
- **deleguje práci napříč systémy** specializovaným "AI kolegům" (agentům), ne že by uživatel musel sám přepínat mezi nástroji

### Transparentní proces odpovědi
Sekce "How Glean Assistant works" popisuje viditelný 5krokový proces: **Find → Plan → Research → Iterate → Deliver**. Uživatel vidí, že asistent hledá napříč nástroji, plánuje, dohledává chybějící kontext, iteruje a až pak dodá výsledek — místo černé skříňky.

### Přístup/governance
"275+ app connectors for personalized and permissions-enforced enterprise search" — každá odpověď respektuje existující oprávnění ze zdrojového systému (ne jen viditelnost celé obrazovky/dlaždice, ale i jednotlivých výsledků/citací uvnitř odpovědi).

### Struktura platformy (z patičky)
Glean rozděluje "Enterprise AI Platform" na vrstvy, které se velmi podobají BigHub fázování:
- **Assistant** (Proactive Intelligence / Data Analysis / Content Creation / Work Execution)
- **Agents** (Agent Builder / Orchestration / Governance / Library / Harness)
- **Enterprise Context** (Enterprise Search / Personal Graph / Enterprise Graph / System of Context)
- **Connectors & Actions / APIs / Model Hub / AI Gateway** — governance a FinOps vrstva je u Glean také oddělená od asistenta, stejně jako u Databricks (viz níže) a stejně jako v BigHub fázování (Fáze 1 UX vs. Fáze 2 backend/token FinOps).

---

## 2. Databricks Genie One / Databricks One — co jsme zjistili

**Zdroj:** databricks.com/product/genie/one

### "Unified Home" — pojmenovaná featurka, přesně Dudaškovo zadání
Databricks to doslova pojmenovává **"Unified Home"**: *"One central place for business users to talk with their knowledge and data, get governed answers, and take action, complete with company branding."* — to je téměř verbatim Dudaškova formulace z dnešního callu.

Vizuál té obrazovky je záměrně **minimalistický, ne hustá dlaždicová mřížka**:
- velký pozdrav uprostřed: "How can I help you?"
- jeden vstupní řádek s přepínačem režimu **Search / Ask** + tlačítko "+"
- pod ním řádek **návrhových akčních štítků**: "Draft a document", "Create a skill", "Schedule a task", "Analyze my data" — konkrétní, akční, ne obecné kategorie

Toto je zásadně jiný vzor než hustá mřížka ikon, kterou má současný BigHub prototyp (28 dlaždic na superadmin obrazovce) — Databricks vsadil na **jeden fokusní bod + kontextové akce**, ne na katalog všeho najednou.

### Persona-based framing
Stránka má přepínač **"Select Experience: Business Teams / IT Teams"** hned nahoře — při přepnutí se mění nadpis i rámování ("AI that works for you, grounded in your data" vs. "The AI coworker you can scale with confidence — unlock governed insights and agentic action"). Je to marketingový vzor, ne in-app simulace, ale validuje přesně tu myšlenku, kterou už má starší Claude Design brief (§8, Simulation mode) — různé role potřebují different framing, ne jen jiná data.

### Governance jako "Governed Insights," ne jako oddělená admin obrazovka
"Built on Unity Catalog to enforce row- and column-level security for all data, with external source permissions respected for every answer." — governance je vlastnost *každé odpovědi*, ne jen přepínač viditelnosti dlaždic na domovské obrazovce.

### "Bring Genie One Anywhere" / Genie One MCP App
Explicitně řeší přesně ten scénář, který je v BigHub review otevřenou otázkou (inline vs. deep-link): *"Bring Genie One into any business tool or application your team already uses"* — přes MCP app, ne přes iframe embed. Chat s Genie One funguje na mobilu, ve Slacku, v Teams i "any productivity tool" — nástroj jde za uživatelem do jeho existujícího prostředí, místo aby uživatel musel přijít na jednu platformu pro všechno.

### AI-Powered Discovery
"Surface AI-recommended insights to help users discover new content that's popular with colleagues and similar users" — stejný princip proaktivního navrhování jako u Glean, tady rámovaný jako "objevování", ne "asistence."

---

## 3. Aplikace na Dr.Max AI Platform — konkrétní doporučení

### 3.1 Nahradit hustou dlaždicovou mřížku "Unified Home" vzorem
Současný multi-role hub (obrazovka 4 z review) i superadmin katalog (28 plochých šedých dlaždic) jsou přesně ten anti-vzor, který Databricks/Glean cíleně nedělají jako *první* věc, kterou uživatel vidí. Doporučení:
- Domovská obrazovka = **pozdrav + jeden vstupní řádek (Search/Ask) + řádek konkrétních akčních štítků** relevantních k roli uživatele (např. pro Logistiku: "Zkontrolovat reklamaci", "Spočítat fakturaci dopravce"; pro IT: "Zkontrolovat technický stav OCR")
- Plný katalog všech nástrojů (dnešní dlaždicová mřížka) zůstává jako **druhá obrazovka** ("AI aplikace" — to je ostatně přesně to, co už specifikuje starší Claude Design brief §3, jen to současný Jurův prototyp zatím nerozlišuje)

### 3.2 Ukázat, odkud odpověď/nástroj čerpá — transparentnost zdrojů
Glean dělá viditelnost zdrojů (Slack/Jira/SharePoint...) součástí samotného vstupního pole. Pro Dr.Max: každá odpověď z Lexie nebo z libovolného agenta by měla ukazovat **odkud čerpá** (interní metodika X, dokument Y) — netýká se to jen FinOps nákladové viditelnosti (Fáze 2), ale i důvěryhodnosti odpovědi už ve Fázi 1.

### 3.3 Proaktivní návrhy místo čistě reaktivního čekání na dotaz
Obě reference (Glean "Proactively find what you need", Databricks "AI-Powered Discovery") staví na tom, že platforma **sama navrhne** relevantní další krok, ne že čeká na dotaz. Pro Dr.Max: domovská obrazovka může ukázat 1-2 kontextové návrhy podle role (např. CC agentovi: "3 nové eskalace čekají na odpověď") — to je i silnější "vizuálně probíhající sjednocení" signál pro Dudaška než statická dlaždicová mřížka.

### 3.4 Granularita governance — na úrovni odpovědi, ne jen obrazovky
Databricks: "row- and column-level security... respected for every answer." Aktuální BigHub prototyp filtruje viditelnost jen na úrovni celých dlaždic/záložek (a dělá to nekonzistentně — viz review nález, kde MaxBuddy ukázal Technický stav všem rolím bez rozdílu). Doporučení: definovat governance model jako "co smí tato role vidět **v obsahu** odpovědi", ne jen "které dlaždice smí kliknout" — jinak model neobstojí ani při současném rozsahu (natožpak při růstu na 9+ produktů).

### 3.5 Inline embedding — jde to i bez rekurzivního iframe
Databricks řeší "bring it anywhere" přes MCP integraci (nástroj se vloží do cizího prostředí), ne přes vnořené iframy uvnitř vlastního shellu. Konkrétně k dnešnímu kritickému nálezu (MaxBuddy rekurzivní vnořování): stojí za zvážení, jestli "inline" nutně znamená "iframe uvnitř iframe uvnitř shellu", nebo jestli existuje čistší technický vzor (např. jeden centrální router, ne vnořené instance celého shellu) — to je otázka na Juru, ne na tento brief, ale referenční vzor stojí za zmínku.

### 3.6 Perzona-based framing i pro copy, ne jen pro obsah
Databricks mění i *nadpis a rámování* podle zvolené persony, ne jen data. Pro Dr.Max Simulation mode (starší Claude Design brief §8): stojí za úvahu, jestli i uvítací text/pozdrav na Domů má znít jinak pro CC agenta ("Rychlé odpovědi pro zákazníky") vs. pro logistiku ("Přehled reklamací a faktur") — ne jen filtrovaný stejný layout.

---

## 4. Co tyto produkty NEdělají (a proč to není náhoda)

Ani Glean, ani Databricks nekombinují "hub + gateway + jeden asistent" do jednoho monolitického kusu — viz předchozí výzkum v této konverzaci (Databricks One vs. Unity AI Gateway jsou oddělené produkty). Benchmark to jen potvrzuje podrobněji: **domovská obrazovka je vždy odlehčená (search + akce), governance/FinOps vrstva je vždy oddělená a neviditelná běžnému uživateli.** To je přímá podpora pro to, aby Fáze 1 zůstala u lehké, search-first domovské obrazovky a Fáze 2 (token/FinOps) zůstala neviditelná admin/technická vrstva — přesně jak už BigHub fázování počítá.
