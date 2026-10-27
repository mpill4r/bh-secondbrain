---
last_updated: 2026-10-27
last_updated_by: manual — conversational
owner: Marek Pillár
---

# Product Requirements

## Product Requirements

**REQ-001** · Product · Open · 2026-10-05
**Source**: Petr Neuman via 2026-10-05-listing-neuman-environmental-claims-bulk-edit-listing-2-0

Listing (future / Listing 2.0): the business team can define a rule (terms to find, context that makes them relevant, replacement or edit instruction) and run it across the whole catalogue, then review the proposed changes against the original text before they are applied. Needed for recurring regulation-driven changes such as the EU environmental-claims rules (10,000+ SKUs) without the manual Magento export / Excel search and its false positives ([[ASM-244]]).

**REQ-003** · Product · Open · 2026-10-05
**Source**: Rudolf Žůrek via 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap

Reklamace email agent: track which supplier claim emails got no reply and send reminders, so the claims clerk no longer has to watch the mailbox. Can be algorithmic. See [[ASM-247]].

**REQ-004** · Product · Open · 2026-10-16
**Source**: Renata Švarcová via 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives

Lexie for accounting: every answer cites the source document (link) and the document's date, and Lexie answers only from the documents, never beyond them. See [[ASM-298]]. Update 2026-10-22: when Lexie finds nothing in the documents, it says so explicitly (Švarcová, 2026-10-22-svarcova-lexie-demo-sharepoint-upload-archive-tas5).

**REQ-005** · Product · Open · 2026-10-16
**Source**: Renata Švarcová via 2026-10-16-svarcova-brno-accounting-lexie-2027-initiatives

Lexie for accounting: Lexie may use archived directive/procedure versions, but must say explicitly that the content is archived and no longer valid. The "ISO standardní postupy" folder is excluded; current company-wide directives come from the intranet. See [[ASM-298]].

**REQ-006** · Product · Open · 2026-10-22
**Source**: CC team (Šárka Andělová) via 2026-10-22-lexie-max-maxie-weekly-sync

Lexie: admins can add temporary notes per department (e.g. a methodology change from a date, for a specific warehouse). Lexie treats them as priority over documents and says so explicitly in the answer; operators see the active notes as a list in the chat and can open attachments. Notes are removed once documents are updated. See [[ASM-334]].

**REQ-007** · Product · Open · 2026-10-22
**Source**: CC team (Šárka Andělová) via 2026-10-22-lexie-max-maxie-weekly-sync

Max: admins maintain a list of words Max must never use with customers (e.g. "skladovost", "pobočka"); Max rephrases instead. See [[ASM-332]].

**REQ-008** · Product · Open · 2026-10-23
**Source**: Petra Kytýrová / Jura Brázdil via 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova

Max: at the start of every conversation, show a clearly legible privacy sentence (incl. special categories) with a link to the chatbot privacy policy, in the empty chat background, separate from the bot's bubbles. Wording from Dr. Max's external lawyer. See [[ASM-341]].

**REQ-009** · Product · Open · 2026-10-23
**Source**: Simona Mertová via 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova

Max: store full conversations server-side for about 30 days for complaints and answer-quality checks, then delete or anonymise them; conversations can be handed to the CC operator system under a "chat" channel. Pending balancing test. See [[ASM-340]].

**REQ-010** · Product · Open · 2026-10-23
**Source**: Míra Švestka via 2026-10-23-max-chatbot-gdpr-legal-review-henychova-kytyrova

Max: show Legal's AI disclaimer (AI can make mistakes; verify the information). Wording from Dr. Max Legal. See [[ASM-343]].

**REQ-011** · Product · Open · 2026-10-23
**Source**: Petr Macháň (via Jindřich Tůma) via 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding

Lexie: next to each citation, show the exact sentence the answer is based on. Highlighting the passage inside the PDF is out for now (hard with chunks + thumbnails). See [[ASM-303]].

**REQ-012** · Product · Open · 2026-10-23
**Source**: Jindřich Tůma via 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding

Lexie: when two or more sources cover the same topic (duplicates or conflicting content), say so and ask which to use or show the differences, instead of silently picking one. See [[ASM-304]].

**REQ-015** · Product · Open · 2026-10-27
**Source**: Renata Švarcová (e-mail 2026-10-26), relayed by PM

Lexie: company-wide directives are read in place from the intranet SharePoint, not copied into the "Lexie" folder (copying would duplicate them and leave updates uncontrolled). Citations link to the intranet original; changed or deleted documents are picked up on sync. Depends on platform access to the intranet folders ([[ASM-346]]). Lexie board ticket 11.

**REQ-014** · Product · Open · 2026-10-26
**Source**: Marek Pillár / Filip Černý via 2026-10-26-listing-filip-supplements-batch-demo-export-plan

Listing: the export returns the client's input Excel filled in, with added or changed values highlighted, so it can be reviewed like in the app (old vs. new). See [[ASM-350]].

## Business Requirements

**REQ-002** · Business · Open · 2026-10-05
**Source**: Tereza Foltová via 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap

Reklamace: for defective medical devices, notify the actual manufacturer's factory (which can differ by batch) with a predefined email, in addition to the supplier. Dr. Max has no manufacturer database today. See [[ASM-251]].

## Data Requirements

**REQ-013** · Data · Open · 2026-10-23
**Source**: Jura Brázdil via 2026-10-23-lexie-departments-intake-sharepoint-access-satura-onboarding

Lexie sources: any text-representable format works (PDF, Word, Markdown, TXT, Excel, PowerPoint); text inside images isn't indexed, so images need a caption. See [[ASM-302]].

## Design Requirements

{Design-type requirements}

## Tech Requirements

{Tech-type requirements}

## Other Requirements

{Other-type requirements}

---

## Entry Format

```markdown
**REQ-NNN** · {Type} · {Status} [· high-priority] · {YYYY-MM-DD}
**Source**: {Person} via {artifact-slug}
[**Addressed in**: {product-scope-{slug}.md} or {FEAT-NNN-{slug}.md}]

{Requirement description — one paragraph, plain language. What the product must do and why.}
```
