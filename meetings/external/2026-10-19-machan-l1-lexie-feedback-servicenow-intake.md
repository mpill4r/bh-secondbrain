---
last_updated: 2026-10-19
type: external
attendees: [Petr Macháň, Jindřich Tůma, Marek Pillár]
recording_link:
---

# Petr Macháň (L1 / ServiceNow) — Lexie Feedback, Source-Data Hygiene & ServiceNow Intake for BigHub AI

**Date**: 2026-10-19
**Attendees**: Petr Macháň (Dr. Max CZE; L1 support, informal ServiceNow owner for CZ, also Change Manager and Problem Manager, STK-069), Jindřich Tůma (BigHub / Dr. Max), Marek Pillár (BigHub, PM)
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: N/A (first meeting)
**Meeting prep**: [2026-10-19-machan-l1-podpora-lexie-2027-meeting-prep](../prep/2026-10-19-machan-l1-podpora-lexie-2027-meeting-prep.md)

> **Transcript note**: The transcript mixes Czech and Slovak. One opening line is labelled "Speaker 10000" (greetings only). "Jura" is Jura Brázdil, "Simona" is Simona Mertová, "Vláďa" is Vladislav Tvarůžek, and "Lukáš Sýč"/"Luky" is Lukáš Szücs. Two new names: **Míša Třísková** (introduced Azure DevOps at Dr. Max) and **Honza Štangl** (knows DevOps, sits in BigHub's office area). The incident manager on Macháň's team is not named ("klučina ode mě", "a guy from my team").

## TL;DR

Macháň demoed how L1 uses Lexie and asked three things: how to prepare source data, how to keep only the current version of a document, and why the large pharmacy-contacts Excel gives poor answers. He also asked for UX changes: a split-screen source viewer, a jump to the matched passage, fuller first answers and consistent answers. Technical questions go to Jura, and UX items go to the product backlog for the owner (Mertová) to decide. The bigger outcome was process. Macháň, who informally owns ServiceNow in CZ, offered BigHub its own resolver group and queue under the **"BigHub AI"** business service (it already exists), with an offering per app, SLAs, and an onward flow into Azure DevOps. Both he and Jindřich agreed the BigHub AI service needs an **IT owner, not Mertová**. A follow-up deep-dive on ServiceNow is to be scheduled this week. 2027 initiatives were not discussed.

## Key Discussion Points

### 1. How L1 uses Lexie and how to prepare source data

- **Macháň** sorted Lexie's sources into folders. He has been pre-processing documents "for better machine reading": handwritten-note PDFs rewritten as text files, glossaries (e.g. for "Farmis" variants), and creation-date headers. He asked whether that effort helps, or whether Lexie "just indexes it anyway", in which case he would stop.
- **Marek**: the file format doesn't matter much (Word, text, etc.). The platform reads the SharePoint folders as its source files.
- **Jindřich**: BigHub assumes Word/PDF on SharePoint. Text files bring no real advantage over Word, and one format is the better strategy, but both work. Detailed format questions go to Jura.
- **Macháň's observations**: Lexie **does not read images**, so diagrams are lost. Claude-generated **Markdown files work poorly**. He likes the **fast refresh**: new files show up in answers quickly.
- **Teaching context (Jindřich)**: users can steer Lexie in the chat ("only from our documents; these two are the key ones") and it will learn. Deeper tuning means prompt changes by Jura.

### 2. Old vs. new versions of the same document

- **Macháň**: if two documents with the same name differ slightly (e.g. updated links), Lexie must use the newer one and ignore the old one. Could a creation date at the top of each document do that? He wants to avoid "new, new-old, old-old" files.
- **Marek**: the simplest proven approach (from another project) is two folders, **current** and **historical**, with the current folder treated as primary. Date-based versioning may also work, but with many documents the risk of hallucination rises.
- **Jindřich**: quality depends on data hygiene. Duplicates and old versions make Lexie hallucinate more, so the focus should be on keeping documentation current.
- **Outcome**: Macháň accepts that L1 must keep the source documentation current (no date-based convention agreed).

### 3. Excel: the pharmacy-contacts list

- L1 has a very large Excel of pharmacy contacts. Asked for "the phone number of pharmacy 191", Lexie returned only the pharmacy phone and mobile, not the manager's or the technician's numbers (four numbers exist). It also answered from a **Markdown copy** and a **text copy** of the same data rather than the Excel. Macháň had uploaded the data in several formats while testing.
- **Root causes seen live**: inconsistent column names ("vedoucí telefon", "mobil", "mobilní") and **several overlapping sources**. Asking for "all phone numbers" worked better.
- **Jindřich**: Lexie should know that "contact" or "phone" means all of them. When it finds several sources, it should **say so or ask** which one to use (Excel vs. Markdown vs. text). Jura could prompt it to do that.
- **Macháň**: "the data is there, but I have to know how to ask, that's the crux" `[translated from Czech]`.
- **Bug**: Lexie repeats the user's question below its answer. Jindřich believes it is already being fixed for CC and will ship in the next upgrade.

### 4. UX requests

- **Split-screen source view**: open the cited document in a right-hand panel, as Claude does, instead of a pop-up that covers the chat and has to be closed to open the next source.
- **Jump to the matched passage**: highlight or scroll to where the answer was found in the source. Jindřich thinks a version may already have this but isn't sure it was deployed, and will check with Jura.
- **Search/input area**: could be smaller and wider, separate from the chat (Macháň says BigHub mentioned this is already planned).
- **Fuller and consistent first answers**: the same question asked three times gives three different answers, and "more?" gives a longer one. He wants everything Lexie has on the first try.
- **Jindřich**: no objection, but Lexie's owner is currently **Simona Mertová**, and design changes need her decision because departments may want different things. The items go into the backlog for approval. Macháň will talk to Simona himself.

### 5. Jindřich's three-layer model for Lexie requests

1. **Questions / recommendations** → technical answer from Jura.
2. **Product-backlog items** (e.g. the split screen) → logged as tasks, and the owner decides. Popular asks across several departments go into a release.
3. **One ticket intake for all departments** (bugs, improvements, features, questions) with visible status, because Lexie is rolling out to **Legal and 2–3 more departments** and requests will grow. Bugs get clear priority; redesigns and ideas collect in an idea bank for the owner.

### 6. ServiceNow and DevOps: how BigHub should plug in

- **Macháň** informally owns ServiceNow and its processes in CZ (L1, plus Change Manager and Problem Manager). He hears of requests like "network access (prostupy) for Mertová's chatbots" arriving outside the standard path. Simona "tries to go around the standards", which "sometimes causes trouble" `[translated from Czech]`. He offered to explain the process (diagrams, network access, changes) early so BigHub doesn't struggle to push changes through later.
- **Jindřich**: today all BigHub infra requests go through Vladislav Tvarůžek by email. BigHub has no visibility and chases him every two days. Tvarůžek has discussed giving BigHub direct ServiceNow access. A home for the product backlog is also needed. BigHub has X-Manager as an option, since he saw ServiceNow as infra/technical only.
- **Macháň's proposed setup**:
  - BigHub gets **at least one resolver licence** and its **own resolver group/queue**.
  - Business service **"BigHub AI" already exists**. Macháň created it earlier, and it currently sits under Lukáš Szücs. **Offerings** go under it per app (e.g. "BigHub AI – Lexie", Maxie), which routes tickets to BigHub's queue and enables per-app reporting.
  - **SLAs** to agree. Tickets are worked in the queue and ideally moved into **Azure DevOps** for development.
  - **Changes**: publishing anything company-wide needs a ServiceNow change record, which BigHub can raise alone or with Macháň.
  - Reporting **dashboards** (SLA ticking, red items): the incident manager on his team can build them.
- **DevOps**: widely used at Dr. Max (Tvarůžek's team uses it, with fortnightly Thursday reviews). Míša Třísková introduced it and can set up a space. Honza Štangl also knows it. Some teams (e.g. Axapta) use Confluence. Jindřich: BigHub uses DevOps only for its own dev Kanban today. What's missing is where business owners like Macháň submit Lexie requests. **Macháň: that is solved by ServiceNow.**
- **Contacts**: Macháň for ServiceNow (access, resolver groups, explanation; he may delegate ticket/dashboard work to a colleague). Lukáš Szücs is a "hidden admin" with legacy rights (ServiceNow is now under BDC) and sits near Jindřich. Míša Třísková or Honza Štangl for DevOps.

### 7. Who owns the BigHub AI service

- **Macháň**: someone must pay for and approve it, and "I don't think Simona is right." The top owner must be **someone from IT**, because operations need an IT person. Mertová can keep her own piece as a smaller offering (e.g. Maxie) with manager/approver roles.
- **Jindřich agreed**: Mertová is business owner only because the first project started with her. As Lexie spreads to other departments, a different owner is needed. Macháň says this needs an internal IT discussion.

## Decisions Made

- Keeping Lexie's source documentation current is L1's responsibility. Old versions are not managed with a date convention (the current/archive folder split is the recommended approach).
- Lexie UX requests (split screen, jump to passage, input area, answer completeness) go to the product backlog. The Lexie owner (currently Mertová) decides whether to build them.
- Source-format and prompt-tuning questions go to Jura Brázdil for a technical answer.
- Direction (not final): Lexie/BigHub AI requests will come in through ServiceNow, with BigHub's own resolver group and an offering per app under the existing "BigHub AI" business service, flowing onward into Azure DevOps. Details at the follow-up meeting.

## Action Items

- [ ] **Jindřich Tůma**: Ask Jura Brázdil for technical answers for Macháň: best source format (Word/PDF vs. text/Markdown; are glossaries and date headers worth it), Markdown performing poorly, images not read — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Jindřich Tůma**: Check with Jura whether "highlight/jump to the matched passage in the source" already exists in a version and whether it is deployed — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Jindřich Tůma / Jura Brázdil**: Prompt Lexie so "contact/phone" returns all matching columns and so it flags or asks when several sources overlap (pharmacy-contacts Excel vs. Markdown vs. text) — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Jindřich Tůma**: Log Macháň's UX requests in the Lexie backlog for the owner's decision (split-screen source view, jump to passage, smaller/wider input area, fuller and consistent first answers) — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Petr Macháň**: Talk to Simona Mertová about the split-screen source view — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Petr Macháň**: Clean up L1's Lexie sources: remove duplicate copies (Excel + Markdown + text) and keep only current versions — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Jindřich Tůma / Petr Macháň**: Schedule a ServiceNow deep-dive this week (process, statuses, dashboards, access) — due week of 2026-10-19 — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Petr Macháň**: Set up ServiceNow access for BigHub, a BigHub resolver group/queue and offerings under the "BigHub AI" business service — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Jindřich Tůma**: Talk to Míša Třísková or Honza Štangl about whether Azure DevOps fits BigHub's product backlog — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake
- [ ] **Petr Macháň**: Raise the BigHub AI service ownership (IT owner instead of Mertová) internally in Dr. Max IT — from 2026-10-19-machan-l1-lexie-feedback-servicenow-intake

## Open Questions

- Who becomes the IT owner (payer/approver) of the "BigHub AI" ServiceNow service? Mertová keeps only a sub-offering?
- How do the ServiceNow intake, Mertová's X-Manager route ([[ASM-018]]) and BigHub's own DevOps Kanban fit together? Which one is the single front door?
- How many resolver licences does BigHub need, who pays for them, and what SLAs can BigHub commit to?
- Is the "jump to passage" feature already built but not deployed?
- 2027 initiatives for L1: not discussed. Follow up separately (department deadline 2026-10-23).

## Sentiment & Tone

Constructive and friendly. Macháň is an engaged power user who tested hard (he loaded the same data in three formats) and came prepared with examples. He is critical of answer quality but not negative about Lexie, and openly praises the fast refresh. The relational signal is his comment that Mertová goes around IT standards, together with his view that she shouldn't own the BigHub AI service. Jindřich agreed openly. This makes Macháň a likely ally for formalising BigHub's intake and infra path, but it is politically sensitive toward Mertová, so handle it carefully. Jindřich was visibly relieved to get a clear ServiceNow path ("a fog for us" `[translated from Czech]`). Marek contributed the current/archive folder recommendation.

## Routing Log

Confirmed by PM 2026-10-19 ("confirm all"):
- **project-assumptions**: added ASM-302 (Decided: L1 keeps sources current; current/archive folders), ASM-303 (Lexie UX requests), ASM-304 (prompt tuning for contacts/overlapping sources), ASM-305 (ServiceNow intake for BigHub AI), ASM-306 (IT owner for BigHub AI service). ASM-018 kept as is; the possible conflict is recorded in ASM-305.
- **project-stakeholders**: STK-069 (Macháň) updated; STK-018 merged into STK-069; STK-017 (Mertová) and STK-031 (Szücs) notes updated; added STK-077 (Míša Třísková) and STK-078 (Honza Štangl).
- **project-knowledge**: new entry "ServiceNow at Dr. Max (BigHub AI service)"; Lexie source-data facts added to Max / Maxie / Lexie; "Lexie users: L1 support" updated.
- **project-daily** (2026-10-19): 11 action items added (incl. Marek collecting L1's 2027 initiatives); Macháň meeting item marked done.
- **project-lessons**: LL-99 (auto).
