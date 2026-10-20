---
last_updated: 2026-10-20
type: external
attendees: [Tereza Foltová, Jan Žižka, Hnilička (Canon), Dušan Hýža, Filip Černý]
recording_link:
---

# Fakturace Doprav — Canon Scanner & Kiosk Hardware: DR-G2 Series, Locked-Down Zebra Kiosk, Driver Test at Pavlov

**Date**: 2026-10-20
**Attendees**: Tereza Foltová (ViaPharma, logistics / AI initiatives), Jan Žižka (ViaPharma, Fakturace doprav business owner), Hnilička (Canon, scanner vendor; in the room with Žižka after a warehouse walk-through), Dušan Hýža (ViaPharma / Dr. Max CZ IT), Filip Černý (BigHub, developer)
**Type**: external
**Recording**: N/A
**Previous session**: [2026-10-14 — Fakturace Doprav: Where Document State Lives](2026-10-14-fakturace-doprav-document-state-zizka-slama.md)
**Meeting prep**: N/A

> **Attribution note**: the transcript's speaker labels are unreliable (the Canon rep sat in Žižka's room and many of his lines are tagged as Filip Černý, Jan Žižka or Dušan Hýža). Statements below are attributed by content: Canon product and Capture On Touch details → Hnilička; network, security and Zebra points → Dušan Hýža. Marek Pillár did not attend.

## TL;DR

After a warehouse walk-through, Canon (Hnilička) ruled out the two small scanners from the email thread (60-sheet trays, no staple detection) and steered everyone to the larger **Canon DR-G2 series: DR-G2090 (USB) or DR-G2110 (adds Ethernet)**. IT (Dušan Hýža) ruled out an open Windows PC as the kiosk because drivers must not be able to leave the app. The working direction is a **scanner on USB to a locked-down Zebra device running BigHub's web app**, ideally with a large external touch monitor. Hýža asks Zebra for such a device, and Tereza arranges a **test with real drivers at Pavlov**. Network scanning stays as a fallback because Zebra's larger screens run only Android.

## Key Discussion Points

### Small scanners are too weak for the volume

Filip Černý opened with the two models Canon had proposed by email (SF-350 / SF-400 class). Either works for BigHub. BigHub prefers **scanning straight to its HTTPS endpoint**, which only the model with the large screen supports. The cheaper one can only scan to a shared folder (SFTP). His concerns: whether the built-in screen is big enough for drivers, and what network access the warehouse allows.

Hnilička (Canon), after walking the warehouse with Žižka, judged **both small models unsuitable**:
- Up to **3 drivers at once, each with ~100 sheets**. Small trays and 60-ppm speed would cause queues.
- **Many documents are stapled.** The small models assume clean loose sheets and would "suffer a lot". The larger model **detects staples and stops**, so the driver sees it and can react (e.g. cut off the corner, which is normal practice in digitisation).
- Proposed the **A3 Canon DR-G2 series**: a **300-sheet feeder**, so one driver's batch takes about a minute. **White rollers** (instead of black) avoid dark edge artefacts that disturb recognition. Canon has used this setup with several customers.

### Recognition: Canon's OCR is not needed

Hnilička asked whether BigHub uses plain OCR. Filip: barcode reading, then OCR, plus **stamp detection/counting** and **ICR for handwriting**. Canon's Capture On Touch bundles a basic IRIS OCR engine. Filip doesn't plan to use it: "it doesn't pay off to do it twice" [translated from Czech].

### Network access is not a constraint

Dušan Hýža (IT): an Ethernet Canon scanner can go into the internal network ("we already use such scanners at the eLabs"), and a USB scanner on a domain PC is also fine. **No infrastructure blocker either way.**

### USB kiosk vs. network scanning

- **Hýža's first instinct: network scanning** to network storage, with BigHub's software picking files up from there. A USB scanner on a single PC is fragile, because a Windows or driver update can stop it, and network scanning is "more foolproof" (~99% success) [translated from Czech]. It would also let several devices validate the scans.
- **Filip**: both variants work for BigHub. (A) watch a shared folder and process new files, or (B) the scanner calls BigHub's endpoint directly. B is "very elegant", because the demo app already calls the same endpoint from the web UI and BigHub would then store only the finished, sorted documents rather than raw pages. Hýža agreed that a direct connection is more efficient.
- **Hnilička on the DR-G2 line**: the **DR-G2090 is USB only**. The **DR-G2110 / G2140** add networking but still need a client app (TWAIN or Capture On Touch); they are not standalone. Only the small 400 runs autonomously. He **does not recommend** running Capture On Touch on a server with the scanner as a thin client in heavy use ("when 50 people rotate through in an hour" [translated from Czech]). In practice the stable pattern is a USB kiosk workstation, as he has seen in Germany. Canon offers a **Capture On Touch SDK** to script what happens after a scan (send to a system, protocol, storage). Filip found this very interesting for the USB kiosk route.
- **Updates**: Canon's view is that a tuned kiosk is simply not updated, and its driver and app updates are conservative. Hýža: a domain machine must get Windows security updates (no "island" PCs), though ViaPharma deploys builds 6–12 months late. Canon cited **Windows 11 24H2**, which broke printing and scanning across all vendors for about 2 months. If a PC kiosk is used, Hýža wants **at least one spare PC** ready.

### Security: drivers must not leave the app

Hýža asked whether users log in. Filip: **no login, scanning is anonymous**. Each document is matched to its route by its own data. The driver has **read-only** access (routes, documents, extracted data, scan previews), confirms at the end, and a new session starts. Filip admitted a browser-based web app on an open PC can be exited, and he hadn't thought about locking it down.

Hýža: this rules out an ordinary Windows PC. ViaPharma already uses **Zebra tablets with a forced kiosk page**. They are industrial, vandal-resistant and remotely managed. "The first thing that will happen is a driver manages to crash it and they'll start calling" [translated from Czech]. Concern: the big Canon scanners' new interface is Windows-first, and **Android support is doubtful**. Hýža then found the **Zebra ET80 (12", Windows 11 Pro)**, which would solve it.

### Screen size: drivers need it big

Jan Žižka: is 12" too small? "We're building it for drivers… it must be fast and work first time, or they won't use it. Nobody will ever zoom or study anything" [translated from Czech]. Filip: 12" is the lower bound, 14"+ preferred, so **go with a large screen**: one tap to check, one to confirm. Hýža will ask Zebra about a robust Windows device, ideally with an **external (touch) monitor**: the tablet is used only to confirm, and the big screen shows the driver everything. Filip asked him to also check whether a second touch screen can replace the built-in one.

Hýža's closing caveat: Zebra's larger devices (e.g. 22") are **Android only**. So **network scanning plus web-app confirmation on a tablet** is still on the table if no large Windows device exists.

### Model choice and trial

Hnilička simplified the choice to **DR-G2090 (USB, 300-sheet feeder)** vs. **DR-G2110 (same, plus Ethernet; still needs a host PC)**. In the kiosk setup either would be connected over USB to the Zebra. He proposes a **first hands-on trial** before any loan: bring the 2090 (maybe the 2110), run real papers through Capture On Touch, and check output quality and how simple it is to use. Truck drivers are "a special category", and phone photos don't work for them, as colleagues in other countries have found [translated from Czech]. Loading the tray is a known failure point too. Žižka wants a loaner and **3 drivers running their real papers**. Tereza will arrange the test **at Pavlov with Mr. Mrdlička**.

### Continuity with 2026-10-14

- The Canon meeting that Tereza owed ([[ASM-281]]) happened: Hnilička's on-site visit plus this call.
- The **standalone scanning demo** (no Axapta) offered on 10-14 was **not shown or discussed**. The driver test at Pavlov is the next hands-on step.
- The document-state topics (billing row before the ZPPV, overwrite, status) were not discussed. [[ASM-280]] and the Žižka/Tereza user description are still open.
- Consistent with [[ASM-055]] (hardware is ViaPharma's procurement) and [[ASM-259]] (the scanner talks only to BigHub's API).

## Decisions Made

- **Small Canon models (SF-350/400 class) dropped**; scanner choice narrowed to **Canon DR-G2090 vs. DR-G2110** (300-sheet feeder, staple detection, white rollers). Rationale: ~3 drivers × ~100 stapled sheets at peak.
- **No open Windows PC as the kiosk.** The device must lock drivers into the app. Working direction: **scanner on USB to a locked-down Zebra (Windows, e.g. ET80) running BigHub's web app, with a large (external touch) screen**; only the Zebra talks to ViaPharma's network. Depends on Zebra's answer.
- **Large screen is a requirement** (12" is the minimum; larger preferred). The driver flow must be one tap to check and one to confirm, with no zooming.
- **Scanning stays anonymous** (no driver login, read-only view + confirmation). Device lock-down is the security control, not authentication.
- **Canon's built-in OCR (IRIS) not used**; BigHub does barcode, OCR, stamps and ICR.
- **Trial with real drivers first** (Pavlov), then a loaner; network scanning (shared folder or direct-to-endpoint) stays the fallback.

## Action Items

- [ ] **Dušan Hýža**: Ask Zebra for a robust, lockable Windows device with a large screen, or an option for an external (touch) monitor that can replace the built-in screen — from 2026-10-20-fakturace-doprav-canon-scanner-zebra-kiosk-hyza
- [ ] **Tereza Foltová**: Arrange the scanner test with drivers at Pavlov with Mr. Mrdlička (3 drivers, real papers) — from 2026-10-20-fakturace-doprav-canon-scanner-zebra-kiosk-hyza
- [ ] **Hnilička (Canon)**: Bring a DR-G2090 (optionally a DR-G2110) for a first trial in Capture On Touch, then lend it for the driver test — from 2026-10-20-fakturace-doprav-canon-scanner-zebra-kiosk-hyza
- [ ] **Filip Černý**: Check the kiosk UI at 12" vs. larger screens and look at the Capture On Touch SDK for the USB kiosk route — from 2026-10-20-fakturace-doprav-canon-scanner-zebra-kiosk-hyza *(implied by the discussion, not explicitly agreed)*

## Open Questions

- Does Zebra have a large-screen **Windows** device, or can an external touch monitor run the UI? If not, fall back to network scanning + Android tablet for confirmation.
- DR-G2090 or DR-G2110? Is the 2110's Ethernet worth it when it still needs a host?
- Do the DR-G2 scanners work with Android at all (Canon's new interface is Windows-first; SDK route?)
- USB route: scan via Capture On Touch (+ SDK) or have BigHub's app drive the scanner directly?
- Network route: shared folder (variant A) or scanner calls BigHub's endpoint (variant B)? Which models support HTTPS scanning?
- How many scanners and stations per warehouse (peak: ~3 drivers at once)? Spare device policy (Hýža wants a spare)?
- Stapled documents: process rule for drivers (no staples, cut the corner) and how the UI handles a staple stop.
- When does the standalone scanning demo ([[ASM-281]]) happen, now that the driver test is next?

## Sentiment & Tone

Constructive and practical. Hnilička brought vendor experience and pushed back on the cheap options. Hýža was firm on security ("we are quite tough on this" [translated from Czech]) but solution-minded and looked up devices live. Filip was open and adjusted quickly ("new information for me"). Žižka kept the focus on the driver as user. Tereza closed with "we're clear on what we want and what the options are" [translated from Czech]. No tension. The main uncertainty is whether a suitable Zebra device exists.

## Routing Log

Confirmed by PM 2026-10-20 (confirm all).
- **project-assumptions**: added ASM-313 (DR-G2090/2110), ASM-314 (locked-down Zebra kiosk, Open), ASM-315 (large screen), ASM-316 (driver test at Pavlov); updated ASM-281, ASM-087, ASM-052, ASM-259
- **project-stakeholders**: STK-066 named Dušan Hýža with sentiment and expectations; STK-071 Hnilička, STK-015 Žižka, STK-013 Foltová updated; added STK-085 Mrdlička
- **project-knowledge**: new entry "Fakturace doprav scanner hardware"; Zebra terminals updated
- **client-overview**: §9 ViaPharma IT security posture
- **project-daily**: 4 waiting action items; Tereza's 2 Canon-meeting items closed
- **project-lessons**: LL-102 (kiosk hardware: involve IT security + vendor site visit early)
