# CorePVS — Project Context

**Version:** 0.1.0
**Last Updated:** 2026-03-12

**See also:**
- Visual guidelines: `<!-- TBD — visual guideline document not yet created -->`
- Roadmap: `PRD260311-pvs-core-roadmap.md`
- DMEA use cases: `SCOP260312-use-cases-demo.md`

---

## Product Vision

Independent, certification-ready components that compose into a white-label practice management system.

**Target vision (DMEA):** "The PVS that masters MVZ complexity — intelligent, connected, scalable."

**Brand promise:** `<!-- TBD -->`

---

## Current Scope

Two parallel work streams:

| Work Stream | Timeline | Focus |
|-------------|----------|-------|
| **Core PVS Prototype (DMEA)** | April 7–10, 2026 | 2 use cases for trade fair demo |
| **Core PVS (ongoing)** | Building modular, certification-ready components | Phase 1 first |

### Feature Status

| Feature Area | Status |
|-------------|--------|
| Patient Data Management (Phase 1) | In progress |
| Diagnosis, Coding & Service Documentation (Phase 2) | Planned |
| Billing & Submission (Phase 3) | Planned |
| Prescription Management / E-Rezept (Phase 4) | Planned |
| Forms, eAU & ePA (Phase 5) | Planned |
| eDMP / eDocumentation (Phase 6) | Planned |
| Foundation & Practice Infrastructure (Phase 7) | Planned |

**Total estimated requirements across all phases: ~1,028**

---

## Problem

### MVZ-specific structural pain points

MVZs (Medizinische Versorgungszentren) face complexity that single-practice PVS systems were never designed for:

- **Multiple locations** — no unified view, no cross-location optimization
- **Multiple specialties** — different workflows, resource types, and billing rules under one organization
- **Changing practitioners** — staff rotates across locations; systems don't follow
- **Centralized control vs. decentralized work** — leadership needs oversight, staff needs autonomy

### Operational blind spots

- No-show rates go undetected — no pattern analysis across locations
- Practitioner performance invisible — no benchmarking within specialties
- Expensive resources underutilized (CT/MRI) — no cross-location capacity balancing
- No cross-location capacity optimization — demand/supply mismatch stays hidden

### Integration failures

- Media disruption between HIS (hospital) and MVZ — paper-based referrals, fax, phone
- Duplicate data entry — patient registered separately in each system
- No real-time data exchange — findings, appointment status, and diagnostic requests transferred manually
- No structured, audit-proof data transfer between sectors

### Management gaps

- Gut-feeling decisions — no operational data to steer the organization
- No transparency across locations — leadership can't see what's happening in real time

`<!-- TBD: quantified market data -->`

---

## Solution

A modular PVS built natively for MVZ complexity:

- **Cross-sector integration (HIS ↔ MVZ)** — structured, audit-proof data transfer via HL7/FHIR; no media disruption, no duplicate data entry
- **Intelligent appointment and resource planning** — rule-based (no AI required); considers specialty, provider availability, device capacity, location utilization
- **Real-time operational dashboard** — traffic-light KPIs (red/yellow/green) with drill-down from high-level overview to detailed breakdown
- **Decision support, not automation** — system suggests next steps, never auto-executes
- **White-label, certification-ready components** — each component is a standalone mini-app that composes into a full PVS
- **Complete patient pathway** — from hospital admission through MVZ treatment to case closure, all in one connected flow

---

## Target Users

Two primary user roles in the practice setting:

### MFA (Medizinische Fachangestellte) — Front Desk

Core tasks:
- Patient registration (eGK card read-in / manual entry)
- Cost carrier resolution (8 scenarios: valid IK, Kassenfusion, dissolved carriers, etc.)
- Schein management (record types 0101–0104, quarter transitions, referrals)
- HZV/FAV enrollment (Teilnahmeerklärung lifecycle, participation management)
- Billing submission (KV billing file generation, 1-Click-Abrechnung)
- Forms processing (eAU, BFB form printing)

### Doctor (Arzt) — Patient Care

Core tasks:
- Diagnosis coding (ICD-10-GM with SDKRW rule engine, Diagnosensicherheit V/G/A/Z)
- Service documentation (GOP entry, OPS procedure codes, psychotherapy documentation)
- Prescriptions (E-Rezept with FHIR bundle generation, QES signing, drug safety checks)
- eDMP management (8 chronic disease programs: Diabetes 1&2, Asthma, COPD, KHK, Heart Failure, Breast Cancer, Depression)
- eArztbrief / ePA exchange (HL7 CDA R2, document upload/retrieval)

### Secondary users (dashboard context)

- **MVZ Management** — operational oversight across all locations
- **Site / Practice Managers** — location-level performance monitoring
- **Medical Directors** — quality and efficiency insights (optional)

`<!-- TBD: deeper persona details -->`

---

## JTBD Ladder

### MFA — Core Jobs

> "When a patient arrives, help me register them quickly and accurately so billing starts correctly."

> "When insurance changes, help me resolve the cost carrier so claims aren't rejected."

> "When the quarter ends, help me submit billing files with zero errors."

> "When a patient enrolls in HZV/FAV, help me manage the Teilnahmeerklärung lifecycle so nothing falls through."

### Doctor (Arzt) — Core Jobs

> "When I see a patient, help me code the diagnosis correctly so it passes SDKRW validation."

> "When I prescribe medication, help me generate a compliant E-Rezept with safety checks."

> "When I treat a chronic patient, help me complete eDMP documentation so nothing is missing."

> "When I receive a hospital referral, help me see the patient's data without re-entering it."

### MVZ Management — Core Jobs

> "When I review operations, help me spot inefficiencies across locations so I can act before they become problems."

> "When resources are underutilized at one location, help me see where demand exists so I can rebalance."

`<!-- TBD: supporting jobs, emotional jobs, social context -->`

---

## Value Proposition

### For MVZ operations

- **Reduction of idle times** through intelligent appointment control
- **Fewer incorrect bookings** due to automated resource logic
- **Improved utilization of expensive resources** (especially CT/MRI)
- **Higher quality of care** through complete, up-to-date patient data
- **Improved patient satisfaction** — fewer waiting times, fewer duplicate examinations
- **First PVS to give MVZ leadership real operational transparency**

### Trade fair pitch (30 seconds)

> "We manage appointments, resources, and patient information across locations — and for the first time give MVZ leadership real operational transparency. Less chaos, better utilization, better care."

### Differentiator vs. single-practice PVS

Orchestration across locations, specialties, and resources. Single-practice systems treat each location as an island. CorePVS treats the entire MVZ as one connected organization.

---

## Competitive Landscape

From source documents: "clear differentiation from single-practice PVS" is the primary positioning.

`<!-- TBD: competitive analysis -->`

---

## Product Architecture (the "Lego Model")

- **Each component = fully working mini-app** (frontend + backend), stands alone
- **White-label**: baseline components get customer-specific branding via design system theming layer
- **Certification-ready baseline**: ~70–80% reused across customers unchanged
- **Customer customization: ~20–30%** — certification constrains how much can diverge
- **After branching for a customer, each version is independent** — changes for one don't affect others
- **No over-engineering for reusability** — focus on solid, certification-ready components; the baseline quality is what matters most
- **Build slim GUI/UX on top of Core PVS Backend** — no external interfaces at this stage
- **Components = big subpages**, not small UI pieces — think independent, modular components

### What designers produce per component

1. **Screens** — every screen with all states (empty, error, loading, current, etc.)
2. **Flows** — step-by-step user journeys
3. **Transitions** — how one state leads to another

**Definition of done:** every PM requirement is checkable against the screens, flows, and transitions.

---

## Roadmap Summary

Seven phases, derived from four requirement sources (KVDT, ICD-10-GM, SV Components, Crucial Workflows). Full details in `PRD260311-pvs-core-roadmap.md`.

**Phase 1 — Patient Data Management** (~72 reqs + SV)
Complete patient registration — eGK card reading, manual entry, cost carrier resolution, Schein lifecycle, and HZV/FAV enrollment and participation workflows.

**Phase 2 — Diagnosis, Coding & Service Documentation** (53 + ~37 reqs + SV)
ICD-10-GM coding with SDICD/SDVA/SDKRW master data, HZV/FAV diagnosis rules, GOP entry, OPS coding, psychotherapy documentation, and HZV/FAV service filtering.

**Phase 3 — Billing & Submission** (~25 reqs + SV)
KVDT billing file generation, XPM validation, XKM encryption, 1-Click submission via KIM, and the complete HZV/FAV billing pipeline.

**Phase 4 — Prescription Management / E-Rezept** (~407 reqs)
Full electronic prescription workflow — drug search, FHIR bundle generation, QES signing, E-Rezept Fachdienst — plus Heilmittel, Hilfsmittel, eVDGA, and BMP.

**Phase 5 — Forms, eAU & ePA** (~82 reqs)
Electronic sick leave certificates, BFB form printing with PDF417 barcodes, electronic doctor letters via KIM, and ePA document operations.

**Phase 6 — eDMP / eDocumentation** (~109 reqs)
Structured data capture for 8 chronic disease management programs and electronic skin cancer screening documentation.

**Phase 7 — Foundation & Practice Infrastructure** (~41 reqs + SV)
System backbone — master data, user/access control, TI reporting, and HZV/FAV contract infrastructure that every downstream module depends on.

---

## DMEA Demo Use Cases

Two use cases designed for the DMEA trade fair (April 7–10, 2026). Full details in `SCOP260312-use-cases-demo.md`.

### Use Case 1: Integrated Patient Pathway (HIS ↔ MVZ)

An adult patient presents at a hospital emergency department. After triage, they're referred to a connected MVZ. The demo shows: structured data transfer from HIS to PVS via HL7/FHIR, clear visual separation of external (read-only) vs. own documentation (editable), digital referral for CT examination back at the hospital, intelligent appointment scheduling considering specialty/device/location, real-time CT report transfer back to MVZ, and complete case documentation and closure.

**Key message:** No media disruption, no duplicate data entry, seamless cross-sector care.

### Use Case 2: Smart PVS Dashboard for MVZ Operational Control

A real-time dashboard for MVZ management showing operational KPIs across all locations using traffic-light logic. The demo shows: high-level overview with red/yellow/green indicators per location, drill-down into no-show patterns by weekday/time/specialty, practitioner-level performance insights (operational, not quality judgment), resource utilization with concrete rebalancing recommendations, and actionable next steps (suggested, never auto-executed).

**Key message:** Data-driven steering instead of gut feeling. First PVS with real MVZ operational transparency.

---

## Design Constraints

| Constraint | Rationale |
|------------|-----------|
| Desktop-only (24" monitors) | Target environment is practice workstations |
| No responsive / no mobile | Not needed for MFA/doctor workflows |
| White-label ready | Product serves multiple customers with their branding |
| Certification scope | ~70–80% baseline must pass certification unchanged |
| Visual guidelines | `<!-- TBD -->` |
| German-language UI | Primary market; domain terms are German healthcare standards |

---

## UX Pillars / Primary Axis

`<!-- TBD: primary UX axis -->`

Hints from existing documentation that can seed the discussion:

- **Operational transparency** — the dashboard use case centers on making the invisible visible
- **Certification compliance** — baseline quality is non-negotiable; every screen must be certification-ready
- **MVZ-native complexity handling** — multi-location, multi-specialty, multi-practitioner as first-class concepts, not afterthoughts

---

## UX Principles

Extractable design patterns from source documents. These are observed patterns, not yet formal principles.

`<!-- TBD: formal UX principle definitions -->`

### Observed patterns

**Traffic-light logic (red / yellow / green)**
Immediate status interpretation without reading text. Used in dashboard KPIs, location health indicators. Every status must be visually parseable at a glance.

**Drill-down pattern: overview → detail**
High-level aggregated view (all locations) → click for detailed breakdown (by weekday, time, specialty, practitioner). Users should never need to navigate away to understand a metric.

**Clear visual separation: external vs. own data**
External data (e.g., hospital records) is read-only and visually highlighted. Own documentation is editable and legally independent. This is both a UX pattern and a legal requirement.

**Decision support, not automation**
System suggests next steps but never auto-executes. Dashboard recommends rebalancing capacity; user decides. This applies across all features — the PVS informs, the human acts.

**All states for every screen**
Empty state, error state, loading state, current/populated state. This is a design deliverable requirement: every screen must show how it behaves in every state.

**Checkable against requirements**
Definition of done for design: every PM requirement must be verifiable against delivered screens, flows, and transitions. Design is not decorative; it's a specification.

---

## Success Metrics

`<!-- TBD: success metrics -->`

---

## Persona Testing Dimensions

`<!-- TBD: persona testing dimensions -->`

---

## Domain Glossary

Key German healthcare terms used throughout CorePVS documentation and UI.

| Term | Definition |
|------|-----------|
| **eGK** | Elektronische Gesundheitskarte — the patient's electronic health insurance card, used for identification and insurance verification |
| **KV** | Kassenärztliche Vereinigung — regional association of statutory health insurance physicians; manages billing between practices and insurers |
| **VKNR** | Versichertenkarten-Nummer — insurance card number used to identify the cost carrier |
| **IK** | Institutionskennzeichen — institutional identifier for cost carriers (insurance companies) |
| **Schein** | Abrechnungsschein — billing case document that links a patient visit to a specific quarter, insurance, and treatment context |
| **KVDT** | KV-Datentransfer — the standardized data format for transmitting billing data from practices to the KV |
| **KBV** | Kassenärztliche Bundesvereinigung — federal association of statutory health insurance physicians; defines standards and master data |
| **BSNR** | Betriebsstättennummer — practice location identifier (9-digit); each physical location has its own BSNR |
| **LANR** | Lebenslange Arztnummer — lifetime physician identifier (9-digit); unique per physician |
| **TI** | Telematikinfrastruktur — Germany's secure health data network connecting practices, hospitals, pharmacies, and insurers |
| **KIM** | Kommunikation im Medizinwesen — secure email system within the TI for exchanging medical documents (eAU, eArztbrief, eDMP) |
| **MVZ** | Medizinisches Versorgungszentrum — multi-physician outpatient care center, often with multiple locations and specialties |
| **MFA** | Medizinische Fachangestellte — medical office assistant; handles front desk, registration, billing, and administrative tasks |
| **HZV / FAV** | Hausarztzentrierte Versorgung / Facharztvertrag — selective contracts between insurers and physician groups for coordinated primary/specialist care |
| **ICD-10-GM** | International Classification of Diseases, 10th revision, German Modification — mandatory diagnosis coding system |
| **GOP** | Gebührenordnungsposition — billing code from the EBM fee schedule; identifies a specific medical service |
| **EBM** | Einheitlicher Bewertungsmaßstab — the uniform fee schedule for statutory health insurance services |
| **Dauerdiagnosen** | Permanent/chronic diagnoses carried forward across quarters; require explicit confirmation and review |
| **Diagnosensicherheit** | Diagnosis certainty qualifier — V (suspected), G (confirmed), A (excluded), Z (status post); mandatory for every diagnosis |
| **eAU** | Elektronische Arbeitsunfähigkeitsbescheinigung — electronic sick leave certificate, transmitted via KIM |
| **ePA** | Elektronische Patientenakte — the national electronic patient record |
| **eDMP** | Elektronisches Disease-Management-Programm — structured chronic disease documentation for 8 programs |
| **BMP** | Bundeseinheitlicher Medikationsplan — standardized medication plan with 2D barcode |
| **E-Rezept** | Elektronisches Rezept — electronic prescription via gematik Fachdienst with qualified electronic signature (QES) |
| **SDKRW** | Stammdatei Kodierregeln — KBV-provided coding rule engine that validates ICD-10 diagnoses against conditional rules |
| **SDICD** | Stammdatei ICD — KBV-provided ICD-10-GM master data file with code descriptions, validity, and metadata |

---

## Changelog

| Version | Date | Who | Changes |
|---------|------|-----|---------|
| 0.1.0 | 2026-03-12 | Ngan | Initial structure — clean version without rationale annotations |
