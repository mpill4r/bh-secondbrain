# Second Brain

> Marek Pillár's personal knowledge system — capturing and sorting thoughts, ideas, and todos from day-to-day PM work at BigHub. Fed by screenshots, messages, notes, and call transcripts. No client — this is a personal tool, not a client engagement.

## Typical Workflow

1. **Start a session** — Claude reads the latest daily and briefs you
2. **Upload documents** — `/project-document` to ingest screenshots, notes, PRDs, research
3. **Upload meetings** — `/project-meeting-upload` to process call transcripts and notes
4. **Enrich artifacts** — `/product-brief`, `/project-knowledge`
5. **Define scope** — `/product-scope {phase-slug}` if a concrete initiative ever needs delivery tracking
6. **Specify features** — `/product-feature FEAT-NNN` for implementation-ready specs, if needed
7. **Review status** — `/project-daily` for today, `/project-weekly` for the week
8. **Close the day** — `/project-daily close` to wrap up and capture lessons

## Command Reference

### Core (used regularly)

| Command | Purpose |
|---------|---------|
| `/project-daily` | Query across daily logs — action items, events, trends |
| `/project-weekly` | Generate weekly status summary |
| `/project-document` | Ingest any document (or screenshot) — summary + routing |
| `/project-meeting-upload` | Process a call transcript or notes into structured notes + routing |
| `/project-meeting-prep` | Generate a meeting prep document from harness context |
| `/project-knowledge` | Review and enrich the personal knowledge base |
| `/project-assumptions` | Review and manage assumptions and decisions |
| `/project-lessons` | Review captured lessons learned |
| `/project-stakeholders` | Review people mentioned across captures |
| `/project-overview` | Review and update the project overview |
| `/product-brief` | Enrich the product brief via coaching Q&A |

### Available if ever needed (delivery/client-oriented, likely unused for this use case)

| Command | Purpose |
|---------|---------|
| `/client-overview` | Client intelligence — N/A, Second Brain has no client |
| `/product-requirements` | Review and manage requirements |
| `/product-scope` | Create or update phase-level scope and delivery tracker |
| `/product-feature` | Create or update a feature specification |
| `/product-slidedeck` | Create, update, or review a slide deck specification |
| `/product-codebase-audit` | Analyze an existing codebase and produce a product baseline |
| `/product-backlog-import` | Import planned work from an external backlog tool |

## Repository Structure

```
bh-secondbrain-new/
├── CLAUDE.md                        # AI co-pilot configuration
├── README.md                        # This file
├── .claude/
│   ├── harness-artifacts-index.md   # Central artifact registry
│   ├── commands/                    # Slash command wrappers
│   └── skills/                      # Skill logic (SKILL.md + TEMPLATE.md)
├── project/management/              # Team, overview, client-overview (N/A), assumptions, lessons, knowledge
├── project/daily/                   # Daily context logs
├── project/weekly/                  # Weekly status summaries
├── product/problem-space/           # product-brief, product-requirements
├── product/solution-space/          # scope + feature specs, if ever used
├── meetings/                        # Call transcripts and meeting notes — internal/client/external/milestone/prep
└── documents/                       # Ingested documents and screenshots — internal/client/external
```

## Team

| ID | Name | Role |
|----|------|------|
| STK-001 | Marek Pillár | PM (sole user) |

## Note on Dr. Max content

Second Brain has no client of its own, but a large share of what flows into it is Marek's real day job — BigHub's delivery work on the Dr. Max (ČLH) account. That content is tracked as regular harness data (stakeholders, assumptions, knowledge, meeting notes), not through `client-overview.md`, since Dr. Max is BigHub's client, not Second Brain's.
