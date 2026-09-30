---
last_updated: 2026-09-30
type: prep
meeting_date: 2026-09-30
attendees: [Petr Neuman, Michaela Vdovicynová, Filip Černý, Marek Pillár]
---

# Príprava — Listing s Petrom Neumanom (30. 9., 11:00)

## Prehľad stretnutia

**Názov**: Listing — odblokovanie vývoja a štart Discovery
**Ciele**: odblokovať vývoj (reálne dáta), nakopnúť fázu Discovery, definovať „system seller“ pre každú fázu
**Typ**: client
**Dátum**: 2026-09-30
**Účastníci (predpoklad)**: Petr Neuman (business vlastník, STK-023), Michaela Vdovicynová (doménová expertka / testovanie), Filip Černý (vývoj, STK-006), Marek Pillár

## S čím by si mal odísť

1. **Odblokovaný vývoj.** Vývoj Listingu **stojí od 23. 9.**, pretože nie je jasné, či existujú **reálne produktové dáta**, alebo robíme na dummy dátach.
2. **Nakopnutie fázy Discovery** (dohodnutej 2. 9., [[ASM-011]]): Michaela ako denný kontakt ([[ASM-074]]) a termín ďalšej pracovnej session.
3. **„System seller“ pre každú fázu:** hlavná hodnota, ktorá danú fázu ospravedlňuje, plus orientačné body do budúcna. Jindřich to chce pri každej iniciatíve ([[ASM-190]]).

## Kontext za 30 sekúnd

- **Nástroj:** PIM + AI pre listing: skórovanie katalógu, generovanie popisov a parametrov, „Listovací minima“ pre každú kategóriu, blacklist medicínskych tvrdení. Pilot = **1 kategória (Proteíny), 72 produktov**. **Zápis späť do Magenta neexistuje** (potvrdené v kóde).
- **Hlavný driver pre Neumana (16. 9., [[ASM-073]]):** dostať tím (5–6 ľudí) **z každodennej práce v Magente**. Magento pri ~80–100 tis. SKU nestíha: ukladanie trvá ~30 s a potom spadne. Tím má pracovať v nástroji a do Magenta posielať dávkový import raz za ~2 týždne. Pôvodný problém so zlými dátami od dodávateľov je až druhoradý.
- **BQ (zdroj pravdy, [[ASM-123]]): ~34 mil. Kč/rok**
  - KPI 1: konverzia +0,1 p. b. → ~31 mil.
  - KPI 2: ≥ 6 000 položiek/kvartál → 8–10 tis.
  - KPI 3: náklad 130 → ~100 Kč/položku, pod 30 min na položku.
- **Trend:** Q1 ~3 600 položiek pri 230 Kč → Q2 ~6 000 pri 130 Kč. Q3 bude slabší kvôli dovolenkám a **novej EÚ regulácii environmentálnych tvrdení**: týka sa ~10 tis. produktov (~4 tis. kritických), pričom kapacita je ~1 tis. za kvartál.
- **Zmeny, ktoré nástroj robia naliehavejším:**
  - Magento ruší parametrické zoskupovanie, takže v každej kategórii sa zobrazí všetkých ~100 parametrov.
  - Šimoník presúva rozpočet z predikcie objednávok na Listing.
  - Neuman chce údajne **rozšíriť rozsah** ([[ASM-125]]: Listing je podľa hodnoty na 2. mieste).
- **Špecifikácia:** klientska verzia mu odišla ~21. 9.; **zatiaľ žiadna spätná väzba**.

## Návrh agendy (45 min)

1. **(5')** Úvod a cieľ: chceme odblokovať vývoj a dohodnúť Discovery.
2. **(10')** Dáta a Magento: otázky 1–3 nižšie.
3. **(10')** Rozsah a hodnota: jeho vízia rozšírenia, EÚ regulácia, čo prinesie každá fáza.
4. **(10')** Špecifikácia: jeho komentáre, otvorené rozhodnutia (blacklist, kategórie).
5. **(10')** Ďalšie kroky: Michaela, človek na import/export, termín.

## Otázky, ktoré treba zodpovedať (podľa priority)

1. **Reálne dáta:** Vieme dostať reálny export dát (aspoň z pilotnej kategórie)? V akom formáte, od koho a kedy? *Toto je blokátor č. 1.*
2. **Zápis do Magenta:** import súboru, alebo priamy zápis? Akú šablónu Magento potrebuje? **Kto je človek na import/export** v jeho tíme? Sľúbil ho priviesť 16. 9.; meno stále nemáme.
3. **Kritérium produkčného nasadenia** ([[ASM-067]]): tím si produkt importuje, upraví a vráti do Magenta bez copy-paste. Platí to stále?
4. **Jeho vízia rozšírenia rozsahu:** čo presne myslí (viac kategórií? nové produkty? dáta od dodávateľov?) a akú to má prioritu?
5. **EÚ environmentálne tvrdenia:** má to nástroj riešiť (hromadné úpravy popisov / blacklist)? Môže to byť najsilnejší driver hodnoty pre Q3/Q4.
6. **Ďalšie kategórie po Proteínoch:** ktoré a koľko celkovo? Špecifikácia odhaduje 500–2 000+, úplne otvorené. Odporúčame začať menšími nefarmaceutickými kategóriami ([[ASM-032]]).
7. **Blacklist:** schválil ho Dr. Max? Má ostať **varovaním**, alebo sa má zmeniť na **blokovanie** pred publikovaním ([[ASM-064]])?
8. **Scraping externých zdrojov (napr. Notino):** blokovaný pre právne posúdenie ([[ASM-033]]). Existuje oficiálny zdroj, alebo radšej súbor od dodávateľa?
9. **Head of listing / druhý business vlastník:** je táto pozícia už obsadená? Kto schvaľuje špecifikáciu?
10. **Špecifikácia:** pošle komentáre? Dokedy?

## Na čo si dať pozor

- **Nesľubuj termíny.** Filip má kapacitu na Reklamácie do 1.–2. 10., na Listing až potom. Pred akýmkoľvek záväzkom to zlaď s Jindřichom ([[ASM-190]]).
- **Neuman nemá rád vymyslené čísla** („mám pocit, že si to vymýšľam“). Pýtaj sa na jeho pohľad, netlač ho na cieľové číslo.
- **Zápis do Magenta neexistuje.** Ak predpokladá, že to funguje, povedz to otvorene: je to kľúčová časť MVP a závisí od jeho človeka na import/export.
- **Drž tempo.** Chce ísť rýchlo („včera už bolo neskoro“).

## Zdroje

2026-09-16-business-quantification-listing-petr-neuman, 2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers, 2026-09-29-management-meeting-debrief-reklamace-thursday-plan, `product/solution-space/listing-specifikace.md`, project-knowledge (AI Listing Tool), BQ tracker (new_Přehled).

**Výsledok stretnutia**: [2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy](../external/2026-09-30-listing-reset-neuman-enrichment-first-doplnky-stravy.md)
