---
last_updated: 2026-09-21
last_updated_by: manual — conversational
type: internal
---

# AI platforma — kompletní sitemap prototypu (screenshoty)

Účel: úplný obrazový inventář všech obrazovek/rout v `aiplatform-shell.brazdil94.workers.dev`, jako podklad pro navazující UX práci. Screenshoty jsou beze zásahu (žádné anotace) — čistý stav prototypu ke dni 2026-09-21. Struktura složek kopíruje uživatelskou cestu: role → přihlášení → obrazovka.

## Jak se prototypem prochází (mechanika)

1. **`/login`** — výběr role/skupiny ze seznamu (simulace přihlášení, žádné skutečné heslo).
2. Klik na roli → krátká **debug stopa** (Entra token / checkMemberGroups / manifest) → automatický redirect na cílovou plochu.
3. Cílová plocha se odvíjí od **počtu ploch, které daná role/kombinace rolí vidí** (viz manifest níže):
   - **1 plocha v 1 projektu** → přímý vstup do té plochy (např. Lexie-CC → `/lexie`).
   - **Víc ploch / víc projektů** → hub/přepínač s dlaždicemi seskupenými podle produktu.
   - **0 ploch** (skupina bez přiřazeného obsahu, např. E-commerce/Listing) → prázdný stav s textem "tým zatím nedeklaroval plochy".
   - **Žádná známá skupina** → `/refused` (bez oprávnění).
4. Superadmin vidí **všech 28 ploch napříč 8 skupinami projektů** — nejrychlejší cesta k jakékoliv jednotlivé obrazovce.

## Zdrojový manifest (přesná mapa rout → role)

Tato tabulka je čtena přímo z `platform/tenants` (Nájemci a oprávnění) — je to jediný zdroj pravdy prototypu pro to, co existuje.

| Projekt | Plocha | Route | Role s přístupem |
|---|---|---|---|
| **Platforma** | Technický stav | `/platform/status` | jen superadmin |
| | Náklady | `/platform/costs` | jen superadmin |
| | Nájemci a oprávnění | `/platform/tenants` | jen superadmin |
| | Přihlášení (audit log) | `/platform/ledger` | jen superadmin |
| **Lexie** | Chat | `/lexie` | CC, IT, CC-Admin, IT-Admin |
| | Report | `/lexie/report` | Report, CC-Admin, IT-Admin |
| | Administrace | `/lexie/administration` | CC-Admin, IT-Admin |
| | Technický stav | `/lexie/status` | CC-Admin, IT-Admin |
| **MaxBuddy** | Kiosk (ukázka) | `/maxbuddy` | Ops, Argumenty |
| | Analytika příprodejů | `/maxbuddy/analytics` | Report, Ops |
| | Argumenty produktů | `/maxbuddy/arguments` | Argumenty, Ops |
| | E-mailový digest | `/maxbuddy/digest` | Ops |
| | Dokumentace | `/maxbuddy/docs` | Ops, Report, Argumenty |
| | Technický stav | `/maxbuddy/status` | Ops |
| **Chatbot Max** | Widget (ukázka) | `/chatbotmax` | CC, Ops |
| | Přehled využití | `/chatbotmax/analytics` | CC, Ops |
| | Publikace a kill switch | `/chatbotmax/publish` | Ops |
| | Dokumentace | `/chatbotmax/docs` | CC, Ops |
| | Technický stav | `/chatbotmax/status` | Ops |
| | Maxie (voicebot) | `/chatbotmax/voicebot` | Ops *(T3 — čeká na Dr.Max)* |
| **Logistika** | Reklamace | `/logistics/claims` | Sklad |
| | Fakturace doprav | `/logistics/transport` | Doprava *(T2 — auth-gate)* |
| | Dokumentace | `/logistics/docs` | Sklad, Doprava |
| | Technický stav | `/logistics/status` | jen superadmin |
| **Servisní protokoly** | Protokoly ke kontrole | `/ocr` | OCR-TechOdd |
| | Export (xlsx) | `/ocr/export` | OCR-TechOdd |
| | Nahrání dokumentů | `/ocr/upload` | OCR-TechOdd *(T3 — čeká na Dr.Max)* |
| | Export do ServiceNow | `/ocr/servicenow` | OCR-TechOdd *(T3 — čeká na Dr.Max)* |
| **E-commerce** | — žádná plocha (bez shell kontraktu) | — | CZ-AI-Ecommerce |
| **Listing** | — žádná plocha (bez shell kontraktu) | — | CZ-AI-Listing |

`T1` = plně funkční demo · `T2` = auth-gate/čeká na integraci · `T3` = čeká na Dr.Max (blokováno mimo BigHub)

## Struktura složek

```
00-role-selector/          — vstupní obrazovka výběru role + superadmin plný katalog
01-role-landings/          — cílová obrazovka PO přihlášení, pro každou ze 9 rolí/kombinací
02-platforma/              — cross-projektová admin vrstva (jen superadmin)
03-lexie/                  — Chat + Report + Administrace (7 pod-obrazovek) + Technický stav
04-maxbuddy/               — všech 6 ploch vč. Argumenty produktů (3 sub-taby)
05-chatbotmax/             — všech 6 ploch vč. otevřeného chat widgetu
06-logistika/              — Reklamace (2 sub-taby) + Fakturace doprav + Dokumentace + Technický stav
09-ocr-techodd/            — Protokoly ke kontrole + ukázka extrakce (deep-link, otevírá se v nové záložce) + zbylé 3 taby
```

`07` a `08` v číslování odpovídají E-commerce/Listing (prázdné stavy — zachyceny jen v `01-role-landings`, žádná vlastní plocha neexistuje).

## Co stojí za pozornost pro navazující UX práci

- **`03-lexie/administrace-*`** (8 screenshotů) je nejbohatší jednotlivá admin sekce v celém prototypu — obsahuje přesně ty koncepty, které starší Claude Design brief navrhoval (Skupiny uživatelů = "Oddělení", limity výdajů/kill-switch = "Limity výdajů", mapování IdM skupin). Dobrý referenční bod pro to, jak by měla vypadat Administrace i u ostatních produktů (dnes mají MaxBuddy/ChatbotMax/Logistika jen jednoduchý "Technický stav", ne plnou Administraci jako Lexie).
- **`02-platforma/najemci-a-opravneni-3-full-manifest-map.png`** je fakticky strojově čitelná sitemapa celého prototypu — nejrychlejší způsob, jak si ověřit, že žádná plocha nechybí.
- **`09-ocr-techodd/ukazka-extrakce-*`** je jediné místo v prototypu, kde "Otevřít" skutečně otevírá NOVOU ZÁLOŽKU (deep-link-out), zatímco všude jinde je chování inline — nekonzistence stojí za sladění před finalizací briefu.
- **`04-maxbuddy/kiosk-ukazka-error-state.png`** zachycuje známou chybu (`/spa neodpovídá žádné ploše v manifestu`) popsanou v předchozím UX review — zůstává nevyřešená.
