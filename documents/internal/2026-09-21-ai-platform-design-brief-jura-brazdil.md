---
last_updated: 2026-09-21
last_updated_by: auto — project-meeting routing (2026-09-21-ocr-progress-ai-platform-prototype-sync)
type: internal
---

# AI platforma — Návrhový brief pro Juru Brázdila (Fáze 1)

## Problém

Dudaško dnes přímo představil svou vizi AI platformy ve třech částech: platforma se musí chovat jako skutečná platforma (každý nástroj, který spotřebovává AI, musí procházet přes ni, aby bylo vidět využití/náklady); jedna domovská obrazovka/adresář podle rolí, který odkazuje na všechny AI nástroje, včetně těch s vlastním frontendem; a jedna sjednocená Lexie místo instancí pro každé oddělení. Dnes je platforma v podstatě jen další chatový produkt — chybí jí pevný bod (anchor) i sjednocený model přístupu.

## Co Dudaško dnes potvrdil

1. **Platforma jako služba (platform-as-a-service)**: vše, co spotřebovává AI — nejen chatová rozhraní — by mělo procházet přes platformu, aby bylo využití/náklady vidět a kontrolovatelné, časem včetně vrstvy „AI gateway" s kontrolami GDPR. Jeho stálý příklad: náklady MaxBuddy na tokeny jsou pro něj dnes neviditelné, protože vůbec neprochází přes platformu.
2. **Sjednocený adresář nástrojů podle rolí („rozcestník")**: jeden vstupní bod ke všem AI nástrojům, včetně těch s vlastním samostatným frontendem — otevírají se **inline**, v rámci jednoho rozhraní platformy, ne přes odkaz na cizí URL. Dnes, pokud nezná URL nástroje, se k němu vůbec nedostane.
3. **Jedna sjednocená Lexie, ne jedna na oddělení**: samostatné instance Lexie (IT, POS/„kasťák", chystaná instance pro Legal) jsou špatný směr — chce jeden chat, řízený podle role, s veřejnou vrstvou dokumentů pro obsah, který by měli vidět všichni bez ohledu na roli. Přístup by měl být modelován stejně, jako už dnes SharePoint řídí přístup k jeho dokumentům, ne jako nový paralelní model.
4. **Excel s maticí schopností** je odsunut na později, dokud se platforma nezačne chovat jako platforma — explicitně Fáze 3, ne blízký horizont.
5. **Nástroj pro tvorbu agentních workflow** (drag-and-drop) byl zmíněn jako dlouhodobé přání, obě strany ho odložily na budoucí konverzaci (orientačně listopad) — teď se neřeší.
6. **Dohodnuté fázování ve 3 krocích**: Fáze 1 — sjednocení UX do jednoho vstupního bodu s přístupem podle rolí a základními metrikami využití/nákladů (tento brief). Fáze 2 — hlubší backendová/tokenová FinOps integrace. Fáze 3 — Excel s maticí schopností, společně prioritizovaný. Dudaško byl jasný, že Fáze 1 je podmínkou pro zbytek, ne paralelní track.

## Směrové zadání (podle požadavku Jindřicha)

Jindřich upozornil, že zcela otevřený brief riskuje, že Jura půjde cestou nejmenšího odporu — část směrového zadání musí být v briefu přímo zakotvena, ne ponechána na jeho odhadu:

- Toto je nejprve **adresář/pevný bod, až poté chatový produkt** — úkolem domovské obrazovky je „dostat mě ke správnému nástroji", ne „být dalším chatovým oknem." Nevolit jako výchozí bod rozvržení zaměřené na chat.
- Viditelnost podle role je **základní mechanika**, ne přepínač v nastavení.
- Preferovat návrh, který viditelně působí jako „probíhající sjednocení" — Dudaško potřebuje vidět směr platformy jako centrálního uzlu, ne jen nový vzhled současného chatového UI.

## ✅ Akceptační kritéria — toto dodáváme v této fázi

Vše ostatní v tomto briefu je kontext/roadmapa. Nic mimo tento seznam není součástí tohoto dodání.

- [ ] Domovská obrazovka zobrazuje adresář všech AI nástrojů, které Dr. Max má — ne jen vlastní chatový produkt platformy.
- [ ] Nativní nástroje platformy (chatoví agenti postavení na platformě) se otevírají inline.
- [ ] Nástroje s vlastním samostatným frontendem (např. dashboard predikce objednávek pro e-commerce, nástroj pro listing/copywriting) se **také** otevírají inline, v rámci jednoho rozhraní platformy na jednom URL — ne jako odkaz ven na cizí web.
- [ ] To, co uživatel na obrazovce vidí, je filtrováno podle role — viditelnost je základní mechanika vykreslování, ne přepínač.
- [ ] Lexie je jeden sjednocený chat, ne samostatné instance podle oddělení (IT, POS/„kasťák", chystaná instance pro Legal).
- [ ] Existuje veřejná vrstva dokumentů v Lexie, viditelná všem uživatelům bez ohledu na roli.
- [ ] Zbytek obsahu v Lexie je řízený podle role uživatele.

## 🚫 Explicitně mimo rozsah Fáze 1

- Samotná backendová integrace směrování tokenů/nákladů (Fáze 2).
- Položky z Excelu s maticí schopností (Fáze 3, prioritizováno později společně).
- Nástroj pro agentní workflow/orchestraci — odloženo na budoucí konverzaci (orientačně listopad).

## Co máme dodat

Varianty UX mockupu (hrubé provedení stačí), na které může Dudaško reagovat — ideálně do **středy 23. 9. 2026**.

## Otevřené otázky k označení, ne k vyřešení

- Přesný termín prvních variant UX mockupu — závisí na Jurově kapacitě, zatím nepotvrzeno.
- Jak přesně bude vypadat inline vkládání nástrojů s vlastním frontendem v rámci jednoho rozhraní (technické detaily necháno na Jurovi).
- Jak granulární má být viditelnost podle role v této fázi oproti hrubšímu prvnímu průchodu.
