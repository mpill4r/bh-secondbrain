---
last_updated: 2026-10-13
classification: Analysis
source: internal
original_location: ~/Downloads/ENRICHMENT_REVIEW_FEEDBACK.md (Filip Černý, provided by PM 2026-10-13)
---

# Listing External Enrichment: Options & Legal Assessment (Filip Černý)

## Document Info

**Title**: Externí obohacení: možnosti a právní posouzení
**Author(s)**: Filip Černý (STK-006), reworked after Marek's 2026-10-05 feedback
**Date**: received 2026-10-13
**Classification**: Analysis
**Source**: Internal (to be sent to Petr Neuman, STK-023)
**Previous version**: ENRICHMENT_LEGAL_REVIEW.md (2026-10-05, not ingested)

## Executive Summary

Describes how Listing's external enrichment works today, what Dr. Max legal must verify, what running it from AKS needs (proxy + network opening), product catalogues as an alternative (Synfony first), and why third-party scrapers (Apify, Tavily) add no legal protection. Recommends three variants: own scraper + proxy + approved sources (smallest change), hybrid with catalogues (target if a pilot confirms coverage/price), managed scraper only for reliability/cost.

## Key Points

**1. Current solution**
- Search a competitor listing via DuckDuckGo, pick the most relevant result containing the same EAN; crawl HTML + JavaScript into Markdown (browser emulation, indistinguishable from a real user); a small LLM strips non-listing content, keeping descriptions and parameter tables; generation uses the original listing + extracted listing + optional user comment.
- A human reads and confirms everything and can edit anything; selected fields can be excluded from generation (manual only).
- **Extraction keeps the original text passages**; own wording happens only at generation. Rewording alone doesn't solve the right to obtain, store and AI-process the source.
- **Legal must verify**: permitted sources and access (site terms for automated reading, access restrictions, consents/licences); scope of use (storage, passing to AI, use as enrichment input; copyright and database rights in systematic collection; unfair competition for competitor sources).
- Possible change: extract **structured facts** instead of text passages. Lowers the risk of copying wording, doesn't solve access.

**2. Proxy for AKS**
- Tested only from a consumer IP; data-centre IPs may be blocked, so a residential proxy is needed and must be tested.
- AKS currently can't reach outside the internal network: Dr. Max must allow outbound connections to the proxy provider.
- Cost: pay-as-you-go; ~1–3k listings/month means low thousands of CZK per month. Deeper analysis on request.
- Proxy gives no right to the content and no right to bypass access restrictions.

**3. Product catalogues**
- Structured supplier data without scraping. Price and real coverage (assortment and required fields) must be checked; both are B2B with no public price list.
- GS1 CZ / Synfony (GDSN): food, drinks, cosmetics, drugstore, FMCG; depends on participating suppliers. Icecat: mainly electronics, also cosmetics/FMCG; not Czech (language). SÚKL open data: medicines, out of early scope.
- Recommendation: contact Synfony sales first. Future: link to the planned supplier portal.

**4. Third-party scrapers**
- Apify / Tavily add no legal protection by themselves; liability doesn't transfer unless a contract says so.
- Benefit: robustness, less maintenance. On average slightly more expensive than own solution + proxy (no figures).

**5. Management recommendation**
1. Own scraper + proxy + approved sources: smallest change; needs legal approval and network cooperation.
2. Hybrid: catalogues / supplier exports, scraping as an approved supplement. Recommended target if a pilot confirms coverage and price.
3. Managed scraper as an operational alternative, only if more reliable or cheaper overall.

**Next steps**: start legal verification of the current approach; agree an owner for checking catalogue coverage and pricing.

## Gaps (PM review, 2026-10-13)
- No cost numbers for third-party services; no breakdown for tens of thousands of SKUs; no human-assisted URL variant; no implementation estimate.
- Typos: "vešekré", "býti", "DuckDuckGO".
- Doesn't say what happened to the earlier scraping legal check.

## Routing

Confirmed by PM 2026-10-13: ASM-277, ASM-278, ASM-279 added; ASM-033 updated; project-daily items updated; project-knowledge entries added.
