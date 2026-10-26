---
last_updated: 2026-10-22
type: external
attendees: [Renata Švarcová, Jura Brázdil, Marek Pillár]
recording_link:
---

# Brno Accounting (Švarcová) — Lexie Demo, Documents Go to SharePoint, Archive Handling & No New Initiatives Until New Systems

**Date**: 2026-10-22, 14:00
**Attendees**: Renata Švarcová (Dr. Max CZE, Brno accounting, STK-063), Jura Brázdil (BigHub, developer, demo), Marek Pillár (BigHub, PM). Jindřich Tůma had a clash; Simona Vaxmonská not present.
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives](2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives.md)
**Meeting prep**: [2026-10-22-svarcova-uctaren-lexie-lekarne-2027-meeting-prep](../prep/2026-10-22-svarcova-uctaren-lexie-lekarne-2027-meeting-prep.md)

> **Transcript note**: "pán Sigeč" = Lukáš Szücs; "paní Mertlová" and "Simona" (CC documents) = Simona Mertová; "Machaň" = Petr Macháň; "Benefit" = the accounting system; "Šimon Ilík" (BDC, TAS owner) was heard on 10-16 as "simona Ilík".

## TL;DR

Jura demoed Lexie on the AI Platform and Švarcová left happy ("we're looking forward to Lexie" `[translated from Czech]`). The demo covered:
- the user chat
- knowledge bases with their own prompts and libraries
- the admin view (technical status, documentation, reporting, settings)
- the yellow broadcast bar

**Sources**: Švarcová has sent Marek links to three intranet SharePoint folders. BigHub still has **no access**; the request runs via Szücs. Her own S: drive documents won't be connected. Instead she **uploads them into the SharePoint "Lexie" folder** for accounting, with her own subfolders and an archive subfolder. Jura sends her the link and requests platform access for her today. BigHub configures everything; she provides users and admins and joins the testing. She wants the intranet directives and CC how-tos available to **pharmacies** too. **No new 2027 initiatives**: her team is buried in a financial audit, an IT audit and the Deloitte review, and is waiting for TAS 5 and the cloud version of Benefit. Lexie is her only ask.

## Continuity (vs. 2026-10-16)

- **Done**: she sent the intranet SharePoint links (3 folders) to Marek.
- **Done**: she decided where her documents go: S: drive content is uploaded to SharePoint; TAS stays out.
- **Done**: her answer rules were confirmed: answers only from documents, says so when nothing is found, always cites the source (REQ-004).
- **Closed**: her 3–4 initiative candidates. None for now (audits, Deloitte, systems change).
- **Open**: BigHub's access to the intranet folders. Szücs hasn't arranged it; Marek pings him or requests access directly.
- **Open**: archive handling (REQ-005); Jura is designing it.
- **Open**: Lexie for pharmacies (Jindřich → Vosmek).
- **Not covered**: the file-transfer monitoring numbers (backlog row), users count, test questions.

## Key Discussion Points

### 1. Sources: intranet + her own documents

- **Marek**: BigHub hasn't got access to the SharePoint documents yet; the request went via Szücs. Lexie works the same as elsewhere: a place with documents, a definition of what to use and ignore, then tuning through testing. Lexie cites sources and links to them.
- **Švarcová**: she sent links to **three intranet SharePoint folders**: company-wide directives for Česká lékárna Holding and CC documents for pharmacies (e.g. how to receive an e-shop parcel), among others. She wants these for accounting and **for pharmacies**, who ask accounting, the IT helpdesk and the CC basic questions they need once a year. On top, a set of **accounting-only** documents: her directives and procedures (e.g. entering a partner in Benefit, making a credit note), today on the S: drive.
- **S: drive (Jura)**: connecting a shared drive is possible if Dr. Max infra allows it. The free option is to put the documents into the SharePoint folder Lexie already reads. **Agreed**: Švarcová uploads them there; Jura sends her the link today. Marek: local drives instead of SharePoint come up in several departments.
- **Structure**: subfolders are fine; the platform shows exactly the SharePoint structure. **Švarcová manages her own folder structure**, so Marek goes to her with questions (unlike the intranet, which Macháň owns).

### 2. Demo: Lexie on the AI Platform

- **User view**: one big chat window. Conversation history sits on the left. A department switcher appears only with more than one department. Knowledge bases ("agents") differ in prompt and source files; active sources show on the right and can be narrowed.
- **Libraries**: sets of documents shared across departments, on or off by default per agent ([[ASM-333]]). Švarcová can have a shared library (intranet directives, also for others) and an accounting-only one.
- **Platform view**: all BigHub apps for Dr. Max will be registered here. As a **Lexie admin** she'll see the tiles:
  - technical status
  - always-current documentation
  - reporting: what to track is up to them, e.g. conversations per department
  - settings: libraries, knowledge bases with instructions, model choice and assigned libraries
  - a **broadcast message**: a yellow bar for all users
- **Indexing**: Lexie reads one SharePoint folder named "Lexie", with subfolders CC source documents, e-commerce, finance Brno, HR, IT, online marketing and legal; some are empty. It **indexes every morning**. Adding a folder means asking Dr. Max infra to grant Lexie access.
- **Visibility**: admins of every department see all documents in the admin view; users see only theirs. **Švarcová: fine, "nothing secret"** `[translated from Czech]`.
- **Effort on her side (Jura, Marek)**: BigHub sets everything up. She provides a **list of users and a list of admins**, arranges document access and joins the **testing**. Testing works with "**golden conversations**": expected answers, positive and negative cases from feedback, used to tune the search engine. The CC has used it for over half a year, and quality improves with feedback.
- The CC still runs on the **old Lexie until next week**. Jura showed it: slower, but the sources can be opened.
- Model: currently GPT-5.4, moving to Luna (better, cheaper). Harder questions that need reasoning cost more.
- **Her expectations**: like ChatGPT, but working **only over the documents**, never going elsewhere, not inventing anything, and **saying when it finds nothing**. Jura: same as for the CC; every answer comes with citations.
- **Marek on Copilot**: Lexie is platform-based and secure, nothing leaves, access is controlled by roles, and answers are consistent across colleagues, unlike ChatGPT / Copilot ([[ASM-329]]).
- Jura mentioned the CC's temporary-notes request ([[ASM-334]]) as an example of what Copilot can't do. Further wishes are welcome; it's long-term development.

### 3. File formats

- Mostly **PDF with a text layer** (Word saved as PDF, not scans), some **Excel**, and some Word guides with **screenshots**. No standalone images.
- Jura: fully scanned PDFs (images only) aren't indexed. Not an issue here.

### 4. TAS

- In scope now: **SharePoint only** (and at most the shared drive). TAS stays out ([[ASM-299]]).
- **Švarcová**: per **Šimon Ilík (BDC, TAS owner)**, **TAS 5** will be able to connect to AI, but will likely **use Dr. Max's own AI models**, not carry built-in AI. This differs from Legal's account (a TAS 5 AI agent promised for ~1.5 years). She suggested BigHub **meet Ilík at BDC**.

### 5. Archive and old versions

- **Švarcová**: she'll keep an **archive subfolder** with older versions, since she sometimes needs them, but Lexie must warn her emphatically when information comes from the archive (REQ-005).
- **Jura**: archives add noise to indexing. Options:
  - (a) a separate **archive library**, switched on deliberately
  - (b) a **per-folder / per-file comment for Lexie** in settings, e.g. "archived, no longer valid"

  He'll think it through; it is solvable.

### 6. Sensitive data

- None. Only procedures and directives; accounting handles no birth numbers or prescription numbers.

### 7. Lexie for pharmacies and 2027 initiatives

- Lexie for pharmacies is still on BigHub's list (Jindřich → Vosmek); it overlaps with the intranet documents she wants pharmacies to reach.
- **2027 initiatives**: her team is overloaded with a financial audit, an IT audit and Deloitte's process review (with an automation angle). Anything now is premature: they wait for **TAS 5** and the **cloud version of Benefit**. Building on the old versions "makes no sense" `[translated from Czech]`; they'll also see what Deloitte finds. **Lexie is the only thing**: "a lovely task for AI… the effect will be immediate" `[translated from Czech]`.

## Decisions Made

- **Accounting documents go into the SharePoint "Lexie" folder** (Švarcová uploads, own subfolders incl. archive); the S: drive is not connected.
- **Intranet directives** (3 folders) are sources once BigHub has access; the shared library may later serve pharmacies too.
- **BigHub configures** libraries, knowledge base, users and admins; Švarcová provides user/admin lists and joins testing.
- **Other departments' admins seeing accounting documents is fine.**
- **TAS out of scope**; meet Ilík (BDC) on TAS 5 separately.
- **No further 2027 initiatives from accounting for now.**

## Action Items

- [ ] **Jura Brázdil**: Send Švarcová the link to the accounting folder in the SharePoint "Lexie" folder and request Entra / platform access for her e-mail — due 2026-10-22 — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5
- [ ] **Renata Švarcová**: Upload her internal directives and procedures into the SharePoint folder (subfolders, archive subfolder) — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5
- [ ] **Renata Švarcová**: Send the list of Lexie users and admins for accounting — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5
- [ ] **Marek Pillár**: Ping Lukáš Szücs about access to the three intranet folders, or request access directly in SharePoint — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5
- [ ] **Jura Brázdil / Marek Pillár**: Set up the accounting library + knowledge base once documents are in; run testing with Švarcová (golden conversations / test questions) — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5
- [ ] **Jura Brázdil**: Design archive handling (separate archive library vs. per-folder/file comment for Lexie) with an emphatic "from archive" warning — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5
- [ ] **Marek Pillár**: Arrange a meeting with Šimon Ilík (BDC) on TAS 5 and its AI connection — from 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5

## Open Questions

- When does BigHub get access to the three intranet folders?
- How many accounting users and admins?
- TAS 5: own AI agent (Legal) or a connector to Dr. Max's models (Ilík via Švarcová)?
- Who owns Lexie for pharmacies, and do the intranet directives become a shared library for them?
- Is the file-transfer monitoring row (2027 backlog) still alive, given "nothing until the new systems"?

## Sentiment & Tone

Warm and positive, a clear improvement on 10-16's guarded skepticism. The concrete demo answered her trust questions (citations, documents only, roles), she asked practical questions (diacritics, subfolders, formats) and volunteered to upload documents the same day. She is firm that nothing else makes sense before the new TAS and Benefit versions, and her team is overloaded (audits, Deloitte). Lexie is now a welcome quick win for her, not a push from BigHub.

## Routing Log

Confirmed by PM 2026-10-22 ("confirm"):
- **project-assumptions**: updated ASM-298, ASM-299, ASM-300, ASM-301; added ASM-338 (documents into the SharePoint "Lexie" folder), ASM-339 (archive handling).
- **product-requirements**: REQ-004 updated.
- **project-stakeholders**: STK-063 Švarcová, STK-012 Szücs, STK-069 Macháň; added STK-086 Šimon Ilík.
- **project-knowledge**: Lexie sources on SharePoint; TAS 5 (accounting view).
- **2027 backlog** (OneDrive): backlog N8 and Lexie sheet (Účtárna Brno, Lékárny) updated.
- **project-daily** (2026-10-22): 7 items added, 4 closed, 2 annotated.
