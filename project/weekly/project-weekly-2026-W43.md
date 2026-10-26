---
status: confirmed
last_updated: 2026-10-23
last_updated_by: manual — /project-weekly
week: 2026-W43
project_status: Amber
---

# Weekly — 2026-W43 (Oct 19 – Fri 23 Oct 2026) — Second Brain (Dr. Max account)

## Project Status

**Amber**, unchanged all week. Real progress landed this week: the CC is on the AI Platform, Max's GDPR path is settled, and Lexie is spreading to new departments. The driver is still **Reklamace**. The 4 November next batch was set on Wednesday, and by Thursday it was already at risk. Sláma is out next week on international WMS meetings, and ViaPharma hasn't committed a date for its inputs ([[ASM-323]], [[ASM-330]]). Max's end-of-November public launch is the second watch item: the CC doubts the date, and it still depends on BDC for drmax.cz access and on conversation storage BigHub hasn't built yet.

No status change during the week.

## Week Summary

The week turned Lexie from a CC tool into a platform product for the whole company. Marek met three new departments in four days: L1 support (Macháň), Legal (Svoboda) and Brno accounting (Švarcová, a live demo). Friday's internal session then set how BigHub handles them. Features go on one Azure DevOps board. Onboarding a department is console configuration, not a ticket. The open question is how Lexie reaches each department's SharePoint, and nobody knows who approves that. Reklamace finally got a client-format roadmap with estimates and a 4 November target, and lost it within a day to Sláma's absence and ViaPharma's missing input date. On the account side, the CZ AI register was mapped, scored and sent to Dudaško for the group (Lesch) register. Friday's GDPR meeting with Dr. Max's DPO and external lawyer cleared Max's longest-standing blocker (open since mid-September): no consent needed, just a legible notice.

## Key Decisions

| # | Decision | Rationale | Assumption ID |
|---|----------|-----------|---------------|
| 1 | CZ rows go straight into Lesch's shared group register (Marek copies them); BigHub proposal scores marked "to confirm with CIO" | Lesch wants one register; scoring ownership still with Dudaško | [[ASM-310]], [[ASM-311]] |
| 2 | Finance registry row = Deloitte/DUVo analysis + 2 pilots; benefits -tbd-; rule-based automation first, human in the loop | Finance called the FTE estimate inflated | [[ASM-307]], [[ASM-308]] |
| 3 | Lexie/BigHub AI requests can flow through ServiceNow (BigHub resolver group under "BigHub AI"); the service needs an IT owner | Macháň's offer; Mertová shouldn't own it | [[ASM-305]], [[ASM-306]] |
| 4 | Fakturace scanner narrowed to Canon DR-G2090/2110 on a locked-down Windows Zebra | IT ruled out an open PC | [[ASM-313]]–[[ASM-316]] |
| 5 | Reklamace client roadmap: static Excel Gantt per phase (BigHub dev → delivery → testing), pessimistic MD; next batch 4 Nov, testing 4–6 Nov | Client wants commitments, not internal reasoning | [[ASM-323]], [[ASM-324]] |
| 6 | AI register gets a "Technical owner" column (definition still being settled) | Each initiative needs a Dr. Max product owner on the IT side | [[ASM-332]] |
| 7 | Lexie Next libraries + temporary notes; Max banned-word list; Max stock from Magento | CC requests at the weekly | [[ASM-333]]–[[ASM-335]] |
| 8 | Department documents go into the SharePoint "Lexie" folder (for now); archive handling to be designed | No drive connections | [[ASM-338]], [[ASM-339]] |
| 9 | Max GDPR: no consent; contract + Art. 9 health-care exception; legible notice + link at chat start; ~30-day chat retention on legitimate interest | External lawyer's view | [[ASM-102]], [[ASM-340]], [[ASM-341]] |
| 10 | One Lexie board in Dr. Max's Azure DevOps (labels per department); onboarding not ticketed; features global | Onboarding is configuration | [[ASM-344]], [[ASM-345]] |
| 11 | TAS: build nothing on it for now | Conflicting signals, promised for months | [[ASM-348]] |

## Milestones & Progress

- **Lexie departments:**
  - First meetings with L1 (Macháň), Legal (Svoboda/Švestka) and accounting (Švarcová, live demo).
  - The "Lexie x Oddělení" sheet now covers 7 departments and was rewritten for scanning.
  - Accounting has its SharePoint folder and the test link; testing is expected from ~Monday.
  - Lexie board created by Jindřich.
- **AI Platform:** the CC has platform access (roles still to fix), and Lexie Next with libraries was demoed. The production switch is planned for the end of next week.
- **Max chatbot:** fixes are on a test candidate for CC testing. GDPR framework agreed; Kytýrová's notice and policy draft is due next week.
- **Reklamace:**
  - Roadmap session with first estimates (Phase 1 ~6 MD, 1.1a 1–3, Phase 2 3–4, Avízo 1–2).
  - Client roadmap Excel built and sent internally.
  - E-mail-agent test setup agreed with ViaPharma.
- **Fakturace doprav:** scanner hardware narrowed. Mapping Excel sent to ViaPharma; the mock deploy without Axapta follows next week.
- **Account / 2027:** CZ AI register mapped (24 CZE rows), scored and sent to Dudaško; first call with Lesch; finance (Deloitte/DUVo) row clarified; 2027 backlog split into initiatives + a Lexie departments sheet.
- **Team:** Lukáš Šatura joined as a developer (TEO/OCR first).

## Risks & Issues

- **Reklamace 4 November batch at risk.** Sláma is out next week and ViaPharma hasn't committed its input date. The AX deadline (30 Oct) and delivery (4 Nov) in the roadmap no longer hold. *Mitigation:* ViaPharma (Foltová + Sláma) commits a date, and Marek re-plans the roadmap from it (5–7 working days of BigHub work left) ([[ASM-330]]).
- **Max end of November.** The CC doubts the date ([[ASM-337]]). Still needed:
  - the drmax.cz contact and network openings via BDC/Tvarůžek ([[ASM-236]])
  - server-side conversation storage, which doesn't exist yet ([[ASM-340]])
  - a check on whether a BigHub–Dr. Max data-processing agreement exists ([[ASM-342]])

  *Mitigation:* the legal texts arrive next week, and Jura has Lukáš as extra capacity.
- **Lexie SharePoint access has no known approver.** Every new department depends on it. Copying files into the Lexie folder works for testing but goes stale ([[ASM-346]]). *Mitigation:* Marek asks Macháň and Jura asks Tvarůžek who approves; BigHub offers Dr. Max three access variants.
- **Platform roles still wrong.** Former Lexie admins are platform SuperAdmins until Tvarůžek binds the security groups. That blocks inviting accounting and fixing the CC roles.
- **Listing at real risk of closing** (Tuesday's BigHub sync). Jindřich has a lunch with Neuman planned.
- **Overdue PM items:**
  - CZ rows into Lesch's register (due 10-21; waiting on Dudaško's confirmation)
  - 2027 initiative collection (department deadline today)
  - Sláma's error-message statements to Filip (10-22)
  - technical-owner definition with Jindřich (10-23)
  - L1's 2027 ideas (now part of the Macháň e-mail)

## Action Items

PM-owned open items at week end: 31. The key ones:

**Marek Pillár**
- 🔴 2027 initiatives: collect from all owners (department deadline passed today; full backlog by end of November)
- 🔴 One e-mail to Macháň (draft ready): technical answers, SharePoint approver, Legal's directives, L1's 2027 ideas — week of 10-26
- 🔴 Fill the Lexie Azure DevOps board with feature items — week of 10-26
- 🔴 Apply Dudaško's changes and copy the CZ rows into Lesch's register — overdue (10-21)
- Revise the Reklamace roadmap once ViaPharma commits its input date
- Agree the technical-owner definition with Jindřich, then contact the rest — overdue (10-23)
- Send Jura the accounting users' e-mails (Grimová so far); set up and test the accounting library with Jura
- Review the CC methodologies in X-Manager; map the front/back-office overlap
- Rearrange the X-Manager kick-off with Machata (back 10-27)
- Get written confirmation of the Fakturace mapping agreement from Žižka / Sláma

**Shared / others (watch)**
- Jura: production switch; CC roles; accounting library + test link; Max banned words + temporary notes; drmax.cz contact; Lukáš onboarding zip
- Kytýrová / Henychová: Max notice + privacy policy draft (week of 10-26); DPA check with Švestka
- Filip: Fakturace mock deploy; Reklamace login + mailbox (10-30)
- Foltová / Sláma: committed input date for Reklamace
- Jindřich: Neuman lunch (Listing); Žůrek steerco; Dudaško on model costs

## Next Week

- **Mon 10-26:** accounting starts testing Lexie (test link) if the security groups are fixed; Macháň e-mail; Lexie board.
- **Mon 10-27:** Machata back → X-Manager kick-off and API key.
- **Wed 10-28:** Czech public holiday. Whether the 10-29 ViaPharma sync happens is still undecided.
- **During the week:** Kytýrová's first draft of the Max legal texts; Fakturace mock deploy; ViaPharma's committed input date and a Reklamace re-plan; Listing sync after Jindřich's lunch with Neuman.
- **End of week:** AI Platform production switch (links return to the production URLs); more MaxBuddy pharmacies after the node-pool switch.

## Team Notes

- **Lukáš Šatura** joined as a developer alongside Jura and Filip, at ~0.5 FTE, starting on TEO/OCR. Dr. Max identity and repo access take ~14 days; Jura is sending a self-contained OCR package meanwhile.
- **Petr Sláma** (ViaPharma) is away next week; **Michal Machata** is back 10-27.
- **Kateřina Kadlecová** leaves at the end of October; the CC hasn't named her successor yet ([[ASM-091]]).
