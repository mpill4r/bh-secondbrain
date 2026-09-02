# product-slidedeck — Skill Logic

> Create slide deck specifications for client and internal presentations. The skill produces a `slidedeck-{slug}.md` brief — a structured markdown file that specifies every slide's content, layout mode, and component composition. This brief is the input for Claude Design (or any design agent) rendering against the house slide master (`DESIGN-SYSTEM.md`). The contract: a brief written by this skill, handed to a design agent following the master spec, produces a deck that needs zero "fix the layout" iterations.

---

## When This Skill Runs

- **PM invokes `/product-slidedeck`** → Create (Section A), Update (Section B), or Review (Section C)

---

## A. Creation Mode

### A1. Load Context

Read the following artifacts for project context (skip silently if any don't exist):

- `product/problem-space/product-brief.md` — problem framing, personas, solution direction
- `product/solution-space/product-scope-*.md` — delivery scope, features, phases
- `project/management/project-overview.md` — project context, goals, timeline
- `project/management/client-overview.md` — client intelligence, strategic priorities
- `project/management/project-stakeholders.md` — who the audience is
- `project/management/project-knowledge.md` — domain terminology, key concepts
- Read `.claude/harness-artifacts-index.md` and load any additional artifacts whose conditions match.

Also read:
- `.claude/skills/product-slidedeck/DESIGN-SYSTEM.md` — the house slide master spec (§5 peer-block types, §9 component patterns). Read this to understand what visual components are available and suggest appropriate layouts. **Never dictate visual properties in the brief** — the design agent owns pixel sizes, paddings, colors, fills. The brief specifies content and component roles only.
- `.claude/skills/product-slidedeck/TEMPLATE.md` — the output format for the brief.

### A2. Mode Detection

- If PM provides a **file path** to an existing `slidedeck-*.md` → **UPDATE** mode (Section B).
- If PM says **"review"** and references an existing file → **REVIEW** mode (Section C).
- Otherwise → **CREATE** mode. Continue below.

### A3. Deck Planning

#### A3.1 Understand the deck

Ask the PM (batch up to 4 questions per round, 1-2 rounds max):

1. **Deck purpose** — what is this deck for? (proposal, demo/deliverable, internal review, marketing/leave-behind, other)
2. **Audience** — who will read/watch this? (client CxO, client technical, internal team, external partner, mixed)
3. **Key message** — what is the single most important takeaway?
4. **Slide count target** — how many slides? (suggest a range based on deck type if PM is unsure)

If the harness has sufficient context (product-brief exists, scope exists, stakeholders identified), auto-populate recommendations for questions 1-3 and present them for confirmation rather than asking open-ended.

#### A3.2 Suggest slide sequence

Based on deck type, suggest an archetype slide sequence. Present it as a numbered list with slide types and one-line descriptions. PM confirms, adjusts, adds, or removes slides.

**Deck-type archetypes:**

**Proposal** (~14-20 slides):
```
1.  Cover
2.  Introduction — context recap + what's next (where we are / where we're going)
3.  TOC divider — first section highlighted
4-5. Section 1 content slides (overview + detail/activities)
6.  TOC divider — second section highlighted
7-8. Section 2 content slides
9.  TOC divider — third section highlighted
10-12. Section 3 content slides (may need more for methodology/evidence)
13. TOC divider — summary highlighted
14. Summary timeline (Gantt)
15. Deliverables & pricing
16. Next steps
17. Closing
```

**Demo / deliverable** (~10-15 slides):
```
1.  Cover
2.  Agenda / TOC
3.  Context recap (problem + goals)
4-8. Solution / demo slides (findings, results, architecture, etc.)
9.  Key metrics / outcomes
10. Recommendations / next steps
11. Closing
```

**Internal review** (~8-12 slides):
```
1.  Cover
2.  Status overview (RAG, timeline, key metrics)
3-6. Topic slides (findings, decisions, blockers)
7.  Open questions / decisions needed
8.  Next steps / action items
9.  Closing
```

**Marketing / leave-behind** (~10-14 slides):
```
1.  Cover
2.  Problem statement
3.  Solution overview
4-5. Differentiators / capabilities
6-7. Case studies / proof points
8.  Methodology / approach
9.  Team / credentials
10. Call to action
11. Closing
```

These are starting points. The PM adjusts based on the actual content needs. Every archetype includes cover + closing as bookends and TOC dividers between major sections (for decks with 3+ sections).

#### A3.3 Define sections

For decks with TOC dividers, define the sections:
- Section number, title, description (one line), slide range
- These go into the deck-level frontmatter and are reused by every TOC divider slide

### A4. Per-Slide Content Authoring

Work through slides sequentially. For each slide:

#### A4.1 Title framing

Draft a title following these rules:
- **1 line preferred, 2 lines max. ~14 words max.**
- **Client-centric** — frame as what the client gets, not what we do ("Acme will receive..." not "We will deliver...")
- **Confident but measured** — use "can" not "will" for uncommitted outcomes; "aiming to" not definitive claims
- **Active, direct, present-tense** — no "we plan to", no filler
- **No hedge words in proposals** ("perhaps", "maybe", "we think")
- **Proper typography** — em-dashes for rhythmic breaks, proper articles and connectors
- **No red emphasis inside the title** — the title is one continuous white statement; red goes in the eyebrow

Present the draft title to the PM. PM confirms or adjusts.

#### A4.2 Content structure

For each slide, determine:

1. **Mode** — 1 (distribute to fill, 2+ peer blocks), 2 (hero centering, single payload), or 3 (cover/divider/closing)
2. **Peer blocks** — select from the closed vocabulary:
   - `text-card` — card with eyebrow + title + body bullets
   - `column-row` — row of N parallel cards (2/3/4)
   - `chip-row` — horizontal row of pills/chips
   - `timeline-strip` — multi-step temporal scaffold (weeks, phases)
   - `gantt-chart` — rows x time-columns
   - `tree-diagram` — hierarchical node tree
   - `architecture-diagram` — layered bands with chip rows
   - `stat-row` — row of stat boxes
   - `bio-row` — person profile
   - `image-block` — standalone image/illustration
   - `pull-quote` — large quoted statement

If the PM describes content that doesn't fit these types, flag it: "This needs a design-team extension — the current component vocabulary doesn't cover [X]. For now, I'll use the closest fit [Y] and add a note for the design agent."

#### A4.3 Content coaching

For each peer block, help the PM articulate the content:

- **Pull from harness** — if the slide maps to harness content (e.g., a "capabilities" slide maps to product-brief §5), pre-populate from the artifact and present for PM refinement.
- **Eyebrow naming** — every distinct content unit gets an eyebrow. Suggest eyebrows for each column, diagram, sub-section.
- **Bullet editing** — keep bullets to 1-2 lines, 2-4 per card. Rewrite verbose PM input into slide-ready phrases.
- **Differentiation check** — when producing multiple items in a same-shape grid (personas, methodology steps, category cards), verify that every item has unique, differentiated text. Flag if any items look similar.
- **Deliverable callouts** — for process/methodology slides, ask: "Which step produces a named deliverable?"

#### A4.4 Evidence and imagery

For slides that benefit from visual proof (methodology, case studies, capabilities):
- Ask the PM: "Do you have screenshots, diagrams, or examples to include?"
- If yes, capture the image path: `image: "assets/{filename}"`
- If not yet available, add a placeholder with description: `image: "assets/TODO-{description}.png"` and a note for the PM to provide later.

### A5. Generate Brief

After all slides are authored, generate the complete `slidedeck-{slug}.md` following the TEMPLATE.md format.

#### A5.1 Quality gate

Before writing, validate against the authoring checklist:

**Structure**
- [ ] Frontmatter has all required fields: `deck_title`, `prepared_for`, `deck_kind`, `slide_count`, `contact_name`, `contact_email`
- [ ] Every slide has a `## Slide N — {name}` header
- [ ] Every slide has a `type` field
- [ ] Cover, every TOC repeat, and closing are present

**Content slides**
- [ ] `mode` declared (1 / 2 / 3)
- [ ] `eyebrow` follows `SECTION › SUBSECTION` format, ALL CAPS
- [ ] Title is roman (no italic), ≤ 2 lines, ≤ ~14 words
- [ ] Each peer block uses a type from the closed vocabulary
- [ ] Same-shape grids have uniform structure across all cells

**Mode picking**
- [ ] Mode 1 iff 2+ peer blocks
- [ ] Mode 2 iff exactly 1 peer block AND "let one thing breathe"
- [ ] Mode 3 iff cover / divider / closing
- [ ] No "little content = Mode 2" — three bullets is still Mode 1

**Eyebrows**
- [ ] Every column in every column-row has an eyebrow
- [ ] Every diagram has an eyebrow naming it
- [ ] Every sub-section within a slide has an eyebrow

**Voice**
- [ ] Active, direct, present-tense
- [ ] No emoji, no exclamation marks
- [ ] No hedge words in proposal decks
- [ ] Bold lead-phrases on bullets where appropriate

**No visual dictation**
- [ ] No pixel sizes, paddings, gaps, colors, fills, fonts in the brief
- [ ] Decorative graphics referenced by path only

Report any failures to the PM. Fix before writing.

#### A5.2 Write the file

Write to `product/solution-space/slidedeck-{slug}.md` (or the PM's preferred path).

#### A5.3 Present for review

Show the PM the complete brief and offer: "Review the brief. You can adjust any slide's content before I finalize. When ready, I'll write the file."

### A6. After Writing

1. **Set frontmatter** — set `last_updated: {today}`, `last_updated_by: manual — /product-slidedeck`, and all required fields from the deck planning phase.
2. **Update project-daily** — if `project-daily` for today does not exist, create it first. Append an audit entry: `[MANUAL] slidedeck-{slug} — created via /product-slidedeck; {deck_kind} deck, {N} slides, for {audience} ({date})`.
3. **Routing review** — scan for decisions, assumptions, or scope items surfaced during authoring. Present routing suggestions if any found.
4. **Handoff instructions** — tell the PM:
   > "The brief is ready at `{path}`. To render slides:
   > 1. Open Claude Design
   > 2. Share `slidedeck-{slug}.md` as the content brief
   > 3. Share `DESIGN-SYSTEM.md` as the visual spec (or reference the house slide master if already loaded)
   > 4. Ask Claude Design to render the deck slide by slide"

---

## B. Update Mode

### B1. Load existing brief

Read the referenced `slidedeck-*.md` file. Parse slide structure.

### B2. PM direction

Ask: "What do you want to update?" Options:
- **Specific slides** — PM names slide numbers or titles to revise
- **Add slides** — PM describes new slides to insert
- **Remove slides** — PM identifies slides to cut
- **Content pass** — PM wants to review and refine all content
- **Structure change** — PM wants to reorder or restructure sections

### B3. Targeted Q&A

Run the relevant parts of Section A (A4 for content updates, A3 for structural changes). Only touch the slides being modified.

### B4. Rewrite

Update the file in place. Preserve all unchanged slides exactly. Run the quality gate (A5.1) on the full deck after changes.

### B5. After Update

1. **Update frontmatter** — set `last_updated: {today}`, `last_updated_by: manual — /product-slidedeck`.
2. **Update project-daily** — if `project-daily` for today does not exist, create it first. Append an audit entry: `[MANUAL] slidedeck-{slug} — updated via /product-slidedeck; {summary of changes} ({date})`.
3. **Routing review** — scan for decisions, assumptions, or scope items surfaced during the update. Present routing suggestions if any found.

---

## C. Review Mode

### C1. Load and validate

Read the referenced `slidedeck-*.md` file. Run the full quality gate checklist (A5.1).

### C2. Report

Present findings organized by severity:

- **Blocking** — must fix before handoff to Claude Design (missing required fields, mode mismatches, no eyebrows)
- **Warning** — likely to cause visual issues (titles > 14 words, > 4 bullets per card, duplicated text across items)
- **Suggestion** — could improve the deck (better title framing, missing deliverable callouts, opportunity to pull harness content)

### C3. Fix

Offer to fix blocking and warning items. PM confirms each fix.

---

## D. Inbound Routing

When a routing skill (`project-meeting`, `project-document`, or another skill's routing review) identifies content relevant to an existing `slidedeck-*.md`, it routes here.

### D1. Determine target

Identify which slidedeck file the content relates to. If multiple exist, ask the PM.

### D2. Assess impact

Classify the inbound content:
- **Title/messaging change** — a strategic reframe that affects slide titles or key messages
- **Content update** — new data, revised deliverables, changed timelines, updated pricing
- **Structural change** — new section needed, slide added/removed, reordering

### D3. Apply

For title/messaging and content updates: update the affected slides in place, preserving structure. For structural changes: flag to the PM — structural changes require a `/product-slidedeck update` session.

### D4. After routing

Update frontmatter: `last_updated: {today}`, `last_updated_by: auto — {source-skill} routing`. Append audit entry to project-daily: `[AUTO] slidedeck-{slug} — {description of routed change} from {source} ({date})`.

---

## E. Content Principles (reference for all modes)

### E1. The brief specifies WHAT, never HOW

The brief defines content and component roles. All visual decisions belong to the design agent and the master spec. Never include pixel sizes, colors, fills, fonts, paddings, or layout instructions in the brief.

### E2. Every word on the slide must be in the brief

Claude Design does not reliably infer, differentiate, or generate text. If the brief says "3 persona cards" but only provides text for 2, the third will be duplicated or hallucinated. **Every card, bullet, quote, label, and eyebrow must have its exact text in the brief.**

### E3. Same-shape grids: structural uniformity, content variation

In a row of equivalent units (methodology steps, comparison columns, persona cards), every cell must share the same structural template — same fields, same composition. Content varies per cell; structure does not.

### E4. Eyebrows are the navigational primitive

Every content unit gets an eyebrow. Without them the slide reads as a wall; with them it reads as an outline. Eyebrows are ALL CAPS, no italic, using ` › ` as hierarchy separator.

### E5. Slide titles are the message, not the topic

Bad: "Tokenisation overview"
Good: "Tokenisation means treating every goX as a traceable digital asset on a distributed ledger."

The title communicates the slide's main claim. The eyebrow names the topic.

### E6. Client-centric framing

Frame deliverables and outcomes from the client's perspective. "Acme will receive a holistic overview..." not "We will deliver a holistic overview..." This is especially important for proposal and marketing decks.

### E7. Image placeholders for methodology slides

Process/methodology slides benefit from visual proof — screenshots of actual work output (scoring matrices, PoC apps, architecture diagrams). Always ask the PM for images on these slides. Use `TODO-` prefix for images not yet available.

---

## Rules

1. **`-tbd-` over fabrication** — unknown fields are always `-tbd-`, never guessed. If the PM hasn't provided content for a slide element, mark it `-tbd-` and flag it.
2. **PM confirms all manual writes** — present the complete brief (or the diff for updates) to the PM before writing. Never write without confirmation.
3. **Preserve existing content** — in Update mode (B), preserve all unchanged slides exactly. Only modify slides the PM has identified for update.
4. **Audit everything** — every write (create, update, routed change) gets an audit entry in project-daily with `[MANUAL]` or `[AUTO]` prefix.
5. **Frontmatter is always current** — `last_updated` and `last_updated_by` must be set on every write.
6. **One file per deck** — each deck gets its own `slidedeck-{slug}.md` file. Never combine multiple decks into one file.
7. **The brief is authoritative until human-edited in Claude Design** — once the PM direct-edits text in Claude Design, those edits take precedence over the brief (per DESIGN-SYSTEM.md §0).
8. **No visual properties in the brief** — pixel sizes, paddings, colors, fills, fonts, and layout instructions are forbidden in the brief. The design agent and DESIGN-SYSTEM.md own all visual decisions.
