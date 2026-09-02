# project-document — Skill Logic

> The document intelligence skill. Ingests any document — text, visual, or structured data — into the harness, produces an adaptive summary, and presents a routing plan for PM review and confirmation before writing to harness artifacts.

---

## When This Skill Runs

This skill runs when the PM invokes `/project-document` with any document input.

---

## A. Accept Input

Accept any of the following as input:
- File path to `.pdf` / `.docx` / `.txt` / `.rtf` / `.md` / `.csv` / `.xlsx` / `.png` / `.jpg` / `.svg`
- Pasted text content
- FigJam board URL (via Figma MCP)
- Figma design file URL (via Figma MCP)

Auto-detect input type and adapt processing:

- **Text files** (TXT, MD, DOCX): Read and process as text. For `.rtf` files, strip RTF formatting codes before processing — extract plain text only.
- **PDF files**: Use PyMuPDF (`fitz`) as the primary text extraction tool — it handles both text-based and scanned PDFs reliably. Fall back to Claude's native visual PDF reading for pages where text extraction quality is poor.
- **Images** (PNG, JPG, SVG): Read visually, describe content, produce summary.
- **Spreadsheets** (CSV, XLSX): Summarize structure (columns, row count, data types) and key content. Do not reproduce the full dataset — focus on what's useful for project context.
- **FigJam boards**: Try `get_figjam` first (extracts text content). If it fails or hangs, fall back to `get_screenshot` (visual read). If the screenshot resolution is too low to read details, ask PM to provide closer screenshots of specific sections or paste the key content as text.
- **Figma design files**: Read via Figma MCP (`get_screenshot` + `get_design_context`). If MCP not active, ask PM for exported screenshots.
- **PDFs with visual content** (slide decks, scanned documents): Read pages visually. If text extraction quality is uncertain, flag it to PM: "This appears to be a scanned document. I can read it visually but some details may be imprecise — please verify key figures and dates."
- **Diagrams and charts**: Describe structurally — what connects to what, what flows where, what the relationships are.
- **Password-protected or encrypted files**: Inform PM the file cannot be read and ask for an unprotected version or pasted content.

### A1. Language Handling

All document summaries and routed harness content are always written in English regardless of the source document language. Process the document in its original language and produce all outputs in English. Direct quotes from non-English documents are translated and marked `[translated from {language}]`.

---

## B. Read Bootstrap Context

Before processing, silently read:
- `documents/index.md` — for duplicate/version detection
- `project/management/project-stakeholders.md` — for cross-referencing extracted names
- Any `product/solution-space/product-scope-*.md` files — for feature/epic awareness
- `product/problem-space/product-brief.md` — for strategic framing

If any of these files do not exist, skip silently and proceed without that context.

### B1. Duplicate/Version Detection

Check `documents/index.md` for a match by filename, title, or content similarity. If a match is found, inform PM: "This appears to be an updated version of {previous document}. Process as update or new document?"

If PM says "update", the flow adapts:
- Create a new summary file and link it to the previous version in Document Info.
- Add a "Changes from previous version" subsection highlighting what changed.
- The routing review only includes net-new or changed items — previously routed content is not re-routed unless it changed.

---

## C. Clarification Q&A

After reading and understanding the document, run a clarification Q&A with the PM. This is not just about classification — it's about ensuring correct understanding.

1. Always confirm: proposed classification and source category (internal / client / external).
2. Beyond that, only ask if there's genuinely something to clarify — ambiguous content, unclear purpose, contradictions. A clear, straightforward document needs only classification and source confirmation. A complex or ambiguous document gets deeper questions.
3. If the document appears to relate to a different project or engagement, clarify with PM: is this for the current project, a prospect, or reference material? A document about a different project may still have routable insights but should not update project-specific artifacts.
4. If anything is ambiguous, contradictory, or unclear, ask about it. Always prefer asking over assuming incorrect information. But do not manufacture questions — if the document is clear, move on quickly.

The Q&A should be conversational and grouped — not a rigid form.

### Classification Values

| Classification | Description |
|----------------|-------------|
| SoW / Proposal | Statement of work, proposal, service agreement, engagement offer |
| Contract | Signed contract, NDA, legal agreement, licensing terms |
| PRD / Requirements | Product requirements document, feature spec, brief |
| Research | Market research, user research, competitive analysis |
| Design | Design spec, brand guidelines, wireframes, mockups, UI screenshots |
| Technical | Architecture doc, API spec, integration guide, system documentation |
| Commercial | Pricing sheet, rate card, invoice, budget, financial model |
| Strategy | Business plan, company strategy, roadmap, vision document |
| Presentation | Slide deck, pitch deck, workshop output |
| Other | Anything that doesn't fit — ask PM for guidance |

Classification is a frontmatter tag — it does not determine folder structure.

---

## D. Write Summary

Produce a structured summary following the template. Write to `documents/{source}/{YYYY-MM-DD}-{document-title-slug}.md`. The date is the ingestion date, not the document's own date. If the `documents/{source}/` subfolder does not exist, create it before writing.

The slug is derived from the title and ingestion date. If the title is unclear, ask during Q&A. The slug must be descriptive — `2026-04-02-rivelo-sow-v1.md` not `2026-04-02-document.md`.

The sections are the default structure. Adapt based on document length and type:
- Short documents (emails, memos) use a compressed structure — not all 9 sections needed.
- Long documents (50+ pages) focus on executive summary and key extractions rather than section-by-section breakdown. Process the full document without truncation.
- Visual documents adapt further — diagrams get structural descriptions, mockups capture UI decisions, slides extract narrative and key takeaways.

Section-specific requirements:

- **Executive Summary**: 3-5 sentences max. Answer: what is this document, what does it say that matters, and what should the project team do with it.
- **Key Points**: Adaptive depth based on document type and length.
- **Extracted Requirements**: Pull out anything that reads as a requirement, constraint, success criterion, or acceptance criterion. Tag each with a document-local ID (DR-1, DR-2) and source reference (page/section if available). These IDs are for summary readability only — when routed, items get the target artifact's ID convention.
- **Extracted Decisions & Assumptions**: Decisions stated or implied, assumptions made. Tag with document-local IDs (DA-1, DA-2) and source references.
- **Key Stakeholders & Contacts**: People mentioned with roles. Report which are new vs. already in `project-stakeholders.md` (e.g. "3 new stakeholders, 4 already in project-stakeholders.md").
- **Open Questions**: Ambiguities, contradictions, or gaps within the document itself. Conflicts with existing harness content are detected during routing (Section E).
- **Routing Log**: Written after PM confirms routing review — includes ID mappings (DR-1→REQ-048, DA-1→ASM-012).

---

## E. Routing Review

After writing the summary, extract all routing candidates and present them to the PM as a structured review list grouped by artifact.

Read `.claude/harness-artifacts-index.md` and assess every registered artifact. Any artifact where relevant content was found — per the routing conditions defined in the index — is included in the routing review. Routing targets are determined by the index — not hardcoded.

While preparing routing candidates, read each target artifact and flag contradictions between the document content and the artifact's current state (e.g. "This SoW states delivery in Q3, but `project-overview` currently shows Q2 — which is correct?"). PM resolves conflicts during the review.

**Product artifact routing classification**: Use the bootstrap context (product-brief, product-scope) to classify candidates:
- **Problem framing, personas, goals, competitive insights, solution direction** → `product-brief` (strategic level)
- **Epic decisions, feature identification, priority shifts, timeline changes, estimation, deferrals** → `product-scope` (delivery planning level)
- **Acceptance criteria, edge cases, UX flows, design decisions for a specific feature** → `product-feature` (implementation detail level — must reference a FEAT-NNN)
- **Raw requirements, constraints, success criteria** → `product-requirements` (capture level)

When content could route to multiple product artifacts, route to each appropriate target — PM confirms per artifact.

The PM can reply "confirm all", skip individual items, or adjust content before anything is written. PM can adjust routing candidates inline in conversation — they type the corrected content and the skill applies it before writing.

If a routing target artifact does not exist, create it by reading the target skill's TEMPLATE.md (at `.claude/skills/{owner-skill}/TEMPLATE.md`) and using it as the scaffold — this ensures correct frontmatter, section structure, and entry format from the start.

If nothing in the document is routable (e.g. a reference diagram with no decisions or requirements), note this, write the summary and index entry, and skip the routing review.

---

## F. After Routing Confirmation

1. Write approved items to harness artifacts. Before writing to any target artifact:
   - **Read the target's TEMPLATE.md** (at `.claude/skills/{owner-skill}/TEMPLATE.md`) to learn the prescribed entry format and section structure.
   - **Conform routed content to that format exactly** — use the template's field names, layout, and conventions. Do not invent table structures, add fields, or use conventions (like MoSCoW priority) that the template doesn't define.
   - **Continue the artifact's ID sequence** — scan the existing artifact for the last used ID (e.g., REQ-047, ASM-012, LL-005) and increment for each new entry.
   - **Place entries in the correct section** — sectioned artifacts (e.g., product-requirements has Product / Business / Data / Design / Tech / Other sections) require entries under the matching section heading, not appended at the end.
   - **Update index tables** — if the template defines an index table (e.g., project-assumptions has an Index table at the top), add a row for each new entry.
2. Write the Routing Log section in the document summary (including ID mappings: DR-1→REQ-048, DA-1→ASM-012).
3. Silently log audit entries to today's `project-daily` — one entry per target artifact using the canonical format: `[AUTO] {target-artifact} — {what changed} from {document-slug} ({date})`. If `project-daily` does not exist, create it first. Audit entries are automatic bookkeeping after confirmation — they are not part of the routing review.
4. Silently trigger `project-lessons` — the skill reviews the full document summary for generalizable insights and writes any lessons autonomously. Before writing, read `.claude/skills/project-lessons/TEMPLATE.md` for the LL-NNN entry format and continue the existing ID sequence. Particularly valuable for retrospective summaries, post-mortem reports, workshop outputs, and lessons-learned documents. This is not part of the routing review and requires no PM confirmation.

---

## G. Document Index

Every ingested document is added to `documents/index.md` with: ingestion date, title, source (internal/client/external), classification tag, summary file link, executive summary excerpt (first 2 sentences), original location reference. If `documents/index.md` does not exist, create it with appropriate headers before adding the first entry.

---

## Rules

- **Original files never stored**: The summary includes a source location reference (file path, URL, or description). Original files are never committed to the harness repo.
- **Any input quality accepted**: Clean docs, messy scans, partial content, blurry screenshots — never refuse to process. Work with what's available and mark gaps explicitly.
- **Human-readable summaries**: Document summaries should make sense to someone who hasn't read the original.
- **PM confirms all routing**: Nothing is written to harness artifacts until PM explicitly confirms. The review step is lightweight — PM can confirm all at once — but nothing is committed without approval.
- **Routing targets from index**: Read `.claude/harness-artifacts-index.md` to determine routing targets — never hardcode artifact lists.
- **Audit entries are automatic**: After PM confirms routing, audit entries are silently logged to `project-daily`. No additional confirmation needed.
- **Classification confirmed by PM**: Always confirm the proposed classification and source during Q&A.
- **`harness-artifacts-index.md` missing**: Configuration error. Notify PM that the index is missing — routing is blocked. The document summary is still written, but routing cannot proceed until the index is restored.
- **`documents/index.md` missing**: Create it with appropriate headers before adding the first entry.
- **English output**: All outputs (summary, routing candidates, routed content) are always in English regardless of source language.
- **Descriptive slugs**: `2026-04-02-rivelo-sow-v1.md` not `2026-04-02-document.md`.
- **Conflicts flagged during routing**: Contradictions between document content and existing harness state are flagged in the routing review with specific details. PM resolves before writing.
- **Versioned documents link to previous**: Updated versions reference the previous summary and only route changes.
- **Adaptive depth**: Structure serves the content — short docs get compressed treatment, long docs get focused extraction, visual docs get structural descriptions.
- **Preserve existing content**: When writing routed content to harness artifacts, preserve all existing content exactly. Only add or update targeted entries.
- **Respect target artifact entry format**: Before writing to any artifact, read its owning skill's TEMPLATE.md (at `.claude/skills/{owner-skill}/TEMPLATE.md`) for the prescribed entry format. Use that format exactly — do not invent table structures, add fields, or use conventions the template doesn't define. The TEMPLATE.md is the authoritative format source.
- **Preserve content richness**: When routing content from a pre-structured document to a harness artifact, preserve the full richness of the source content. Do not summarize, truncate, or simplify multi-sentence descriptions, rich table entries, or structured data unless the target artifact's format explicitly requires compression.
