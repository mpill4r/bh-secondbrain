---
last_updated: 2026-09-09
last_updated_by: manual — conversational (added §12: questions for Claude Design to check with PM during build)
owner: Marek Pillár
---

# Dr. Max AI Platform — Design Brief for Claude Design

**Prepared for:** Claude Design (clickable prototype build)
**Prepared by:** Marek Pillár (BigHub), via Product Harness
**Date:** 2026-09-08
**Status:** Ready for prototype build — Phase 1 of the agreed 3-phase AI platform delivery plan (UX rework → migrate existing projects → admin/reporting from Dudaško's backlog)

---

## 1. What this is and why it exists

Dr. Max (client) already runs 9 live/in-development AI products built by BigHub, each currently accessed through its own disconnected URL that people have to be individually told about. There is no shared home, no unified view of what exists, no visibility into cost or usage, and no way for an admin to pause something that's misbehaving.

**Tomáš Dudaško** (Dr. Max's Head of IT, holds the BigHub budget) has asked for a real platform: one place where every AI product lives, organized by who needs it, with usage/cost visibility and administrative control. This request came out of a large 48-item technical governance/compliance capability register he produced (identity management, audit trails, policy-as-code, egress control, etc.) — but per internal agreement between BigHub's PM and dev lead, **this first prototype deliberately does not attempt to surface most of that register as UI.** It stays backend/architecture. The goal of this specific deliverable is narrower and sharper: give Dudaško something concrete and clickable that he can react to, covering exactly four things (see §4). Overbuilding this pass risks (a) blowing the timeline before there's client buy-in, and (b) diluting focus on what actually drives adoption — a good home experience — with governance theater nobody asked to see yet.

**The product is named: Dr. Max AI Platform.**

A visual reference (screenshot, provided separately) already exists showing the intended home-screen layout, styled in Dr. Max's brand. Treat that screenshot as the primary visual anchor — match its layout, spacing, component style, and color usage closely. Where this brief adds detail beyond the screenshot, follow the brief; where the screenshot is authoritative on visual style, follow the screenshot.

**Before you start, and periodically during the build: see §12 for a list of specific open questions to check with Marek rather than silently guessing at.** This brief was written with context (internal meetings, the client's capability register, roadmap history) that doesn't automatically travel with it — where it's silent or only gives an illustrative example, that's usually §12's territory, not an invitation to invent an answer.

---

## 2. Brand & design language

**Primary source:** the reference screenshot (already Dr. Max-branded) — this is the strongest signal available and should be treated as ground truth for color, spacing, and component style.

**Secondary source:** drmax.cz (the client's public consumer site) was the intended brand reference but could not be scraped directly (bot-protected, 403). Claude Design should independently pull current Dr. Max brand cues from drmax.cz if it has live browsing capability; if not, extrapolate conservatively from the screenshot and flag any color/typography choice that isn't directly confirmed by it.

**What's visible in the screenshot, to carry through precisely:**
- Logo: "Dr.Max+" wordmark, red cross/plus accent, top-left, on white
- Primary accent: a muted sage/leaf green (used for the active nav item, the hero banner background gradient with a leaf photograph, and primary link color)
- Neutral palette: white background, light warm-gray card backgrounds, dark near-black text for headings, medium gray for body/secondary text
- Typography: clean geometric sans-serif, bold for headings, regular weight for body — no serif anywhere
- Cards: white background, soft shadow, generously rounded corners (~12-16px), consistent internal padding, icon in a soft-tinted rounded square (each product category gets its own icon tint — e.g. purple for MaxBuddy, green for Reklamace, red/pink for order prediction, blue for Fakturace doprav, teal for chatbot)
- Category badges/pills: small rounded-pill labels under each card, color-coded per category
- Buttons: primary action ("Otevřít") is a text link with a right-arrow, not a heavy filled button — keeps the UI feeling light
- Filter chips: horizontal pill row, active state filled dark, inactive state outlined/light
- A small tagline block bottom-left of the sidebar: "Lepší péče. S podporou AI." — keep this or something equivalent; it's doing brand work (AI in service of care, not AI for its own sake)
- Left sidebar navigation, collapsible sort/view toggle (grid/list) on content areas, search-first hero pattern

**Tone of voice (Czech copy throughout):** warm, plain, non-technical. This is a tool for pharmacists, CC agents, logistics staff, and e-commerce/IT people — not developers. Avoid engineering jargon in any user-facing copy (no "agent," "LLM," "token" in the main UI — save that vocabulary for the admin/governance areas where the audience is technical).

---

## 3. Information architecture

Left sidebar navigation, matching the screenshot exactly in items and order:

1. **Domů** (Home) — personalized landing: hero + favorites + full app grid. *Full screen, in scope.*
2. **AI aplikace** (AI Apps) — the complete catalog, dedicated screen with fuller filter/search/sort controls than Home's condensed view. *Full screen, in scope.*
3. **Novinky** (News/Updates) — *Nav item present, not designed this pass. Static placeholder page ("Coming soon") is fine.*
4. **Školení** (Training) — *Not designed this pass. Placeholder.*
5. **Nápady** (Ideas) — presumably a suggestion/feedback intake for new AI use cases. *Not designed this pass. Placeholder.*
6. **Dokumentace** (Documentation) — *Not designed this pass. Placeholder.*
7. **Podpora** (Support) — *Not designed this pass. Placeholder.*
8. **Administrace** (Admin) — *Full screen(s), in scope. This is where the other 3 of the 4 core deliverables live: Usage Reports, Kill Switch, and User Group management.*

Persistent header (all screens): search icon, help icon, user avatar + name + role chip (top right, matches screenshot's "Jindra Tůma" pattern) — **plus a new Simulation control** (see §7).

---

## 4. The four things this prototype must deliver

1. **Home / AI app catalog, organized by user group** (§5)
2. **Usage reports per product**: cost, usage volume, adoption (§6)
3. **Kill switch, per product and per underlying model** (§7)
4. **Simulation mode** — view the platform as another user group would see it (§8)

Everything else in this brief exists to support building those four well. Do not let scope creep into the other 44 governance-register items (audit trail viewers, policy editors, agent registries, HITL approval queues, etc.) — none of that is in this pass.

---

## 5. Screen: Domů (Home)

Matches the reference screenshot closely. Structure top to bottom:

**Header row:** Dr.Max+ logo (top-left) · search/help icons + user avatar/role + Simulation control (top-right)

**Hero banner:** light sage-green gradient background with a leaf photograph bleeding in from the right edge. Headline: "Vítejte v **Dr.Max AI Platform**" (bold, large). Subhead: "Všechny vaše AI nástroje na jednom místě." Below that, a large search input: "Hledat AI aplikace, use-casy, klíčová slova…"

**Oblíbené (Favorites) row:** user-pinned/most-used apps, 3-up card row, "Zobrazit všechny →" link top-right of the section

**Moje AI aplikace (My AI Apps):** filter chip row — **the chips are the user's group's visible categories**, not a fixed global list (see §8 on how group membership drives this). Default/example set: Vše, Obecné, Logistika, E-commerce, CC, HR, IT, OnlineMKT, Další. A sort dropdown ("Řadit podle: Název (A-Z)") and grid/list view toggle sit at the right edge of the filter row.

**App grid:** 3-column card grid. Each card: colored icon tile (top-left), overflow "⋮" menu (top-right, for pin/unpin etc.), product name (bold), one-line description, one category pill, "Otevřít →" link bottom-right.

### Product catalog (real data — use exactly this, do not invent products)

| Product | Category (pill) | Icon tile color | Card description (Czech) |
|---|---|---|---|
| MaxBuddy | Obecné | Purple | Asistent integrovaný do Farmisu, který lékárníkovi na základě obsahu košíku doporučuje vhodnou doplňkovou/podpůrnou léčbu vč. zdůvodnění a ověření dostupnosti. |
| Max Chatbot | CC | Teal/green | Webový chatbot pro samoobslužné vyřešení vybraných zákaznických scénářů (otevírací doba, stav objednávky, eRecept, reklamace) bez nutnosti kontaktovat Customer Care. |
| Maxie | CC | Green | Hlasový asistent obsluhující 24/7 rutinní scénáře zákaznické linky a telefonátů na lékárny, aby se snížilo zatížení Customer Care. |
| Lexie | Obecné | Purple/blue | Interní znalostní asistent pro Customer Care, který operátorům umožňuje rychle čerpat a kombinovat informace z interních metodik. |
| Reklamace | Logistika | Green | Digitalizace a automatizace zpracování příjmových a skladových reklamací — evidence, fotodokumentace, komunikace s dodavatelem a auditní stopa. |
| Fakturace doprav | Logistika | Blue | Digitalizace a automatizace zpracování podkladů od dopravců/řidičů pro fakturaci doprav a jejich evidenci v Axaptě. |
| Řízení poptávky (Predikce objednávek) | E-commerce | Red/pink | Přehled a predikce vývoje objednávek pro e-commerce tým — včasná identifikace rizika nesplnění obchodního plánu. |
| Listing | E-commerce | Red/pink | AI podpora tvorby a správy produktového listingu — návrh obsahu, struktury a doplnění chybějících dat s minimem manuální práce. |
| TEO_OCR | IT | Orange/yellow | Automatizace zpracování servisních listů a revizních dokumentů technického oddělení — OCR vytěžení dat s kontrolou před předáním do ServiceNow. |

**Card click behavior:** "Otevřít" deep-links out to the product's real environment in a new tab (these are separate deployed apps, not embedded in this platform — at least not in this pass). For the prototype, this can be a non-functional link or link to a placeholder — do not attempt to embed the real tools as iframes.

**Empty/filtered state:** if a Simulation view or group filter leaves zero visible apps, show a clear empty state (not a blank grid) — e.g. "Tato skupina zatím nemá přiřazené žádné AI aplikace."

---

## 6. Screen: Administrace → Přehledy (Usage Reports)

New tab under Administrace. Audience: admins/executives (Dudaško's own ask) — can use more precise/numeric language than the consumer-facing Home screen, but stay readable, not a raw data dump.

**Per the confirmed scope, three metric families, per product:**

1. **Náklady (Cost)** — spend attributed to the product, e.g. token/API cost over the selected period, trend vs. previous period, budget-vs-actual if a budget is set (ties into the Kill Switch screen's budget controls in §7 — these two screens should feel like one system, not two disconnected tools).
2. **Využití (Usage)** — volume: queries/conversations/sessions per period, a simple trend chart (sparkline or small line chart per card, full chart on drill-in).
3. **Adopce (Adoption)** — unique users, broken down by department/user group, so it's visible whether a product is reaching who it's meant for.

**Layout suggestion:** a top-level summary row (total platform spend, total usage, total active users — the "one glance" numbers Dudaško wants), then a per-product table or card list below, each row/card expandable or click-through to a per-product detail view with the fuller trend charts and department breakdown.

**Time range control:** a period selector (e.g. Posledních 7 dní / 30 dní / 90 dní / Vlastní rozsah) — standard SaaS dashboard pattern, apply globally to the whole Přehledy screen.

**Data for the prototype:** use realistic-looking placeholder numbers (the real integration doesn't exist yet — this is a UX/IA prototype, not a live dashboard). Where real qualitative signal exists from actual product context, prefer it for flavor even if the exact number is illustrative — for example, MaxBuddy's real adoption problem (recommended-tile impressions far outstripping actual clicks) is a genuine known issue and would make a more credible demo number than something invented from nothing. Do not fabricate precise real financial figures — round, illustrative numbers are expected and fine.

---

## 7. Screen: Administrace → Kill Switch

New tab under Administrace. This is the control-room screen — should feel serious/technical, unlike the friendly consumer Home screen. Dark-mode-adjacent or at least a visually distinct, higher-contrast treatment from Home would help signal "this is a different kind of screen, handle with care."

**Two independent control axes, per the confirmed scope — no single global "kill everything" master switch, deliberately:**

1. **Per product/agent** — every row in §5's product catalog gets its own on/off toggle here, with current state (Aktivní / Pozastaveno) and — ideally — a required confirmation step before switching a live product off ("Opravdu chcete pozastavit Max Chatbot? Zákazníci ztratí přístup k chatu okamžitě." style modal), since this is a genuinely consequential action.

2. **Per underlying AI model** ("brain") — a second control layer, listing the LLM models actually powering the platform (e.g. GPT-4.1, GPT-5, or whatever's in use), each with its own toggle, independent of which product uses it. **Flag clearly in the prototype (a visible note, not just this brief) that the exact mechanics of this control — what "off" actually means when multiple products may share a model, whether there's an automatic fallback model, etc. — are still to be finalized with the engineering lead (Jura Brázdil) and are being designed provisionally for this prototype.** Don't let Claude Design (or a viewer of the prototype) treat this control's behavior as fully specified — it isn't yet.

**Suggested layout:** two clearly separated sections/tabs within the Kill Switch screen — "Podle aplikace" and "Podle modelu" — rather than merging them into one table, since they're different mental models (one is "stop this product," the other is "stop this piece of infrastructure that many products might depend on").

Also reasonable to include here (ties to the existing capability register's "Budgets, quotas & hard stops," already partially built): a budget ceiling per product, so an admin can set a spend cap that auto-pauses the product rather than only manually flipping switches. Not required for this pass, but a natural adjacent control if there's room — flag as optional/stretch rather than core.

---

## 8. User groups & Simulation mode

This is the most structurally important part of the brief — get this model right and the rest (catalog filtering, admin permissions, simulation) falls into place naturally.

**The model, as confirmed by the PM:** access is governed by **flexible, admin-defined user groups** — not a fixed department list. A group can be built by any convention that makes sense (department, project team, seniority, a specific cross-functional initiative — whatever) and defines:
- **Which apps/categories are visible** to members of that group on Home/AI aplikace
- **What permission level** members have (e.g. can only use apps, vs. can also see that product's usage numbers, vs. full admin including Kill Switch access)

A user can belong to more than one group, and **individual-level overrides** are supported on top of group membership (a specific person can be granted or denied something outside what their group(s) would normally give them).

**New admin screen needed to support this: Administrace → Skupiny uživatelů (User Groups)**
- List of existing groups, each showing: name, member count, which apps/categories it grants, permission level
- Create/edit a group: name it, assign apps/categories, set permission level, add/remove members
- A user detail view showing their group memberships plus any individual overrides layered on top

This doesn't need to be deeply fleshed out with real backing logic for the prototype — but it needs to *exist as a screen*, because the Simulation control (below) only makes sense once "groups" are a visible, tangible concept in the product, not just an invisible backend rule.

**Simulation control (header, all screens):** a dropdown near the user avatar, e.g. "Simulace: Vy (Jindra Tůma)" by default, opening to a list of existing user groups (and optionally specific users) to preview as. Selecting one:
- Applies a persistent, unmissable banner across the screen (e.g. a colored strip at the very top: "Prohlížíte jako: **Logistika** — Ukončit simulaci") so nobody mistakes a simulated view for their real one
- Re-renders Home/AI aplikace filtered to exactly what that group would see (fewer/different app cards, filter chips limited to that group's categories)
- Does **not** grant the admin the ability to take real actions as that group (e.g. no submitting things "as" a simulated user) — this is a read-only preview, not impersonation for action-taking

This is explicitly about previewing *visibility*, not stepping into someone else's account.

---

## 9. Screens explicitly out of scope for this pass

Do not design full, functional versions of these — nav items can exist (per §3) as placeholders, but no effort should go into fleshing them out:

- Novinky, Školení, Nápady, Dokumentace, Podpora (nav items present, static/placeholder only)
- Agent registry/inventory screen (capability #41 — Must-have per the governance register, but not this pass)
- Human-in-the-loop approval queue UI (capability #48 — explicitly Q3 roadmap, not now)
- Audit trail / immutable log viewer (capability #12 — backend concern, no UI this pass)
- Policy-as-code editor, egress-control config, any of the other governance-register screens
- Actual authentication/login flow — assume the prototype opens directly into an already-authenticated Home screen (SSO/Entra ID login is real infrastructure, not something to design here)
- In-platform embedding of the real product tools (chat widgets, dashboards, etc.) — "Otevřít" is a deep-link/placeholder only

---

## 10. Open items / things not yet finalized

Flag these visibly in the prototype where relevant (e.g. a small note on the Kill Switch screen) rather than presenting them as settled:

1. **Per-model kill switch mechanics** — needs a technical conversation with Jura Brázdil (engineering lead) before the exact behavior can be considered final. Design it, but mark it provisional.
2. **Brand fidelity** — this brief's color/typography guidance is derived from the reference screenshot, not a verified pull from drmax.cz (site blocked automated access). Worth a quick manual sanity-check against the live site or actual Dr. Max brand guidelines before this goes in front of Dudaško.
3. **User group definitions** — no real groups exist yet; the screenshot's category chips (Obecné/Logistika/E-commerce/CC/HR/IT/OnlineMKT) are a reasonable illustrative starting set for the prototype's default/example group, but the actual group structure Dr. Max wants is undefined and will need a real conversation with them.
4. **Usage report numbers** — illustrative/placeholder only; no live cost or usage integration exists yet.

---

## 11. Success criteria for this prototype

Per the PM's stated goal for this deliverable: this needs to make Dudaško **want** what he sees — walk into the eventual presentation and say "yes, this is what I want" — not just technically satisfy his governance checklist. Prioritize a genuinely good, credible Home screen experience over broad governance coverage. Simple and polished beats broad and rough.

---

## 12. Questions to check with Marek during the build

This brief was written with full context from BigHub's internal meetings, the client's capability register, and the existing product roadmap — context that doesn't automatically carry over into a fresh Claude Design session. **Where the brief itself is silent or only gives an illustrative example, don't silently invent an answer and don't wait until the end to surface it — check in with Marek at the relevant point in the build.** Each item below includes what to do if he's not immediately available, so a check-in never has to fully block progress.

**Brand & visual**
1. Do you have exact Dr. Max brand assets (hex codes, font names, logo files, a style guide) beyond the reference screenshot? *Default if not: proceed from the screenshot alone, and flag every color/font choice not directly visible in it as inferred.*
2. The screenshot's product icon colors don't map cleanly to a single system — some are per-category (both Logistika cards use different colors, both E-commerce cards share the same red/pink), others read as just per-product for visual distinctness. Which convention should the remaining products follow — a strict category-color system, or continue picking distinct colors per product like the screenshot does? *Default: match the screenshot's existing choices exactly where a product is already shown there, and pick visually distinct (not category-locked) colors for the rest.*

**Product data & content**
3. Should "Favorites" be a real per-user feature (manual pin/unpin) or just a hardcoded illustrative row for the prototype? *Default: hardcoded for now, matching the screenshot's 3 examples (Predikce objednávek, Max Buddy, Max chatbot) — no working pin/unpin interaction needed.*
4. Is the product list in §5 final for this prototype, or are there other products/agents Marek wants shown that aren't in the current 9-product roadmap (e.g. anything from the AI platform's own build, once it exists)? *Default: exactly the 9 listed, nothing added.*

**Access model**
5. How many example user groups should the Skupiny uživatelů screen show, and what should they be named/scoped? The screenshot's filter chips (Obecné, Logistika, E-commerce, CC, HR, IT, OnlineMKT, Další) are a plausible illustrative set, but not confirmed as real. *Default: use those chip names as the example groups, each granting the matching category of apps.*
6. Is the 3-tier permission example in §8 (use apps / see usage / full admin) the right shape, or does Marek want something simpler (e.g. just "user" vs "admin") for this pass? *Default: keep it simple — 2 tiers (user, admin) rather than 3, since nothing in the confirmed scope actually requires a middle tier yet.*
7. Does Simulation mode need to support previewing as an individual named user, or is previewing by group sufficient for this prototype? *Default: groups only — no individual-user simulation this pass.*

**Kill switch**
8. What's the real, current list of LLM models in use (for the "per-model" kill switch view)? This is explicitly flagged in §7/§10 as needing Jura Brázdil's input — don't ship a plausible-looking but wrong model list without checking. *Default: use clearly-labeled placeholder names (e.g. "Model A", "Model B") rather than guessing at real model names, until confirmed.*
9. Is the confirmation-modal copy in §7 (example: "Opravdu chcete pozastavit Max Chatbot?...") good to use as-is, or does Marek want to write/approve the actual wording before it's baked into a client-facing prototype? *Default: use the example copy, mark it clearly as draft copy pending review.*

**Usage reports**
10. Are the specific placeholder numbers used in the Usage Reports screen okay to leave as invented-but-illustrative, or does Marek want to review them before the prototype is shown to anyone at Dr. Max (given they could be mistaken for real figures)? *Default: keep numbers clearly rounded/approximate-looking (e.g. "~2 400" not "2 417") so they read as illustrative rather than real data.*

**Interaction scope**
11. Should "Otevřít" on a product card be a dead/inert click, or should it visibly do *something* (even just a toast or a modal saying "V reálném prostředí by toto otevřelo [produkt]") so the interaction doesn't feel broken in a click-through demo? *Default: a lightweight placeholder interaction (toast/modal) rather than a fully dead link.*
12. Does this prototype need to work on tablet/mobile breakpoints, or is desktop-only acceptable for a first internal-facing demo to Dudaško? *Default: desktop-only.*

If any of these come up mid-build and Marek isn't around to answer immediately, proceed with the stated default, mark the choice clearly (e.g. a code comment or a visible "draft" indicator in context), and surface the full list of what was defaulted at the end of the session rather than letting it silently disappear.
