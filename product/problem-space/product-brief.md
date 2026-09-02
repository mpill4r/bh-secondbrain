---
last_updated: 2026-09-02
last_updated_by: manual — conversational (product-brief staleness Q&A)
---

# Product Brief — Second Brain

## 1. Product North Star

Zero-loss capture: nothing Marek encounters at work — an idea, a todo, a decision, a risk — is ever lost or forgotten. Everything lands somewhere structured and retrievable.

## 2. Problem Definition

Marek's thoughts, ideas, and todos are scattered across screenshots, messages, notes, and call transcripts from his day-to-day work as a PM at BigHub, with no single structured place to sort and retrieve them.

### Why Current Approaches Fail

| Current Approach | Why It Falls Short |
|-----------------|-------------------|
| Scattered notes apps, screenshots, messages | No structure — nothing links together or gets surfaced again when needed |
| Memory + ad-hoc reminders/calendar entries | Doesn't scale past a handful of active threads; relies entirely on Marek personally remembering to check |
| Generic PM tools (Notion, Jira, etc.) | Built for tickets, not the messy reality of PM work — meetings, stakeholder sentiment, evolving assumptions, audit trails |

## 3. Target User Personas

### Persona: Marek Pillár

| Field | Value |
|-------|-------|
| Role / Title | PM at BigHub |
| Context | Sole user of this second brain; captures thoughts via screenshots, messages, notes, and call transcripts |
| Primary Goal | Keep thoughts, ideas, and todos sorted and easy to retrieve |
| Pain Points | Ideas and todos scattered across many capture sources with no central place |
| Success Looks Like | Full trust in the harness's records (no need to re-verify dailies/stakeholders/assumptions himself) combined with fast context recall — walking into any meeting or situation and getting fully up to speed in under a minute instead of scrolling old notes |

## 4. Business Goals & Success Metrics

Not a commercial product — there's no revenue/growth metric. Success is measured as: nothing falls through the cracks — zero missed action items or follow-ups across all accounts over a sustained stretch of time (e.g. a month).

## 5. Solution Definition

### Product Perspective
A personal knowledge system that ingests free-form captures (screenshots, messages, notes, call transcripts) and routes them into structured artifacts — daily logs, action items, knowledge base.

### Business Perspective
N/A — not a commercial product.

### Market Perspective
N/A — personal use only.

### Technology Perspective
Claude Code driving a git-tracked markdown file structure — no separate app, database, or hosted service. Skills/commands (this Product Harness) define the entire behavior; the artifacts themselves are the persistence layer.

## 6. Market Positioning

N/A — personal tool only, no market.

## 7. Scope Boundaries

Strictly single-user (Marek only) — no sharing, no team collaboration features are ever in scope. Work/client-account content only — personal life and non-BigHub notes stay out.

This harness is intended to remain the umbrella library across all of Marek's Dr. Max-related work; as individual Dr. Max streams/projects mature, they may eventually get their own dedicated project-oriented harnesses — splitting those off is explicitly out of scope for this harness itself, which stays the central library rather than narrowing to any one project.

## 8. High-Level Phasing

| Phase | Focus | Target Release | Key Outcomes |
|-------|-------|---------------|-------------|
| Phase 1 | Get the harness stood up and stable while using it live to ramp onto the Dr. Max account — building toward this harness serving as the umbrella covering all Dr. Max projects | Ongoing — no fixed date | Full Dr. Max coverage (all active streams/stakeholders/assumptions captured and kept current) and a solid daily-use habit (dailies, meeting routing) with no gaps |

> Detailed scope for each phase: see `product-scope-{phase-slug}.md`
