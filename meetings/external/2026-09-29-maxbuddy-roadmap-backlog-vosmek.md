---
last_updated: 2026-09-29
type: external
attendees: [Luboš Vosmek, Jura Brázdil, Marek Pillár, Alana Sihelská]
recording_link:
---

# MaxBuddy Roadmap & Backlog Planning with Luboš Vosmek

**Date**: 2026-09-29
**Attendees**: Luboš Vosmek (Dr. Max CZE, regional director, MaxBuddy business owner), Jura Brázdil (BigHub, MaxBuddy developer), Marek Pillár (BigHub, PM, organiser), Alana Sihelská (BigHub, joined briefly for one question)
**Type**: external
**Recording**: N/A (Fireflies transcript, pasted)
**Previous session**: [2026-09-17-business-quantification-maxbuddy-vosmek](2026-09-17-business-quantification-maxbuddy-vosmek.md)
**Meeting prep**: N/A

> **Transcript note**: Jindřich Tůma ("Indra") had replied "maybe" and did not join. Speaker labels were wrong in several places. Slovak lines labelled "Jura Brázdil" are Marek Pillár: the second half of 02:24, 02:52, 04:36, the first half of 11:24, 12:11, the first half of 16:53, 18:07 (first half), 18:50, the summary part of 21:26, 22:18, and "Tak potom beriem späť…" inside 22:40. The Slovak line inside Vosmek's 13:57 turn ("celkom pekná featura…") is also Marek. The Czech lines inside Vosmek's 07:19 turn ("budu počítat s tím, že na prst…") are Jura. The 05:51 question on margin/age sorting is Alana Sihelská: Vosmek says "Alana se hlásí" just before it. "Katajár" at 12:11 is Jiří Trajer; Marek names him in the closing summary.

## TL;DR

This was the follow-up to the 2026-09-17 BQ call: a first backlog conversation on Vosmek's wishlist. Marek opened by saying Tomáš Dudaško liked the BQ results and sees MaxBuddy as one of the most interesting initiatives in the portfolio. Vosmek set the priority to the end of the year as UI/UX "beauty" work (Dr. Max branding, a zoom for truncated benefit text, a missing-photo placeholder). The one real blocker is a Farmis focus bug: tapping a MaxBuddy tree takes over the barcode-scanner input, and Farmis is fixing it today. The larger items are not started: profitability- and age-based offering, product-info click-through, and seasonal logos. For profitability, Vosmek wants absolute profit in CZK, not % margin, with 3 tiers shown 7/2/1 in 10 expeditions. Jura wants receipt data so the system can learn. Marek will take this to Jiří Trajer and aim for the start of next year. The coverage overview Vosmek asked for on 09-17 now has an owner: Jura will add it to the existing filling interface.

## Key Discussion Points

### Context: BQ results landed with Dudaško

Marek recalled the business-quantification call two weeks earlier (2026-09-17) on expectations, savings/revenue and KPIs. He said it had been presented to Tomáš Dudaško, who "liked the results a lot" `[translated from Slovak]`, and that MaxBuddy came out as one of the most interesting initiatives in the whole portfolio. That is why Marek set up this meeting to move the initiative forward.

### Vosmek's wishlist email

Vosmek had sent "everything that came to mind, from small things to bigger ones — some already in progress, some new, some from the drawer" `[translated from Czech]`. He sent it to Jura late last week, and Jura had missed it. Marek asked Jura to forward it so he has the full list. Vosmek promised to copy everyone in future. This is the scope-expansion wishlist that was open from 2026-09-17.

Items Vosmek walked through (his own summary at 06:18):
1. **Dr. Max branding.** The pilot pharmacists asked why the logo isn't in Max colours. The 5 rotating logos and the landing page look "more like Benu than us" `[translated from Czech]`. Vosmek sent a web screenshot of Dr. Max's visual style, but the image doesn't load for Jura (OneDrive issue), so Vosmek will resend it.
2. **Tree click / cursor focus.** This is the Farmis bug below.
3. **Benefit text ("užitek") too small or cut off.** This came from last week's pilot-pharmacy meeting and is new to Jura. Vosmek imagines something like an Excel comment: hover and the full text appears in a larger font. Jura checked the hardware: the kiosks are **touchscreens**, so there is no hover. He will design a finger-friendly "magnifier" instead.
4. **"Photo not available" placeholder.** When a product image fails to load, staff should see this instead of waiting.
5. **Offering by profitability and by age.** Vosmek said these are "big points and we don't have them worked out at all" `[translated from Czech]`.

### The one real blocker: MaxBuddy steals the scanner input (Farmis)

Vosmek called this the most important item and said it probably sits with Farmis. When a pharmacist taps a MaxBuddy tree, the cursor stays in MaxBuddy and the dispensing case ("expediční případ") switches off. Client cards, eRecepty and so on then don't load automatically. Vosmek raised it with Jura ~14 days ago while Lukáš was on holiday, and today spoke with Lukáš Sýč (Szücs). **Farmis already knows and is working on it this afternoon.**

Jura's explanation: in August, after complex care ("komplexní péče") went live, the data showed pharmacists were **not clicking the trees**. He suspects Farmis reads the barcode scanner as keyboard input. Once someone taps into MaxBuddy, the scanner input goes to MaxBuddy, which ignores text, so the scan "gets eaten and disappears" `[translated from Czech]`. He passed it to Farmis as soon as Vosmek reported it. Vosmek: once this is fixed, "the rest is beauty" `[translated from Czech]`.

This probably explains the low tree click-through seen since August (see the 2026-09-07 analytics and the 09-17 click-tracking item). It may be focus loss, not only pharmacist behaviour.

### eRezervace vs. MaxBuddy conflict (unconfirmed)

Some pilot pharmacies say MaxBuddy and an active **eRezervace** block each other. With eRezervace, a customer reserves a product online, and Farmis pops up a window in the pharmacy asking staff to confirm stock. Vosmek hasn't reproduced it. He asked whether it's the same focus problem.

Jura's view: MaxBuddy can only take keyboard input if someone taps into it, so it may be the focus bug by coincidence. He had a second hypothesis: a reservation takes the item out of stock, so if the last unit is reserved and then scanned, MaxBuddy may misbehave on an out-of-stock item. The test Farmis can't create an active eRezervace, so Jura can't test it himself. **Vosmek will try to reproduce it live in a pilot pharmacy.**

### Profitability- and age-based recommendations

Alana Sihelská asked whether margin-based ordering and age-group targeting had been agreed or had "fallen on the lawyers". Vosmek: it **can't be done with AI** (legal), but they are still considering doing it through the underlying data.

Jura said BigHub has no access to any financial data on the products. A dimensionless 0–1 "how much do you want to sell this" score would be enough if Dr. Max doesn't want to share margins.

Vosmek set two principles:
- **Optimise on absolute profit, not % margin**: "the cheapest products paradoxically have the highest percentage margin, and we want to sell the pricier, value-added, expert things" `[translated from Czech]`.
- **3-tier segmentation**: tier 1 shown in 7 of 10 expeditions, tier 2 in 2 of 10, tier 3 in 1 of 10 "so it isn't forgotten and gets into their heads" `[translated from Czech]`. Every product box would carry a tier code. Jura: "no problem at all."

Jura's "technically ideal" alternative is to connect to **receipts** and let the system learn and optimise live. Fixed groups miss seasonality ("sunscreen won't sell in October"). He called it "good old machine learning, not today's AI" `[translated from Czech]`. It works across the whole range, can explore new products, and can still favour private labels and promotions. Vosmek found the self-learning idea interesting.

Marek asked what the blocker is. Jura needs two things: **(1) for each expedition, the product codes that appeared on the receipt (expedition number + product codes only), and (2) the profitability of each product.** "That's enough." Marek will go to **Jiří Trajer** (Vosmek agreed Marek can contact him directly), define and analyse the data table, then come back to Vosmek to specify the feature together. The target is to have it ready for **the start of next year**.

### Private-label product info click-through

Pilot pharmacists want to read more about a product (especially new graduates: MaxBuddy "is a dream for them", but as responsible pharmacists they want detail). The idea is to open product info in a separate page and study it later. Jura isn't sure Farmis lets him open a window, because MaxBuddy runs inside a Farmis webview. He can take over the MaxBuddy panel, but it has little space. He'll run a **feasibility experiment**. It may need Farmis to catch an event from MaxBuddy and open a window beside it. Marek framed it as a nice feature with no complications if feasible.

### Seasonal / event logos and self-service campaigns

Vosmek wants to break the pharmacists' routine about **every 14 days** with themed visuals. Examples: the "muscle men" on 3 September 2027 for International Fitness Day, then Mikuláš (St Nicholas), Christmas and so on. Later he may add attention-grabbers ("a cuckoo at noon"). He was clear this matters to him: when staff say "I don't notice it anymore", he wants something to pull their attention back.

Agreed sequence:
1. First tune the current 5 logos to Dr. Max branding until Vosmek likes the style.
2. Then Jura asks an AI tool to produce significant Czech dates, each with an image in the same style, for Vosmek to approve. **Start with Mikuláš, then Christmas.**
3. Marek proposed a **self-service** option so Vosmek doesn't have to email Jura each time: a campaign with a date range, saved and reusable the next year. Jura: easy once parts of the AI Platform land. The admin interface (which will also hold SPC changes and similar) could let Vosmek ask for "a new Mikuláš logo", get ~6 AI variants, and pick one with a from–to date. Vosmek: give him an environment and someone on his side will manage it.

### Coverage overview (from the 09-17 wishlist)

Vosmek's side will keep adding indications, complex-care items and benefits. He wants an automatic, interactive overview of which main and complementary groups are already in MaxBuddy, have a benefit, are approved and are working. Without it, the loop is email ping-pong: "we give Jirka something, ask if he sent it, I write to Juraj 'do you have it', he says 'approve it', we approve, and again 'are you showing it yet?'" `[translated from Czech]`.

Jura: "fairly simple". He'll add a covered/not-covered overview to the interface where "Jirka" currently fills the data in. He had already asked Jirka if he wanted anything added; Jirka said no, but Jura thinks it makes sense. Vosmek asked Jura to check with **"Lukáš z IČ"**, whom he has been pushing on this for about a month, in case he has already designed something. Jura asked Marek to log "coverage overview" (Fireflies was recording it).

### Workload and rollout outlook

Vosmek: finishing the beauty items by year-end would satisfy him. He thinks the current list is "enough work for the first half-year" `[translated from Czech]`, and more will come later. He hopes rollout to the other pharmacies is **"within days"**. After that he expects a wave of pharmacy ideas. He has already told pilot staff this is not the time for fanciful requests, but simple, clear ones (like the logo colours) are welcome and made him "ashamed" he hadn't noticed.

Marek asked Vosmek to send any pharmacist feedback or requests to him directly (Teams or email) so nothing gets lost. He also suggested thanking users for fresh-eyes feedback. Vosmek agreed with a "cobweb" analogy: you stop seeing what you look at every day.

### Tracking

With Jindřich absent, Marek asked whether MaxBuddy items are tracked as DevOps tasks. Jura: **they are not.** Marek: "we'll talk about it then."

## Decisions Made

- **MaxBuddy priority to year-end is UX/"beauty" work** (branding, benefit-text zoom, photo placeholder), with the Farmis focus bug as the one blocking item. Vosmek considers the current list enough for H1 2027.
- **Profitability-based offering optimises on absolute profit (CZK), not % margin.** Vosmek's starting model is 3 tiers shown 7/2/1 in 10 expeditions, with a tier code per product. Jura's preferred target is receipt-based learning. The next step is data discovery with Jiří Trajer, aiming for the start of next year.
- **Seasonal logos come after brand alignment.** The current 5 logos get Dr. Max styling first. Then AI-generated seasonal logos in that style, starting with Mikuláš and Christmas, about every 14 days.
- **Self-service campaign scheduling** (date range, reusable yearly, AI-generated variants) goes into the AI Platform admin interface.
- **Coverage overview goes into the existing data-filling interface**, owned by Jura. This resolves the 09-17 open question on who builds it.
- **Pharmacist feedback and requests from Vosmek's side go to Marek directly.**

## Action Items

- [ ] **Jura Brázdil**: Forward Vosmek's wishlist email to Marek Pillár — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Luboš Vosmek**: Resend the Dr. Max branding sample (the OneDrive image doesn't load for Jura) — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Restyle the 5 rotating logos and the landing page in Dr. Max colours and logo — before year-end — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Farmis (via Lukáš Szücs)**: Fix MaxBuddy taking over the scanner/keyboard input when a tree is tapped (the dispensing case switches off) — in progress 2026-09-29 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Design a touch-friendly zoom for small or truncated benefit ("užitek") text — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Show a "photo not available" placeholder when a product image fails to load — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Luboš Vosmek**: Try to reproduce the eRezervace/MaxBuddy conflict live in a pilot pharmacy — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Look into the eRezervace conflict (focus-bug overlap vs. reserved last unit / out-of-stock scan) — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Feasibility experiment: can MaxBuddy open a pop-up/window for private-label product info from inside the Farmis webview, or does Farmis need to catch an event — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Marek Pillár**: Contact Jiří Trajer about receipt data (expedition number + product codes) and per-product profitability; define and analyse the data table — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Marek Pillár**: Once there's a first version, specify the profitability-based recommendation with Vosmek (3-tier model and/or receipt-based learning) so it can start early next year — due start of 2027 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: After the logos are tuned, AI-generate seasonal logos for significant Czech dates in the same style for Vosmek's approval, starting with Mikuláš then Christmas — before 2026-12-06 — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Add self-service campaign/logo scheduling (date range, reusable yearly, AI variants) to the AI Platform admin interface — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Jura Brázdil**: Add a coverage overview (which groups have a benefit, are approved, are live) to the data-filling interface; first check with "Lukáš z IČ" whether he has already designed something — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek
- [ ] **Marek Pillár**: Agree with Jindřich Tůma where the MaxBuddy backlog is tracked (not in DevOps today) and get this meeting's items into it — from 2026-09-29-maxbuddy-roadmap-backlog-vosmek

## Open Questions

- **Legal boundary.** Vosmek says profitability/age-based offering "can't be done with AI". Does Jura's receipt-based ML optimisation fall under that restriction, or is it allowed like the anonymised receipt data already noted in project-knowledge? This needs a legal read before the early-2027 spec.
- **Profitability data.** Will Dr. Max share actual per-product profitability, or only a 0–1 score or 1/2/3 tier? Who owns the tier assignment on Dr. Max's side?
- **Age-based offering.** It was mentioned but not discussed. What is the data source and the legal position?
- **Rollout timing.** Vosmek expects rollout to the other pharmacies "within days". [[ASM-027]] has the full rollout blocked on new AKS access (~1 month of work after the grant), and on 09-24 the infra access was still blocked. Which is current?
- **"Jirka".** Who fills indications/benefits in the admin interface? Probably a Dr. Max expert-side person, not Jiří Trajer (data feed only).
- **"Lukáš z IČ".** Is this Lukáš Szücs, or someone else?
- **Tracking.** Where should the MaxBuddy backlog live (Azure DevOps per [[ASM-163]])?
- **09-17 items not revisited.** Vosmek's exact revenue-uplift %, the single-item dispensing baseline, and the tree click-through tracking did not come up.

## Sentiment & Tone

Warm, relaxed and cooperative, consistent with 09-17. Vosmek is an engaged, hands-on champion. He brought a full list, owned his own slip (not copying everyone), and was openly self-deprecating about missing the logo-colour point ("I was ashamed"). He came across as protective of his pilot pharmacists' experience and attention. The seasonal-logo idea is not cosmetic to him: it is an adoption lever against "stereotype screen" fatigue, and he said directly it is "terribly important". He is also managing his own users' expectations, having already told pilot staff not to send fanciful requests.

**Relationship signals:** He is comfortable with Jura on first-name terms and familiar with Farmis and Lukáš Sýč. He readily accepted Marek as the new intake channel and agreed to Marek contacting Jiří Trajer directly. Dudaško's positive read of the BQ gives this initiative momentum, and Vosmek's appetite is modest and realistic ("beauty by year-end, enough work for H1").

**Watch-outs:**
- Vosmek's "within days" rollout expectation may not match the AKS reality. If the infra block still holds, expectations need managing before he promises it to the network.
- He expects a flood of pharmacy ideas after rollout, so intake and prioritisation need a home, and today there is no tracked backlog.
- Jura said "no problem" to several items without estimates (tiering, self-service campaigns, coverage overview). Capacity should be checked before these become commitments.

## Routing Log

- **Transcript fixes**: Speaker corrections and identities (Alana at 05:51, "Katajár" = Jiří Trajer, "Lukáš Sýč" = Lukáš Szücs) confirmed by the PM.
- **project-assumptions**: Added ASM-196 (year-end UX priority), ASM-197 (profitability offering, absolute CZK profit), ASM-198 (Farmis scanner-focus hypothesis), ASM-199 (webview click-through feasibility), ASM-200 (seasonal logos + self-service), ASM-201 (coverage overview in filling interface), ASM-202 (backlog not tracked), ASM-203 (rollout "within days" vs. ASM-027, logged as an open expectation gap). ASM-027 annotated.
- **project-stakeholders**: Updated STK-011 (Vosmek; Last interaction → 2026-09-29), STK-026, STK-049, STK-031, STK-004, STK-010.
- **project-knowledge**: Enriched MaxBuddy and Farmis; added eRezervace.
- **project-daily**: 5 PM-owned action items (incl. the recap email) + Key Event.
- **project-lessons**: LL-70 (rule out host-system interaction before reading low usage as an adoption problem).
- **meetings/index**: Entry added.
