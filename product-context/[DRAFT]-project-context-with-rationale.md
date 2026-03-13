# CorePVS — Project Context

**Version:** 1.1.0
**Last Updated:** 2026-03-13

**See also:**
- Design system: [tini-library](https://github.com/tini-works/tini-library)
- Copy & tone: `..docs/guidelines/copy-guidelines.md`

---

## Product Vision

Independent, certification-ready components that compose into a white-label practice management system.

**Target vision:** "The PVS that masters MVZ complexity — intelligent, connected, scalable."

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

> **Rationale:** The use-cases-demo document lists MVZ pain points qualitatively (multiple locations, no-show rates undetected, gut-feeling decisions) but provides no quantified data. Numbers like % of MVZs affected, average revenue loss from no-shows, or total MVZ count in Germany would strengthen the problem statement. This data likely exists in KBV or Zi reports but was not included in any source document provided.

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

## Value Proposition

### For MVZ operations

- **Reduction of idle times** through intelligent appointment control
- **Fewer incorrect bookings** due to automated resource logic
- **Improved utilization of expensive resources** (especially CT/MRI)
- **Higher quality of care** through complete, up-to-date patient data
- **Improved patient satisfaction** — fewer waiting times, fewer duplicate examinations
- **First PVS to give MVZ leadership real operational transparency**

### Differentiator vs. single-practice PVS

Orchestration across locations, specialties, and resources. Single-practice systems treat each location as an island. CorePVS treats the entire MVZ as one connected organization.

---

## Competitive Landscape

From source documents: "clear differentiation from single-practice PVS" is the primary positioning.

`<!-- TBD: competitive analysis -->`

> **Rationale:** The use-cases-demo document positions CorePVS as "clear differentiation from single-practice PVS." However, no source document names specific competitors or analyzes their MVZ capabilities. Market research is needed to map competitors (e.g., CGM TURBOMED, medatixx, T2med, x.isynet), assess which ones target MVZs, and build a positioning matrix. The key question: does any existing PVS offer cross-location orchestration, or is that genuinely unoccupied territory?

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

> **Rationale:** The roadmap defines MFA and doctor (Arzt) tasks in detail (eGK read-in, ICD-10 coding, E-Rezept signing, etc.), and the use-cases-demo adds MVZ management as a dashboard user. However, no source document includes persona-level details: daily environment, digital skill level, goals beyond task completion, frustrations, or quit triggers. The roles are clear; the humans behind them are not. UX research (interviews or contextual inquiry in MVZ settings) is needed to fill this gap.

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

> **Rationale:** Core functional jobs were inferred from the roadmap's phase descriptions (registration, billing, coding, prescriptions). But the roadmap is a requirements document — it describes *what the system must do*, not *what users feel or fear*. Emotional jobs (e.g., "help me feel confident I won't cause a billing rejection"), supporting jobs (e.g., "help me hand off a patient to a colleague without losing context"), and social context (e.g., certification pressure, legal liability awareness) require UX research with actual MFAs and doctors (Ärzte) in MVZ settings.

---

## Current Scope

Building modular, certification-ready components. Phase 1 first.

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

## Design Constraints

| Constraint | Rationale |
|------------|-----------|
| Desktop-only (24" monitors) | Target environment is practice workstations |
| No responsive / no mobile | Not needed for MFA/doctor workflows |
| White-label ready | Product serves multiple customers with their branding |
| Certification scope | ~70–80% baseline must pass certification unchanged |
| Design system | [tini-library](https://github.com/tini-works/tini-library) — baseline visual identity; customer theming applied on top |
| German-language UI | Primary market; domain terms are German healthcare standards |

---

## Primary UX Axes

Three measurable axes that guide every design decision:

### Speed
Time to complete key tasks.

`<!-- TBD: targets per UX moment (e.g., registration <2 min, diagnosis coding <30s) -->`

### Safety / Clarity
Read-only vs. editable is unambiguous at a glance.

`<!-- TBD: how measured (e.g., user can identify editable fields within X seconds, zero misclicks on read-only data) -->`

### Density
Supports high-volume clinical workflow without "scroll hunting."

`<!-- TBD: measurable criteria (e.g., key actions visible without scrolling on 24" monitor, information density benchmarks) -->`

---

## UX Principles

Extractable design patterns from source documents. These are observed patterns, not yet formal principles.

`<!-- TBD: formal UX principle definitions -->`

> **Rationale:** The patterns below were extracted from the use-cases-demo (traffic-light logic, drill-down, external vs. own data separation, decision support) and the Notion brief (all states for every screen, checkable against requirements). These are observed design patterns, not formal principles. Formal principles need a name, a rationale (why this matters for CorePVS users), and implementation rules (what designers/developers must do). The jelvo product-context has examples of this format (e.g., "Clear Decision Paths: max 3 actions per screen, most important step highlighted"). CorePVS needs equivalent rigor, adapted for desktop-first, certification-constrained, MVZ-complexity workflows.

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

> **Rationale:** No source document defines KPIs or success criteria. The roadmap is requirement-driven (~1,028 reqs across 7 phases) but doesn't specify how to measure whether the product *succeeds* beyond passing certification. The use-cases-demo implies operational metrics (no-show rates, utilization, treatment duration) but only as dashboard *features*, not as product success measures. PM input is needed to define KPIs per user type — suggested structure:
>
> - **MFA:** registration time per patient, billing error rate, Schein completion rate
> - **Doctor (Arzt):** diagnosis coding time, SDKRW violation rate, E-Rezept completion rate
> - **MVZ Management:** dashboard adoption, time-to-insight, action rate from recommendations
> - **System:** certification pass rate, component reuse rate across customers

---

## Persona Testing Dimensions

`<!-- TBD: persona testing dimensions -->`

> **Rationale:** No source document defines pass/fail criteria for testing designs against user types. The roadmap describes *what* each role does but not *how well* they should be able to do it. The use-cases-demo shows dashboard interactions but doesn't specify usability thresholds. UX research is needed to establish benchmarks. Suggested structure based on tasks from the roadmap:
>
> **MFA — Efficiency & Accuracy Benchmark**
> | Dimension | Pass | Fail |
> |-----------|------|------|
> | Registration speed | <2 min with eGK | >5 min |
> | Cost carrier resolution | Correct on first attempt | Requires supervisor help |
> | Error recovery | Can fix without starting over | Must re-enter from scratch |
>
> **Doctor (Arzt) — Clinical Workflow Benchmark**
> | Dimension | Pass | Fail |
> |-----------|------|------|
> | Diagnosis coding | Finds correct ICD-10 code in <30s | Scrolls through long lists |
> | SDKRW feedback | Understands violation and fix immediately | Confused by error message |
> | External data | Clearly distinguishes hospital vs own data | Unsure what's editable |

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
| 1.1.0 | 2026-03-13 | Ngan | Remove DMEA-specific content (demo use cases, trade fair pitch, brand promise, event timeline); add primary UX axes (Speed, Safety/Clarity, Density) |
| 1.0.0 | 2026-03-12 | Ngan | Initial structure with partial content from roadmap, use cases, and Notion brief |
