---
last_updated: 2026-09-11
classification: Technical
source: internal
original_location: /Users/marekpillar/Downloads/Chatbot-Max-product-spec.cs.pdf, /Users/marekpillar/Downloads/Chatbot-Max-tech-spec.cs.pdf
---

# Chatbot Max — Product & Technical Specification (Release 1438820, TEST)

## Document Info

**Title**: Chatbot Max — Produktový přehled (Product Overview) + Technická specifikace (Technical Specification), Release 1438820 (TEST)
**Author(s)**: Not attributed in either document
**Date**: 2026-09-10
**Classification**: Technical (paired with PRD/Requirements-level content from the product spec — combined into one summary per PM's request, since both describe the same release)
**Source**: Internal — two PDFs, originally in Czech, provided by the PM
**Previous version**: N/A — first ingestion of formal Max Chatbot specs into the harness

## Executive Summary

Two paired, formally-written specs (product overview + technical architecture) for Max Chatbot's currently-piloted release (1438820, TEST environment, VPN-only), dated 2026-09-10. They document, in much more precise detail than anything previously captured in the harness, exactly what the chatbot does (product search, pharmacy stock lookup, nearest-pharmacy lookup, order status, eRecept status + "where to buy"), what it deliberately never does (no medical advice, no Rx sales, no accounts/memory), and how it's built (a shadow-DOM/iframe widget loader, a stdlib-Python backend with an LLM tool loop capped at 4 rounds, a "core.tools" layer explicitly shared with the future voicebot, and a caching/politeness layer sitting in front of Dr. Max's unofficial public API). The project team should treat this as the authoritative reference for Max Chatbot's actual current capabilities and constraints going into the client roadmap presentations — it resolves several previously-vague roadmap items (public-launch blockers, kill-switch mechanics, Maxie/Chatbot core-sharing) with concrete technical detail.

## Key Points

### Product overview (customer-facing)

- **Core functions**: product search (with price/availability/Rx-flag), stock-near-me, nearest open pharmacy (distance/hours/phone/directions), order status (requires order number + email/phone together), eRecept status with a "kde koupit?" (where to buy) button per prescribed medicine.
- **Free text**: an AI model maps any phrasing to the above actions; ambiguous queries (e.g. "paralen") become a single-choice carousel. Every function also works via menu buttons with no AI involved.
- **Deliberately out of scope**: no medical/pharmaceutical advice of any kind (polite refusal + referral to a pharmacist); prescription medicines are never sold, only "where to buy" is shown; no accounts, no login, no cross-page memory, no stored health data.
- **Deployment control**: a single embed line on drmax.cz, controlled entirely BigHub-side (enable/disable/rollback in minutes, no further web-team involvement); three states — hidden (default at launch, team-only), live, off (kill switch).
- **Integrations**: Dr. Max product search, stock service, pharmacy list (hourly refresh), Rx catalog (matched via official SÚKL code, no guessing), Orders/eRecept service (internal, authenticated; TEST runs on sample data), Azure OpenAI (sees only chat text, never orders or health data, not used for training).
- **Current state / before public launch**: full feature set running on internal TEST (VPN) with sample orders/prescriptions. Still needed before public launch: edge-network rate limiting, finalized disclaimer copy, a privacy decision on eRecept lookup, and production data for orders/eRecept. Usage analytics (what people ask, where it fails) is a further planned step.

### Technical architecture

- **Widget delivery**: `widget.js` loader is the only thing the host page references — renders a launch pill into a closed shadow root (host CSS/JS can't reach in) and lazily creates the chat panel as a cross-origin iframe; `postMessage` is the only bridge, origin-pinned both ways.
- **Release mechanics**: immutable, content-hash-named bundles (`chat.<hash8>.html`, cached immutable for 1 year); the only mutable file is `manifest.json` (60s TTL) — it maps channels (stable/beta, previewable per-browser via localStorage) and the kill switch. Publish/rollback/kill-switch are all just a values change, never a rebuild. Frontend and backend images build from the same commit SHA and are promoted together, so the widget↔API contract can never drift permanently out of sync.
- **Backend**: pure-stdlib Python; `/api/*` is a tool proxy plus the LLM "brain" — the Azure OpenAI API key never reaches the browser. A **`core.tools` layer** (search, stock, pharmacies, orders, eRecept, Rx catalog) is explicitly built channel-independent and **shared with the future voicebot** — i.e. Maxie.
- **LLM tool loop**: free text POSTs the transcript tail to `/api/chat`; the brain (Azure OpenAI, gpt-5-mini) runs a capped tool loop (≤4 rounds, output/transcript trimmed) and returns a short reply plus structured cards, rendered by the same components as the deterministic flows. If the brain is unavailable, the widget falls back to deterministic/regex flows — it's designed to never end in dead UI.
- **Guardrails** (explicit list in the tech spec): no medical advice (hard refusal + pharmacist redirect); order privacy via a narrow model whitelist (unknown order number and wrong contact are indistinguishable by design — "no oracle"); health-data minimization (eRecept ID and prescribed products never enter LLM context — Rx "where to buy" resolved server-side by SÚKL code only); tool results treated strictly as data, never as instructions (prompt-injection posture); coordinates/city names resolved against BigHub's own pharmacy data, never the model's say-so; hard spend ceilings (4-round cap, output-token limit, transcript trimming).
- **Session context (CTX)**: the widget collects structured facts it already has (rendered product SKUs/names, a verified order + contact) and sends them with every chat call — lets "that paralen" resolve even after the transcript window has scrolled past it, and lets the brain reuse a SKU from session without re-searching.
- **UI-not-prose principle**: ambiguity and data-collection slots always render as UI (variant-picker carousels, canonical inline forms for order number/contact/eRecept ID) — the model never asks for these in prose, and the text reply is suppressed server-side once a form fires.
- **Streaming**: `/api/chat` supports SSE — content streams token-by-token, and each tool call emits a status event (drives the "thinking" label, e.g. "hledám produkty"). Pre-first-event failures preserve real HTTP status codes (503 still triggers the regex fallback); mid-stream failures become an `error` event with a retry chip. Backwards/forwards compatible — an old widget gets plain JSON, a new one accepts either.
- **Caching / upstream politeness**: the tool layer sits in front of Dr. Max's own **unofficial public website endpoints** and is deliberately polite — request coalescing (concurrent identical queries merge into one upstream call), stale-while-revalidate, negative caching (empty results cached too, short TTL), stale-on-error (upstream outage serves last-good value), and a per-host politeness token bucket that smooths spikes without ever rejecting a request. Search caches by normalized query (TTL 3 min + 3 min SWR grace); stock caches per-SKU (TTL 60s, ordering computed per-request); Rx catalog resolves by exact SÚKL code with its own 10 min cache; the full pharmacy list (~800 branches) refreshes hourly, single-flight, serves stale on upstream outage. Orders and eRecept are never cached. The LLM system prompt/tool definitions are a stable prefix, so Azure's automatic prompt cache covers every brain call for free.
- **Operations**: environment naming `chatbotmax-<env>.cz.dr-max.global`; TEST is VPN-only with mocked orders/eRecept; branch→environment is master→PROD, everything else→TEST. Readiness health check requires the pharmacy cache to be warmed with real rows (stale counts as ready, zero rows doesn't). Degradation: LLM outage → 503 → regex flow; manifest outage → loader fails closed (no widget, never a broken one). Secrets: Azure OpenAI credentials flow via a central KeyVault → ExternalSecrets → pod env, never in git or the browser. PII: order/eRecept identifiers are stripped from access logs, full chat bodies are never logged; tester feedback (opt-in transcript) goes to a temporary emptyDir + pod log only. Test suite: 289 tests — unit (mocked upstreams, an egress tripwire), architecture-as-code rules, and opt-in live integration probes.
- **Explicitly out of scope for v1**: any medical/pharmaceutical advice; public exposure (blocked on the platform's public entry path — Cloudflare rate limiting on `/api/*` is assumed infrastructure; the channel gate is presentation only, not access control); conversation persistence across page navigation (pending a data-retention decision). In progress, not in this release: usage analytics (allowlisted business events only, no free text/contacts/identifiers/Rx identity → Postgres → a static Czech report) — on a branch, lands once the shared platform's Postgres is available.

## Extracted Requirements

| ID | Requirement | Source |
|----|-------------|--------|
| DR-1 | Chatbot must never give medical/pharmaceutical advice — symptom/dosage/interaction questions get a polite refusal + pharmacist referral | Product spec §2 |
| DR-2 | Prescription medicines are never sold via the chatbot — "where to buy" only shows pharmacies that stock it | Product spec §2 |
| DR-3 | No accounts, no memory — no login, no cross-page history, no stored health data | Product spec §2 |
| DR-4 | Widget must support 3 states (hidden/live/off) controlled entirely BigHub-side, without touching the client's website | Product spec §3 |
| DR-5 | Visual style must match Dr.Max branding (green action color; desktop panel, full-screen mobile) | Product spec §3 |
| DR-6 | Order-status lookup requires both the order number AND email/phone together — knowing only one isn't enough | Product spec §1 |
| DR-7 | eRecept lookup by ID shows status plus a "where to buy" action per prescribed medicine | Product spec §1 |
| DR-8 | Ambiguous free-text product queries resolve via a single-choice carousel, not a text list | Product spec §1 |
| DR-9 | Before public launch: edge rate limiting, finalized disclaimer copy, a privacy decision on eRecept lookup, and production order/eRecept data are required | Product spec §5 |
| DR-10 | Widget must never end in dead/broken UI — falls back to deterministic flows whenever the LLM brain is unavailable | Tech spec §1, §2 |
| DR-11 | LLM tool loop is hard-capped at ≤4 rounds with output-token and transcript-trim limits | Tech spec §2 |
| DR-12 | Prescription IDs and prescribed products must never enter the LLM context — Rx "where to buy" is resolved server-side by SÚKL code only | Tech spec §2 |
| DR-13 | Tool results are treated strictly as data, never as instructions — prompt-injection posture; location/city resolution never trusts model choice | Tech spec §2 |
| DR-14 | Ambiguous choices and data-collection slots always render as UI components, never requested via free-text prose | Tech spec §2 |
| DR-15 | Azure OpenAI API key must never reach the browser | Tech spec §1, §5 |
| DR-16 | Frontend and backend images build from the same commit SHA and are promoted together — the widget↔API contract can never permanently drift | Tech spec §1 |
| DR-17 | Order/eRecept identifiers are stripped from access logs; full chat bodies are never logged | Tech spec §5 |
| DR-18 | Orders and eRecept data are never cached | Tech spec §4 |
| DR-19 | Public exposure requires Cloudflare rate limiting at the platform's public entry path — the channel gate is presentation only, not access control | Tech spec §6 |
| DR-20 | Test suite currently at 289 tests (unit w/ mocked upstreams + egress tripwire, architecture-as-code rules, opt-in live integration probes) | Tech spec §5 |

## Extracted Decisions & Assumptions

| ID | Decision/Assumption | Source |
|----|---------------------|--------|
| DA-1 | The `core.tools` layer (search, stock, pharmacies, orders, eRecept, Rx catalog) is deliberately shared with the future voicebot (Maxie), not incidental overlap | Tech spec §1 |
| DA-2 | Product search/stock/Rx-catalog matching integrate against Dr. Max's own **unofficial** public website endpoints, mitigated by a deliberately "polite" caching/rate-limiting client rather than an officially sanctioned API | Tech spec §1, §4 |
| DA-3 | Conversation persistence across page navigation is explicitly deferred pending a data-retention policy decision — not merely deprioritized, actively blocked on a decision | Tech spec §6 |
| DA-4 | Usage analytics (allowlisted business events only) is in progress on a separate branch and lands once the shared AI platform's Postgres is available | Tech spec §6 |
| DA-5 | A kill-switch mechanism already exists and is live for Max Chatbot specifically, via a ConfigMap-mounted `manifest.json` (60s TTL) controlling per-channel rollout and a kill switch | Tech spec §1 |

## Key Stakeholders & Contacts

None named in either document — both specs are unattributed. All 6 people currently in `project-stakeholders.md` associated with Max Chatbot (Jura Brázdil, Honza Zelený, etc.) are already tracked; no new names surfaced here.

## Open Questions

- Privacy approach for eRecept lookup/retrieval is explicitly flagged as undecided (product spec §5) — needs a decision before public launch.
- Final disclaimer wording is not yet finalized.
- Data-retention policy for cross-page conversation persistence is undecided, blocking that feature.
- Neither document names an author or owning team — contextually this is almost certainly Jura Brázdil's work (per existing stakeholder notes), but that's inferred, not stated in the source.

## Routing Log
