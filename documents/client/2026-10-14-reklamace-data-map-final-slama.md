---
last_updated: 2026-10-14
last_updated_by: auto — project-document ingestion
classification: Technical
source: client
---

# Reklamace Supplier-Data Map: Final (Sources & Target Storage)

## Document Info

| Field | Value |
|-------|-------|
| Title | Reklamace dodavatelů: zdroje a cílové umístění dat ("Mapa dat – final") |
| Source | Client (logistics / Petr Sláma finalized it; BigHub-authored structure) |
| Classification | Technical |
| Language | Czech (summary in English) |
| Format | XLSX, one sheet "Mapa dat – final", 33 rows × 12 columns |
| Ingested | 2026-10-14 |
| Original location | `~/Desktop/Mapa_zdroju_a_umisteni_dat_reklamace.xlsx` (not stored in repo) |
| Previous rounds | Walked through 2026-10-01 (meeting `2026-10-01-viapharma-reklamace-email-agent-demo-data-map-review`); Sláma's column J + BigHub's column K handled 2026-10-12 (meeting `2026-10-12-reklamace-slama-data-map-feedback-fakturace-state-conflict`). First time the file itself is ingested. |

## Executive Summary

This is the final version of the Reklamace supplier-data map. For each data field it lists the original source, what the field holds, which storage options are technically possible (Excel, Axapta, Confluence/SharePoint, SharePoint Lists), Sláma's comments (J), BigHub's answers (K) and the **final decision (L)**. Column L is the binding outcome. Axapta keeps only the supplier account (the key) and the case-only fields (claim number, RD, issue date), sent to the platform via the claim-closing API. Every other supplier-specific field (return and pickup-warehouse addresses, all contacts, pickup type, notes, photo instructions, okamžité avízo, follow-up procedures) lives in the knowledge base, outside AX. The team should now write column L into the Reklamace client spec and update the Axapta API contract.

## Structure

- **Columns**: A original source · B consolidation · C what it contains now · D field · E description · F–I technical storage possibility (Excel / Axapta / Confluence-SharePoint / SharePoint Lists; feasibility, not preference) · J logistics comments (PETSLA) · K BigHub comments · **L Decision (final)**.
- **18 field rows** in two groups: supplier data (from the consolidated Excel + paper logs, ~300 suppliers) and delivery-note data from the Axapta claim case.
- **Options table**: pros/cons and BigHub's position for Excel (strongly not recommended), Axapta (only what's essential), Confluence/SharePoint (possible alternative), SharePoint Lists (recommended).
- **Open questions block** (9 questions, written before the final round) and a **Result** block with BigHub's recommendation: "from Axapta only what's essential, everything else in one table".

## Key Points: Final Decision per Field (column L, context from K)

| # | Field | Final decision (L) | Context (J / K) |
|---|-------|--------------------|-----------------|
| 1 | Supplier account (účet dodavatele) | **Axapta (key)** | AX primary key, already in the API. It's "účet dodavatele", not "číslo dodavatele". Elsewhere it is only a link column. |
| 2 | Return address | **Knowledge base (outside AX)** | K: the return address lives in the KB, so no AX API is needed. Supersedes the agreed ~2 h manual copy into AX and the original spec 3.5 ("Excel KB" + AI migration). |
| 3 | Pickup type (own pickup yes/no) | **Knowledge base (outside AX)** | ~70–75 suppliers collect their own claims. Printed on the delivery note, where it drives the warehouse's two-pile sorting. |
| 4 | Delivery-note (rozvozový list) template | **AI platform + link in AX** | The platform generates the PDF (AX data + address + pickup type), stores it and sends AX the link. K: we believe the link is already in the API, so only the AX-side implementation remains. Printing is out of scope. |
| 5 | Main contact (e-mail) | **Knowledge base (outside AX)** | K: all contacts (external 1–n and internal) live in the KB and are not split between AX and the KB. This changes the approved API contract, which had main contact in AX. |
| 6 | Other contacts | **Knowledge base (outside AX)** | Unstructured text, 0–2 per supplier, partly outdated. |
| 7 | Contact by step / role (claim vs. transport) | **Knowledge base (outside AX)** | K: BigHub designs the contact-by-step structure. |
| 8 | Okamžité avízo (flag) | **Knowledge base (outside AX)** | K: the flag marks a supplier that wants a preliminary příjem s výhradou avízo (daily summary at 23:00), e.g. Zentiva. Few suppliers, lower priority. |
| 9 | Follow-up email procedure (new functionality) | **Knowledge base (outside AX)** | Procedures per supplier sit in the notes. K: we have only ~7 real email conversations and asked for more. |
| 10 | Notes (poznámky) | **Knowledge base (outside AX), shown in AX** | J/K: notes are stored in the KB, the platform sends them in the Claim-cases API as a note field, and AX displays them (e.g. as an infolog). |
| 11 | Standard / specific procedure flag | **Dropped (no flag)** | K: if the supplier has a KB instruction, follow it; otherwise use the standard procedure. |
| 12 | Photo instructions | **Knowledge base (outside AX)** | K: easy to add to the app, but the instructions don't exist yet. Which suppliers have them? |
| 13 | Způsob vyřízení (resolution method) | **Not sent to the AI platform (PETSLA)** | The quality officer fills it in AX from a code list per claim. K questioned the direction (should the platform propose it?). Final answer: the field is not needed in the platform. |
| 14 | Claim number (číslo reklamace) | **Axapta (API)** | Sent in the claim-closing API (Uzavření reklamace). |
| 15 | Document number (RD) | **Axapta (API)** | J: AX sends it in the closing API, in field `Case_number`, together with the link to the "Návratka dodavateli" file. |
| 16 | Issue date (datum vystavení) | **Axapta (API)** | Added to the claim-closing API. |
| 17 | Warehouse address and contact (Brno / Praha / Pavlov) | **Knowledge base (outside AX)** | J: AX knows the workplace (PVL / OST / BRN), but suppliers sometimes collect in Brno goods delivered to Pavlov (internal transfer), and AX doesn't know that. K: who knows where the supplier collects? |
| 18 | Manual fields (box count, operator text) | **Manual (outside project)** | Written with a marker on the printed note. Another internal project moves these into AX. |

## Extracted Requirements

- **DR-1**: The supplier account is the only key linking KB data to Axapta, and no field may be stored in two systems (row 1).
- **DR-2**: The knowledge base must hold, per supplier: return address, pickup type, main contact, other contacts (external + internal), contact by step/role, okamžité avízo flag, follow-up email procedures, notes, photo instructions, and pickup-warehouse address (rows 2–3, 5–10, 12, 17).
- **DR-3**: The platform generates the delivery-note PDF from AX data plus KB data (address, pickup type), stores it, and sends Axapta a link to the stored file (row 4).
- **DR-4**: The platform sends supplier notes to Axapta in the Claim-cases API as a note field; Axapta displays them (e.g. infolog) without internal logic (row 10).
- **DR-5**: Axapta sends the claim number, RD number and issue date to the platform in the claim-closing API (RD in `Case_number`, together with the link to the Návratka dodavateli file) (rows 14–16).
- **DR-6**: The resolution method (způsob vyřízení) is not part of the platform's data (row 13).

## Extracted Decisions & Assumptions

- **DA-1**: Final storage per field = column L (table above). Supersedes the 10-01 direction and the 10-12 open rows.
- **DA-2**: Return address and main contact move out of Axapta into the KB. Parts of the approved API contract (address, main contact in the supplier endpoint) change, and the AX "~2 h manual address copy" is no longer needed.
- **DA-3**: The standard/specific procedure flag is dropped.
- **DA-4**: Způsob vyřízení: not sent to the platform.
- **DA-5**: Manual delivery-note fields stay on paper, handled by a separate internal ViaPharma project.
- **DA-6**: The storage tool for the KB isn't named. Column L says "knowledge base (outside AX)"; BigHub's options table still recommends SharePoint Lists, while X-Manager is under evaluation internally ([[ASM-243]]).

## Key Stakeholders & Contacts

- Petr Sláma (column J / "PETSLA", final decisions): already in `project-stakeholders.md`.
- Jana Egrmaierová (consolidated the supplier Excel): already in `project-stakeholders.md`.
- Petr Spilka (named as a possible approver): already in `project-stakeholders.md`.
- 0 new stakeholders, 3 already present.

## Open Questions

These are content gaps that BigHub raised in column K. None of them blocks a storage decision.
- Who supplies the pickup-warehouse information (internal transfers, e.g. delivered to Pavlov, collected in Brno)? (row 17)
- Which suppliers have specific photo instructions? (row 12)
- Can logistics provide more real follow-up email threads beyond the ~7 we have? (row 9)
- Is the delivery-note PDF link already in the API, so that only the AX implementation remains? (row 4)
- The options/open-questions block still lists unresolved items from earlier rounds: KB owner on the Dr. Max side, Graph API access, and whether AX supplier headquarters addresses are needed for other purposes. The KB storage tool is still not chosen.

## Routing Log

Confirmed by PM 2026-10-14 ("confirm all").

- **project-assumptions**: DA-1, DA-2, DR-1, DR-3, DR-5 → **ASM-282** (new, Decided). DR-4 → ASM-260 Decided. DA-4 / DR-6 → ASM-262 Decided. Row 17 (warehouse address) → ASM-263 Decided. DA-3 → ASM-261 update. Updates on ASM-228, ASM-229, ASM-184. Open questions (content gaps) → ASM-264 update.
- **project-knowledge**: "Data-map Excel columns J / K / L" (updated), "Způsob vyřízení" (updated), "Uzavření reklamace (claim-closing API)" (new).
- **project-daily**: new to-dos for Filip (Swagger update) and Marek (KB content gaps + `case_number` question); Sláma data-map call item closed; spec items annotated.
- **Client spec**: worked into `Final/3. Reklamace - klientská verze v2.docx` as tracked changes (2026-10-14).
