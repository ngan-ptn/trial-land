# Dedalus MVZ PVS Product Context

## TLDR (agent)
- Persona: **GP/Hausarzt in an MVZ**. 
- Platform: **desktop only**.
- Visual target: **OrbisU-familiar, modernized like garrio**. Do not copy 1:1.
- Data: **realistic-looking synthetic only**. No real patient data.

## Product vision (from Google Doc)
The PVS that masters MVZ complexity. Intelligent, connected, scalable.

Typical MVZ pain points:
- multiple locations
- multiple specialties
- changing practitioners
- centralized control vs decentralized work

## Canonical terminology
- `MVZ`: Medizinisches Versorgungszentrum (medical care center)
- `PVS`: Praxisverwaltungssystem (practice management system)
- `KIS`: Krankenhausinformationssystem (hospital information system)
- `OrbisU`: Dedalus hospital `KIS` product

## Primary UX axes (measurable, fill values when decided)
- Speed: time to complete key tasks (TBD targets per UX moment).
- Safety/clarity: read-only vs editable is unambiguous at a glance (TBD how measured).
- Density: supports high-volume clinical workflow without “scroll hunting” (TBD).

## Primary persona
**Persona:** GP/Hausarzt in an MVZ.

When testing or reviewing a screen, score it on:
- Speed (TBD thresholds)
- Clarity (can I tell what to do next in 3 seconds?)
- Safety (external `KIS` data cannot be edited by mistake)
- Density (key data visible without extra clicks)
- Error recovery (undo/edit/cancel paths are obvious)
- Copy tone (professional, clinical, no fluff)

## Key UX moments (optimize for these)
1. Ingestion: GP sees a new post-ER referral pushed from hospital, no “import file” vibe.
2. Split view: external `KIS` package vs internal `PVS` documentation, read-only vs editable is obvious.
3. Smart booking: CT referral with visible availability and clear confirmation.
4. Loop closure: CT result arrives, next step decision, case closure.

## Use cases
Source of truth: Google Doc
- Google Doc: https://docs.google.com/document/d/1-BXXdk1dnt6iwSN93ndtFu0jEaROxx-6DhrkVnQRwi8/edit?usp=sharing

### Use case 1 (core): integrated patient pathway `KIS` ↔ `PVS`
Goal: seamless cross-sector workflow with clear ownership of external vs internal records.
Consent for data transfer is part of the demo. If consent is missing, data transfer from `KIS` → `PVS` is blocked (see `S3`).

Initial situation example (use in designs):
- Symptoms: increasing right lower abdominal pain for 3 days, subfebrile temperature, nausea (no vomiting)
- Vitals: stable, no signs of shock
- Triage: Manchester example. Urgency level: yellow
- Suspected diagnosis: appendicitis vs inflammatory bowel disease

---

Step ID legend:

| Step ID | Use case step |
|---|---|
| S1 | Patient admitted in hospital ER (registered in `KIS` + triage tooling) |
| S2 | Triage/screening. Urgency: yellow. No inpatient admission. MVZ follow-up |
| S3 | Consent captured for data transfer |
| S4 | Transfer selected data from `KIS` to `PVS` via HL7/FHIR |
| S5 | MVZ GP opens record in `PVS` with transfer package pre-loaded |
| S6 | Clear visual separation: external `KIS` package (read-only) vs internal `PVS` documentation (editable, legally distinct) |
| S7 | Event-driven updates (e.g., CT completed) |
| S8 | Digital referral back to hospital for CT. No paper referral |
| S9 | Intelligent CT slot suggestion (capacity, location, utilization, avoid peak times) |
| S10 | Optional teaser: digital patient engagement (forms/questionnaires/uploads) |
| S11 | CT performed and documented in `KIS` |
| S12 | CT report transferred to `PVS` in real time. GP decides outpatient vs inpatient admission |
| S13 | Case closure documented in `PVS` (diagnosis, recommendation, next steps) |

---

Screen mapping (recommended groupings only, not a requirement). Steps can be merged/split across screens.

| Screen/Panel ID | Screen name | Goal | Includes step IDs | Key UI artifact(s) | Required data (fields) | States/edge cases |
|---|---|---|---|---|---|---|
| A | Worklist / dashboard (ingestion) | Surface post-ER referrals and urgency, fast triage of the day | - S1<br>- S2<br>- S3<br>- S7 | - Incoming referral card/row<br>- Triage badge<br>- Consent indicator<br>- Status timeline snippet | - Patient demographics (name, DOB)<br>- Insurance status<br>- Pre-existing conditions (if available)<br>- Triage system + level<br>- Symptoms<br>- Suspected diagnosis<br>- Consent status + timestamp (TBD)<br>- Events/status timeline | - Consent missing (blocks transfer)<br>- Triage missing<br>- Delayed/stale updates |
| B | Patient chart (split view) | Compare external ER snapshot vs internal MVZ documentation without mixing records | - S4<br>- S5<br>- S6<br>- S7 | - Split view layout<br>- “External (KIS)” vs “Internal (PVS)” labels<br>- Read-only markers<br>- Copy-to-note action<br>- Timeline | - Transfer package: history<br>- Transfer package: vitals<br>- Transfer package: labs (if available)<br>- Transfer package: ER assessment/note<br>- Transfer package: suspected diagnosis<br>- Events/status timeline<br>- Internal MVZ note | - Partial package (labs missing)<br>- Patient not found/duplicate (TBD)<br>- Copied values tracking (TBD) |
| C | Referral + scheduler | Create CT referral and book a slot with clear confirmation | - S8<br>- S9 | - CT referral form<br>- Slot picker (availability + recommended)<br>- Confirmation state | - Referral type (“CT”)<br>- Reason/indication<br>- Slot list (time, location, availability)<br>- Capacity/utilization cues | - No slots today<br>- Conflicts<br>- Multi-location choice<br>- Missing required fields (TBD) |
| D | Results inbox + report | Receive CT result, review report, decide next step | - S11<br>- S12 | - Inbox item<br>- Report preview/viewer<br>- Next-step prompt | - Status: “CT completed”<br>- CT report text/summary<br>- Result timestamp | - Result delayed<br>- Multiple results |
| E | Case closure | Document final decision and next steps cleanly | - S13 | - Diagnosis<br>- Decision<br>- Next steps summary | - Diagnosis<br>- Treatment decision<br>- Next steps<br>- Optional feedback to hospital/shared record (if used) | - Closure incomplete<br>- Missing diagnosis |
| X | Optional teaser | Show optional patient engagement without building it | - S10 | - Teaser card/section | - Forms/questionnaires/uploads (TBD) | - Keep optional<br>- Can omit |

MVZ value proposition (from Google Doc):
- Reduction of idle times through intelligent appointment control
- Fewer incorrect bookings due to automated resource logic
- Improved utilization of expensive resources (especially CT/MRI)
- Higher quality of care through complete, up-to-date patient data
- Improved patient satisfaction (fewer waiting times, fewer duplicate examinations)
- Strong for DMEA: classic MVZ problem, immediately explainable visually (calendar + utilization), clear differentiation from single-practice PVS

---

### Use case 2 (stretch): smart PVS dashboard for MVZ operational control
Goal: consolidated operational view across locations, specialties, practitioners, and resources.
Rules: explainable, non-automating recommendations. No medical text generation.

Actors (from Google Docs):
- MVZ management
- Site/practice managers
- Optional: medical directors

Preconditions (from Google Doc):
- Multiple MVZ locations active in system
- Appointment, treatment, and resource usage data available (simulated or historical)
- Rule-based and/or lightweight model-based analytics enabled

Demo flow essentials (from Google Doc):
1. Entry point: open “Smart PVS Dashboard” from PVS start screen
2. High-level operational overview: traffic-light logic (red/yellow/green) for KPIs
   - Example: Location B high no-show rate (red)
   - Example: Specialty X above-average treatment duration (yellow)
   - Example: Device Y underutilized (green)
3. Drill-down: show pattern + context
   - No-show rates by weekday, time of day, specialty
   - Example pattern: “Tuesday mornings show a 23% higher no-show rate vs MVZ average.”
   - Rule: insight is rule-based thresholds or simple statistical models, not text generation
4. Practitioner view: performance metrics, anonymized or named (role-based)
   - Example: “Practitioner A requires an average of 8 minutes longer per treatment than specialty benchmark.”
   - Show context: case mix similarity, room/device usage, peer comparison
   - Explicitly label: operational observation, not quality judgment
5. Resource utilization: identify low utilization + available slots
   - Example recommendation: “Available capacity at Location C could absorb appointment demand from Location B.”
   - Basis: geographic proximity, compatible specialties, device availability, historical patient flow
6. Actionability: suggest next steps visually, but do not execute automatically
   - Adjust appointment templates, redistribute slots, introduce reminder workflows for high-risk time slots
