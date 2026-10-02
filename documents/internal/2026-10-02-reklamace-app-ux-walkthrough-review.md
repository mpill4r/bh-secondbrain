---
last_updated: 2026-10-02
classification: Design
source: internal
original_location: Pasted by PM in session 2026-10-02 (PM-written UX review of the recording Logistick-UCs-status_2026-09-03.mp4, ~14:56–23:00)
---

# Reklamace Mobile App — UX/UI Walkthrough Review (2026-09-03 demo)

## Document Info

**Title**: Senior UX/UI Design Review & Walkthrough: Warehouse Mobile Claims (Reklamace)
**Author(s)**: Marek Pillár (PM), written from the meeting recording
**Date**: Describes the 2026-09-03 demo; ingested 2026-10-02
**Classification**: Design
**Source**: Internal
**Previous version**: N/A. Related meeting note: [2026-09-03-viapharma-logistics-status-reklamace-demo](../../meetings/external/2026-09-03-viapharma-logistics-status-reklamace-demo.md)

## Executive Summary

A screen-by-screen UX review of Filip Černý's live Reklamace app demo at the 2026-09-03 ViaPharma logistics sync. It covers four screens of the damaged-goods claim flow, the two-step příjem s výhradou flow, and two stakeholder discussions (English error messages, login approach). It ends with five UX recommendations. **It reflects the app as of 2026-09-03.** Several statements have since been superseded by newer sources (see "Superseded or inaccurate"), so use it as a UX baseline and checklist, not as the current specification.

## Key Points

### Flow as demoed (2026-09-03)

1. **Krok 1, SP štítek**: camera scanner with a manual text fallback ("Kód ze štítku") and a full-width "Načíst →" button. An unknown label showed a red inline error in English ("No product found for SP štítek (NMVExpedici): SP00488233") with a "Naskenovat znovu" button. Filip recovered by typing a known code (SP01478866).
2. **Krok 2, potvrzení zboží**: a read-only card with data from Axapta (expedition, item number, name, supplier, supplier delivery-note number), a quantity stepper (−/+) labelled "MAX 1", "Zboží souhlasí →" as the main button and "Naskenovat znovu" as the escape.
3. **Krok 3, vyfocení poškození**: counter "(0/2)", rule "Min. 1 foto, max. 10. SP štítek nepřekrývejte", a thumbnail gallery with "+", an optional note, and "Odeslat reklamaci →" with a disabled "Odesílám…" state to prevent double submits.
4. **Success screen**: "Reklamace nahrána" with a large case ID (963714987), and the buttons "Další položka" (main, loops back to Krok 1 without a new login) and "Ukončit".
5. **Příjem s výhradou** (own tab): scan the MS label → 1–10 photos plus a note → "Zaznamenat výhradu →" → Axapta returns a reservation ID. It's for whole damaged shipments at the dock, so the truck can leave and detailed inspection happens later.

### Stakeholder discussion

- **English error text**: Petr Sláma spotted it. Jakub Turner said a PR to translate all error states into Czech was pending.
- **Login**: test-phase hardcoded per-user logins, Entra ID later. Sláma: individual identity is needed so Axapta records who created each claim (audit trail).

### UX recommendations (author's)

1. An aiming frame on the camera view.
2. All error codes mapped to plain Czech text with a recovery step.
3. A clear button hierarchy: solid main action, outline "Naskenovat znovu".
4. Client-side image downscaling (max ~1080p, ~80 % JPEG).
5. A larger, more visible photo counter (e.g. a green badge once the minimum is met).

### Superseded or inaccurate (checked against newer sources, 2026-10-02)

| Review says | Current state |
|---|---|
| Users are drivers; subheader "Samoobslužný terminál řidiče" | Reklamace users are the příjem foreman (and quality staff for Fáze 2). The driver kiosk is Fakturace doprav. The subheader was likely a leftover in the test build. |
| Two tabs: Příjem s výhradou / Příprava | Three equal flows (tabs): příjmová reklamace, skladová reklamace, příjem s výhradou (Filip Černý, 2026-10-01) |
| Photos pushed through Boomi into Axapta | Photos are stored in Azure Blob; Axapta gets direct links (SAS token). Contract v0.9.10: "only links go to Axapta, not binaries" |
| Images sent raw | Spec v3/v4: photos are downsized before sending |
| Success screen shows the Axapta ID | Agreed with Egrmaierová/Sláma: show the RD number if it exists, never the internal axapta_ref (Filip Černý, 2026-10-01; spec v4) |
| Hardcoded test logins, Entra ID later | Superseded: per-user login through one shared Entra registration, week of 2026-10-05 ([[ASM-217]]) |
| Some framing (Zebra terminals, gloves, supplier legal disputes over hidden labels) | Not evidenced in harness sources; treat as illustrative, not fact |

## Extracted Requirements

- **DR-1**: User-facing error messages must be in Czech with a clear recovery step, with no raw English backend strings (Sláma, 2026-09-03; Jakub Turner's PR pending then).
- **DR-2**: The photo step requires 1–10 photos, and the SP label must not be covered (on-screen rule).
- **DR-3**: Each claim must be attributable to an individual user in Axapta (Sláma, audit trail). Already covered by [[ASM-182]] / [[ASM-217]].
- **DR-4**: After a successful upload, the user can continue to the next item without logging in again.

## Extracted Decisions & Assumptions

- **DA-1**: Testing started on hardcoded per-user logins, Entra ID later (2026-09-03). Superseded by [[ASM-217]].
- **DA-2**: Příjem s výhradou is a separate fast flow at the dock (MS label + photos), linked to item claims later by Axapta. Consistent with the contract and spec v4.

## Key Stakeholders & Contacts

Filip Černý (STK-006), Jakub Turner (STK-007), Petr Sláma (STK-034), Jan Sovka (STK-002), Jan Kopecký (STK-032). All are already in project-stakeholders.md. 0 new.

## Open Questions

- Did the Czech error-message PR ship? Not confirmed anywhere since 2026-09-03.
- The quantity stepper said "MAX 1" but showed 2: is the max limit enforced correctly?
- Is the "Samoobslužný terminál řidiče" subheader still in the Reklamace build?
- Which of the five UX recommendations, if any, go to Filip's backlog before UAT?

## Routing Log

{Written after PM confirms routing review}
