---
last_updated: 2026-09-02
type: external
attendees: [Jindřich Tůma, Jura Brázdil, Lukáš Szücs, Vladislav Tvarůžek, Honza Zelený, Viliam Gago]
tldv_link:
---

# AKS & Atlantis Infrastructure Sync

**Date**: 2026-09-02
**Attendees**: Jindřich Tůma (BigHub, PM/coordination lead — leads the sync), Jura Brázdil (BigHub, developer — logistics/reklamace, largely silent), Lukáš Szücs (Dr. Max CZE, Project Manager), Vladislav Tvarůžek (Dr. Max CZE, infrastructure access approvals — primary technical presenter), Honza Zelený (raises the Atlantis/ElevenLabs topic; tagged "EXT" in the source attendee list), Viliam Gago (raises a separate Terraform/redeployment question; also tagged "EXT" in the source attendee list, though recorded internally as BigHub — see Open Questions)
**Type**: external
**Recording**: N/A (Fireflies PDF export)
**Previous session**: N/A — first infra-specific sync of this kind
**Meeting prep**: N/A

> **Data quality note**: this transcript is heavily fragmented (many one-line utterances) with several likely ASR mis-transcriptions on proper nouns — notably a passage about historical MaxBuddy infrastructure work where names ("Matěj Šutý", "Max Badi"/"Max Barry", "Martin Hrášek", "Lukáš Lančík") are inconsistent and may include the product name "MaxBuddy" itself mis-heard as a person's name. Treat names in that passage as low-confidence. Speaker attribution itself is reliable (proper diarization).

## TL;DR

A short infrastructure status sync focused on two topics: AKS access provisioning (progressing well, optimistic ETA today or tomorrow morning) and the Atlantis/voicebot telephony integration (ownership and public-IP/contact questions surfaced, no blocker yet). Jindřich explicitly thanked Vladislav Tvarůžek for prioritizing BigHub's access requests.

## Key Discussion Points

### AKS access — status and timeline

Vladislav Tvarůžek reported good progress: he received the needed data (addresses, etc.) the night before from a Dr. Max-side colleague referred to as "Martin," who has since delegated related namespace work to another internal team (name transcribed unclearly, possibly "Kozi"). One issue flagged: namespaces weren't created correctly and need fixing on Martin's side; node pools already exist. Tvarůžek can now begin configuring the VPN address. His optimistic timeline: finish today (2026-09-02), worst case tomorrow morning (2026-09-03). Once firewall/permission requests are formally submitted, turnaround is now roughly an hour — a major improvement, with the Network Team owning that provisioning (previously described elsewhere in this account as taking up to two weeks).

Jindřich explicitly thanked Tvarůžek: *"Thank you for making it a priority, we really appreciate it — it's very important to us."*

Separately, Tvarůžek mentioned a pending "datacenter" request with a contact named Lukáš (surname unclear — possibly Lukáš Szücs, present in this meeting) still awaiting confirmation.

Jindřich also referenced having sent Tvarůžek information on something called **"AKSO"** — Tvarůžek admitted he hadn't read it yet, explaining that **"Planning Wizard"** (a separate Dr. Max-side initiative, not previously seen in this account) had displaced AKSO as his priority for about two days, causing the delay. He committed to reading the AKSO/Atlantis info shortly. *(Whether "AKSO" is a distinct workstream from "AKS" or a transcription artifact is unclear — see Open Questions.)*

### Atlantis / voicebot integration

Honza Zelený raised that Atlantis would connect directly to **ElevenLabs** (voice AI provider, implicitly for the voicebot's speech capability), and separately flagged that port 5060 (SIP signaling) is already open, with something related to T-Mobile also mentioned.

Tvarůžek clarified Atlantis's setup: it runs on Dr. Max's own datacenter hardware (their VMs), but is operated as a vendor service — Atlantis's own staff administer it, including public addresses and communications, which Tvarůžek believes Atlantis manages independently. He named a specific Atlantis-side contact, **"Tecl,"** as the person to track down for this. Atlantis currently functions as the central PBX for the entire Dr. Max call center and all T-Mobile data lines — every inbound call to the call center currently routes through this existing SIP connection. Adding further SIP lines directly is not expected to be a technical problem.

The team will need a public IP or public domain configured for a new element (implicitly the voicebot integration) — this needs to be worked out with Atlantis directly, since they own that piece end-to-end. Tvarůžek will chase this via email/contact with Tecl and noted he's "pinned it so I don't forget."

### Aside: legacy MaxBuddy infrastructure (Terraform vs. manual)

Viliam Gago asked whether some earlier PTU/model-related infrastructure had been set up manually or via a Terraform-style tool, in case a redeployment is needed. Tvarůžek wasn't present for that work and didn't know. Jindřich recalled it was clicked manually, naming a person no longer confirmed reliably in this transcript (see data-quality note above) — the consensus was that it was ad hoc manual work, the people most involved are no longer easily reachable ("always a nut to crack" per Tvarůžek), and no structured IaC state exists for it. Consensus: leave it alone since it currently works — *"when it stops working, we'll know it's broken."*

### Wrap-up

Jindřich confirmed AKS and Atlantis were the only two infra topics for today and reiterated BigHub is available if Dr. Max needs anything. Tvarůžek confirmed he'll push the problematic AKS deliverables (worked on yesterday and this morning) and pass along the Atlantis items to get that moving, using the existing chat channel for contact.

## Decisions Made

- Leave the legacy, manually-configured MaxBuddy infrastructure untouched for now — no redeployment or IaC migration planned unless it breaks.

## Action Items

- [ ] **Vladislav Tvarůžek**: Finish AKS VPN/access configuration — target today (2026-09-02), worst case tomorrow morning (2026-09-03) — from 2026-09-02-aks-atlantis-infra-sync
- [ ] **Vladislav Tvarůžek**: Identify and reach the Atlantis contact "Tecl" regarding public IP/domain configuration for the voicebot integration — from 2026-09-02-aks-atlantis-infra-sync
- [ ] **Vladislav Tvarůžek**: Read the AKSO/Atlantis information Jindřich sent (deferred due to "Planning Wizard" priority) — from 2026-09-02-aks-atlantis-infra-sync

## Open Questions

- Is "AKSO" a distinct Dr. Max workstream from "AKS," or a transcription artifact of the same thing?
- What is "Planning Wizard" — a new Dr. Max-side project not previously seen in this account?
- Both Honza Zelený and Viliam Gago are tagged "EXT" in this meeting's source attendee data — Viliam Gago is currently recorded as BigHub-internal (STK-027). Is the "EXT" tag meaningful (e.g. contractor status) or just an artifact of the recording tool's calendar-domain detection?
- Who exactly did the original manual/ad hoc MaxBuddy infrastructure work, given the name inconsistencies in this transcript?

## Sentiment & Tone

Collaborative and low-friction — a routine technical status sync with no visible tension. Jindřich is explicitly appreciative of Tvarůžek's prioritization, and Tvarůžek is proactive and transparent about the delay (openly attributing it to a competing priority rather than deflecting). The legacy-infrastructure aside has a light, joking tone ("four useless MacBooks lying around").

## Routing Log

- **project-stakeholders**: Added STK-033 (Tecl, low-confidence); enriched STK-016 (Vladislav Tvarůžek — name corrected from "Tvarušek"), STK-027 (Viliam Gago), STK-029 (Honza Zelený — role firmed up). Declined to create new entries for "Martin," "Matěj Šutý," "Martin Hrášek," "Lukáš Lančík" (too thin/unreliable) — captured as a project-knowledge historical footnote instead.
- **project-knowledge**: Enriched Atlantis (vendor/telephony detail), AKS (access timeline), MaxBuddy (legacy manual-infra footnote), Max/Maxi/Lexi (Mertová spelling correction); added Planning Wizard, ElevenLabs entries.
- **project-daily**: Added 3 action items (all Vladislav Tvarůžek); closed the pre-existing carry-forward item on pushing AKS access with Vláďa Tvarušek, now resolved by this meeting.
