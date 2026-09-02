---
last_updated: 2026-09-01
type: internal
attendees: [Marek Pillár, Filip Černý]
tldv_link:
---

# Introduction to the Dr. Max Listing Project

**Date**: 2026-09-01
**Attendees**: Marek Pillár (Product Manager — listening/asking questions), Filip Černý (presenting — prior owner/builder of the Listing project; role and organization not stated in transcript, likely BigHub given references to owning the build himself)
**Type**: internal (project intro)
**Recording**: N/A
**Previous session**: N/A
**Meeting prep**: N/A

> **Data quality note**: the source transcript's speaker diarization failed — every line is labeled "Marek Pillár" regardless of who was actually speaking. Per PM confirmation, Marek was listening/questioning and Filip Černý was presenting. Individual lines below could not be reliably re-attributed, so this note summarizes by topic rather than quoting with speaker attribution. Treat direct-quote-style lines as approximate, not verified per-speaker.

## TL;DR

Filip walked Marek through the Listing project he previously built largely solo, plus two adjacent projects (fakturace dopravy / shipping invoicing, and reklamace / complaints) that share infrastructure with it. Core theme: Dr. Max's product category and variant data is deeply messy, no clean single source of truth exists, and every integration currently runs through fragile Magento import/export rather than direct system access — which is treated as an acceptable interim approach for now.

## Key Discussion Points

### Project landscape and ownership

Filip described three related projects: **Listing** (his one-man show — most recent, most current knowledge), **Fakturace dopravy** (shipping invoicing — detailed spec exists from Honza, complex due to authentication work, largely a classic software build), and **Reklamace** (complaints — mostly built by "Kuba Turner," with "Flurimo" also involved; Filip did some of it, Lukáš now does too). Fakturace dopravy and Reklamace share a spec and a logistics domain and are effectively a monorepo. Neither has significant data-science/GNI content — Listing is the one with real data-science and integration weight.

### Boomy / integration architecture

Communication between BigHub's systems and Dr. Max flows through a middleware called **Boomy** — a low-code/no-code tool, owned not by "Dr. Max Česko" but by the parent entity **Dr. Max BDC**. Filip described the people managing Boomy on the client side as not very technical, causing friction; he spent significant time debugging integration issues on Reklamace through it. Communication with the actual technical contact behind Boomy has reportedly been unclear/inconsistent — a person Filip suspects may be overworked or under-resourced (framed sympathetically: "hard to say if it's incompetence or he's drowning").

### Listing project — current state and blockers

- Listing is live/in production ("version 1" per Filip's framing) but not integrated with live client data yet — currently running on **hardcoded test data** chosen by the client team. Export/import to live data is the single biggest open challenge.
- Underlying data is described as a genuine mess: a listing spreadsheet with roughly **45,000 rows × ~1,200 columns** covering attributes like flavor, price, payment eligibility (e.g. Eden Red benefit cards), visibility rules (some products hidden from the e-shop for regulatory/sensitivity reasons), SEO parameters, and marketplace-specific fields.
- **Variant handling** is unresolved: products can have colour/flavor variants that should share a base description with auto-propagated differences (a "paneling" feature the client explicitly wants), but the client's own data isn't clean enough yet — e.g. duplicate or inconsistent IDs across what should be the same product's variants.
- **Category definitions** are not owned or clearly defined on the client side. Listing/testing categories (e.g. "proteins") turned out to have contradictory rules (different stocking minimums depending on whether an item is a food/drink addition vs. a substitute). Filip proposed a hierarchical listing-minimum structure to the client contact **Neumann**, who responded positively, but the client side still hasn't formally decided or delivered the category system. This is currently the main blocker to a clean integration.
- A related, not-yet-decided idea from the client: reduce the ask from ~100+ granular categories to about **10 categories** that matter most over the next six months, iterating from there.
- Client-side team for Listing: **pan Neumann** (handles all listings, reports to a bigger boss), **paní Vdovicinová** (leads the listing team, owns content — descriptions, parameters — with people working under/with her).
- A separate, not-fully-overlapping client-side initiative exists: a **"vendorský portál"** (supplier portal) meant to let suppliers submit listings directly in a unified format — not built by BigHub, possibly not built by anyone yet, but its scope partially overlaps with Listing's validation/labeling needs.
- Interim integration approach (agreed workable): rather than direct system access, use a lightweight scheduled **import/export via Magento**, roughly a 10-minute weekly task, with the client able to revert changes easily if needed.

### Data science / demand forecasting workstream

Filip referenced a parallel workstream — **order/demand management** ("řízení poptávky") — built with help from **U.R.A.I.**, particularly **Juraj Kmetz** (nicknamed "Dury"/"Košičan" — distinct from another contact simply named "Jura," who works with dogs/pets, not statistics) and a contact named **Uray**. This modeling work covers forecasting order volume and revenue, split into strategic-planning-level (daily/weekly, high-level) and logistics-level (shift planning, 6–12 hour granularity) consumers, with largely identical underlying data/models. The team has been "doing genuinely hard hours" on this with URAI; it's a difficult task partly because clean historical data barely exists (roughly the last two years are usable; further back is disrupted by "the war" — presumably a reference to COVID-period or an actual conflict-driven business disruption, not otherwise specified).

### Fakturace dopravy & Reklamace — apps and status

Several purpose-built internal apps support these flows:
- A **mobile app for logistics/reklamace field staff** to scan a barcode/SP label (already tested, working) and pull data from **Exapta**, letting the worker confirm/adjust quantities.
- A **complaint-photo/documentation app** ("last app," described as heavily under construction) for photographing damaged goods and generating a workflow/email to the relevant party.
- A **shipping-invoice document app**: the core idea is that couriers arrive with paper delivery documents, which get scanned at a kiosk. The client insists paper is the source of truth — no user editing of scanned values; if a date is misread, the driver corrects the physical form and rescans, rather than editing digitally. Backend for this is implemented and stable in a private version; the kiosk-facing frontend still needs work, inspired by an existing "newewbcoding" demo Excel/design language Filip was shown.
- Both Fakturace dopravy and Reklamace integrate against **AXAPTA** (people involved: **Kopecký**, **Sláma**) and **Boomy** (contact: **pan Koupčík**). Business owners: **paní Egermajerová/Majerová** for Reklamace (Filip described her warmly — "fajn paní"), and **pan Jan Žižka** as a business owner Filip has not personally met (described half-jokingly). Filip has also not met **Petr Spilka** or **Marie Ulešová**, who apparently also touch this area.
- A related internal tool ("My Cloud Endpoint" or similar — exact name uncertain) appears to be a client-side BI/analytics layer covering all complaint cases; treated as a black box BigHub can plug into rather than something to build.

### Marek's context-gathering plan

Marek explained he's been sitting on the sidelines for this project (per Honza, he'll be one of the incoming project/product people looped in) and is trying to reconcile several partial sources: an existing FigJam board, various markdown/chat notes from Honza, an "obří tabulka" (giant spreadsheet) from the client, and now Filip's walkthrough — aiming to build a single high-level map for himself before syncing further with the client. He flagged that he still needs to connect with **Radoslav ("Rado")** to track down a complete version of the current spec, since no single document currently holds it end-to-end.

Filip offered Marek access to a local ("Krno") environment with real data so Marek can explore the listing tool himself, since Marek doesn't currently have a webpage/hosted version to test against.

## Decisions Made

- Interim Listing/e-commerce integration will continue via scheduled Magento import/export rather than direct system access, accepted as a reasonable short-term tradeoff.
- Filip will give Marek access to a local ("Krno") environment with real data so he can explore the Listing tool directly.

## Action Items

- [ ] **Marek**: Sync with Radoslav ("Rado") to locate a complete, current version of the Listing spec — due -tbd- — from dr-max-listing-introduction
- [ ] **Neumann / client side**: Formally define and deliver the category system (or the proposed hierarchical listing-minimum structure) needed to unblock integration — due -tbd- — from dr-max-listing-introduction
- [ ] **Filip**: Set Marek up with access to the local ("Krno") environment/real data for the Listing tool — due -tbd- — from dr-max-listing-introduction
- [ ] **Marek**: Consolidate FigJam, Honza's notes, the client's giant spreadsheet, and this walkthrough into one high-level map — due -tbd- — from dr-max-listing-introduction

## Open Questions

- What is Filip Černý's role/organization on this account? (Not stated in transcript — needs confirmation.)
- Who exactly is "Ono"/the technical contact behind Boomy, and can communication with them be made more reliable?
- Will the client formally reduce their category ask to ~10 categories, or continue with the current more granular set?
- What is the "My Cloud Endpoint"-type internal client tool actually called, and who owns it?
- Is there a real prior spec covering Listing end-to-end anywhere, or does Marek need to write one from scratch?

## Sentiment & Tone

Collegial knowledge-transfer session, generous and detailed on Filip's part, with visible relief/pride at how far the Listing project has come from an early rough prototype to something demoed to the client. Some frustration is evident around client-side data quality and the unresponsive/unclear Boomy technical contact, but it's expressed matter-of-factly rather than adversarially. Marek is candidly still assembling context ("I'm scrolling through the chat too") and is honest about his own information gaps rather than pretending familiarity.

## Routing Log

{Written after PM confirms routing review}

> Migration note: ported from the predecessor repo (`bh-secondBrain`) on 2026-09-02, where this note existed but was never routed to harness artifacts (Routing Log was still an empty placeholder there too). That unrouted state is preserved here — no routing was performed during migration. Header/type field updated to conform to the fixed `internal | client | external | milestone` type enum (original free-form type: "project intro").
