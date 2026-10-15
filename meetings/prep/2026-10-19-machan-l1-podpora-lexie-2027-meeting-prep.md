---
last_updated: 2026-10-14
last_updated_by: manual — /project-meeting-prep
type: prep
meeting_date: 2026-10-19
attendees: [Petr Macháň, Marek Pillár]
---

# Príprava na stretnutie — Petr Macháň (L1 podpora): požiadavky na Lexie + iniciatívy 2027

## Prehľad stretnutia

**Ciele** (odvodené z harnessu, PM ich neupresnil, pred stretnutím ich uprav):
1. Pochopiť, ako L1 podpora **dnes používa Lexie** a čo jej chýba.
2. Pozbierať a zoradiť **požiadavky na Lexie** (bugy vs. nové funkcie vs. obsah/zdroje).
3. Pozbierať prípadné ďalšie **AI iniciatívy na rok 2027** pre L1 podporu.
4. Dohodnúť ďalší krok a cestu, ktorou budú požiadavky chodiť (X-Manager cez Mertovú).

**Typ**: externé (prvé stretnutie)
**Dátum**: pondelok 2026-10-19 (čas `-tbd-`)
**Účastníci**: Petr Macháň (STK-069, Dr. Max, vedúci prevádzky / L1 podpora), Marek Pillár

## Kontext z harnessu

- **Odkiaľ prišiel**: Jindřich Tůma ho 2026-10-14 (Teams) odporučil: L1 podpora už Lexie používa a má na ňu požiadavky. Marek ho v ten deň oslovil (požiadavky na Lexie + iniciatívy 2027) a stretnutie je na pondelok.
- **Lexie**: interný asistent Dr. Max nad dokumentmi/SharePointom. Vlastníci: Simona Mertová (produkt/prevádzka, STK-017), Tomáš Dudaško (IT/rozpočet, STK-010). Beží na zdieľanej AI platforme BigHubu (Jura Brázdil, Viliam Gago).
- **Ako chodia požiadavky**: všetky požiadavky na Max/Lexie/Maxie idú cez X-Manager a jediný kontakt je Simona Mertová ([[ASM-018]]). Požiadavky od L1 teda treba poslať touto cestou, nie priamo do vývoja.
- **Oprávnenia**: dnes prístupy riadia Entra ID skupiny Dr. Max (Lexie má 22 skupín). Na testovanie sa používajú 4 samostatné účty oddelení bez 2FA ([[ASM-063]]). **Novinka 2026-10-14**: Dudaško schválil správu používateľov priamo v platforme (3 Entra skupiny: Users/Admins/SuperAdmins, admin oddelenia si sám pridáva ľudí a prístupy, audit logy, testovací používatelia). Ak L1 potrebuje pridávať ľudí alebo testovacie účty, pôjde to cez platformu, keď ju Jura dorobí.
- **Dizajn**: Mertová už skôr povedala, že Lexie vyzerá menej uhladene ako Max. O dizajne rozhoduje úroveň AI platformy (Dudaško), nie samotná aplikácia.
- **Nejasné**: či L1 podpora patrí do jedného zo 4 CC pododdelení Lexie, alebo je to samostatný tím (`-tbd-`, over na stretnutí).
- **Iniciatívy 2027**: termín pre oddelenia koniec októbra (v e-mailoch 23. 10.), celý backlog koniec novembra. Tracker: `OneDrive/2. Business Quantification/2027/AI_Initiatives_Backlog_2027.xlsx`.
- **Formát BQ**: problém, kto to robí dnes, objem/frekvencia, čas na jednotku, očakávaný prínos, KPI a **spôsob merania**.

## Navrhovaný program (~30 min)

1. Krátke predstavenie, čo L1 podpora robí (tímy, kanály, objemy) (5 min)
2. Ako dnes používajú Lexie: na čo, kto, ako často, čo funguje (10 min)
3. Požiadavky: čo chýba alebo nefunguje, priorita každej položky (10 min)
4. Ďalšie nápady na 2027 a ďalší krok (5 min)

## Otázky, ktoré treba zodpovedať

- Čo presne L1 rieši (zákazníci, lekárne, interní používatelia)? Koľko ľudí, koľko tiketov alebo hovorov denne?
- Odkedy a koľko ľudí používa Lexie? Na aké typy otázok?
- Odpovedá Lexie správne? Kde sa mýli alebo nevie odpovedať? Chýbajú jej nejaké dokumenty alebo zdroje?
- Konkrétne požiadavky: je to bug, nová funkcia, alebo chýbajúci obsah? Čo je pre neho číslo 1?
- Má L1 vlastný účet/skupinu v Lexie, alebo zdieľa CC prístup?
- Sú zapojení do Mertovej X-Manager procesu? Kto za L1 zadáva požiadavky?
- Iné opakované, manuálne úlohy (triedenie tiketov, šablóny odpovedí, prepisovanie), ktoré by sa dali automatizovať v 2027? Ako by sa meral prínos?

## Talking points a na čo si dať pozor

- Neprisľubovať termín: kapacitu BigHubu treba najprv overiť s Jindřichom ([[ASM-190]]).
- Požiadavky na Lexie smerovať cez Mertovú a X-Manager ([[ASM-018]]). Daj mu vedieť, že ich tam zapíšeš alebo pošleš jej.
- Rozlišuj **úpravy Lexie** (bežný backlog) a **nové iniciatívy 2027** (tracker + BQ formát). Pri automatizácii mimo Lexie nie je isté, či ju pokryje AI rozpočet ([[ASM-233]]).
- Výstup k iniciatívam zapíš rovno do formátu trackeru 2027 (prínos + KPI + spôsob merania).
