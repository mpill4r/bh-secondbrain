---
last_updated: 2026-09-24
last_updated_by: manual — conversational
type: internal
---

# TEO/OCR: Excel výstup a AI framing — odporúčania pre Radima

**One-pager pre Alanu.** Zhrnutie problému, analýza možností a konkrétne, priamo použiteľné odporúčania pre komunikáciu s Radimom Švarcom.

## Účel tohto dokumentu

Dve nezávislé pripomienky (Alana k formátu výstupu, Marek k chýbajúcej AI asistencii v review kroku) plus opakujúci sa vzorec u Dudaška (odmieta čokoľvek, čo pôsobí ako "digitalizácia"/"dátový projekt" namiesto "AI") ukazujú na jeden a ten istý problém pri TEO/OCR: **Radimov výstup je dnes čistý Excel bez akéhokoľvek viditeľného AI odtlačku.** Tento dokument problém rozoberá do hĺbky a končí konkrétnym zoznamom krokov, ktoré môžeme dať Radimovi.

## 1. Kontext a problém

### 1.1 Súčasný stav (potvrdené 2026-09-22/23)

Radim postavil funkčný end-to-end proces na strane Dr. Max:

1. **Intake**: nová schránka `automat.revize@drmax.cz` + priečinok `914 Technicke/revize/automat/nové` — Power Automate (PA) číta PDF/PNG prílohy.
2. **Odoslanie do BigHub**: dvakrát týždenne PA flow posiela dokumenty do BigHub Blob storage.
3. **Sledovanie výstupu**: denný lokálny PA Desktop + Python skript na Radimovom stroji kontroluje nové spracované batch-e (cez lokálny CSV), z každého vytvorí **nový Excel** (`{batchID}_processed_at.xlsx`), PDF súbory premenuje a presunie do priečinka „čaká".
4. **Manuálna kontrola**: Míša ručne kontroluje a opravuje riadky v Exceli (rovnaká štruktúra, akú posiela Jura, s odkazom na konkrétnu stranu PDF) → presun do priečinka „hotovo".
5. **Príprava na SNOW**: presun do „hotovo" spustí ďalší PA flow, ktorý Excel oseká na potrebné stĺpce a vytvorí importnú kópiu; PDF sa archivujú.
6. **SNOW import**: zatiaľ ručne cez formulár; automatický import je zvažovaná, nie postavená možnosť.

Tento proces je zámerne postavený na Exceli namiesto webového rozhrania s „vybranými zaujímavými stĺpcami" pre Míšu — toto bolo explicitne rozhodnuté 2026-09-22, primárne z dôvodu rýchlosti dodania, nie preto, že by Excel bol koncepčne lepšia voľba.

### 1.2 Dve nezávislé pripomienky proti tomuto dizajnu

- **Alana**: nechce, aby výstup na strane Radima/klienta bol Excel.
- **Marek** (zachytené ako ASM-130, 2026-09-23): celý review krok je **100 % manuálna Exceľová práca bez AI asistencie** — a to napriek tomu, že samotná extrakcia (dual GPT-5/GPT-5-mini, Document Intelligence pre checkboxy) je plne AI-driven. Nesúlad medzi tým, čo BigHub reálne dodáva (AI pipeline), a tým, čo Radim reálne vidí (surová tabuľka).

### 1.3 Paralela s Reklamáciami — prečo na tomto vzorci záleží

Presne rovnaký vzorec sa už raz prejavil na Reklamáciách (viď ASM-122, 2026-09-22/23):

- Keď sa Reklamácie postupne ukázali byť skôr digitalizačným/konsolidačným projektom (jeden zdroj dát v Axapte namiesto Excelu, „knowledge base" napokon iba jeden parameter) než pôvodne predpokladanou AI predikciou, Dudaško na to **zareagoval negatívne** a začali kolovať informácie, že „BigHub niečo nechce dodať".
- Vyžiadalo si to priame kalibračné stretnutie s klientskou stranou a napokon manažérske rozhodovanie o ďalšom postupe (Dudaško, Žůrek, Spilka, Žižka).
- Ponaučenie: **Dudaško má nízku toleranciu na čokoľvek, čo navonok pôsobí ako „dátový"/„digitalizačný" projekt namiesto „AI" projektu — aj keď je reálna hodnota identická alebo vyššia.**

TEO/OCR nesie presne to isté riziko. Extrakcia je AI. Výstup, ktorý Radim (a nepriamo aj Dudaško) reálne vidí, je Excel — čo je vizuálne a konceptuálne to najviac „dátovo" pôsobiace rozhranie, aké existuje. Ak sa to dostane pred Dudaška v súčasnej podobe, hrozí rovnaká reakcia ako pri Reklamáciách — len s oneskorením, kým si to niekto všimne.

## 2. Prečo je toto skutočný problém, nie len estetika

- Extrakčná vrstva **je AI** (91 % presnosť na rukou písanom texte, 94 % na štruktúrovanom obsahu, dual-model architektúra — viď production spec v1.1). Problém nie je v substancii, ale v tom, že to navonok nie je vidno.
- Radim už investoval reálnu prácu do automatizácie okolo Excelu (mailbox, PA flow 2×/týždeň, lokálny sledovací skript, priečinkový workflow nové→čaká→hotovo→archív). **Táto infraštruktúra sa nemusí a nemala by zahadzovať.**
- Skutočný problém teda leží vo **vizuálnej/komunikačnej vrstve výstupu**, nie v backendovej architektúre. To výrazne zužuje, čo je reálne potrebné zmeniť.

## 3. Analýza možností

### Možnosť 1 — Viditeľné AI signály priamo v existujúcom Exceli
**Náročnosť: nízka**

- Pridať stĺpec/farebné zvýraznenie „AI istota" na úrovni poľa (napr. zelená = auto-potvrdené, žltá = odporúčaná kontrola, červená = povinná kontrola).
- Na začiatok každého batch exportu pridať súhrnný riadok alebo sprievodný e-mail: „AI spracovala X protokolov, Y označených na kontrolu, Z % presnosť poľa."
- Tieto dáta BigHub **už interne počíta** (accuracy tabuľky, „silent error" rate z production spec v1.1) — ide o prezentačnú zmenu, nie o nový vývoj.

Rieši: čiastočne Marekov koncern (Excel zostáva, ale teraz nesie viditeľné AI stopy); čiastočne aj Dudaškov framing problém (ak sa naň niekedy pozrie, jednoznačne to vyzerá AI-driven).
Nerieši: ak je Alanin odpor namierený proti formátu Excel ako takému (nielen proti chýbajúcim AI signálom), toto samo osebe nebude stačiť — pozri otvorenú otázku nižšie.

### Možnosť 2 — Samostatná (standalone) review appka nad rovnakými dátami
**Náročnosť: stredná**

- Rovnaké dáta, ale namiesto surového Excelu vlastná, samostatná webová appka na review — rámcuje to ako „AI Review Queue" namiesto tabuľky, s vlastným UI pre Míšu.
- **Toto je presne ten istý vzorec, akým doteraz vznikol každý produkt na tomto účte** — MaxBuddy, Chatbot Max aj Lexie všetky vznikli ako samostatné (standalone) appky mimo platformy a až následne sa (resp. práve teraz sa) migrujú pod spoločnú AI platformu (viď 2026-09-23-ai-platform-prototype-walkthrough — Jura práve migruje MaxBuddy a Chatbot Max priamo pod platformu). Nejde teda o odbočku od zabehnutého postupu, ale o jeho pokračovanie.
- Postavené štandalone teraz neznamená zahodenú prácu neskôr — presne rovnaká appka sa neskôr napojí na platformu ako jeden z jej modulov (Možnosť 3), rovnako ako sa to deje s MaxBuddym a Chatbot Maxom práve teraz.

Rieši: priamo aj Alanin, aj Marekov koncern; silnejší dojem „AI produktu" pre Dudaška už teraz, nie až keď dozreje platforma.
Nerieši ihneď: vyžaduje si vlastný vývoj (viac než Možnosť 1), ale investícia sa neskôr priamo zúročí pri integrácii do platformy — nejde o duplicitnú prácu, ale o prvý krok tej istej cesty.

### Možnosť 3 — TEO/OCR ako vlastný modul na AI platforme
**Náročnosť: vyššia, ale je to prirodzené finále, nie alternatíva k Možnosti 2**

- Jura práve stavia AI platformu presne na manifest-based, modulárnom princípe pre tento účel — každý projekt (Lexie, MaxBuddy, Chatbot Max...) dostáva vlastný reporting/dokumentáciu/technický stav ako samostatný modul (viď 2026-09-23-ai-platform-prototype-walkthrough).
- TEO/OCR by mohol dostať rovnaké miesto. Dudaško by AI charakter projektu videl **zakaždým, keď otvorí platformu** — nielen náhodou, keď sa pozrie na Radimov Excel.
- Priamo nadväzuje na už rozhodnutú separáciu „platforma" vs. jednotlivé projekty (ASM-144) a na to, že design/vizuálna vrstva platformy sa zámerne rieši až po overení navigácie s Dudaškom (ASM-147).
- Toto je krok, ktorý príde **po** Možnosti 2, nie namiesto nej — presne tak, ako sa dnes deje s MaxBuddym a Chatbot Maxom: appka existuje samostatne, a keď je platforma pripravená (DB prístup, bezpečnostná medzera ASM-145 vyriešená), appka sa pod ňu napojí ako modul.

Rieši: dlhodobo najsilnejšie rieši framing problém, konzistentne s celkovou platform-first stratégiou.
Nerieši ihneď: časovo najnáročnejšie ako samostatný prvý krok; preto dáva zmysel ako druhá fáza nadväzujúca na Možnosť 2, nie ako náhrada za ňu.

## 4. Odporúčanie

Postup zodpovedá vzorcu, akým doteraz vznikol každý produkt na tomto účte: **samostatná appka teraz → integrácia do AI platformy neskôr.**

| Horizont | Odporúčanie |
|---|---|
| **Teraz, nízke náklady, okamžitý efekt** | Možnosť 1 — okamžite komunikovať Radimovi požiadavku na confidence/flagging vrstvu priamo v Exceli, kým appka (nižšie) nie je hotová |
| **Teraz/strednodobo — hlavný smer** | Možnosť 2 — postaviť samostatnú review appku pre TEO/OCR, rovnakým spôsobom ako vznikli MaxBuddy, Chatbot Max a Lexie |
| **Dlhodobo — prirodzené finále** | Možnosť 3 — keď AI platforma dozreje (DB prístup, bezpečnostná medzera ASM-145), napojiť appku z Možnosti 2 ako plnohodnotný modul platformy |

## 5. Konkrétne odporúčania pre Radima

1. **Do exportovaného Excelu pridať stĺpec/farebné označenie „AI istota"** (zelená/žltá/červená podľa istoty poľa) ako okamžitú preklenovaciu úpravu, kým nie je hotová appka — dáta z internej accuracy logiky (production spec v1.1) sa dajú namapovať priamo, bez nového modelovania.
2. **Na začiatok každého batch exportu pridať krátky súhrnný riadok alebo sprievodný e-mail** s číslami (spracovaných X, označených na kontrolu Y, presnosť Z %) — platí rovnako pre Excel aj pre budúcu appku.
3. **Postaviť samostatnú review appku pre TEO/OCR** (Možnosť 2) — Míša v nej robí presne to, čo dnes v Exceli (kontrola/oprava riadkov, odkaz na konkrétnu stranu PDF), len vo vlastnom rozhraní namiesto tabuľky. Zachovať existujúcu backend automatizáciu bezo zmeny (mailbox, PA flow, priečinkový workflow nové→čaká→hotovo→archív) — appka nahrádza iba prezentačnú/review vrstvu, nie backend.
4. **Plánovať appku od začiatku s výhľadom na napojenie na AI platformu** (Možnosť 3) — rovnaká štruktúra ako Jura práve používa pri migrácii MaxBuddyho a Chatbot Maxu, aby integrácia neskôr nebola prerábka od nuly.
5. **Pri akejkoľvek budúcej prezentácii TEO/OCR Dudaškovi** (status, AI platform demo) explicitne rámcovať komunikáciu okolo AI metrík (presnosť, review rate, silent error rate) a okolo appky ako AI produktu, nie okolo „Excel tabuľky" — rovnaké ponaučenie, aké sme sa naučili pri Reklamáciách (ASM-122).

## 6. Otvorené otázky

- **Kapacita a vlastníctvo vývoja appky (Možnosť 2)**: postaví ju Radimova strana (ako doteraz stavia svoju automatizáciu), BigHub, alebo spoločne? Toto priamo určuje harmonogram a treba to vyjasniť predtým, než sa appka formálne zaradí do backlogu.
- **Časový rámec Možnosti 3** závisí od vyriešenia DB prístupu na strane Jury (aktuálne blokované) a bezpečnostnej medzery v MCP registrácii (ASM-145) — bez jasného ETA je ťažké dať Dudaškovi konkrétny dátum, kedy appka dostane svoje miesto na platforme.

## Zdroje

- `meetings/external/2026-09-22-teo-ocr-technical-sync-spedos-disambiguation-reversal.md`
- `meetings/internal/2026-09-23-ai-platform-prototype-walkthrough-navigation-modular-reporting.md`
- `documents/internal/2026-09-16-teo-ocr-production-spec-v1-1.md` (accuracy dáta, silent error rate)
- [[ASM-122]] (Reklamácie — digitalizačný reframe, precedens pre Dudaškovu reakciu)
- [[ASM-130]] (Marekov koncern — Excel bez AI asistencie v review kroku)
- [[ASM-144]] (separácia „platforma" vs. „Lexie" ako koncept)
- [[ASM-145]] (bezpečnostná medzera v MCP registrácii — blokuje Možnosť 3)
- [[ASM-147]] (dizajn AI platformy zámerne odložený, kým sa neoverí navigácia s Dudaškom)
