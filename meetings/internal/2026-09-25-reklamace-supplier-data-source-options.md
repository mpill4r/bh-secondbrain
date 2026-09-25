---
last_updated: 2026-09-25
type: internal
attendees: [Jindřich Tůma, Filip Černý]
recording_link:
---

# Reklamace Supplier-Data Source Options, Axapta Gaps & Email-Agent Demo

**Date**: 2026-09-25
**Attendees**: Jindřich Tůma (PM, Dr. Max account), Filip Černý (Developer, Reklamace dev owner)
**Type**: internal
**Recording**: N/A (Teams transcript, 1h 11m, Czech)
**Previous session**: N/A (unplanned call). Related: [2026-09-23 cross-project status sync](2026-09-23-cross-project-status-sync-reklamace-fallout-listing-blockers.md)
**Meeting prep**: N/A

## TL;DR

Jindřich and Filip went column by column through the Reklamace supplier-data table to decide where each attribute should live. The only fields Axapta has committed to are supplier account, address and main contact. Other contacts, notes and pickup type have no agreed home, because Petr Sláma's team won't build more on an Axapta that Dudaško plans to retire. BigHub will give logistics an options table (Excel on SharePoint, which is possible but not recommended, SharePoint Lists, or Confluence), each with its risks, and let the client choose and own the risk. Filip will build a ~1 MD email-agent demo as a goodwill gesture for next Thursday's (2026-10-01) logistics meeting. A new gap also surfaced: the rozvozový list fields that come from Axapta (reklamace number, document/RD number, issue date) are missing from the API contract.

## Key Discussion Points

### Why Excel on SharePoint is risky

Logistics keeps asking for the supplier data to stay in an Excel file on SharePoint. Filip doesn't recommend it ("a very unprofessional solution, to put it politely" [translated from Czech]). He named three risks:
1. **No synchronization.** People at different warehouses can download local copies, edit them, and never upload them back.
2. **No change audit trail.** Nobody can tell who changed what, or why.
3. **Weak authorization control.**

A fourth, technical concern: it's unclear whether BigHub can read the file automatically through a SharePoint API, or whether user download/permission restrictions would block that. Filip thinks each risk could be solved on its own, but solving all three together is "another level of problems."

Jindřich wants this in business language, not technical detail: three main risks plus a fourth point for "other unclear items to be discovered along the way." The client should then choose its own path: "it's enough that people know about the risk."

### Alternatives: SharePoint Lists and Confluence

Filip raised **SharePoint Lists**, which he called "SharePoint tables": an Excel-like table that lives natively on SharePoint and can't easily be downloaded. He described it as halfway between a real database and Excel, with better security, simple automated reads, and implicit synchronization because there's only one table. He has heard of it but never used it, and called it "a bit of amateurism technically… a solution for a shop with 20 items, but let's offer it."

Jindřich raised **Confluence**, which Dr. Max already uses. Filip sees it as overkill for tabular data where the longest cell is a two-sentence note, but acceptable if it gives a secured table, easy data reads, authorization and ideally an audit trail: "we just need a table that's secured and easy to read data from. That's all." [translated from Czech]

Expected user count: Jana Egrmaierová suggested about **2 editors per warehouse**. Viewer count is unknown and equals the number of claims workers. Jindřich will plan for 3–4.

A bare database table would solve sync and automated reads, but not safe editing, audit or authorization, and it has no UI. Filip considers building an editor for it a bad idea.

### Why logistics clings to Excel

Jindřich has now heard twice (the day before yesterday and today) that "it was agreed it would be Excel." He says it was never presented that way. The client is grabbing onto it partly because the spec talked about Excel from the start. Filip had also earlier demoed an improved Excel (a data sheet plus a print sheet with lookups), which may have been read as a commitment. Filip says he always told them in joint meetings that he's "a small guy" who can't decide this, and that the decision has to come from Dr. Max or from someone senior at BigHub.

Jindřich's read on the real motivation: logistics has no other tool, and they won't use Axapta because it's being retired. It isn't a UX preference. Filip was relieved to hear this, because it means any secured table would do.

### Axapta: what's promised and what isn't

Per Jindřich, Petr Sláma's position (relayed yesterday alongside Dudaško) is that Axapta "will be killed," so his team won't do development on the Axapta side. Dudaško separately wants something else even at higher development cost.

Filip is frustrated that Sláma "quickly goes to aggression." He says Sláma often says something can't be done without saying why, and offers no counter-proposals. Because BigHub is the consultancy, it gets blamed by default.

Filip's architecture concern: a separate BigHub database creates an Axapta-sync problem and stale snapshots, since supplier accounts change and suppliers leave. His principle: **any non-Axapta store must be an extension of Axapta**, keyed by supplier account, and "definitely we don't want the same information in two places."

### Supplier-data attributes, column by column

| Attribute | Current source | Axapta status | Notes |
|---|---|---|---|
| **Účet dodavatele** (supplier account; not "číslo dodavatele") | Already in Axapta | Needs to be exposed via the API contract. Filip is "almost sure" Sláma won't object | BigHub only learned last week that this field exists |
| **Adresa** (address) | Excel holds the real warehouse return addresses. Axapta only holds supplier HQ | Axapta agreed to add them after pressure from purchasing, but hasn't done it yet | **Manual data entry is needed on the Axapta side**: no development, roughly 2 hours of copying from the Excel |
| **Typ odvozu** (pickup type: own pickup yes/no) | Excel only | Not in Axapta; would need a new field. Not agreed | About 70–75 suppliers collect returns themselves, often while making their own delivery. Warehouses keep two separate piles. The flag is printed on the rozvozový list so staff can sort. Filip thinks it belongs more with Instructions/follow-up than with supplier master data |
| **Hlavní kontakt** (main contact, email only) | Excel only | Promised; already in the approved contract | Drives the email draft. Exception: fewer than 5 suppliers route by goods category (food → person A, drugs → person B). The concept covers ~95–97% of suppliers. Filip: keep it. Jindřich: handle the exceptions in the spec |
| **Kontakty** (other contacts) | Excel only. Unstructured free text (names, emails, phones), some for people who have left | Not agreed | Typically 0–2 per supplier, almost always under 5, mostly 0–1. Per Jana Egrmaierová, the right contact is sometimes picked by type of goods and sometimes just by staff experience |
| **Poznámky** (notes) | Excel only | Not agreed | — |

Jindřich grouped the attributes into four sections: basic supplier info; main contact for the email draft; **Instrukce** (Instructions), a rename because Jindřich wants to "kill" the term "knowledge base"; and the follow-up email process. Filip suggested merging the follow-up section into the email-draft section.

Filip credited Jana Egrmaierová with a huge consolidation effort. She reduced the original ~300-sheet Excel (one sheet per supplier, each a pre-filled rozvozový list template with scattered notes around it) to a single ~300-row × ~10-column table.

### The claims worker can't see supplier info

Filip flagged a UX gap. Two different people handle a claim:
- The **příjem foreman** (receiving foreman) uses BigHub's mobile app. He scans the label and photographs the damage, and the app creates the case in Axapta.
- The **zaměstnanec reklamací** (claims worker) is a different person, often in a different part of the warehouse, and has never used the app. They work in Axapta and used to rely on the multi-sheet Excel: one sheet per supplier, showing the rozvozový list and the relevant notes together.

With a flat table in any tool, the claims worker has to search a large table for one row, which is "quite unpleasant." Filip suggested a small web app for the claims worker, about 1–2 MD: process info, a rozvozový list preview before printing, and possibly inputs such as crate count. It's outside the spec, and Filip also dislikes creating a new system to maintain for a small need.

Jindřich: BigHub doesn't have to solve everything. Present the options, flag this as an open question and let the client decide. Filip agreed, but wants it mentioned constructively as something BigHub discovered.

### Email-draft flow and the email-agent demo

Current state (per Filip): Jakub Turner has finished the main part. It's still blocked on infra delivering **Microsoft Graph API** access.
- **Flow**: The worker clicks a button in Axapta, which sends a request (generate rozvozový list / close case) with supplier data. BigHub generates the rozvozový list and returns it to Axapta for printing, and the same request triggers an Outlook email draft. The worker reviews it and sends.
- **Follow-up**: A supplier reply arriving in the inbox triggers an LLM. For example, it can read which of a multi-warehouse supplier's warehouses to ship to (about 5 such suppliers), print that address on the rozvozový list, and draft the next reply in the thread.
- Filip expects drafts to be threaded and the claims worker to work mostly from the Drafts folder. He's **cautious about promising the draft appears directly inside the thread**, since it isn't implemented yet.

Filip will build a **~1 MD demo** of this email agent (using text files, not wired to Outlook) as "the bone we throw them": "sorry, we didn't do everything ideally either; here's something we've partly built." Full integration would take considerably longer. Jindřich approved it for next Thursday's (2026-10-01) logistics meeting. The management meeting has been pushed to the following week because Dudaško has no time next week. The aim for next week is to calm logistics down, agree the table, and show the demo.

Jindřich floated a unified web interface with a per-case communication timeline. Filip attributed the idea to Jan Sovka: it's one sentence in the spec, with no response from the client so far. He estimated it at weeks of work, "a new project." **Jindřich killed the idea.**

Filip noted that a capable email agent could in theory make it unnecessary to show the claims worker anything. He still prefers that the worker can see the notes the agent works from, rather than using the email draft as the frontend.

### New gap: rozvozový list fields from Axapta

Filip showed the rozvozový list the app generates. **Reklamace number, document number (RD) and issue date** all come from Axapta but **are not in the API contract**. Filip called this "half our fault": Lukáš worked on it earlier while still new, and it was missed. Filip flagged it about a week ago. Sláma didn't respond; only Jana Egrmaierová replied.

The warehouse address and contact person at the bottom could come from a location lookup table (Brno / Praha / Pavlov, e.g. derived from the machine's IP) instead of Axapta. That's for consideration. Handwritten fields such as crate count filled in with a marker are "probably OK," but would be another argument for the small web app.

Jindřich wants **one complete requirements package for Axapta**, so nothing else is discovered later. Filip will openly present the gap as BigHub's own debt: "no point pointing fingers, let's just solve it now."

## Decisions Made

- **Present options with risks; the client chooses and owns the risk.** Supplier data outside Axapta goes to logistics as an options table with a BigHub preference marked. Excel on SharePoint is possible but not recommended (sync, audit trail, authorization, plus unknowns). The original Axapta preference is withdrawn as unrealistic. The other options are SharePoint Lists and Confluence. If logistics accepts the Excel risks, BigHub can deliver it as they want.
- **The "knowledge base" term is dropped** and renamed **"Instrukce"** (Instructions).
- **The main-contact concept is kept** (it covers ~95–97% of suppliers). The fewer than 5 category-conditional exceptions will be handled in the spec.
- **Any non-Axapta supplier store extends Axapta**, keyed by supplier account. No field is duplicated between the two systems.
- **The per-case communication timeline/dashboard idea is killed.** It's out of scope and weeks of work.
- **Filip builds a ~1 MD email-agent demo** for the 2026-10-01 logistics meeting, framed as a goodwill gesture rather than a commitment.
- **The claims-worker display gap is raised with the client as an open question**, not solved unilaterally by BigHub.
- **The rozvozový list Axapta-field gap is presented as BigHub's own debt**, inside one complete Axapta requirements package.

## Action Items

- [ ] **Jindřich Tůma**: Send Filip the supplier-attribute table (Excel) — due 2026-09-25 — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Review the table and add input per section; write up the 3 main Excel-on-SharePoint risks in business language, plus a 4th "open unknowns" point — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Research SharePoint Lists (what it can and can't do: security, audit trail, automated reads) and send Jindřich a short write-up — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Jindřich Tůma**: Research Confluence as a supplier-data store (fit, licensing) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Jindřich Tůma**: Find the number of editors and viewers who would access the supplier data (via Jana Egrmaierová, not Tereza) — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Build the ~1 MD email-agent demo (text files, not Outlook) — due before 2026-10-01 — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Filip Černý**: Send Jindřich the link to the Teams discussion on the rozvozový list fields missing from the Axapta contract — from 2026-09-25-reklamace-supplier-data-source-options
- [ ] **Jindřich Tůma**: Consolidate the supplier-data options and the complete Axapta requirement list into the Reklamace spec, and prepare materials for the 2026-10-01 logistics meeting — due 2026-10-01 — from 2026-09-25-reklamace-supplier-data-source-options

## Open Questions

- Where do **Kontakty**, **Poznámky** and **Typ odvozu** live? None of them is agreed in Axapta.
- Can BigHub read an Excel or SharePoint List automatically via API, given Dr. Max's SharePoint permission setup?
- Is Confluence's licensing workable for about 2 editors per warehouse plus all claims workers as viewers?
- How does the claims worker see supplier info and Instructions without the old multi-sheet Excel: the table directly, a small web app (~1–2 MD), or the email agent only?
- Will Axapta add **reklamace number, RD document number and issue date** to the API contract? Sláma hasn't responded.
- Warehouse address and contact on the rozvozový list: a location lookup (IP-based) or Axapta?
- Can a follow-up draft appear directly inside the supplier's reply thread in Outlook? It isn't implemented or verified yet.
- When is the Axapta manual address entry (~2 hours) scheduled, and who owns it?

## Sentiment & Tone

Collaborative and candid. Filip was apologetic and self-critical ("I'm almost ashamed to keep bringing up special cases"; "maybe I should have pushed this harder"). He was openly frustrated with Petr Sláma's "no without reasons" stance and with BigHub being treated as the default culprit. Jindřich was supportive and protective ("nobody wants you carrying that responsibility… we just need it communicated well and signed off by them"). He was pragmatic about scope, killing the timeline dashboard quickly. There's underlying pressure from the logistics relationship: the "it was agreed to be Excel" narrative and the need to "calm them down" next week. The demo is explicitly a relationship-repair move.

## Routing Log

Confirmed by PM on 2026-09-25 (confirm all). The two flagged conflicts were resolved with the proposed defaults: the Axapta-as-single-source claim was narrowed in project-knowledge and ASM-122; the pushed "management meeting" is read as the Reklamace continue-or-close meeting, separate from the 2026-09-29 meeting (unverified).

- **project-assumptions**: ASM-169–ASM-173 (Decided), ASM-174–ASM-176 (Open); updates on ASM-122, ASM-139, ASM-143
- **project-knowledge**: Reklamace entry updated; new naming entry "Reklamace supplier-data naming"
- **project-stakeholders**: STK-006, STK-007, STK-034, STK-044
- **client-overview**: Ways of Working entry
- **project-daily**: 8 action items
- **project-lessons**: LL-062, LL-063, LL-064
