# product-slidedeck — Output Template

> This defines the exact format of the `slidedeck-{slug}.md` brief. The brief specifies **what each slide says and what role it plays** — never how it looks. All visual decisions belong to the design agent and are governed by `DESIGN-SYSTEM.md`.

---

## 1. Deck-Level Frontmatter

Every brief starts with a YAML frontmatter block:

```yaml
---
last_updated: YYYY-MM-DD
last_updated_by: manual — /product-slidedeck
deck_title: "Project Name — Deck Purpose"
subtitle: "Optional subtitle"
date: "Month YYYY"
prepared_for: "Client Name"
prepared_for_logo: "assets/client-logo.svg"    # optional
deck_kind: "proposal"                           # proposal | demo | marketing | leave-behind | internal
contact_name: "PM Name"
contact_email: "pm@example.com"
slide_count: NN
sections:                                       # required for decks with TOC dividers
  - group: "SECTION GROUP LABEL"                # ALL CAPS group name (e.g. "DISCOVERY PILLARS")
    items:
      - number: 1
        title: "Section Title"
        description: "One-line description"
        page_range: "slides N–M"
      - number: 2
        title: "Section Title"
        description: "One-line description"
        page_range: "slides N–M"
  - group: "SUMMARY"
    items:
      - number: 4
        title: "Timeline, pricing, and next steps"
        description: ""
        page_range: "slides N–M"
---
```

**Required fields**: `deck_title`, `prepared_for`, `deck_kind`, `slide_count`, `contact_name`, `contact_email`.

---

## 2. Slide Block Syntax

Every slide is a markdown section:

```markdown
## Slide N — {short reference name}

type: {cover | divider | content | closing}
mode: {1 | 2 | 3}
eyebrow: "SECTION › SUBSECTION"
title: |
  Slide title in roman white, one or two lines.
peer_blocks:

  - type: {peer-block-type}
    ...

notes: |
  Optional context for the design agent.
```

---

## 3. Slide Types

### 3.1 Cover (Mode 3)

```markdown
## Slide 1 — Cover

type: cover
title: "Deck Title"
subtitle: "Optional subtitle"
date: "Month YYYY"
prepared_for_block:
  label: "PREPARED FOR"
  logo: "assets/client-logo.svg"
hero_decoration: "assets/symbol-red.svg"
```

### 3.2 Section Divider / TOC (Mode 3)

```markdown
## Slide N — TOC: {active section name}

type: divider
active_section_index: N
```

The design agent renders the TOC from the deck-level `sections` frontmatter. `active_section_index` (0-based) determines which section is highlighted. All dividers share identical layout — only the active index changes.

### 3.3 Content (Mode 1 or 2)

```markdown
## Slide N — {reference name}

type: content
mode: 1
eyebrow: "SECTION › SUBSECTION"
title: |
  The slide's main message as a complete statement.
peer_blocks:

  - type: column-row
    columns:
      - eyebrow: "COLUMN EYEBROW"
        title: "Column title"
        sub: "Optional italic subtitle"
        body:
          - "First bullet point"
          - "Second bullet point"
        deliverable: "Deliverable name"
        image: "assets/image.png"

  - type: timeline-strip
    eyebrow: "TIMELINE LABEL"
    active_step_index: 0
    steps:
      - eyebrow: "WEEK 1"
        title: "Step name"
      - eyebrow: "WEEK 2"
        title: "Step name"
      - eyebrow: "WEEK 3"
        title: "Step name"
        deliverable: "DELIVERABLE"

notes: |
  Context for the design agent — what the slide should accomplish.
```

### 3.4 Closing (Mode 3)

```markdown
## Slide N — Closing

type: closing
closing_statement: "Thank you."
contacts:
  - name: "PM Name"
    email: "pm@example.com"
hero_decoration: "assets/symbol-red.svg"
prepared_for_block:
  label: "PREPARED FOR"
  logo: "assets/client-logo.svg"
```

---

## 4. Peer-Block Types — Closed Vocabulary

### 4.1 `text-card`

A single card with optional eyebrow, title, and body bullets.

```yaml
- type: text-card
  eyebrow: "CARD LABEL"
  title: "Card title"
  sub: "Optional subtitle in italic"
  body:
    - "Bullet one"
    - "Bullet two"
```

### 4.2 `column-row`

A row of N parallel cards (2, 3, or 4). **Every column must share the same structural template** — same fields present, even if some values differ. This is the same-shape grid rule.

```yaml
- type: column-row
  eyebrow: "ROW-LEVEL EYEBROW"          # optional, labels the whole row
  columns:
    - eyebrow: "COLUMN 1"
      title: "Title"
      sub: "Subtitle"
      body:
        - "Bullet"
      deliverable: "Named deliverable"    # optional
      image: "assets/image.png"           # optional
    - eyebrow: "COLUMN 2"
      title: "Title"
      sub: "Subtitle"
      body:
        - "Bullet"
      deliverable: ""                     # empty but present — structural uniformity
      image: ""
```

### 4.3 `chip-row`

A horizontal row of pills/chips — for tagging, meta info, or component enumeration.

```yaml
- type: chip-row
  eyebrow: "ROW LABEL"
  chips: ["Chip 1", "Chip 2", "Chip 3", "Chip 4"]
  chip_state: outline                    # outline | dark | red
```

### 4.4 `timeline-strip`

A multi-step temporal scaffold (weeks, phases, stages).

```yaml
- type: timeline-strip
  eyebrow: "N-WEEK TIMELINE"
  active_step_index: 0                   # which step gets fill emphasis
  steps:
    - eyebrow: "WEEK 1"
      title: "Step description"
    - eyebrow: "WEEK 2"
      title: "Step description"
    - eyebrow: "WEEK 3"
      title: "Step description"
      deliverable: "DELIVERABLE"
```

### 4.5 `gantt-chart`

A Gantt chart with row groups x time columns.

```yaml
- type: gantt-chart
  eyebrow: "GANTT LABEL"
  rows: ["Row 1", "Row 2", "Row 3", "Row 4"]
  columns: ["W1", "W2", "W3", "W4", "W5", "W6"]
  bars:
    - row: "Row 1"
      label: "Activity name"
      start: 1
      end: 3.5
    - row: "Row 1"
      label: "Parallel track"
      start: 2
      end: 4
      track: 2                           # stacked within the same row
  deliverables:
    - row: "Row 1"
      label: "Deliverable description"
    - row: "Row 2"
      label: "Deliverable description"
```

### 4.6 `tree-diagram`

A hierarchical node tree (left-to-right or top-to-bottom). Every node tier shares the same internal template — ALL-CAPS tier kicker + node name.

```yaml
- type: tree-diagram
  eyebrow: "DIAGRAM LABEL"
  direction: left-to-right               # or top-to-bottom
  tiers:
    - name: "root"
      kicker: ""                          # root may not need a kicker
    - name: "area"
      kicker: "AREA"
    - name: "objective"
      kicker: "OBJECTIVE"
    - name: "use-case"
      kicker: ""
  nodes:
    - id: "root"
      tier: "root"
      name: "AI use-cases"
    - id: "area-1"
      tier: "area"
      name: "goX app focus"
      parent: "root"
    - id: "obj-1"
      tier: "objective"
      name: "Earn-side engagement"
      parent: "area-1"
    - id: "uc-1"
      tier: "use-case"
      name: "Transactional analytics & AI tips"
      description: '"Where did I earn most rewards? Earn-again!"'
      parent: "obj-1"
    - id: "uc-ghost"
      tier: "use-case"
      name: "+ more to be mapped together..."
      ghost: true                         # dashed/dimmed node
      parent: "obj-4"
  footnote: |
    Illustrative starting point — the mapping exercise expands this tree
    jointly with your team, then prioritises and selects 2-3 use-cases for PoC.
```

### 4.7 `architecture-diagram`

Layered architecture bands with chip rows. At most one band is the focal band (red-fill emphasis).

```yaml
- type: architecture-diagram
  eyebrow: "DLT ARCHITECTURAL DIAGRAM"
  focus_band_index: 2                    # 0-based; the focal band gets red emphasis
  bands:
    - label: "APPLICATION SURFACES"
      chips: ["User app", "Merchant app", "Admin app", "Partner apps"]
    - label: "TOKEN & BUSINESS LOGIC"
      chips: ["Wallets", "Mint / burn", "Transfer", "Settlement", "Cashback", "Exchange"]
    - label: "DLT LAYER"
      chips: ["Notary service", "BFT consensus", "Signing", "Hash chain", "Merkle tree"]
    - label: "SOURCE-OF-TRUTH & PERSISTENCE"
      chips: ["Castore event sourcing", "SQL", "Immutable archive"]
```

### 4.8 `stat-row`

A row of stat boxes — red-filled cards emphasizing numbers or short payoff phrases.

```yaml
- type: stat-row
  stats:
    - number: "4.5M"
      description: "Programme members"
    - number: "4"
      description: "Countries (SK/CZ/PL/AT)"
    - number: "3"
      description: "Applications built"
```

### 4.9 `bio-row`

Person profile — used standalone or within a `column-row` for leadership grids.

```yaml
- type: bio-row
  avatar: "assets/avatar.png"
  name: "Person Name"
  title: "Role / Title"
  body:
    - "Credential or bio point"
    - "Second point"
```

### 4.10 `image-block`

A standalone image or illustration.

```yaml
- type: image-block
  src: "assets/diagram.png"
  caption: "Optional caption"
```

### 4.11 `pull-quote`

A large quoted statement — typically Mode 2 (hero centering).

```yaml
- type: pull-quote
  quote: "The quote text."
  attribution: "Speaker Name, Role"
```

---

## 5. Composite Slide Patterns

Common multi-block slide compositions for reference:

### 5.1 Two-zone horizontal split

Two peer blocks side by side (left context, right forward-looking):

```yaml
peer_blocks:
  - type: text-card
    eyebrow: "WHERE WE ARE"
    title: "Context recap"
    body: ["...", "..."]
  - type: column-row
    eyebrow: "WHAT'S NEXT"
    columns:
      - eyebrow: "1"
        title: "First area"
        body: ["Description"]
      - eyebrow: "2"
        title: "Second area"
        body: ["Description"]
```

### 5.2 Overview + detail (vertical stack)

Overview structure on top, detail below:

```yaml
peer_blocks:
  - type: timeline-strip
    eyebrow: "3-WEEK TIMELINE"
    steps: [...]

  - type: column-row
    columns:
      - eyebrow: "WORKSHOP 1"
        title: "Detail"
        body: [...]
      - eyebrow: "WORKSHOP 2"
        title: "Detail"
        body: [...]
```

### 5.3 Categories + pipeline

Multiple category cards alongside a process pipeline:

```yaml
peer_blocks:
  - type: column-row
    eyebrow: "IMPROVEMENT AREAS"
    columns:
      - eyebrow: ""
        title: "Category 1"
        body: ["Item", "Item", "Item"]
      - eyebrow: ""
        title: "Category 2"
        body: ["Item", "Item"]
      - eyebrow: ""
        title: "Category 3"
        body: ["Item", "Item"]

  - type: text-card
    eyebrow: "SCOPING PIPELINE"
    body:
      - "**1 Requirements collection**: business, user, tech"
      - "**2 Prioritisation**: value vs. effort"
      - "**3 Concept design**: rapid prototyping"
      - "**4 Solution architecture**: technical & process"
      - "**5 Detailed spec & estimate**: only selected features"
    deliverable: "Detailed v3 delivery plan"
```

### 5.4 Deliverables + pricing

Deliverable blocks followed by a pricing band:

```yaml
peer_blocks:
  - type: column-row
    columns:
      - eyebrow: ""
        title: "1) Pillar name"
        body: ["Deliverable 1", "Deliverable 2", "Deliverable 3"]
      - eyebrow: ""
        title: "2) Pillar name"
        body: ["Deliverable 1", "Deliverable 2", "Deliverable 3"]
      - eyebrow: ""
        title: "3) Pillar name"
        body: ["Deliverable 1", "Deliverable 2", "Deliverable 3"]

  - type: stat-row
    stats:
      - number: "EUR 40,000 – 50,000"
        description: "Fixed-fee, 6 weeks. Final price based on agreed scope."
```

---

## 6. Writing Conventions

- **Titles**: 1 line preferred, 2 lines max, ≤ ~14 words. Title communicates the message (a claim), not the topic. The eyebrow names the topic.
- **Bullets**: 1-2 lines each, 2-4 per card. Short phrases, not sentences.
- **Eyebrows**: ALL CAPS. Hierarchy uses ` › `. No italic.
- **Bold lead-phrases**: `**Bold label**: descriptive text` for emphasis inside bullets.
- **Italic**: sparingly, for inline emphasis in body copy only. Forbidden in titles, eyebrows, section headers.
- **No emoji**. No exclamation marks. No hedge words in proposals.
- **Deliverable field**: renders as a small red-fill chip. Can appear on some cells and not others — content variation within structural uniformity.
