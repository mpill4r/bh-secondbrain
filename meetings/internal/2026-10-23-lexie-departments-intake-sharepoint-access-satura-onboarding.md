---
last_updated: 2026-10-23
type: internal
attendees: [Jindřich Tůma, Jura Brázdil, Marek Pillár, Lukáš Šatura]
recording_link:
---

# Lexie Expansion to Departments — Request Intake, SharePoint Access Model & Lukáš Šatura Onboarding

**Date**: 2026-10-23 (Friday, ~53 min)
**Attendees**: Jindřich Tůma (BigHub, account lead), Jura Brázdil (BigHub, platform/Lexie developer), Marek Pillár (BigHub, PM), Lukáš Šatura (BigHub, new developer alongside Jura Brázdil and Filip Černý — first official meeting)
**Type**: internal
**Recording**: N/A
**Previous session**: N/A (follows the department meetings: [L1 / Macháň 10-19](../external/2026-10-19-machan-l1-lexie-feedback-servicenow-intake.md), [Legal / Svoboda 10-21](../external/2026-10-21-svoboda-legal-lexie-copilot-scraping-contract-headers.md), [Lexie weekly 10-22](../external/2026-10-22-lexie-max-maxie-weekly-sync.md), [Švarcová demo 10-22](../external/2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5.md))
**Meeting prep**: N/A

## TL;DR

BigHub-internal walkthrough of the "Lexie x Oddělení" sheet, department by department. Agreed: one Lexie board in Dr. Max's Azure DevOps for real feature work, labelled per department. The CC stays in X-Manager, and onboarding a department (e-mails + SharePoint folder → library + agent, ~5 minutes) isn't ticketed. The SharePoint access model is the open issue. Today departments copy files into one "Lexie" folder, which is a burden and goes stale. BigHub will offer Dr. Max three variants (Lexie folder / named folders / blanket access with file selection in the platform), but nobody knows who approves SharePoint access. Accounting can test from ~Monday on the test link; Lukáš Šatura starts at 0.5 FTE on TEO/OCR.

## Key Discussion Points

Transcript note: speaker labels are unreliable; many lines labelled "Jura Brázdil" are Marek (Slovak) or Jindřich. Attribution below follows content and language.

### Tracking Lexie requests

- Jindřich wants a place to log department requests now that L1 support is live. The only option is Dr. Max's Azure DevOps (the CC project there is empty because the CC uses X-Manager).
- Marek proposed one board for Lexie only, not split per department; Jindřich agreed: **one board, labels per department**. The CC stays in X-Manager. Jindřich creates the board; Marek fills it from the Excel and the L1 items.
- Jura also wants in-Lexie feedback later (like the Max chatbot), but explicit requests still go to tickets.
- Marek's "heretical" question: does onboarding a department need tickets at all? Jura: no — "send me four e-mails and say 'make this department'", five minutes. **Only real development (features) goes on the board**; onboarding needs e-mails + SharePoint folders. Goal: Marek, as super admin, onboards departments himself; the platform moves work "from code, deployment and provisioning into a click console" [translated from Czech] (Jura).
- Jura: features are **global**, not per department. Feature flags are possible, but he'd avoid building different products for different departments.

### Recurring questions → Q&A in platform docs

Jindřich expects the same questions in every department (best source format, which of several sources is right). Agreed to keep answers in a Q&A in the AI platform documentation (Jura: documentation exists, Q&A fits there), so BigHub can point people to it.

### Source formats

Jura: anything that can be represented as text is indexed — PDF, Word, Markdown, TXT, Excel, PowerPoint (IT's sources already mix docx, md, pptx, pdf, txt, xls). No format is faster or slower. **Images aren't indexed** — they need a caption. Describing images with a model would mean running every document through OCR, which is costly relative to indexing.

### SharePoint access model (main open issue)

- Today: Dr. Max created a "Lexie" folder in its SharePoint with one subfolder per department; Lexie indexes only that. Departments must copy documents in. Marek: unrealistic for Švarcová, who maintains many directives — after an update she must remember to re-upload, or Lexie answers from stale files. She also mentioned a shared drive.
- Jura: Lexie doesn't copy documents; it keeps a reference, the index (embeddings) and thumbnails. With wider rights, the platform could list everything and index on demand when someone first selects a file.
- Variants to present to Dr. Max (Jindřich: present them without long negotiation):
  1. The "Lexie" folder — departments put in what they want.
  2. Departments name the folders they want; Dr. Max grants the platform's managed identity access. New folders = a request to Dr. Max infra.
  3. Blanket SharePoint access for the platform's service identity; platform super admins choose which files may be used. Same precedent as user management, which Dr. Max accepted; "fits Dudaško's idea of the platform" [translated from Czech]. Needs development; possible security concern.
  - Also possible (Dr. Max side): a **one-way SharePoint sync** from a department's folder into the Lexie folder. Jura: "give us rights and we'll handle it" is fastest.
- **Approver unknown.** Technically trivial (Tvarůžek, or BDC via ticket), but BDC needs a "stamp" from someone. For user permissions it's ultimately Dudaško; for SharePoint nobody knows. Legal (Švestka, Svoboda) don't know their own SharePoint structure — Macháň manages it. Marek asks Macháň; Jura asks Tvarůžek.

### Accounting (Švarcová)

- For testing, accounting puts PDFs into its folder in the "Lexie" folder; Jura adds the users as platform admins, builds a library + agent, and they can test **from ~Monday**.
- Blocker: the platform still uses the old Lexie security group, so every former Lexie admin is a platform super admin. Tvarůžek must bind the security groups to the app before Jura sends invitations. Marek sends Jura the users' e-mails.
- **Test link, not production**: Jura isn't redeploying production while iterating; test has the newest features. As admins they'll see Lexie and Lexie Next and the whole Lexie row (reporting, documentation, technical status).
- Links: the platform currently borrows Lexie's registered URLs (hence "Lexie test/platform"); after next week's production switch links return to the original production URLs.
- Jura sent Marek the SharePoint link to the Lexie folder; Marek isn't sure his account has access (two accounts). Lukáš Szücs hasn't arranged BigHub access to the intranet folders yet.
- Marek asked for a ~20-minute walkthrough so he can set up departments himself; Jura first wants to simplify the library/knowledge-base UI ("not final yet").

### CC front / back office

The CC wants two roles with two knowledge bases (one sees both, one only back office). Covered by libraries: a back-office library switched **off by default** that operators can turn on. Marek checks the methodologies the CC put in X-Manager and maps the overlap with the CC.

### L1 support (Macháň)

- Marek replies to Macháň by e-mail: formats don't matter; images need captions; the "which document is current" rule is theirs (BigHub recommends current vs. archive folders).
- Jura already **deduplicated** in the new Lexie Next engine (identical documents filled the top results; the indexer now shows one). He can apply rules Dr. Max defines (e.g. "prefer the newer document"), but can't guarantee currency.
- **Passage highlighting**: Jura parked it. Showing the exact supporting sentence next to the citation is feasible (one extra model call). Highlighting the location inside the PDF is hard: answers come from chunks, the viewer runs on thumbnails, and the location would have to be reconstructed. → backlog.
- **Split-screen source view**: a global feature, not a department one → backlog, owner decision.
- **Duplicate/conflicting sources** (Jindřich): Lexie should say "careful, two sources". Jura: partly does it already (e.g. "change of delivery address" → asks which delivery type, links three PDFs); needs a concrete failing example → backlog ticket.
- **Pharmacy-contacts Excel**: Lexie returned only some contacts until asked for "all". That contact data was duplicated ~100× across Excel/Markdown/text. Jura rebuilt the engine (benchmarked against Viliam Gago's version) and will retest on Lexie Next; Marek tells Macháň to retry → small ticket.
- **Input box overlapping text**: bug in the old production Lexie; Lexie Next (new frontend, no framework dependencies) fixes it in the next release.
- **Wider input box**: Jindřich questioned the narrow strip; compared with ChatGPT (same layout) → low priority, no change.
- Jura's direction: **reusable platform tools** — e.g. Lexie should read pharmacy contacts from the live pharmacy API (as Max/MaxBuddy do), not from PDFs; same for eRecepty, SPC and SPC changes.

### Legal, pharmacies, acquisitions, TAS

- **Legal**: typical Lexie case (non-sensitive, well-versioned PDFs on SharePoint; testing Copilot). Marek's next step: confirm they can send SharePoint links; same process as accounting. Two further initiatives (SÚKL scraping, marketing materials) are a separate discussion.
- **Lexie for pharmacies**: the CC liked the idea; go to Vosmek → backlog (Jindřich didn't remember the agreement).
- **Acquisitions (Šišo)**: no reply on Teams since the meeting; Marek handles it.
- **TAS**: conflicting signals (Copilot will connect to TAS vs. TAS gets its own agent); everyone agrees it's been promised for months and isn't there. Don't build on TAS now; at most a low-priority opportunity, possibly to discuss with Dudaško.

### Lukáš Šatura onboarding

- First official meeting; ~0.5 FTE to start on **TEO/OCR** (he also has another ~0.5 FTE project).
- Jura asked Tvarůžek for Lukáš's Dr. Max identity/e-mail (~14 days typical); repo access only after that. Today Jura sends a self-contained zip: cleaned-up OCR code (engine, inputs/outputs), documentation and session logs.
- "DevOps" here means Dr. Max's Azure DevOps (ticketing), not BigHub's.
- Jindřich: no pressure; plenty of OCR work. He adds Lukáš to Easy Project for time reporting (search "Lexie", "OCR").

## Decisions Made

- One Lexie board in Dr. Max's Azure DevOps, labels per department; the CC stays in X-Manager. Jindřich creates it, Marek fills it.
- Department onboarding (users + SharePoint folder → library + agent) is not ticketed; only feature development is.
- Lexie features are built globally, not per department (avoid per-department variants).
- Recurring source questions get a Q&A in the AI platform documentation.
- Present Dr. Max three SharePoint access variants (Lexie folder / named folders / blanket access + platform file selection); "give us rights" preferred.
- Accounting tests on the test link (newest features), not production.
- TAS: don't build anything on it for now; low-priority opportunity at most.

## Action Items

- [ ] **Jindřich Tůma**: Create the Lexie board in Dr. Max's Azure DevOps (labels per department) and send it to Marek — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: Fill the Lexie board with feature items from the "Lexie x Oddělení" sheet and L1 (passage highlighting, split-screen view, duplicate-source warning, contacts retest, input bug, wider input — low) — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: E-mail Petr Macháň the technical answers (any text format; images need captions; version rule is theirs — current vs. archive folders; duplicates handled in Lexie Next; retry the contacts question) — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: Ask Petr Macháň who approves SharePoint access for the platform identity — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jura Brázdil**: Ask Vladislav Tvarůžek about SharePoint access for the platform identity / one-way sync and who must approve — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: Send Jura the accounting users' e-mails — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jura Brázdil**: Get Tvarůžek to bind the security groups to the platform app; then add accounting as admins, build the library + agent and send the test link — due ~2026-10-26 — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: Check his access to the SharePoint "Lexie" site (two accounts) — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jura Brázdil**: Give Marek a ~20-min walkthrough of department setup (after simplifying the library UI) — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: Review the CC methodologies in X-Manager and map the front/back-office overlap with the CC — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Marek Pillár**: Legal — confirm they can send SharePoint links/storage details; same process as accounting — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jura Brázdil**: Retest the pharmacy-contacts question on Lexie Next — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jura Brázdil**: Add a Q&A on sources (formats, images, versions) to the platform documentation — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jura Brázdil**: Send Lukáš Šatura the zipped OCR code, docs and session logs — due 2026-10-23 — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding
- [ ] **Jindřich Tůma**: Add Lukáš Šatura to Easy Project (Dr. Max projects) — due 2026-10-23 — from 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding

## Open Questions

- Who at Dr. Max approves SharePoint access for the platform identity (folder owner, Macháň, BDC, Dudaško)?
- Which variant will Dr. Max accept — and is blanket access a security issue for them?
- Does Švarcová's shared drive (S:) content need to reach Lexie, or does she move it to SharePoint? (10-22: she uploads to the Lexie folder.)
- Can Švarcová write to the Lexie folder herself, or must files go via BigHub?

## Sentiment & Tone

Relaxed and productive; Friday team call. Jura praised Marek's department sheet ("absolute bomb"). Light friction on process: Marek pushed back on ticketing trivial onboarding, and Jura agreed. Jura is confident and opinionated on platform direction (global features, reusable tools, admin-console instead of provisioning). Real frustration is with Dr. Max access bureaucracy (security groups, unknown SharePoint approver), not within the team. Lukáš engaged and keen for material.

## Routing Log

Confirmed by PM (2026-10-23, "confirm all"; Lukáš Šatura = STK-060, new developer alongside Jura and Filip):

- **project-assumptions**: added ASM-344 (Lexie board), ASM-345 (global features), ASM-346 (SharePoint access model), ASM-347 (reusable platform tools), ASM-348 (TAS deprioritised); updated ASM-299, ASM-302, ASM-303, ASM-304, ASM-305, ASM-337, ASM-338.
- **product-requirements**: added REQ-011, REQ-012, REQ-013.
- **project-stakeholders**: STK-060 named Lukáš Šatura; updated STK-026, STK-003, STK-069, STK-061, STK-016, STK-063.
- **project-knowledge**: Lexie indexing and platform access; Easy Project.
- **project-daily**: 15 action items added; 3 closed; 8 annotated (Ilík/TAS kept open, deprioritised).
- **project-lessons**: LL-109.
