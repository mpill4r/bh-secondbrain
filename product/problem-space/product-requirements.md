---
last_updated: 2026-10-05
last_updated_by: auto — project-meeting routing
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

## Business Requirements

**REQ-002** · Business · Open · 2026-10-05
**Source**: Tereza Foltová via 2026-10-05-reklamace-next-steps-zurek-pilot-roadmap

Reklamace: for defective medical devices, notify the actual manufacturer's factory (which can differ by batch) with a predefined email, in addition to the supplier. Dr. Max has no manufacturer database today. See [[ASM-251]].

## Data Requirements

{Data-type requirements}

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
