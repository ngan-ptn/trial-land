# PVS-Core Implementation Roadmap

| Version | Date | Classification |
|---------|------|---------------|
| 4.0 | 11 March 2026 | Internal |

---

## Table of Contents

- [Scope](#scope)
- [Overview Diagram](#overview-diagram)
- [Phase 1: Patient Data Management](#phase-1-patient-data-management)
- [Phase 2: Diagnosis, Coding & Service Documentation](#phase-2-diagnosis-coding--service-documentation)
- [Phase 3: Billing & Submission (GKV + HZV/FAV)](#phase-3-billing--submission-gkv--hzvfav)
- [Phase 4: Prescription Management (E-Rezept)](#phase-4-prescription-management-e-rezept)
- [Phase 5: Forms, eAU & ePA](#phase-5-forms-eau--epa)
- [Phase 6: eDMP / eDocumentation](#phase-6-edmp--edocumentation)
- [Phase 7: Foundation & Practice Infrastructure](#phase-7-foundation--practice-infrastructure)

---

## Scope

This roadmap covers the full PVS-Core build plan derived from four requirement sources. HZV/FAV selective contract requirements (SV Components) are integrated into each phase rather than isolated as a separate module.

| Source | Scope | Reqs |
|--------|-------|------|
| **KVDT Anforderungskatalog V6.04** | Practice management, patient data, Schein, billing, service codes | ~175 |
| **ICD-10-GM Anforderungskatalog V3.10** | Diagnosis entry, SDKRW coding rules | 53 |
| **SV Components (HZV/FAV)** | Selective contract — merged into Phases 1–7 | 278 |
| **Crucial Workflows (selected)** | eEB, Prescription Mgmt, eAU/Forms/ePA, eDMP/eDocumentation | ~522 |

**Total estimated requirements: ~1,028**

**SV Components Distribution:**

| SV Functional Area | Target Phase |
|--------------------|-------------|
| Teilnahmeerklärung lifecycle + Participation Mgmt + Import/Sync | Phase 1 |
| Documentation — diagnosis rules (ICD-10, Dauerdiagnosen, multimorbidity) | Phase 2A |
| Documentation — service/referral rules (GOP filtering, OPS, referrals) | Phase 2B |
| Billing (preparation, validation, submission, corrections) | Phase 3 |
| Stammdaten & Infrastruktur (master data, contract config, VP-ID) | Phase 7 |

---

## Overview Diagram

[![PVS-Core Roadmap Overview](https://diashort.apps.quickable.co/e/e2e280cf/no-phase-numbers)](https://diashort.apps.quickable.co/d/e2e280cf/no-phase-numbers)

---

## Phase 1: Patient Data Management

**Source:** KVDT §2–§4 (~72 reqs) + SV Encounter (TE + Participation + Import)

Complete patient registration — card reading, manual entry, cost carrier resolution — billing case (Schein) lifecycle, and HZV/FAV enrollment and participation workflows.

### 1.1 eGK Card Read-In
Patient data capture from eGK, field mapping per KBV spec, cost carrier assignment from VKNR/IK, VSDM verification, card read date management. (~15 reqs)

### 1.2 Cost Carrier Resolution
Eight resolution scenarios (FALL 1–10): valid IK assignment, billing capability check, Kassenfusion handling, dissolved carriers, expired IK override, unknown IK temp records. (~8 reqs)

### 1.3 Patient Matching & Insurance Changes
Duplicate prevention on card read, insurance change detection, Besondere Personengruppe assignment, AsylbLG hints. (~4 reqs)

### 1.4 Manual Entry / Ersatzverfahren
Full manual entry per Tabelle 5, cost carrier search by IK/name/VKNR, eEB via KIM (receive FHIR Coverage resources, QR code generation, quarterly duplicate detection), SKT special handling (Bundeswehr), PLZ validation, gender capture. (~22 reqs)

### 1.5 Schein Management
Record type selection (0101–0104), TSS/Terminservice handling with surcharges, quarter transition rules, insurance change splitting, referral Schein (Muster 6/10/39), pseudo-Behandlungsfälle. (~29 reqs)

### 1.6 European Health Insurance
Patient declaration for European health insurance card holders. (1 req)

### 1.7 HZV/FAV Teilnahmeerklärung Lifecycle
TE form printing (HZV DIN A4, FAV), signature capture (HZV: 2 signatures + TE-Code, FAV: 1 + TE-Code), status lifecycle (Erzeugt → Gedruckt → Fehlerhaft → Erfolgreich), transmission prerequisites, daily unsent-TE notifications, online/offline enrollment per BSNR. (~18 SV reqs)

### 1.8 HZV/FAV Participation Management
Contract participation requests, multi-location support, status management (activate/end/reverse/cancel), insurance change checks, module contract prerequisites, FAV status checks, external links (specialist search, therapy facilities). (~14 SV reqs)

### 1.9 HZV/FAV Import & Data Synchronization
Patient master data conflict resolution, ICode management, pre-import validation, PTV import, standard import rules with exception handling, import protocol. (~7 SV reqs)

---

## Phase 2: Diagnosis, Coding & Service Documentation

**Source:** ICD-10-GM §1–§2 (53 reqs) + KVDT §6 (~37 reqs) + SV Documentation

ICD-10-GM coding with the full SDICD/SDVA/SDKRW master data stack, HZV/FAV-specific diagnosis warnings, and complete service code documentation including GOP entry, OPS coding, psychotherapy, and HZV/FAV service filtering.

### Part A — Diagnosis & Clinical Coding

#### 2A.1 Acute Diagnosis Entry
ICD-10-GM coded diagnoses with mandatory Diagnosensicherheit (V/G/A/Z — no default), Seitenlokalisation, Erläuterungstext, SDICD Klartext display. No automatic diagnosis addition. (~9 reqs)

#### 2A.2 Dauerdiagnosen & Anamnestische Diagnosen
Separate categories from acute, explicit user confirmation for carry-over adoption, Diagnosensicherheit review on adoption, 4th/5th digit completion prompts. (~11 reqs)

#### 2A.3 SDICD Master Data Validation
Mandatory KBV-provided SDICD (immutable, current at quarter start). Validates: code existence, billability, Kreuz-Stern pairing, gender/age plausibility, rare-disease warnings, IfSG alerts, free-text search. (~15 reqs)

#### 2A.4 SDVA Coding Instructions
Mandatory KBV-provided SDVA with context-sensitive display per ICD code, full browse mode, annual change highlighting. (6 reqs)

#### 2A.5 SDKRW Coding Rule Engine
Conditional mandatory rule engine: per-case and cross-quarter execution, three-block rule processing (condition → check → error handling), correction types (DELETE/REPLACE/ADD) with user confirmation, violation overview. (16 reqs)

#### 2A.6 HZV/FAV Diagnosis Rules
ICD-10-GM documentation for HZV/FAV, permanent diagnosis carry-forward, terminal code selection, acute-as-permanent warnings, repeated suspected diagnosis warnings, disease pattern check / multimorbidity surcharge. (~7 SV reqs)

### Part B — Service Code Documentation

#### 2B.1 Core Service Entry
Treatment day / GOP entry, justification texts, day separation rules, service marking, fee rule application. (~6 reqs)

#### 2B.2 Billing Justification
Visit billing justification (Besuche), key table values, validation rules, free-text fallback. (~4 reqs)

#### 2B.3 Genetic Testing Documentation
OMIM/HGNC gene symbols, indication documentation, informed consent tracking, material/method documentation, panel/exome scope. (~7 reqs)

#### 2B.4 OPS Procedure Codes
SDOPS master data, bilateral side coding (R/L/B), dual function as billing justification + §295 documentation. (~5 reqs)

#### 2B.5 Psychotherapy Documentation
Psychotherapy service documentation, combination treatment by two therapists, group therapy billing, Tagesprofil, PTV 3/10 forms, termination notices via KIM. (~16 reqs)

#### 2B.6 EBM Master Data Functions
Patient receipt texts from EBM, age-based GOP selection, advanced lookup functions. (~3 reqs)

#### 2B.7 HZV/FAV Service Documentation
EBM-on-KV-billing warning, HZV/FAV-specific GOP entry with BSNR/LANR/VP-ID, service filtering by KV region and insurance IK, substitute doctor rules, blank billing codes, nursing home flat-rate, FAV participation online check. (~18 SV reqs)

#### 2B.8 HZV/FAV Referral & OPS Rules
Referral form auto-text, FAV referral cover letter, OPS documentation for FAV. (~3 SV reqs)

---

## Phase 3: Billing & Submission (GKV + HZV/FAV)

**Source:** KVDT §5 (~25 reqs) + SV Billing

KVDT billing file generation, XPM validation, XKM encryption, 1-Click submission via KIM, patient receipts, lab proficiency testing, ASV billing, and the complete HZV/FAV billing pipeline.

### 3.1 KV Billing File Generation & Transmission
Encrypted billing file, 1-Click-Abrechnung via KV-Connect and KIM, billing statistics, file packaging, transmission confirmation, billing correction workflows. (~6 reqs)

### 3.2 Patient Receipts
Orientation values from EBM, receipt generation per Tabelle 11 layout, optional Euro amounts and diagnosis texts. (~5 reqs)

### 3.3 Laboratory Proficiency Testing
Certificate management, participation obligation checks, pnSD diagnostics query, practice-specific analyte selection, RVSA dataset transmission. (~10 reqs)

### 3.4 ASV Billing (§116b SGB V)
ASV implementation, team number management, GOP marking with FK 5100, Begründungstexte. (~4 reqs)

### 3.5 HZV/FAV Billing Preparation
Fee schedule management, billing case management, billing preparation, preventive case auto-add code 80092.2, substitute doctor billing. (~5 SV reqs)

### 3.6 HZV/FAV Validation & Prerequisites
Diagnosis prerequisites, birth date validation, HPM billing validation, referral/accident/OPS prerequisites, material cost checks, error and warning protocols. (~10 SV reqs)

### 3.7 HZV/FAV Submission & Result
Online/offline submission, success confirmation and transmission protocol, duplicate billing prevention, late submission warning. (~4 SV reqs)

### 3.8 HZV/FAV Special Cases & Corrections
KV billing warning for HZV patients, misdocumented EBM services, diagnosis correction (code 999999), post-submission modification, pre-enrollment service UHU35. (~5 SV reqs)

---

## Phase 4: Prescription Management (E-Rezept)

**Source:** Crucial Workflows — Workflow 3 (~407 reqs)

Full electronic prescription workflow — drug search, FHIR bundle generation, QES signing, E-Rezept Fachdienst submission — plus Heilmittel, Hilfsmittel, eVDGA, and BMP.

### 4.1 E-Rezept Core (~201 reqs)
Prescription builder (4 medication types: PZN/Ingredient/Compounding/FreeText), FHIR resource generator (ERP bundles v1.1.0, v1.3.3), patient copy with DataMatrix barcode, MVO handler, comfort signature manager (up to 250/day), prescription queue with batch signing.

**Integrations:** gematik E-Rezept Fachdienst (FHIR R4), IDP (OAuth 2.0) → VAU → eHBA QES

### 4.2 Drug Database & Safety (~62 reqs)
Drug search engine (PZN, ingredient, indication), dosage calculator (weight/age-based), economic prescribing engine (aut-idem, biosimilar, generics, rebate contracts), drug interaction alerts, Red Hand Letter warnings.

**Integration:** MMI Drug Database (daily updates), Regional ARV Data

### 4.3 Heilmittel — Therapeutic Remedies (~35 reqs)
Therapeutic remedy prescriptions, quantity limit tracking, LHM/BVB handling.

### 4.4 Hilfsmittel — Medical Aids
Muster 8, 8A, 15, 16 prescriptions; GKV-Hilfsmittelverzeichnis integration; supplier selection.

### 4.5 eVDGA — Digital Health Apps (~57 reqs)
DiGA prescriptions, eVDGA FHIR bundle generation. **Integration:** BfArM DiGA Directory (API)

### 4.6 BMP — Medication Plan (~52 reqs)
Create/edit medication plan, rearrange items, multi-version support, 2D barcode reading. **Integration:** BMP Generator (API), BMP Scanner (USB)

---

## Phase 5: Forms, eAU & ePA

**Source:** Crucial Workflows — Workflow 4 (selected; ~82 reqs)

Electronic sick leave certificates, form printing with PDF417 barcodes, electronic doctor letters via KIM, and ePA document operations.

### 5.1 BFB Form Printing (~24 reqs)
Form layout rendering, PDF417 barcode generation, field positioning.

### 5.2 eAU — Electronic Sick Leave (~29 reqs)
Structured data capture (KBV_PR_EAU_Bundle v1.2.1), QES with eHBA, KIM transmission with S/MIME envelope and DSN tracking, barcode for patient/employer copies, cancellation workflow (120-day window), insurer feedback processing.

### 5.3 eArztbrief — Electronic Doctor Letter (~27 reqs)
HL7 CDA R2 assembly, PDF/A generation, KIM S/MIME envelopes, delivery status tracking, incoming letter matching to patients, auto-billing GOP 86900/86901.

### 5.4 ePA — Electronic Patient Record
PDF/A conversion (PDF/A-1b/3b), document upload (eArztbrief, eAU, eMP, NFD, DPE with MIO profiles), document retrieval, entitlement management, patient locator across Aktensystem providers.

**Integration:** Ere.health Gateway (REST API — handles VAU, IDP, ePA-Aktensystem)

---

## Phase 6: eDMP / eDocumentation

**Source:** Crucial Workflows — Workflow 2 (selected; ~109 reqs)

Structured data capture for 8 chronic disease management programs and electronic skin cancer screening documentation.

### 6.1 eDMP Form Engine (~98 reqs)
8 disease programs: Diabetes Type 1 & 2, Asthma, COPD, KHK, Heart Failure, Breast Cancer, Depression. Disease-specific field sets, completeness validation, XPM validation, KIM-based transmission to regional KV.

### 6.2 eDocumentation — eHKS (~11 reqs)
Electronic skin cancer screening documentation: data entry, validation rules, submission preparation.

### 6.3 Supporting Components
Scoring calculators (PHQ-9, DAS-28), audit trail service per §630f BGB.

### 6.4 Integration
KV submission via KIM (S/MIME), XPM pre-submission validation. Internal dependencies: ICD-10-GM diagnosis (Phase 2A), billing case/Schein (Phase 1), service codes/GOPs (Phase 2B).

---

## Phase 7: Foundation & Practice Infrastructure

**Source:** KVDT §1 (~41 reqs) + SV Stammdaten & Infrastruktur

System backbone — master data, user/access control, TI reporting, and HZV/FAV contract infrastructure — that every downstream module depends on.

### 7.1 System Integrity & Date Controls
Complete data entry, system date protection, forward-dating prevention, replacement values for mandatory fields, date validation. (~5 reqs)

### 7.2 User & Practice Administration
User/rights management with LANR + location assignment, practice location management (BSNR), billing file generation per BSNR, pseudo-LANR support, LANR/BSNR uniqueness. (~7 reqs)

### 7.3 TI Connector Reporting
Connector ProductTypeVersion reporting, TI application support attestation, certificate expiry display, connector product name transmission. (~4 reqs)

### 7.4 KBV Master Data Files
Quarterly deployment of SDKT (cost carriers), SDKV (regional), SDAV (physicians), PLZ, SDEBM (fee schedules). Immutability enforcement, regional priority rules, extensibility for user-added GOPs. (~18 reqs)

### 7.5 Validation & Crypto Modules
XPM validation and XKM crypto module deployment, ICD-10-GM application requirements, form printing catalog, AMV certification, fee schedule pre-population. (~7 reqs)

### 7.6 HZV/FAV Contract Infrastructure
KBV KT-Stammdatei, KVK-to-eGK mapping, KVDT compliance, contract management & configuration, VP-ID generation, contract document viewing/printing, participation return data, care management, forms management, user manual, change documentation, software module distribution. (~12 SV reqs)
