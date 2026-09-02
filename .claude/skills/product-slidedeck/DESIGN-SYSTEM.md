# Slide Master Layout Spec — v3

**Scope.** Layout system for all decks — proposals, internal demos, marketing, leave-behinds. One generic master, no deck-type variants. Color palette, typography family, iconography, and motion are upstream design-system concerns; this spec references them by role and locks only the layout rules.

**Source of truth.** v3 supersedes v2 with consistency, numbering, and unit fixes. The April 2026 goX v3 discovery proposal is the canonical reference deck — every rule below is testable against that deck. Where v1/v2 conflict with the goX v3 production result, v3 reflects the production result (most notably: the vertical-distribution rules in §6 replace v1's "top-anchored, leave bottom open" guidance).

**Intended consumers.** Figma slide master, react-pptx pipeline, Storybook, designers and PMs producing decks, AI agents producing deck output from a content brief.

**Scope clarification.** v3 specifies **dark decks only** (`--sudo-dark-90` background). Tokens for light backgrounds are listed in §11.2 for reference but layouts, surface colors, and component variants in §5–§10 assume a dark canvas. Light-deck variants are out of scope.

**Units.** All sizes, gaps, paddings, and positions in this spec are in **CSS pixels (px)** at the 1920×1080 canvas. Type sizes match the `.t-*` classes in §11.3. The spec does not use `pt` anywhere — if a value reads `pt` in your tooling, treat it as a typo and use the px value from §11.3.

---

## 0. Workflow rule — text is locked once edited

When a human direct-edits the text of any element on a built slide, that text is **locked**. It must never be regenerated from the original spec, normalized against duplicates on other slides, or auto-corrected on subsequent passes.

- If duplicate or near-duplicate text appears across multiple nodes after their direct edits, the duplicates stand.
- If a direct-edit conflicts with the source spec, the direct edit wins.
- If a later instruction would overwrite a direct-edit, the agent asks first.

This rule precedes every visual rule below.

---

## 1. Canvas

| Property | Value |
|---|---|
| Aspect ratio | 16:9 |
| Resolution | 1920 × 1080 px |
| Origin | Top-left (0,0) |
| Units | px |

---

## 2. Spacing scale — strict 8-base, with three documented 12 px exceptions

**Every gap, margin, and padding — horizontal or vertical — must come from the spacing scale.**

```
4 · 8 · 16 · 24 · 32 · 40 · 48 · 56 · 64 · 80
```

No 18s, 22s, 25s, 36s, 52s, 72s. The most-used values:

- **80 px** — outer slide margin (left/right/top/bottom safe frame)
- **56 px** — card internal padding (top-level cards)
- **48 px** — generous bottom buffer below content blocks
- **40 px** — grid gutter, gap between sibling cards
- **32 px** — card internal padding (nested cards), inter-section gap inside a card
- **24 px** — paragraph gap, default inline group gap
- **16 px** — list item separation, inter-pill gap
- **8 / 4 px** — inline tight gaps (eyebrow → divider, etc.)

### 2.1 Horizontal vs. vertical behaviour

- **Horizontal values are fixed at their scale value.** Card padding is 56 — not 50, not 60. Inter-card gutter is 40 — not 36, not 48 unless the layout calls for the next bracket up.
- **Vertical values may expand from scale-minimum to fill the content zone**, but must remain on-scale at every snapshot. A gap of 32 expands to 40 → 48 → 56 → 64 → 80 — never to 37 or 52.

### 2.2 Documented 12 px exceptions

12 is **not** on the main scale. It is permitted only in these three places:

1. §9.2 — between a red section header and its body
2. §9.4 — between a stat-box number and its description
3. §9.5 — between a bio name baseline and its first bullet

Anywhere else, 12 is a bug.

### 2.3 Distribution math

When N peer blocks must distribute across a content zone of height `H`:

1. Compute total content height `C = sum of block heights`.
2. Compute slack `S = H − C`.
3. Compute raw gap `g_raw = S / (N − 1)`.
4. **Snap `g_raw` down to the nearest scale value** (`g`). The remainder reads as bottom margin.
5. Validate: `g ≥` the block's declared minimum gap (typically 32). If not, the content is over-budget — escalate to the designer.

This guarantees on-grid distribution. The leftover remainder at the bottom (a few px to ~one scale step) reads as natural bottom margin.

---

## 3. Grid

A **12-column grid** with fixed gutters.

| Property | Value |
|---|---|
| Columns | 12 |
| Column width | 110 px |
| Gutter | 40 px |
| Outer L/R margin | 80 px |
| Content width | 1760 px |

Verification: `12 × 110 + 11 × 40 = 1760` ✓

### 3.1 Canonical splits

Pick from this set; do not improvise asymmetric splits.

| Split | Region widths (px) | Used for |
|---|---|---|
| 12 | 1760 | Full-bleed container, single block |
| 6 \| 6 | 860 \| 860 | Two-column comparison, two cards |
| 4 \| 4 \| 4 | 560 \| 560 \| 560 | Three equal cards / steps |
| 3 \| 3 \| 3 \| 3 | 410 \| 410 \| 410 \| 410 | Four equal cards / stat row |
| 5 \| 7 | 710 \| 1010 | TOC slide, sidebar + main |
| 4 \| 8 | 560 \| 1160 | Narrow callout + main content |

Region gutter is one grid gutter (40 px) and is not added to either region's width.

---

## 4. Safe area

No content (text, logos, photos, card edges) crosses the safe frame. Decorative gradients can extend further only at <0.2 alpha.

| Edge | Inset |
|---|---|
| Left / Right / Top / Bottom | 80 |

---

## 5. Title zone

Every content slide has a title in the top band. The pattern is **eyebrow + white title** — never red emphasis inside the title itself.

```
┌──────────────────────────────────────────────────────────┐
│  EYEBROW › OPTIONAL SUBSECTION        ← Y=80 cap-top     │
│                                                          │
│  Title line 1 (white)                 ← Y=128 cap-top    │
│  Title line 2 (white, optional)                          │
│                                                          │
│  ──── 64 px gap ────                                     │
│                                                          │
│  Content zone                                            │
└──────────────────────────────────────────────────────────┘
```

### 5.1 Eyebrow

| Property | Value |
|---|---|
| Position | X=80, Y=80 (cap-top) |
| Style | `.t-chapter` (see §11.3) |
| Color (leading section label) | `--sudo-red` |
| Color (trailing subsection label, after ` › `) | `--sudo-dark-50` |
| Case | ALL CAPS |
| Hierarchy separator | ` › ` (chevron with surrounding spaces) |
| Format | `SECTION` or `SECTION › SUBSECTION` |

Concrete values from `.t-chapter`: 20 px, Söhne Breit Kräftig (500), line-height 1.00, tracking −0.025 em (−2.5%). Italic is forbidden (see §11.5).

The eyebrow is the deck's primary navigational mechanism. Without it, slides read as a wall; with it, they read as an outline. **Every distinct content unit gets an eyebrow naming what it is** — slides, sub-sections, column groups, diagrams.

### 5.2 Title

| Property | Value |
|---|---|
| Position | X=80, Y=128 (cap-top) |
| Style | `.t-title` (see §11.3) |
| Color | `--sudo-white` |
| Max lines | 2 |
| Max width | 1760 px |

Concrete values from `.t-title`: 64 px, Söhne Breit Kräftig (500), line-height 0.96, letter-spacing −0.010 em.

**No red emphasis inside the title.** Red goes in the eyebrow. The title is one continuous white statement.

### 5.3 Title block height (planning aid)

- 1 line: ~62 px → bottom at Y≈190 → content zone starts Y≈262 (with 64 px gap → 254; rounded up to 262 for a clean Y_start)
- 2 lines: ~124 px → bottom at Y≈252 → content zone starts Y≈332

For agent calculations, use the `Y start` values in §6 directly.

---

## 6. Content zone — the three vertical-arrangement modes

| Property | Value |
|---|---|
| X start | 80 |
| X end | 1840 |
| Width | 1760 |
| Y start (1-line title) | 262 |
| Y start (2-line title) | 332 |
| Y end | 1000 (top of bottom safe inset) |

Every content slide picks **one of three vertical-arrangement modes**. The mode is determined by the count of peer blocks and the slide's role.

**Definition: peer block.** A peer is a *top-level* block in the content zone, not every visual element inside it. A card containing 5 bullets is one peer. A two-column row of 4 stats per column is one peer (the row). A diagram with 4 bands is one peer.

### 6.1 Mode 1 — Distribute to fill (default)

**Used when**: 2 or more peer blocks share equal weight.

Gaps between peers expand from scale-minimum to fill the content zone. The slide reads as a **unified rectangle of content with proportional rhythm** — no top-anchored stack with empty floor, no centered cluster floating in dead space.

**Algorithm**:

1. Lay out peer blocks at their natural heights.
2. Compute the slack between (Y_end − Y_start) and the sum of block heights + the count-1 minimum gaps.
3. Distribute the slack as gap-expansion, snapping each gap to the nearest scale value below the computed value (per §2.3).
4. The leftover remainder (≤ one scale step) reads as natural bottom margin.

**Anti-patterns this rule eliminates**:

- Tight clusters of content floating in an otherwise empty zone.
- Top-anchored stacks that leave a dead rectangle of empty space at the bottom.
- Bottoms of paired columns ending at different y-coordinates.

**Used by**: ~95% of content slides.

### 6.2 Mode 2 — Hero centering

**Used when**: exactly 1 peer block, and the design intent is "let this one thing breathe."

The peer's geometric center sits at the **midpoint of the content zone**:

- 1-line title slide: Y_center = (262 + 1000) / 2 = **631**
- 2-line title slide: Y_center = (332 + 1000) / 2 = **666**

Not a fixed Y=540. The midpoint depends on title height.

**Used by**:

- Single big stat (e.g. "$1B+ value created" at `.t-cover` 120 px or `.t-headline` 80 px)
- Pull-quote
- Single hero diagram or chart that needs breathing room

**Heuristic for picking Mode 2**: if you'd be tempted to set the payoff at 80 px (`.t-headline`) or larger, you're in Mode 2. Otherwise, you're in Mode 1. Three short bullets are *not* Mode 2 — they're Mode 1 with generous gaps.

Note: Section-divider / TOC slides are Mode 3 per §10.2, **not** Mode 2 — they have a fixed compositional template, not a centered single payload.

### 6.3 Mode 3 — Anchored composition

**Used when**: the slide's role dictates a fixed composition template — covers, closings, and TOC dividers.

Specific elements anchor to specific positions per the slide type's template (§10.1, §10.2, §10.4). Not distributed, not centered — composed.

### 6.4 Mode-selection rule

```
IF slide_type IN {cover, closing, section-divider/TOC}:
    Mode 3 — Anchored composition (§10.1, §10.2, §10.4)
ELSE IF peer_block_count == 1 AND payoff_intent == "single dominant element":
    Mode 2 — Hero centering (§6.2)
ELSE:
    Mode 1 — Distribute to fill (§6.1)
```

### 6.5 Other content-zone principles

- **Symmetric horizontal padding inside cards.** Asymmetric horizontal padding inside a card is forbidden.
- **Body text is left-aligned.** Centered body is reserved for stat boxes and decorative type only.
- **Diagrams center horizontally** in their available region. When a fixed-size chart sits below a title, wrap it in a centering flex — don't pin to a corner.
- **All peer blocks in a row share the same height.** If one column has less content, its container matches the rest.

---

## 7. Page numbering

Every content slide has a page number. Cover, section-divider/TOC, and closing slides do not.

| Property | Value |
|---|---|
| Format | `NN / TT` (two-digit, with surrounding spaces) |
| Position | Right-aligned, baseline at Y=1024 |
| Right edge | X=1840 |
| Style | `.t-page-num` (22 px, see §11.3) |
| Color | `--sudo-dark-50` |

Examples: `02 / 17`, `14 / 17`.

---

## 8. Surface system — the 3-fill scale

These slides express visual hierarchy by **fill density alone**, never by hue rotation. There are exactly three fill states for any container, chip, or band:

| State | Treatment | Semantic role |
|---|---|---|
| `outline` | Transparent fill, 1 px border at `--rule-dark` | Items, atoms, elements being enumerated |
| `dark-fill` | Solid `--sudo-dark-80` fill, no border (or hairline) | Containers, groups, processes that hold the items |
| `red-fill` | `--sudo-red` fill, white text | The single most important thing on the slide |

**Reference example** — Slide 4 of the goX v3 deck: outlined chips inside dark-fill bands, with the "DLT layer" band and its chips elevated to red-fill to mark it as the focus. Three weights coexist on one diagram, all without changing hue.

**The system has no fourth color.** Yellow, amber, blue, green, "warm" or "cool" tints are out — even for semantic differentiation. If two things need to feel different, differentiate by *fill density*, not by hue.

### 8.1 Surface roles

| Role | Token |
|---|---|
| `surface/slide` | `--sudo-dark-90` (`#15002E`) |
| `surface/card` | `--sudo-dark-80` (`#26123F`) |
| `surface/card-accent` | `--sudo-red` (`#EE0000`) |

### 8.2 Card padding (depth-based)

| Depth | Padding (all sides) |
|---|---|
| Top-level card on slide | 56 |
| Card nested inside a card | 32 |

Cards beyond depth 2 are forbidden.

### 8.3 Card geometry — hard-edged, no radius

This is a hard-edged brand. **All cards, bands, chips, and shapes are pure rectangles or perfect circles.** Border radius is **0** for everything except circular elements (avatars, the section-numeral background — when used).

| Property | Value |
|---|---|
| Corner radius (any card, band, chip, pill) | **0** |
| Corner radius (avatar, circular badge) | full circle (`9999px` / `50%`) |
| Border (default card on dark) | none — separation comes from fill density (`--sudo-dark-80` on `--sudo-dark-90`) |
| Border (accent / red-fill card) | none |
| Border (outline-state chip) | 1 px `--rule-dark` (`#786A89`) |
| Drop shadows, inner shadows, glows | **forbidden** |
| Gradients on cards/bands/chips | **forbidden** (gradients exist only on `symbol-red.svg`) |

### 8.4 Card vertical rhythm (inside a card)

| Between… | Gap |
|---|---|
| Card top → first content | (handled by padding) |
| Section header (red) → its body | **12** (documented exception) |
| Body paragraph → next section header | 32 |
| List item → list item | 16 (or expanded per Mode 1) |
| Last body block → bottom-anchored stat row | flex, ≥ 32 |

---

## 9. Component patterns

### 9.1 Pill / chip — rectangular

Inline rectangular container for a short label. **Not rounded** — the brand is hard-edged. One geometry covers all use cases (tags, meta info, diagram chips); fill state and text style vary per context.

| Property | Value |
|---|---|
| Height | 56 |
| Padding (V / H) | 16 / 24 |
| Corner radius | 0 |
| Inter-pill gap | 16 |
| Text style — ALL CAPS labels (tags, status) | `.t-label` (24 px display, 500) |
| Text style — title-case content chips (in diagrams, meta strips) | `.t-page-num` (22 px display, 500) used in title case |
| Text color on a filled pill (dark or red) | `--sudo-white` |
| Text color on an outline-state chip (dark slide) | `--sudo-white` |

Pills come in all three fill states (outline, dark-fill, red-fill) per §8.

**Why one geometry.** 56 height + 16 V padding gives 24 px inner space — comfortable for both 22 px and 24 px display text at line-heights 1.00–1.06. Larger text (`.t-body` at 32 px) is not a pill; it's a card or band.

### 9.2 Section header (red)

Inline subsection label inside a card or content block (e.g. "Challenge", "Methods", "Outputs", "Our Approach").

| Property | Value |
|---|---|
| Style | `.t-toc-section` (32 px display, see §11.3) |
| Color | `--sudo-red` |
| Space above | 32 (or 0 if first in card) |
| Space below | **12** (documented exception) |

Section headers and inline content labels are **title-case, not uppercase**. Uppercase is reserved for eyebrows (§5.1).

### 9.3 Numbered list

| Property | Value |
|---|---|
| Indent (number-x → text-x) | 32 |
| Item-to-item gap | 16 |
| Number color | `--sudo-white` (default) — `--sudo-red` is allowed for emphasis lists |
| Wraps align | under text, not under number |
| Bold prefix style | `**Bold label**: descriptive text` (Aeonik Bold inline, body color) |

### 9.4 Stat box (`surface/card-accent`)

Red-filled card emphasizing a number or short payoff phrase.

| Property | Value |
|---|---|
| Min height | 160 |
| Padding (V / H) | 32 / 24 |
| Number / headline style | `.t-headline` (80 px) — bold by family default |
| Number → description gap | **12** (documented exception) |
| Description style | 24 px display (`.t-label` size, but mixed-case sentence text — not ALL CAPS), line-height 1.30 |
| Inter-box gap (in a row) | 16 |
| Text alignment | center |
| Vertical alignment | center |

For pricing/totals, **the container carries the emphasis (size, prominence), not the number.** Keep the number readable but not gigantic; let the box's prominence do the work.

### 9.5 Bio row

Person profile composed as `[avatar][gap][name + title + bio block]`.

**Vertical (stacked rows):**
| Property | Value |
|---|---|
| Avatar diameter | 96 |
| Avatar → text gap | 24 |
| Name style | `.t-toc-section` (32 px display, 500), `--sudo-red` |
| Title (parens, after name) | `.t-toc-section` (32 px display, 400), `--sudo-white` |
| Name baseline → first bullet | **12** (documented exception) |
| Row-to-row gap | 64 |

**Horizontal (leadership grid):**
| Property | Value |
|---|---|
| Avatar diameter | 120 |
| Avatar → name gap (vertical) | 24 |
| Name style | `.t-toc-section` (32 px display, 500), `--sudo-white` |
| Title style | `.t-page-num` (22 px display), `--sudo-dark-30` |
| Bio paragraph style | `.t-body` (32 px), line-height 1.40 |
| Person-to-person horizontal gap | 40 (one grid gutter) |

### 9.6 Timeline / week strip

Multi-step temporal scaffold (e.g. "Week 1 / Week 2 / Week 3").

| Property | Value |
|---|---|
| Cell layout | equal-width columns, one grid gutter (40) between |
| Active cell | dark-fill or red-fill (one cell only) |
| Inactive cells | outline-only |
| Cell internal padding | 32 |
| Cell label | small ALL CAPS eyebrow ("WEEK 1") in `.t-chapter` style above content title |

**Exactly one cell carries fill emphasis** at any time — the "where we are" or "where this slide is about" cell. Don't fill all of them, don't fill none. (See §8 — the 3-fill scale applies inside a timeline too.)

### 9.7 Hierarchical-diagram node

Node boxes in tree/flow diagrams (e.g. area→objective→use-case tree).

| Property | Value |
|---|---|
| Internal template | `[ALL-CAPS tier kicker]` + `[node name]` |
| Tier kicker style | `.t-chapter` (20 px ALL CAPS), `--sudo-red` |
| Tier kicker → name gap | 8 |
| Node name style | `.t-body` (32 px) or `.t-body-bold` (32 px, weight 700) |
| Box width | wide enough that **labels never wrap** |
| Box height | uniform within a tier |

**All node boxes in a hierarchical diagram share the same internal template across tiers** (see §12.5). When you have multiple tiers (Area / Objective / Use-case), each tier reads identically — kicker on top naming the tier, name below. Visual consistency across tiers makes the hierarchy legible.

**Parent nodes sit on the geometric vertical midpoint of their children's bounding box** — not at the top, not at fixed offsets.

### 9.8 Gantt / timeline chart

| Property | Value |
|---|---|
| Column header | filled chip (dark or red), white text — never plain text |
| Row label column | width matches the longest label so labels never wrap |
| Row heights | uniform across all rows |
| Bar start/end | may be fractional (e.g. start at column 1.5 if real-world phasing is mid-week) |
| Row-level callouts (deliverables, etc.) | span and center vertically inside the row |
| Single-purpose column header | omit — a labeled "DELIVERABLES" header above a single deliverables column is redundant |
| Chart placement | wrap in a centering flex so the chart centers horizontally and vertically in the available content area |

### 9.9 Architecture-band diagram

A vertical stack of horizontal **bands**, each band representing a layer of an architecture (e.g. Application Surfaces / Token & Business Logic / DLT Layer / Source-of-Truth). Each band contains a row of chips representing the components in that layer.

| Property | Value |
|---|---|
| Stack direction | vertical |
| Band height | uniform across all bands; height set by the densest band's content |
| Band internal padding | 32 (top/bottom), 32 (left/right) |
| Band corner radius | 0 |
| Inter-band gap | 16 |
| Band label | `.t-chapter` (20 px ALL CAPS) in `--sudo-red`, **centered above** the chip row, with **12 px** gap to the chips below (documented exception, treated as a section-header→body relation) |
| Chips inside a band | pill per §9.1 (height 56, 16/24 padding) — `.t-page-num` (22 px) text in title case, dark-fill state by default |
| Inter-chip gap inside a band | 16 |
| Chip alignment | centered horizontally within the band |
| Wrapping | chips wrap to a second row if total width exceeds band width; gap between rows = 16 |
| Diagram eyebrow | every architecture diagram gets a slide-level eyebrow above it (e.g. "DLT ARCHITECTURAL DIAGRAM" in `.t-chapter`, X-aligned with band left edge), **24 px** above the topmost band |

**Focus band rule (§8 3-fill scale applied)**: at most **one** band is the focal band. The focal band carries:
- A **1 px `--sudo-red` border** around the band perimeter
- The **band-label eyebrow in `--sudo-red`** (already the default, but stays red even when other labels go to `--sudo-dark-30` for de-emphasis if the slide narrative calls for it)
- All chips inside the focal band switch to **red-fill** state (`--sudo-red` background, white text)

Non-focal bands stay in dark-fill (band) + dark-fill (chips) — quiet but legible. **Never** elevate a chip to red while leaving its parent band in dark fill, or vice versa — the band and its chips share fill state.

### 9.10 Summary / total card (pricing slides)

Used on pricing or total-investment summary slides — one row of deliverable cards across the top, then one full-width emphasis band beneath them carrying the total figure or summary statement.

| Property | Value |
|---|---|
| Top row | row of deliverable cards, structurally uniform per §12.5 |
| Card padding | 56 (top-level) |
| Inter-card gutter | 40 |
| Total / emphasis band | full content-width (1760), height **160–200**, padding 48 (V) / 56 (H) |
| Total band fill | `--sudo-dark-80` (dark-fill) by default; `--sudo-red` (red-fill) when the total is THE payoff |
| Total band layout | left-aligned label (e.g. "Total investment"), right-aligned figure |
| Total figure style | `.t-headline` (80 px) — readable but not gigantic. The **container carries the emphasis** (size, prominence, isolation), not the digits. Never set the total at `.t-cover` (120 px) inside this band. |
| Gap between row and band | distributed per Mode 1 (§6.1) — typically expands to 80 px on a sparse slide, 48 px on a denser one |

### 9.11 Deliverable callout

A small red-filled chip or tag attached to a step, week, or row to mark "here's what comes out of this."

| Property | Value |
|---|---|
| Treatment | red-fill, white ALL CAPS text in `.t-chapter` style |
| Placement | top-right corner of its parent cell, OR right-aligned within the parent row |
| Size | small — never larger than the surrounding content's primary text |

**Same-shape grid rule (see §12.5)**: deliverable callouts can appear on some cells and not others — content can vary — but the *cell template* must remain identical across the row. The callout fits *into* the template; it doesn't break it.

---

## 10. Standard slide types

Four slide types cover every deck. Use the smallest set that tells the story.

### 10.1 Cover (Mode 3 — Anchored composition)

Opening slide of every deck. **Bookend rule**: cover and closing must mirror each other — same logo size, same hero brand-mark placement, same composition language.

| Element | Spec |
|---|---|
| Background | `--sudo-dark-90` (`#15002E`) |
| Eyebrow / page number | none |
| Brand logotype | `assets/logotype-white.svg`, **height 112 px**, anchored top-left at `(X=80, Y=80)`. ~3× the working-slide chrome size of 36 px. |
| Project title | `.t-title` (64 px). White. X=80. Geometric center at **slide-midpoint Y=540** (this is the *slide* midpoint, 1080/2; covers have no content zone in the §6 sense). Max 2 lines. |
| Subtitle (optional) | `.t-subtitle` (48 px display, weight 400), `--sudo-dark-30`. Below title with **16 px** gap. |
| Date label | `.t-chapter` (20 px ALL CAPS) or `.t-page-num` (22 px), `--sudo-dark-30`. Below subtitle with **24 px** gap. Separate metadata line — does not share subtitle size. |
| Hero decoration | `assets/symbol-red.svg` (the gradient red "S" mark) at **height ~520 px**, **fully inset** top-right, anchored at `(right=80, top=80)`. **Never bled off the slide.** |
| "PREPARED FOR" block | Label `.t-chapter` (20 px ALL CAPS, `--sudo-dark-50`), then client logo below with **16 px** gap. Anchored bottom-left at `(X=80, baseline=1024)`. |

**Title sizing.** Always `.t-title` (64 px) for v3 — single rule, no thresholds. If a title needs more impact, route it through a section-divider slide (§10.2) instead of upsizing the cover title.

**Only the recipient/client gets a footer mark.** The agency mark is the logotype at top-left; no duplicated agency string at the bottom.

**No invented decoration.** Generated gradient blobs, hand-drawn shapes, or stand-in graphics are forbidden. The cover's only sanctioned decorative move is the `symbol-red.svg` placement above.

### 10.2 Section divider / TOC (Mode 3 — Anchored composition)

Recurring divider between deck sections — a TOC where the current section is highlighted, others are dimmed. The same template repeats before each new section.

| Element | Spec |
|---|---|
| Background | `--sudo-dark-90` |
| Eyebrow | `CONTENTS` in `.t-chapter` style (20 px ALL CAPS, `--sudo-red`), at `(X=80, Y=80)`. No subsection. |
| Title | "Table of contents" in `.t-title` (64 px Söhne Breit Kräftig, **roman, never italic**), white, at `(X=80, Y=128)`. |
| Layout split | `5 \| 7` per §3.1 — left region (X=80→790, width 710) holds title + decorative S-symbol; right region (X=830→1840, width 1010) holds the section list. |
| Section list eyebrow (right region) | A short ALL-CAPS label (e.g. `DISCOVERY PILLARS`, `SUMMARY`) in `.t-chapter` style, `--sudo-red`, anchored at the top of the right region with a 1 px `--rule-dark` hairline beneath it spanning the right region width. |
| Section row | One row per section. Format: `[NN]   [Section title]   [page range]`. Row height **80 px**, row-to-row gap **24 px**. |
| Section-row type | `.t-toc-row` (44 px Söhne Breit Kräftig) for title; `.t-toc-section` (32 px) for the page-range trailing label. |
| Active section | Number and title in `--sudo-white` at full brightness; numeral in `--sudo-red`; thin `--sudo-red` 1 px underline beneath the row, full row width. |
| Inactive sections | Number and title in `--sudo-dark-30` at full opacity (the color itself reads as dim against `--sudo-dark-90`). No underline. |
| Decorative graphic | `assets/symbol-red.svg` at **height ~360 px**, anchored bottom-left of the left region at `(X=80, bottom=80)`. |
| Page number | none |

**Bookend rule**: every TOC repeat in a deck uses the identical template — same composition, same graphic placement, same type sizes. Only `active_section_index` changes.

### 10.3 Content (the default — Mode 1 or Mode 2)

Every other slide. Title zone (§5), content zone (§6), page number (§7). Compose with §8 surfaces and §9 components. Vertical arrangement per §6 modes 1 or 2.

### 10.4 Closing / contact (Mode 3 — Anchored composition)

Final slide of every deck. **Mirrors the cover exactly** — same logo size, same hero brand-mark placement, same composition.

| Element | Spec |
|---|---|
| Background | `--sudo-dark-90` |
| Brand logotype | `assets/logotype-white.svg`, **height 112 px** (matches cover §10.1), top-left at `(X=80, Y=80)`. Optional partner/client logo to the right with **24 px** gap. |
| Closing statement | e.g. "Thank you." — `.t-cover` (120 px) for very short messages, `.t-headline` (80 px) for longer. White. X=80. Geometric center at **slide-midpoint Y=540** (matching cover §10.1). |
| Hero decoration | `assets/symbol-red.svg` at **height ~520 px** (matches cover), fully inset top-right at `(right=80, top=80)`. |
| "CONTACT" block | Label `.t-chapter` at `(X=80)` near the bottom; below it 1–2 contact rows with `[avatar 96 px circle][24 px gap][name (.t-toc-row, white) + role (.t-body, --sudo-dark-30) + email (.t-body, white)]`. Baseline of bottom row at Y=1024. |
| Eyebrow / page number | none |

---

## 11. Design tokens — type, color, fonts

Full tokens live in `colors_and_type.css` in the design-system project. This section locks the values the slide master depends on so a fresh agent can produce on-brand output without round-tripping.

### 11.1 Font families

| Token | Stack | Use |
|---|---|---|
| `--font-display` | `"Sohne Breit", "Söhne Breit", ui-sans-serif, system-ui, sans-serif` | Titles, eyebrows, section headers, labels, page numbers, ToC, button text, all uppercase chrome |
| `--font-body` | `"Aeonik", ui-sans-serif, system-ui, sans-serif` | All body copy, bullets, paragraphs, quotes |

**Söhne Breit** ships in two cuts only: **Buch (400)** and **Kräftig (500)**. Kräftig is the workhorse — use it for titles, eyebrows, section headers, labels, ToC rows, page numbers. Buch is for the section-divider sub-header (48 px).

**Aeonik** uses **Regular (400)** for body, **Bold (700)** for highlighted phrases, **Italic (400)** for quotes only. Air/Light/Thin/Medium/Black weights are reserved for unique scenarios — do not use them in a standard deck.

### 11.2 Color tokens

| Token | Hex | Role |
|---|---|---|
| `--sudo-dark-90` | `#15002E` | Default dark slide bg, primary text on light |
| `--sudo-white` | `#FFFFFF` | Primary text on dark, default light bg accent |
| `--sudo-dark-80` | `#26123F` | Card surfaces on dark slides (`surface/card`) |
| `--sudo-dark-70` | `#382550` | Image placeholders, deeper card variants |
| `--sudo-dark-60` | `#493761` | Hairlines on dark, muted text on light |
| `--sudo-dark-50` | `#756984` | Tertiary text on dark (chapter labels, page numbers) |
| `--sudo-dark-40` | `#8E839D` | Muted text on light (light decks — out of scope for v3) |
| `--sudo-dark-30` | `#A79CB6` | Secondary text on dark, hairlines on light |
| `--sudo-red` | `#EE0000` | Solid accent — eyebrows, deliverable callouts, focus emphasis |
| `--sudo-red-bright` | `#F40000` | Logotype/symbol red, gradient stops (`symbol-red.svg`) |
| `--sudo-red-deep` | `#B7202D` | Press state, deep accent shapes |
| `--rule-dark` | `#786A89` | Hairlines on dark backgrounds |

**Surface roles map to tokens (dark-deck only — v3 scope):**

| Master role | Token |
|---|---|
| `surface/slide` | `--sudo-dark-90` |
| `surface/card` | `--sudo-dark-80` |
| `surface/card-accent` | `--sudo-red` (solid; gradients are forbidden in cards — see §8.3) |
| `text/primary` | `--sudo-white` |
| `text/secondary` | `--sudo-dark-30` |
| `text/tertiary` (page numbers, dim metadata) | `--sudo-dark-50` |
| `accent` | `--sudo-red` |
| `border/default` (outline-state chips, hairlines) | `--rule-dark` |

Tokens for light decks (`--sudo-dark-40`, light-bg hairlines) are listed for completeness but no spec layout in §5–§10 supports a light canvas. Light-deck variants are out of scope for v3.

### 11.3 Typography scale

Sizes are calibrated for the 1920×1080 canvas in **px**. The spec uses px exclusively; if any field elsewhere reads `pt`, treat it as a typo and use the px value here.

| Role | Class | Family | Weight | Size (px) | Line height | Tracking |
|---|---|---|---|---|---|---|
| Cover title | `.t-cover` | display | 500 | 120 | 0.96 | −0.010 em |
| Section divider title | `.t-section` | display | 500 | 120 | 0.96 | −0.010 em |
| Big headline | `.t-headline` | display | 500 | 80 | 1.06 | −0.010 em |
| Slide title | `.t-title` | display | 500 | 64 | 0.96 | −0.010 em |
| Subtitle | `.t-subtitle` | display | 400 | 48 | 0.96 | −0.010 em |
| ToC row | `.t-toc-row` | display | 500 | 44 | 1.10 | −0.010 em |
| ToC section header / inline section header | `.t-toc-section` | display | 500 | 32 | 1.00 | −0.025 em |
| Standout body / pull-quote | `.t-standout` | body | 400 | 40 | 1.20 | +0.010 em |
| Body | `.t-body` | body | 400 | 32 | 1.20 | −0.010 em |
| Body bold | `.t-body-bold` | body | 700 | 32 | 1.20 | −0.010 em |
| Body italic (quotes) | `.t-body-italic` | body italic | 400 | 32 | 1.20 | −0.010 em |
| Label / button (ALL CAPS) | `.t-label` | display | 500 | 24 | 1.06 | −0.010 em |
| Chapter / eyebrow (ALL CAPS) | `.t-chapter` | display | 500 | 20 | 1.00 | −0.025 em |
| Page number | `.t-page-num` | display | 500 | 22 | 1.00 | −0.025 em |

**Italic is forbidden in all display type** — titles, eyebrows, section headers, ToC titles, stat headlines, labels. Aeonik italic is reserved for inline emphasis and quotes inside body copy (`.t-body-italic`). This is a brand-wide rule.

**Note on `.t-section-numeral` (400 px).** A 400 px display numeral class exists in the underlying type system for an alternate numeric-divider variant. v3 does not use it — TOC dividers (§10.2) use `symbol-red.svg` for decoration. If this variant is reintroduced in a future version, it becomes the §10.2 alt.

### 11.4 Eyebrow / chapter label — concrete spec

The eyebrow defined in §5.1 maps to `.t-chapter`:
- **20 px**, Söhne Breit Kräftig (500), ALL CAPS
- Line-height 1.00, tracking −0.025 em (−2.5%)
- Color: `--sudo-red` for the leading section label; `--sudo-dark-50` for the trailing subsection label
- Chevron separator: plain text ` › ` in the same color as the trailing label

Example: `TOKENISATION › OVERVIEW` — "TOKENISATION" in red, ` › OVERVIEW` in `--sudo-dark-50`.

### 11.5 ALL-CAPS rule

**Use ALL CAPS in labels, eyebrows, chapter chrome, and button text only.** Slide titles are title-case. Body copy is sentence-case. Section headers (§9.2) are title-case. Nothing else is uppercase.

### 11.6 Hairlines

1 px solid. **`--rule-dark` (`#786A89`)** on dark backgrounds. Used as section separators (e.g. under the section-list eyebrow on TOC slides per §10.2, between standout blocks and body content). Never as containment (cards do not have hairline borders — see §8.3).

---

## 12. Composition rules (the meta-rules that govern the whole deck)

These are the rules that surfaced repeatedly across every revision pass. They are higher-priority than any single component spec — when a component rule and a composition rule conflict, the composition rule wins.

### 12.1 Distribute, don't stack (§6.1)

Content slides fill the content zone from title bottom to bottom safe margin. Two anti-patterns to eliminate: tight clusters floating in an empty zone, and top-anchored stacks leaving dead floor.

### 12.2 Equalize peers

If two things are visually peers, they must be **pixel-equal on every measurable axis**: heights, widths, paddings, eyebrow margins, divider thicknesses, font sizes, opacities. Auditing peer-equality is a final-pass design step, not optional polish.

### 12.3 Eyebrow as the navigational primitive

Every distinct content unit on a slide gets an eyebrow naming what it is — sections, sub-sections, column groups, diagrams, special widgets. Without eyebrows the slide reads as a wall; with them it reads as an outline.

### 12.4 Three-fill scale, no fourth color (§8)

Importance is expressed by fill density: outline → dark → red. No yellow, blue, green, amber tints — even for semantic differentiation.

### 12.5 Same-shape grids: structural uniformity, content variation

In a grid of equivalent units (4-step methodology, comparison columns, deliverable rows), every cell must share the same **structural template**: same width, same internal layout, same fonts, same paddings, same eyebrow position, same component composition.

**Content can vary**: one cell may carry a "DELIVERABLE" callout, another may have a different image, the bullet text is per-cell. But the *visual rhythm* of the row stays uniform — the difference is contained within the template, never disrupting the slide's smoothness.

What this rules out: special-case columns where one cell uses a different layout, a different padding, a different size, or a different chrome. If the spec markdown asks for cell N to have a unique structure, the design pushes back — either every cell gets the structure, or it lives in a separate slide.

### 12.6 No AI-slop tropes

The deck looks more confident with less. The following are forbidden:

- Generated decorative gradients, blobs, or invented shapes when a brand asset exists
- Italic display type (titles, eyebrows, section headers)
- Yellow / amber / blue / green / "warm" / "cool" accent variants
- Decorative scaffolds that duplicate content meaning (e.g. a week-strip below an already-numbered 1→2→3→4 step row)
- Redundant column headers on single-purpose columns
- Uppercased mid-content labels (uppercase is for eyebrows only)
- Rounded-corner left-border-accent containers
- Emoji as design elements

When in doubt, remove the decorative element rather than add one.

### 12.7 Bookend slides are a matched pair

Cover and closing share a visual vocabulary: same hero logotype size, same brand-mark placement, same composition. Body slides may vary; the anchors cannot. Every TOC repeat across the deck uses the identical template.

### 12.8 Diagrams are labeled, centered, structurally-rigorous artifacts

Every diagram (architecture, tree, Gantt, methodology) needs:

- An **eyebrow** naming what it is ("DLT ARCHITECTURAL DIAGRAM")
- **Centered placement** in the available space (horizontal and vertical)
- **Uniform repeating elements** (chips, nodes, rows) per the §9 component patterns

A diagram missing any of these reads as a free-form sketch and is not finished.

### 12.9 Generous defaults — the "slide is not a webpage" rule

Default vertical spacing in a deck is roughly 2× what feels right on a webpage:

- Bullet gaps in card lists: ≥ 24
- Inter-section gaps within a slide: ≥ 80
- Bottom slide buffer below the lowest content element: ≥ 48

Slides are read at a distance and demand more air.

### 12.10 Hard-edged, no decoration except sanctioned brand assets

This is a hard-edged brand:
- Border radius is **0** for all containers (cards, bands, chips, pills). Circles only for avatars.
- **No drop shadows. No inner shadows. No glows.**
- **No blurs. No frosted glass. No semi-transparent overlays.**
- **No textures. No patterns. No grain.**
- **Gradients exist only on `symbol-red.svg`** — never on cards, bands, chips, backgrounds.
- The only sanctioned decorative graphics are: `assets/symbol-{red,violet,white,outline}.svg`. **Nothing else may be drawn.** If the brief asks for an icon set, substitute Lucide at 2 px monochrome and flag it.

### 12.11 Hierarchical-diagram template uniformity

In any tree, flow, or tiered diagram with multiple node types (e.g. Area / Objective / Use-case), **every node tier shares the same internal template**: ALL-CAPS tier kicker on top in `--sudo-red`, node name below in `.t-body` or `.t-body-bold`. Different tiers may differ in box width or background fill, but never in the number, ordering, or styling of internal text elements. This is §12.5 (same-shape grids) applied vertically across diagram tiers.

---

## 13. Reference and audit trail

The rules in this spec are derived from the **goX v3 Discovery Proposal (April 2026)** as the canonical reference deck. A slide-by-slide diff log of changes from the initial agent-generated draft to the final approved output lives at `deck-diff-log.md`. When a rule is unclear or appears to conflict with another, consult the diff log for the original evidence.

The companion authoring skill — `SKILL.md` — defines the markdown brief format that PMs use to feed this spec. The brief specifies *what* each slide says; this spec governs *how* it looks. The two together should produce on-brand decks with zero layout iterations.

---

## 14. QA checklist

Run before any deck ships. A failing item is a layout bug.

**Spacing & grid**
- [ ] All gaps come from the spacing scale (4 · 8 · 16 · 24 · 32 · 40 · 48 · 56 · 64 · 80). Twelve only appears in the three documented places (§2.2). No 22s, 25s, 36s, 72s.
- [ ] No element crosses the 80 px safe frame.
- [ ] All cards in the same row are the same height (lock to the tallest).
- [ ] Sibling cards in a row are separated by exactly one gutter (40 px).
- [ ] Card padding is 56 (top-level) or 32 (nested). No exceptions.
- [ ] No card nesting beyond depth 2.

**Title & navigation**
- [ ] Title is white-only — no red emphasis runs inside the title.
- [ ] Title is roman — no italic display type anywhere in the deck.
- [ ] If present, the eyebrow is red, ALL CAPS, at Y=80.
- [ ] Title cap-top at Y=128 — not floating freely.
- [ ] Page number `NN / TT` on every content slide; omitted on cover/divider/closing.

**Vertical arrangement**
- [ ] Every content slide picks one of the three modes (§6).
- [ ] Mode 1 slides distribute to fill — no dead floor below the lowest content element, no tight cluster floating in empty space.
- [ ] Mode 2 slides center the payload at the content-zone midpoint (Y=631 for 1-line title or Y=666 for 2-line title), not at fixed Y=540.
- [ ] Mode 3 slides match the cover/closing/divider templates exactly. Cover and closing use slide-midpoint Y=540 — this is intentional and distinct from the Mode 2 anti-pattern.

**Surface & color**
- [ ] Only three fill states are used: outline, dark-fill, red-fill. No fourth color.
- [ ] At most one element on a slide carries red-fill emphasis — the focal point.
- [ ] Text on coloured chips/pills/bands is white.

**Composition**
- [ ] Body text is left-aligned. Centered text is for stat boxes only.
- [ ] List item gap is 16 px (or expanded per Mode 1); wraps align under text.
- [ ] Diagrams have an eyebrow label and are centered in their region.
- [ ] Section dividers reuse the same TOC template across the deck.
- [ ] Cover and closing mirror each other (logo size, brand-mark placement).
- [ ] Every distinct content unit on a slide has an eyebrow naming what it is.

**Structural integrity**
- [ ] Same-shape grids are structurally uniform — every cell shares the template, even when content varies.
- [ ] No AI-slop tropes (§12.6): no invented decoration, no italic display, no fourth color, no redundant scaffolds, no emoji.
- [ ] All node boxes in hierarchical diagrams share the same internal template across tiers (§12.11).
- [ ] Parent nodes in tree diagrams are vertically centered on their children's midpoint.
- [ ] Direct-edited text has not been auto-overwritten (§0).

**Brand tokens & hard-edged rules (§11, §12.10)**
- [ ] Display type uses Söhne Breit Kräftig (500); body uses Aeonik Regular (400). No other families.
- [ ] All sizes in px — if any spec field reads `pt`, the px value from §11.3 wins.
- [ ] Slide background is `--sudo-dark-90` (`#15002E`). Cards are `--sudo-dark-80` (`#26123F`).
- [ ] Red used is `--sudo-red` (`#EE0000`) — never any other red, orange, or warm hue.
- [ ] All cards, bands, chips, pills have border-radius 0. Circles only for avatars and the symbol mark.
- [ ] No drop shadows, inner shadows, glows, blurs, or semi-transparent overlays.
- [ ] No gradients except inside `symbol-red.svg` itself.
- [ ] Cover and closing use `assets/logotype-white.svg` at 112 px height and `assets/symbol-red.svg` at ~520 px height, both fully inset (not bled).
- [ ] Working slides use the small chrome logotype only when needed (or omit — the eyebrow + page number identify the deck).
- [ ] Decorative graphics are limited to: `assets/symbol-*.svg`. No other drawn graphics.
