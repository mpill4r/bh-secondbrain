---
last_updated: 2026-10-14
type: external
attendees: [Luboš Vosmek, Jura Brázdil, Marek Pillár]
recording_link:
---

# MaxBuddy Redesign, Zoom & Rollout by Thirds with Luboš Vosmek

**Date**: 2026-10-14
**Attendees**: Luboš Vosmek (Dr. Max CZE, regional director, MaxBuddy business owner), Jura Brázdil (BigHub, MaxBuddy developer), Marek Pillár (BigHub, PM)
**Type**: external
**Recording**: N/A (Teams transcript, pasted)
**Previous session**: [2026-09-29-maxbuddy-roadmap-backlog-vosmek](2026-09-29-maxbuddy-roadmap-backlog-vosmek.md)
**Meeting prep**: N/A

> **Transcript note**: The speaker labels are badly mixed (only two labels for three people). PM confirmed this reading: the Czech developer voice (redesign, Farmis focus, AKS/production, Entra groups, audit logs) is Jura Brázdil; the Slovak lines are Marek Pillár; the pharmacy, region and Farmis-call lines are Luboš Vosmek. Míra Suchý (regional, invited) skipped for a training; Jindřich Tůma didn't join. "VDC" in the transcript is BDC. The Farmis contact Vosmek called is not named here (name unclear).

## TL;DR

Jura showed the cross-sell card redesign. Kiosks give MaxBuddy only ~656 px, so long benefit texts force small fonts. Vosmek's pilot pharmacists dislike two stacked texts, so the title goes back beside the product box, the benefit is shown partly, and a tap-to-enlarge **zoom** shows it in full. The zoom waits for Farmis to release scanner focus, which still hasn't started; Vosmek will chase Farmis. Rollout: everything works end-to-end on test; production setup is with Martin Dubina (BDC). After a night-time switchover (01:00–03:00), MaxBuddy goes out **by thirds, by region**, starting with Vosmek's own (~200 pharmacies). This narrows the 09-29 "within days" gap ([[ASM-203]]). Jura also asked to move platform access management from Entra groups into the AI Platform, and Vosmek says Tomáš Dudaško must decide.

## Key Discussion Points

### Card redesign and the space limit

Jura showed the redesign he'd sent as screenshots. On the test kiosks Farmis gives MaxBuddy only **656 px** of height. With a long cross-sell argument (e.g. Amoxiclav 1 g) only 3 cards fit; a 4th fits only if all content shrinks. The layout picks from ~8 size variants to fill the space, and shrinks everything when more is added. Jura would ship it as is ("better than what we have now"). In the current design only ~2 cases no longer fit (earlier, about half of the benefits didn't fit). A fixed character limit on arguments (cut or rewrite the long ones) is another option; any shortening lets the text grow.

Vosmek had discussed it with the pilot pharmacies: they dislike **two texts stacked** (image, product name, then benefit text). "It feels like a lot to read." `[translated from Czech]` He suggested name, image, then text to break it up. Jura: possible, with the image in the middle and labels to its right. But the full title doesn't fit beside the box.

### Zoom ("lupa"): tap, not hover

Half of the dispensing staff use the touchscreen and half a mouse. Jura will build the zoom **for tap**, which covers both. Doing hover and tap together would conflict. Marek suggested cutting the benefit to two lines and expanding on tap, since staff will learn the products over time. Jura warned the arguments aren't written to be read partly: a cut-off sentence can lose its meaning.

Tapping a card expands and enlarges it at the expense of other content, like the existing "more cross-sells" tap. The next tap or the next dispensing case resets it.

Vosmek then dropped the format change: **keep the box with the title beside it and part of the benefit below; tap to enlarge and show it all.** A cut-off title is fine: "Vitamin C — whether it's 150, 250 or a thousand… We don't show the box you must dispense, because we don't know which patient is in front of you. We say: consider vitamin C." `[translated from Czech]` The start of the name is always right. Jura already moved the own-brand marker into an icon to free the title.

### Farmis scanner focus still blocks the zoom

Tapping into MaxBuddy still takes the scanner focus. Jura now blocks the panel "aggressively" with a "scanner disconnected" warning until the user taps back into Farmis. He said that's poor UX, and with a zoom it would be "annoying", so the zoom waits for Farmis. **The scanner matters more than cross-sell.** MaxBuddy is a guest in the webview: it knows whether it has focus but can't give it back. The fix is on Farmis: when someone clicks outside the webview, Farmis takes the focus back.

Per Lukáš Szücs, Farmis **hasn't started** on it. Jura admitted he hadn't escalated it as a blocker ("it sounds like a small thing"). Vosmek called a Farmis contact during the meeting (call-back pending) and will report back.

Vosmek fears the red exclamation mark: to pharmacists it means "hands off, do nothing". Marek: users don't need to know why, only that they must tap back. Jura will **replace "scanner disconnected" with a large, bold "Please tap back into Farmis."** Jura repeated that the August stats showed nobody clicking complex care, likely because the scanner disconnected ([[ASM-198]]).

### Logos

Vosmek reminded Jura of the Dr. Max-styled logos ("logo, clothing"), which aren't done. He needs them for the rollout. "I don't want to launch it looking like Benu. Since they told me, I see it." `[translated from Czech]`

### Rollout plan

- **Status (Jura)**: everything works end-to-end on test, "a big step". Production requirements went **yesterday to Martin Dubina** (Vladislav Tvarůžek's colleague, BDC). Production has a different GitOps and cloud setup, so Jura can't just copy test. He expects it can be done in one day if Dubina has time. Vosmek: Dubina is very reliable; if there's no response tomorrow, Vosmek will chase him. The worst part, aligning with BDC on how to switch, is behind them. A BDC colleague (likely Štěpán) helped a lot.
- **Switchover**: new production runs in parallel with the current one and is tested. Then a **night switch in AKS** to the new node pool: restart all services, reconnect the databases, shut down the old one. Jura expects 1–2 hours of downtime if issues appear and wants someone from Vosmek's side on the phone for network-access hiccups. Lowest traffic is **01:00–03:00** (Vosmek), when only 24/7 pharmacies run. The 20 pilot pharmacies move first; if all is well, rollout starts.
- **By thirds** (Vosmek): he now prefers thirds over a big-bang rollout. Dr. Max has 3 regions; he starts with **his own** (~200 pharmacies, where Míra Suchý and Kuba Mísař helped and feedback is quick), then moves east. Pharmacies must know in advance, so they're chosen by region, not by percentage. Jura is preparing **two MaxBuddy environments** (canary) so the first wave and later changes can go in parts. He'll enlarge the database for ~200 himself.
- **Capacity**: sized for ~600 pharmacies plus reserve. It's extrapolated from the 21 pilots, which are stronger, busier pharmacies, plus resources for other projects. Platform monitoring is ready and already caught an issue, so per-pharmacy problems will show at once.
- **Exclusions**: Vosmek must exclude the pharmacies with his **small monitors** (about 8).
- **Priority**: Marek said, for Jindřich, that he pushed the rollout and **Jindřich confirmed it's a priority in infrastructure**. Jura: "we've been pushing since August."

### AI Platform: access management out of Entra

Jura asked to move "who sees what in the platform" from Entra into the platform. Today Lexie alone has **22 Entra groups** (user/admin/superadmin per department). Adding MaxBuddy and the chatbot would mean ~50 groups and constant add/remove requests. Instead: **3 Entra groups** (platform user, admin, superadmin), with the mapping done inside the platform. A superadmin or department admin adds people by Dr. Max email and picks which tiles they see. Login and change **audit logs** are ready, so every user-management change is traced. Technically nothing changes, since Jura already maps groups to rights; it shifts responsibility and lets him move much faster.

Marek: account management at platform level was also requested by Dudaško. Vosmek: makes sense to him and he has nothing against it, but **the decision is Tomáš Dudaško's**. They'll take it to him. Jura couldn't recall a second thing it would unlock.

**Post-meeting update (Teams, 2026-10-14 11:47–11:55; screenshot shared by PM)**: Jura messaged Tomáš Dudaško the same day. **Dudaško approved**: "sounds completely fine to me" `[translated from Czech]`. His paraphrase, which Jura confirmed: Entra AD will hold only **3 AI groups** (Users, Admins, SuperAdmins), and the platform manages roles below them. An **Admin** administers the parts of the platform a **SuperAdmin** assigns to them and grants users access to those parts; the SuperAdmin can do everything. Access to individual use cases and functions sits in the platform database, with auditable logs of all interactions (already built). The second unlock Jura couldn't recall in the meeting: **test users**, which at least the CC team wants ([[ASM-063]]). Dudaško also asked for an **API**, so access could later be driven automatically from an IDM (Dr. Max doesn't have one yet): assign a role in IDM and the platform sets access. Jura: no problem technically; the platform just needs to issue API keys.

### 2027 initiatives

Marek will send the standard email on next year's initiatives: think about what else could be done (like MaxBuddy), then a quick meeting on value, how to measure it and the yearly figure. Vosmek has "cast some nets" and has ideas.

## Decisions Made

- **Card layout stays**: product box with title beside it (title may be cut), benefit partly below. No switch to name/image/text.
- **Zoom is tap-to-enlarge** (covers touch and mouse users; no hover). One card expands at the expense of others and resets on the next tap or dispensing case. Built after Farmis fixes focus.
- **The scanner beats cross-sell**: no zoom until Farmis returns focus on outside click.
- **Focus warning becomes a plain call to action**: large bold "Please tap back into Farmis" instead of "scanner disconnected".
- **Rollout by thirds, by region**, after a night switchover (01:00–03:00) to the new AKS: the 20 pilots first, then Vosmek's region (~200), then eastwards. The ~8 small-monitor pharmacies are excluded.
- **Platform access management outside Entra** (3 groups + in-platform mapping + audit logs) goes to Tomáš Dudaško for a decision. **Approved by Dudaško the same day (Teams)**, with an API for future IDM-driven access added.

## Action Items

- [ ] **Jura Brázdil**: Move the title back beside the product box (benefit partly below) and prepare the tap-to-enlarge zoom, ready to switch on once Farmis fixes focus — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Jura Brázdil**: Replace the "scanner disconnected" warning with a large, bold "Please tap back into Farmis" — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Luboš Vosmek**: Chase Farmis on returning focus when someone clicks outside the MaxBuddy webview; report back — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Jura Brázdil**: Finish the Dr. Max-styled logos before the rollout — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Martin Dubina**: Set up MaxBuddy production in the new AKS from Jura's requirements (sent 2026-10-13) — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Luboš Vosmek**: Chase Martin Dubina if there's no response by 2026-10-15 — due 2026-10-15 — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Jura Brázdil**: Enlarge the database for a first wave of ~200 pharmacies and prepare the two-environment (canary) setup — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Luboš Vosmek**: Define the first-wave pharmacies (his region, ~200), exclude the ~8 small-monitor pharmacies, and name someone on Dr. Max's side to be on the phone during the night switchover — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [x] **Luboš Vosmek / Jura Brázdil**: Take the platform access-management proposal (3 Entra groups, in-platform mapping, audit logs) to Tomáš Dudaško for a decision — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek — done 2026-10-14: Jura asked on Teams, Dudaško approved
- [ ] **Jura Brázdil**: Build in-platform user management on 3 Entra groups (Users, Admins, SuperAdmins): admins manage the parts the SuperAdmin assigns, with audit logs, test users, and an API (API keys) for future IDM-driven access — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek
- [ ] **Marek Pillár**: Send Vosmek the 2027 initiatives email, then hold a short BQ meeting on his list — from 2026-10-14-maxbuddy-redesign-zoom-rollout-thirds-vosmek — partial 2026-10-14: e-mail sent

## Open Questions

- **Farmis timing**: when will Farmis start the focus fix? Nobody has a date, and the zoom depends on it.
- **Argument length**: is a hard character limit on cross-sell arguments still worth doing, given the tap-to-enlarge zoom? Who on Dr. Max's side would rewrite long ones?
- **Switchover date**: not set. It depends on Dubina's production setup and a parallel-run test.
- ~~**Who decides the platform access model**~~: resolved the same day. Dudaško approved on Teams.
- ~~**Second unlock**~~: resolved. Test users (the CC team wants them).
- **Entra groups for the new model**: who creates the 3 AI groups on Dr. Max's side, and what happens to Lexie's 22 existing groups during the migration?

## Sentiment & Tone

Practical and friendly, and more concrete than 09-29. Vosmek is still the hands-on champion. He tested the design with pilot pharmacists, called Farmis during the meeting, and offered to chase BDC. He is protective of his users: he worries red warnings will scare them and he doesn't want to launch "looking like Benu". He moved from big-bang to thirds himself, a sign of trust in the canary approach.

**Relationship signals:** Jura was open about not escalating the Farmis blocker strongly enough, and Vosmek took it calmly. The "within days" expectation gap from 09-29 is closing: Vosmek now asks for the steps and accepts a night switchover. The access-management request was raised with the MaxBuddy business owner, who correctly pointed it to Dudaško. Jura asked Dudaško directly within the hour and got a yes in minutes, which shows a short, trusting line between them.

**Watch-outs:**
- The zoom and part of the UX polish now hang on Farmis, which hasn't started. Without a date, the "beauty by year-end" plan ([[ASM-196]]) is at risk.
- Production setup depends on one BDC person's time (Dubina).
- The logos are a rollout gate for Vosmek, not a nice-to-have.

## Routing Log

- **Transcript fixes**: Speaker attribution (Jura / Marek / Vosmek), Martin Dubina's name, "Juraj" = Jindřich Tůma, Farmis contact left unnamed: confirmed by PM.
- **project-assumptions**: Added ASM-287 (card layout + zoom), ASM-288 (tap-back warning), ASM-289 (rollout plan by thirds), ASM-290 (platform access management, decided with Dudaško), ASM-291 (argument length limit, open). Updated ASM-198, ASM-203, ASM-027, ASM-196, ASM-200.
- **project-stakeholders**: Updated STK-011 (Vosmek), STK-026 (Jura), STK-010 (Dudaško); STK-070 identified as Martin Dubina; added STK-073 Míra Suchý, STK-074 Kuba Mísař.
- **project-knowledge**: MaxBuddy kiosk/rollout facts; AI Platform access model.
- **project-daily** (2026-10-15): Jura, Vosmek and Dubina items added as waiting; the 2027 e-mail to Vosmek logged as sent on 2026-10-14; the "confirm rollout date" item closed on 2026-10-14.
- **Not routed**: product-scope / product-feature (no MaxBuddy scope or FEAT files exist).
