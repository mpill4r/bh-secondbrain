---
status: confirmed
last_updated: 2026-09-25
last_updated_by: manual — /project-weekly
week: 2026-W39
project_status: Amber
---

# Weekly — 2026-W39 (Sep 21 – Fri 25 Sep 2026) — Second Brain (Dr. Max account)

## Project Status

**Amber**, measured on PM-actionable streams only. The driver is **Reklamace**: the continue-or-close decision is open, only part of the process is specified (phases 3–5 not at all), and Sláma disputes the reframe ([[ASM-181]]). That puts the October 15–16 full-UAT start at risk. Marek has owned the documentation since Friday ([[ASM-177]]). Secondary: the 5 Fakturace doprav contradictions are unresolved and queued behind Reklamace.

*Watch (owned by others, no PM action):* DB access on the new cluster gates the end-of-September Max go-live phases, the MaxBuddy migration and the first AI Platform release ([[ASM-100]], [[ASM-164]]). Kadlecová has no successor yet ([[ASM-091]]).

## Week Summary

The week opened with Dudaško setting out his AI Platform vision for the first time. It closed with him accepting Jura's Phase 1 prototype ("after a very long time I can tell BigHub: good job") and making the BQ tracker the mandatory intake standard for every new AI initiative. So the relationship at the top has turned clearly positive. Logistics went the other way. Reklamace was reframed from AI to digitization, and that led to a "BigHub doesn't want to deliver" narrative on Tuesday and a tense standoff with Petr Sláma on Thursday. By Friday there was a way forward: BigHub will bring the supplier-data options, each with its risks, to the 2026-10-01 meeting and let the client choose. Marek has taken ownership of the Reklamace documentation and is the single logistics contact, which Tereza Foltýnová received well. The open risk going into next week is infrastructure, not the client: until DB access on the new cluster is confirmed, the September go-live phases and the first platform release can't move.

## Key Decisions

| # | Decision | Rationale | Assumption ID |
|---|----------|-----------|---------------|
| 1 | BQ tracker is the mandatory intake standard for new AI initiatives; the tracker (`new_Přehled`) is the source of truth for business values | Dudaško wants every initiative quantified and comparable | [[ASM-158]] |
| 2 | Every KPI needs a measurement method; department AI backlogs due end of November | Management needs 2027 goals from a ready backlog | [[ASM-159]], [[ASM-161]] |
| 3 | AI Platform Phase 1 prototype accepted; design work deliberately deferred; Zabbix integration added | Validate navigation and structure first | [[ASM-147]], [[ASM-162]] |
| 4 | MaxBuddy value settled at 81M Kč/yr (revenue uplift); stage recorded as Nasazování (the tracker still says Deployed) | Tracker reconciliation; PM correction | [[ASM-140]] |
| 5 | Reklamace supplier data: BigHub presents options with explicit risks (Excel on SharePoint, SharePoint Lists, Confluence) and the client chooses and owns the risk | Axapta commits only to supplier account, address and main contact; Sláma's team won't build further on Axapta | [[ASM-169]], [[ASM-176]] |
| 6 | Logistics Part A/B: Marek owns the Reklamace documentation (~2-week focus, ahead of Fakturace doprav); Tereza drafts new initiatives and validates with Spilka, then Žůrek | Reklamace scope isn't closed (phases 3–5 undescribed) | [[ASM-177]], [[ASM-178]] |
| 7 | TEO/OCR: Excel stays for the autumn 2026 cycle; a review solution that isn't Excel comes before spring 2027 | Protocols arrive twice a year and the autumn cycle is already running | [[ASM-165]] |
| 8 | Max chatbot tone input is keywords only | Max runs on GPT-5 mini and has hit its instruction ceiling | [[ASM-149]], [[ASM-150]] |

## Milestones & Progress

- **AI Platform:** vision call (Mon), UX review, benchmark and sitemap delivered to Jura, then prototype accepted by Dudaško (Thu). The written work-in-progress spec/roadmap moves to next week.
- **Business Quantification:** tracker reconciled as the source of truth (MaxBuddy 81M, Listing 34.12M with +0.1 pp conversion, Reklamace 425k for phase 1 only). A Czech reference document of the 9 running initiatives was produced for Dr. Max.
- **Fakturace doprav:** spec redline finalized (`new_2. Fakturace doprav v2.docx`). The code audit found 5 contradictions ([[ASM-131]]–[[ASM-135]]); reconciling them with Filip moves to next week.
- **TEO/OCR:** SPEDOS confirmed as the 3rd autumn pilot vendor ([[ASM-127]]), and the phasing is agreed.
- **Max/Maxie/Lexie:** a large batch of Max fixes shipped. Maxie is to replicate the existing IVR solution ([[ASM-154]]).
- **Harness hygiene:** 09-24 Reklamace standoff and 09-14 notes routed late; 3 notes from 09-01 marked superseded; indexes completed. MVP-scoping item ([[ASM-104]]) closed as stale.

## Risks & Issues

- **The infra blocker is putting the September go-live phases at risk.** DB access on the new cluster has been blocked for 6–7 weeks, behind a single BDC contact (Vláďa Tvarůžek). If it isn't confirmed early next week, the end-of-September internal phases slip, and the first platform release (~4 weeks after access) moves into November. *Mitigation:* Jindřich escalates at the 2026-09-29 management meeting, up to CEO level if needed.
- **Reklamace continue-or-close is still open, and Sláma disputes the reframe.** He says the original vision was an AI-driven branching email workflow, flagged in writing on 2026-05-20 ([[ASM-181]]), and his sentiment has dropped from leaning Champion to Neutral. Only part of the process is specified. *Mitigation:* options table and Filip's ~1 MD email-agent demo at the 10-01 meeting; Sláma invited to the Dudaško/Žůrek decision meeting; Marek builds a near-final shared spec.
- **Axapta data gaps on Reklamace.** The rozvozový list fields (reklamace no., RD no., issue date) are missing from the API contract ([[ASM-174]]). Contacts, notes and pickup type have no agreed home ([[ASM-176]]). The two-address shipment case is unhandled ([[ASM-183]]). Each is small, but together they can stall testing.
- **Losing the CC domain expert.** Kadlecová's departure leaves Max/Maxie/Lexie content sign-off without an owner ahead of the end-of-October public launch ([[ASM-091]]).
- **MCP security gap in the AI Platform** ([[ASM-145]]): secrets can leak to agents reading server descriptions. It must be sealed before further build-out.

## Action Items

Only PM-owned items are tracked. Items owned by others were moved to `action-items-archive.md`.

- Reklamace documentation to near-final depth; questions for Tereza, Jana and Spilka.
- Review Tereza's draft logistics table (Wed/Thu); in-person meeting at Florentinum Wed 09-30 10:00.
- Ask Dudaško whether the cross-department tracker can be shared.
- KPI measurement-method column; BQ sign-offs (Šimoník, Mertová); department backlogs (end of November).
- Next week, lower priority: reconcile the Fakturace doprav contradictions with Filip and the AR-pairing key with Sláma; AI Platform work-in-progress spec with Jindřich.
- Capacity-pool talk with Jindřich ([[ASM-167]]); ElevenLabs barge-in check with Jura; the ASM-119 and ASM-088 conflicts with Jura.
- Older, low priority: Filip's business questions; Maxie roadmap drift; Figma roadmap comments (blocked on Honza Sovka); Reklamace brief review; the ~9 remaining BQ initiatives (deprioritized).

## Next Week

The week is short: **Monday 09-28 is a Czech public holiday.**
- **Tue 09-29**: management meeting. PR value stories; escalation of the infra bottleneck.
- **Wed 09-30**: in-person meeting with Tereza Foltýnová at Florentinum (10:00).
- **Thu 10-01**: logistics status. Supplier-data options table, Filip's email-agent demo, Axapta requirement list. Also the Lexie/Max/Maxie weekly (Max model cost projection due).
- **Fri 10-02**: logistics initiatives validation debate with Tereza (internal, not final).
- **During the week**: Vosmek MaxBuddy wishlist call; Reklamace continue-or-close meeting (Dudaško, Žůrek, Spilka, Žižka, Sláma) to be scheduled; end-of-September internal Max go-live phases (at risk).

## Team Notes

- **Marek's focus:** his focus moves to Reklamace for about 2 weeks, and Fakturace doprav waits.
- **Capacity:** BigHub's Dr. Max capacity is understood to be a flexible ~3 FTE (~60 MD/month) annual pool, possibly with unused budget accumulated since May ([[ASM-167]], open). It's unclear whether Jindřich counts inside the pool.
- **Availability:** Marek Šimoník is on vacation, so BQ sign-off is pending. Petr Spilka is unavailable next week.
