# Scope for Exploration v3 — JTBD Extended

> This file preserves the **original structure and content** of SCOPE-FOR-EXPLORATION v3.
> The **only change** is the addition of **one new row: JTBD** in every User Story table, placed **at the top**.

---

## 1.1 Epic: Onboarding

### US 1.1.1: Prominent Appointment Booking on Home Screen

| Field | Details |
|---|---|
| **JTBD** | When I open the app for the first time, I want to immediately understand how to book an appointment, so I can start my healthcare task without searching or hesitation. |
| User Story | **As a new patient**, I want to see the main "Book Appointment" function prominently on the home screen, so I can quickly start booking. |
| Acceptance Criteria | 1. The "Book Appointment" button must be visible within 3 seconds after app start<br/>2. The button takes up at least 20% of the visible screen area<br/>3. Legal mandatory information (Imprint, Privacy Policy, Terms of Service) is accessible via a menu<br/>4. The home screen loads within 5 seconds even on slow connections |
| Notes | Performance expectations, native feel, no random logouts |

---

### US 1.1.2: OAuth Registration (Google/Apple)

| Field | Details |
|---|---|
| **JTBD** | When creating an account, I want to reuse an existing trusted identity, so I can get access quickly without friction or extra credentials. |
| User Story | **As a new patient**, I want to register with my Google or Apple account, to save time and avoid managing additional passwords. |
| Acceptance Criteria | OAuth sign-in, fast processing, fallback to manual registration |
| Notes | Forced re-login and slowness frustrations |

---

### US 1.1.3: Email/Password Registration

| Field | Details |
|---|---|
| **JTBD** | When I don’t use social login, I want a clear and secure way to create an account, so I can access healthcare services with confidence. |
| User Story | **As a new patient without Google/Apple account**, I want to register with email and secure password, to use the app. |
| Acceptance Criteria | Password rules, validation, email verification |
| Notes | Submission failures and re-login pain |

---

### US 1.1.4: SMS Phone Number Verification

| Field | Details |
|---|---|
| **JTBD** | When securing my account, I want to confirm my phone number easily, so I feel protected without being confused or blocked. |
| User Story | **As a new patient**, I want to verify my mobile phone number via SMS, to use secure two-factor authentication. |
| Acceptance Criteria | Code delivery, resend, rate limits |
| Notes | Anxiety about errors; need reassurance |

---

### US 1.1.5: Biometric Authentication

| Field | Details |
|---|---|
| **JTBD** | When accessing sensitive health information, I want a fast but secure way to unlock the app, so my data stays private without slowing me down. |
| User Story | **As a security-conscious user**, I want to enable Face-ID/Touch-ID, to protect my health data from unauthorized access. |
| Acceptance Criteria | Optional biometric, fallback to PIN/password |
| Notes | Privacy sensitivity |

---

## 1.2 Epic: Appointment Booking and Management

### US 1.2.1: Book Appointment by Specialty

| Field | Details |
|---|---|
| **JTBD** | When I don’t know a specific doctor, I want to search by medical need, so I can find appropriate care without insider knowledge. |
| User Story | **As a new patient**, I want to book an appointment based on medical specialty. |
| Acceptance Criteria | Specialty list, retry on error |
| Notes | Long wait times; telemedicine alternative |

---

### US 1.2.2: Save Favorite Doctors

| Field | Details |
|---|---|
| **JTBD** | When I repeatedly see the same doctors, I want quick access to them, so repeat bookings require minimal effort. |
| User Story | **As a returning patient**, I want to save my preferred doctors, to save time on the next booking. |
| Acceptance Criteria | Persist favorites, sorting, removal |
| Notes | Fragmentation pain |

---

### US 1.2.3: Select Appointment Type

| Field | Details |
|---|---|
| **JTBD** | When booking, I want to clearly state why I’m visiting, so the practice can prepare and I get appropriate care. |
| User Story | **As a patient**, I want to select an appointment type (Acute, Prevention, Follow-Up), to communicate the reason for my visit. |
| Acceptance Criteria | Type-specific inputs |
| Notes | Wait-time transparency |

---

### US 1.2.4: Book Appointments for Dependents

| Field | Details |
|---|---|
| **JTBD** | When managing family healthcare, I want to handle appointments for others from my account, so I don’t juggle multiple systems. |
| User Story | **As a patient with children**, I want to book appointments on behalf of my children. |
| Acceptance Criteria | Dependent profiles, selection |
| Notes | Family coordination |

---

### US 1.2.5: Real-Time Appointment Status

| Field | Details |
|---|---|
| **JTBD** | When I request an appointment, I want to know what’s happening without guessing, so I can plan my time confidently. |
| User Story | **As a patient**, I want to see the status of my appointment request in real-time. |
| Acceptance Criteria | Status states, notifications |
| Notes | Waiting anxiety |

---

### US 1.2.6: Export Appointment to Calendar

| Field | Details |
|---|---|
| **JTBD** | When I have a confirmed appointment, I want it reflected in my personal calendar, so my existing reminders keep me on track. |
| User Story | **As a patient**, I want to export a confirmed appointment to my calendar, so I don't forget it. |
| Acceptance Criteria | .ics export, confirmed-only |
| Notes | Fragmentation |

---

### US 1.2.7: Appointment Reminders

| Field | Details |
|---|---|
| **JTBD** | When an appointment is approaching, I want timely nudges, so I can confirm, cancel, or prepare without stress. |
| User Story | **As a patient**, I want to receive reminders before my appointment. |
| Acceptance Criteria | Timed notifications, actions |
| Notes | Notification failures |

---

### US 1.2.8: Appointment List Overview

| Field | Details |
|---|---|
| **JTBD** | When managing my care history, I want a clear overview, so I always know what’s upcoming and what’s already done. |
| User Story | **As a patient**, I want to see all upcoming and past appointments in a clear list. |
| Acceptance Criteria | Tabs, sorting, filters |
| Notes | Performance issues |

---

### US 1.2.9: Modify Confirmed Appointment

| Field | Details |
|---|---|
| **JTBD** | When my schedule changes, I want to adjust appointments safely, so I don’t miss care or cause issues for the practice. |
| User Story | **As a patient**, I want to modify a confirmed appointment. |
| Acceptance Criteria | Time limits, rebooking |
| Notes | No-show disputes |

---

### US 1.2.10: Cancel Appointment

| Field | Details |
|---|---|
| **JTBD** | When I can’t attend, I want to cancel clearly and early, so others can take the slot and I avoid penalties. |
| User Story | **As a patient**, I want to cancel an appointment. |
| Acceptance Criteria | Cutoff rules, confirmation |
| Notes | Blame avoidance |

---

## 1.3 Epic: Post-Appointment Follow-Up

### US 1.3.1: Automatic Feedback Request

| Field | Details |
|---|---|
| **JTBD** | When a visit is completed, I want an easy way to share my experience, so service quality can improve without effort from me. |
| User Story | **As a system operator**, I want to automatically collect feedback. |
| Acceptance Criteria | Timed request, rating form |
| Notes | Elderly sensitivity |

---

## 1.4 Epic: Customer Account Management

### US 1.4.1: Complete Account Deletion

| Field | Details |
|---|---|
| **JTBD** | When I no longer trust or need the app, I want to fully remove my data, so my privacy rights are respected. |
| User Story | **As a privacy-conscious patient**, I want to completely delete my account. |
| Acceptance Criteria | Warnings, confirmation |
| Notes | Privacy fears |

---

### US 1.4.2: Change Password

| Field | Details |
|---|---|
| **JTBD** | When I feel my account security is at risk, I want to update my credentials easily, so I regain peace of mind. |
| User Story | **As a patient**, I want to change my password. |
| Acceptance Criteria | Validation, confirmation |
| Notes | Forced re-login |

---

## 1.5 Epic: Appointment Changes by Practice

### US 1.5.1: Practice-Initiated Appointment Changes

| Field | Details |
|---|---|
| **JTBD** | When a practice changes an appointment, I want to be informed immediately, so I can react and adjust my plans. |
| User Story | **As a practice system**, I want to transmit appointment changes to the app. |
| Acceptance Criteria | Fast propagation, notification |
| Notes | Day-of cancellations |

---

## 1.6 Epic: Content Management

### US 1.6.1: Edit Home Screen Content Without Technical Knowledge

| Field | Details |
|---|---|
| **JTBD** | When information changes, I want to update user-facing content quickly, so the app stays accurate and trustworthy. |
| User Story | **As a content creator**, I want to edit home screen content without technical knowledge. |
| Acceptance Criteria | WYSIWYG, preview |
| Notes | Language consistency |

---

## 1.8 Epic: Additional User Stories

### US 1.8.3: Granular Data Usage Consent

| Field | Details |
|---|---|
| **JTBD** | When sharing sensitive data, I want clear control over its usage, so I feel safe and respected. |
| User Story | **As a patient**, I want to granularly control how my data is used. |
| Acceptance Criteria | Opt-ins, revocation |
| Notes | Privacy anxiety |

