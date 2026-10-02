---
status: confirmed
last_updated: 2026-10-02
last_updated_by: manual — /project-weekly
week: 2026-W40
project_status: Amber
---

# Weekly — 2026-W40 (Sep 28 – Fri 2 Oct 2026) — Second Brain (Dr. Max account)

## Project Status

**Amber**, measured on PM-actionable streams. The driver is still **Reklamace**, but its risk has changed. The scope and supplier-data standoff from last week has largely been unlocked: Sláma's May comment was accepted as direction, Excel is out, and supplier data is converging on one SharePoint List ([[ASM-223]], [[ASM-228]]). The new risk is commercial. Monday 2026-10-05 brings Žůrek, Dudaško and Spilka together on "next steps", and Spilka himself called Reklamace's saving small next to cenařky ([[ASM-242]]). Still open: Sláma's column-J feedback, an owner for the List ([[ASM-215]]), the recap email to logistics, and whether the one-week testing extension moves the 15–16 Oct UAT ([[ASM-227]]).

No status change during the week.

## Week Summary

The week began with Reklamace stuck: a disputed reframe, half a spec, and no agreed home for supplier data. Marek took the documentation over properly. He built a data-source map that put every disputed field in one table with a recommendation, and a phase-based spec (v3 → v5) that answers every comment. Thursday's logistics meeting was the first good one in weeks. Sláma's May comment was accepted, Filip's email-agent demo landed ("a big step forward"), and Sláma converged on BigHub's single-store recommendation. By Friday, though, the question had moved from *how* to build Reklamace to *whether it's worth it*. Logistics reset its initiative list from a green field, Spilka championed cenařky, and Monday's senior meeting will likely weigh Reklamace's ~425k–700k value against the bigger opportunities. Elsewhere, the TEO/OCR offline route proved itself (Rakun: no silent errors, ~1 Kč per page), Listing was re-scoped to enrichment-first, and Max moved to staging with a cheaper-model trial.

## Key Decisions

| # | Decision | Rationale | Assumption ID |
|---|----------|-----------|---------------|
| 1 | Sláma's May spec comment (automatic emails, Zentiva sequence) accepted as the Reklamace 1.1b direction; MD impact via change request | Unanswered comments were taken as accepted; arguing the history gained nothing | [[ASM-223]], [[ASM-186]] |
| 2 | Supplier data: Excel out; one SharePoint List keyed by supplier account, entered in one place; Axapta minimal. Not final until Sláma's column J | Axapta is unfriendly for addresses and contacts; a split store drifts | [[ASM-228]], [[ASM-214]] |
| 3 | Email-agent additions: ViaPharma CC, thread archived as PDF on the Axapta claim, alternative drafts per recipient | Finance reads claim history; terminals have no Outlook | [[ASM-224]] |
| 4 | Problem-type phasing: damaged on receipt → damaged in warehouse → other ~19 types | Ship something first | [[ASM-225]] |
| 5 | Reklamace phase 1 testing extended by one week | Logistics request | [[ASM-227]] |
| 6 | Spec is the contract; decisions confirmed in writing; UX feedback handled operationally | Client comments resurfaced months later | [[ASM-185]], [[ASM-186]], [[ASM-226]] |
| 7 | Logistics initiatives rebuilt from a green field (old tracker rows historical); cenařky analysed by BigHub if it ranks top | Old rows were unclear even to logistics | [[ASM-230]], [[ASM-232]] |
| 8 | Listing: Magento out of the MVP; enrichment first with a food-supplements batch (~2,000 SKUs) | Magento imports blocked; CZ moving to a global PIM | [[ASM-207]], [[ASM-208]] |
| 9 | TEO/OCR: autumn stays offline; ~1 Kč per page accepted; číselník gaps solved via the pharmacy API | Infra not ready; value already visible | [[ASM-218]]–[[ASM-220]] |
| 10 | Max tested on drmax-space.cz; cheaper-model trial approved; order status built from CC's X-Manager tables | Cost-down with Mertová's approval | [[ASM-234]]–[[ASM-237]] |
| 11 | Okamžité avízo: optional nightly automatic supplier notice; doesn't block testing | Some suppliers require ~24 h notice | [[ASM-240]] |

## Milestones & Progress

- **Reklamace:**
  - Data-source map finalized (`Final_Mapa_zdroju_a_umisteni_dat_reklamace.xlsx`) and walked through with logistics.
  - Spec moved from v3 to v5, with all 27 Filip comments answered, the 10-01 outcomes and contract facts added, and data-map items marked purple.
  - Both API contracts saved (Axapta v0.9.10, inbound v0.4.0). The RD number is already in the contract; only the issue date is missing.
  - Email-agent PoC demoed to logistics.
- **TEO/OCR:** Termetal and Rakun processed offline (Rakun: 84 protocols, no silent errors). The client proposal was cross-checked against the sync and sent to Radim. Next sync 2026-10-14.
- **Listing:** reset with Neuman (enrichment first); recap sent.
- **Order prediction:** v2 demoed and very well received; Šimoník praised BigHub at the management meeting.
- **MaxBuddy:** first backlog call with Vosmek (UX polish to year-end, profitability recommendation in 2027).
- **Max/Lexie:** Max on staging orders and Rx stock, with throttling added.
- **Account:** Jindřich's management meeting went well; Dudaško praised the BQ/initiatives table.

## Risks & Issues

- **Reklamace may be questioned on Monday (10-05).** The initiatives Excel values phase 1 at ~425k Kč/yr (~700k overall per Marek), against tens of millions for MaxBuddy and Listing, and Spilka called the saving "a promise not backed by data". If the senior attendees decide to stop or shrink it, the spec and data-store work pauses. *Mitigation:* Marek and Jindřich prepare together (Jan Sovka is staying out deliberately). Frame what's built and phase 1's cost to finish, and offer cenařky analysis as the bigger follow-on ([[ASM-232]]).
- **Supplier-data decision depends on Sláma.** He was out ~14 days on the A-frame launch and is on leave 10-02. Column-J feedback is expected early next week, and the 10-09 knowledge-base decision ([[ASM-184]]) depends on it. The List also needs a named Dr. Max owner. The contracts still take the address and contact from Axapta, so they'll need changing.
- **UAT date unclear.** Phase 1 testing gained a week; whether the 15–16 Oct full UAT moves isn't confirmed. Graph API and mailbox access remain blocked behind the AKS escalation at Max.
- **Overdue PM items:** the 10-01 recap and spec to logistics (due 10-02); the four-point internal-sync summary (09-29); the MaxBuddy recap to Vosmek and Jura (09-29); the Tereza initiatives review (09-30).
- **Capacity:** Marek covers Reklamace, Listing, BQ, TEO/OCR and more at once. Sustainable now, but flagged to Jan Sovka.

## Action Items

PM-owned open items at week end: 44. The key ones:

**Marek Pillár**
- 🔴 Prepare the Monday 10:00 Reklamace meeting with Jindřich — due 10-05
- 🔴 Accept/reject v5, then send logistics the 10-01 recap + spec with open questions (check written answers to Sláma's May comments) — overdue (10-02)
- 🔴 Chase Sláma's column-J feedback → knowledge base decided by 10-09
- Read Jan's March 2026 logistics use-case email — due 10-05
- Ask logistics about the okamžité avízo (which suppliers, deadline, phase, automatic send)
- Ask Filip to check the current build (Czech errors, quantity max, driver subheader) and pick UX fixes before UAT
- Rewrite the Listing spec/roadmap (enrichment first); Monday in-person session with Neuman
- Clean the master AI-initiative tracker (rows from 13 down)
- Overdue: four-point internal summary to the business group (09-29); MaxBuddy recap (09-29)
- TEO/OCR: review the proposal with Radim early next week, then Burda

**Shared / others (watch)**
- Jindřich: ask Dudaško whether automation can be funded from the AI budget ([[ASM-233]]); Atlantis/BDC Maxie meeting 10-05
- Filip: Graph API request for the List; master-label bug; per-user login from 10-05
- Tereza / Jana: problem-type list to Marek; green-field initiative list

## Next Week

- **Mon 10-05:** Reklamace "next steps" (10:00, in person: Žůrek, Dudaško, Spilka, Tereza); Listing session with Neuman; Atlantis/BDC Maxie meeting.
- **Early week:** Sláma's column-J notes; recap + spec to logistics; Radim review of the TEO/OCR proposal.
- **Wed 10-07:** sync with Tereza on the green-field list; 1:1 with Jan Sovka.
- **By 10-09:** Reklamace knowledge-base decision.
- **Wed 10-14:** TEO/OCR sync. Per-user login for UAT expected during the week.

## Team Notes

- **Jan Sovka** steps back from logistics to near zero and won't attend Monday's meeting ([[ASM-241]]). He onboards a new BigHub colleague, Lukáš, on 10-05.
- **Marek and Jindřich** reset their working arrangement: Jindřich handles Dr. Max-side people and politics, Marek delivery and prioritisation. It worked well this week.
- **Kadlecová** (Dr. Max CC) leaves at the end of October; no successor named yet ([[ASM-091]]).
- **Jura** is under heavy infra load; TEO/OCR batches are best-effort.
