# Screen List - Calo Tracker

**Last Updated:** Jan 6, 2026
**Derived from:** [User Flows](../userflows/user-flows-complete.md)
**Source:** [OOUX Dot Map](./OOUX-dot-map.md)

---

## Derivation Methodology

```
OOUX DOT MAP                    USER FLOWS                      SCREEN LIST
─────────────────────          ─────────────────────           ─────────────────────
7 Objects                  →   10 Jobs-to-be-done         →   17 Screens + 1 Toast
~30 Actions                    ~50 Flow moments
                               Decision points = screens
                               Input moments = screens
                               View moments = screens
                               Feedback = overlays
```

---

## Screen Identification from Flow Moments

| Flow Moment | Type | Screen Needed? | Rationale |
|-------------|------|----------------|-----------|
| Entry point | Decision | Yes → **Entry Hub** | User chooses HOW to log |
| Search input + results | Input + View | Yes → **Search** | Active input + scrollable results |
| Category browse | View | Merge with Search | Same results pattern, filter |
| Portion selection | Input | Yes → **Portion Picker** | Focused decision, shared across flows |
| Feedback confirmation | Feedback | No → **Toast** | Non-blocking, undo support |
| Favorites grid | View | Yes → **Favorites** | Visual recognition pattern |
| Manual entry form | Input | Yes → **Manual Entry** | Multiple fields, form validation |
| Camera viewfinder | Capture | Yes → **Scan Camera** | Full-screen camera |
| Scan confirmation | Decision | Yes → **Scan Results** | Confirm/reject match |
| Template list | View | Yes → **Templates** | List with preview |
| Template items edit | Input | Yes → **Template Logging** | Checkbox per item |
| Template editor | Input | Yes → **Template Editor** | Create/edit form |
| Dashboard summary | View | Yes → **Home** | Primary landing |
| Log history | View | Merge with Home | Part of daily view |
| Goal settings | Input | Yes → **Goal Settings** | Form with sliders |
| Profile settings | View | Yes → **Profile** | Settings hub |
| Login form | Input | Yes → **Login** | Auth form |
| Registration form | Input | Yes → **Registration** | Auth form |
| Onboarding goals | Input | Yes → **Onboarding** | First-time flow |
| Favorites management | Input | Modal or merge | Edit mode on Favorites |

---

## Consolidated Screen List

| ID | Screen | Derived from Flow(s) | Primary Purpose |
|----|--------|---------------------|-----------------|
| **AUTH** |
| S01 | **Login** | J10 | Credential input |
| S02 | **Registration** | J10 | Account creation |
| S03 | **Onboarding** | J10 | Initial goal setup |
| S04 | **Password Reset** | J10 | Recovery flow |
| **HUB** |
| S10 | **Home** | J6, all flows end here | Dashboard + log history |
| S11 | **Action Sheet** | J1-J5 entry points | Entry method selection (modal) |
| **FOOD ENTRY** |
| S20 | **Search** | J1 | Query input + results + category filter |
| S21 | **Portion Picker** | J1, J2, J3, J4 | Portion selection (shared) |
| S22 | **Manual Entry** | J3 | Custom food form |
| S23 | **Scan Camera** | J4 | Camera viewfinder |
| S24 | **Scan Results** | J4 | Match confirmation |
| **FAVORITES** |
| S30 | **Favorites** | J2, J7 | Grid view + manage mode |
| **TEMPLATES** |
| S40 | **Templates List** | J5, J8 | List + preview |
| S41 | **Template Logging** | J5 | Item selection before log |
| S42 | **Template Editor** | J8 | Create/edit template |
| **PROFILE** |
| S50 | **Profile Settings** | J9 | Settings hub |
| S51 | **Goal Settings** | J9 | Calorie + macro targets |
| S52 | **Profile Switcher** | Multi-user | Context switch (modal) |
| **FEEDBACK** |
| T01 | **Toast** | All logging flows | Confirmation + undo (overlay) |

---

## Screen-to-Job Mapping

| Screen | Jobs Supported |
|--------|----------------|
| S01 Login | J10 |
| S02 Registration | J10 |
| S03 Onboarding | J10 |
| S04 Password Reset | J10 |
| S10 Home | J1, J2, J3, J4, J5, J6 |
| S11 Action Sheet | J1, J2, J3, J4, J5 |
| S20 Search | J1 |
| S21 Portion Picker | J1, J2, J3, J4 |
| S22 Manual Entry | J3 |
| S23 Scan Camera | J4 |
| S24 Scan Results | J4 |
| S30 Favorites | J2, J7 |
| S40 Templates List | J5, J8 |
| S41 Template Logging | J5 |
| S42 Template Editor | J8 |
| S50 Profile Settings | J9 |
| S51 Goal Settings | J9 |
| S52 Profile Switcher | Multi-user |
| T01 Toast | J1, J2, J3, J4, J5 |

---

## User Flow with Screens

```mermaid
flowchart TB
    %% ==================== ENTRY ====================
    START([App Launch])

    %% ==================== AUTH ====================
    subgraph AUTH ["🔐 Auth"]
        S01["S01<br/>Login"]
        S02["S02<br/>Registration"]
        S03["S03<br/>Onboarding"]
        S04["S04<br/>Password Reset"]
    end

    %% ==================== HUB ====================
    subgraph HUB ["🏠 Hub"]
        S10["S10<br/>Home"]
        S11{{"S11<br/>Action Sheet"}}
    end

    %% ==================== ENTRY METHODS ====================
    subgraph ENTRY ["🍜 Food Entry"]
        S20["S20<br/>Search"]
        S21["S21<br/>Portion Picker"]
        S22["S22<br/>Manual Entry"]
        S23["S23<br/>Scan Camera"]
        S24["S24<br/>Scan Results"]
    end

    %% ==================== FAVORITES ====================
    subgraph FAVS ["⭐ Favorites"]
        S30["S30<br/>Favorites"]
    end

    %% ==================== TEMPLATES ====================
    subgraph TEMPS ["🍽️ Templates"]
        S40["S40<br/>Templates List"]
        S41["S41<br/>Template Logging"]
        S42["S42<br/>Template Editor"]
    end

    %% ==================== PROFILE ====================
    subgraph PROFILE ["👤 Profile"]
        S50["S50<br/>Profile"]
        S51["S51<br/>Goals"]
        S52{{"S52<br/>Profile Switcher"}}
    end

    %% ==================== FEEDBACK ====================
    T01(["T01 Toast"])

    %% ==================== AUTH FLOWS ====================
    START -->|"logged out"| S01
    START -->|"logged in"| S10
    S01 -->|"new user"| S02
    S01 -->|"forgot"| S04
    S01 -->|"success"| S10
    S02 -->|"registered"| S03
    S03 -->|"complete"| S10
    S04 -->|"reset"| S01

    %% ==================== HUB FLOWS ====================
    S10 -->|"FAB"| S11
    S10 -->|"settings"| S50
    S10 -->|"avatar"| S52
    S10 -->|"search bar"| S20
    S10 -->|"tap log"| S21

    %% ==================== ACTION SHEET ====================
    S11 -->|"Search"| S20
    S11 -->|"Manual"| S22
    S11 -->|"Scan"| S23
    S11 -->|"Favorites"| S30
    S11 -->|"Templates"| S40
    S11 -->|"cancel"| S10

    %% ==================== SEARCH FLOW (J1) ====================
    S20 -->|"select food"| S21
    S20 -->|"back"| S10

    %% ==================== PORTION PICKER (shared) ====================
    S21 -->|"log"| T01
    S21 -->|"+ favorite"| S21
    S21 -->|"cancel"| S10

    %% ==================== MANUAL FLOW (J3) ====================
    S22 -->|"save"| S21
    S22 -->|"cancel"| S11

    %% ==================== SCAN FLOW (J4) ====================
    S23 -->|"detected"| S24
    S23 -->|"cancel"| S11
    S24 -->|"confirm"| S21
    S24 -->|"retry"| S23
    S24 -->|"manual"| S22

    %% ==================== FAVORITES FLOW (J2, J7) ====================
    S30 -->|"select"| S21
    S30 -->|"back"| S11

    %% ==================== TEMPLATES FLOW (J5, J8) ====================
    S40 -->|"select"| S41
    S40 -->|"create"| S42
    S40 -->|"edit"| S42
    S40 -->|"back"| S11
    S41 -->|"log all"| T01
    S41 -->|"cancel"| S40
    S42 -->|"save"| S40
    S42 -->|"cancel"| S40

    %% ==================== PROFILE FLOW (J9) ====================
    S50 -->|"goals"| S51
    S50 -->|"logout"| S01
    S50 -->|"back"| S10
    S51 -->|"save"| S50
    S52 -->|"switch"| S10
    S52 -->|"back"| S10

    %% ==================== TOAST FEEDBACK ====================
    T01 -->|"undo"| S10
    T01 -->|"edit"| S21
    T01 -.->|"auto-dismiss"| S10

    %% ==================== STYLING ====================
    style START fill:#000,stroke:#000,color:#fff

    style AUTH fill:#E3F2FD,stroke:#1565C0
    style S01 fill:#90CAF9,stroke:#1565C0
    style S02 fill:#90CAF9,stroke:#1565C0
    style S03 fill:#90CAF9,stroke:#1565C0
    style S04 fill:#90CAF9,stroke:#1565C0

    style HUB fill:#FFF3E0,stroke:#E65100
    style S10 fill:#FFB74D,stroke:#E65100,stroke-width:3px
    style S11 fill:#FFE0B2,stroke:#E65100

    style ENTRY fill:#F3E5F5,stroke:#7B1FA2
    style S20 fill:#CE93D8,stroke:#7B1FA2
    style S21 fill:#AB47BC,stroke:#7B1FA2,color:#fff,stroke-width:3px
    style S22 fill:#CE93D8,stroke:#7B1FA2
    style S23 fill:#CE93D8,stroke:#7B1FA2
    style S24 fill:#CE93D8,stroke:#7B1FA2

    style FAVS fill:#E0F7FA,stroke:#00838F
    style S30 fill:#4DD0E1,stroke:#00838F

    style TEMPS fill:#FCE4EC,stroke:#C2185B
    style S40 fill:#F48FB1,stroke:#C2185B
    style S41 fill:#F48FB1,stroke:#C2185B
    style S42 fill:#F48FB1,stroke:#C2185B

    style PROFILE fill:#E8F5E9,stroke:#2E7D32
    style S50 fill:#81C784,stroke:#2E7D32
    style S51 fill:#81C784,stroke:#2E7D32
    style S52 fill:#A5D6A7,stroke:#2E7D32

    style T01 fill:#ECEFF1,stroke:#455A64
```

---

## Screen Frequency (Expected Usage)

| Frequency | Screens |
|-----------|---------|
| **Every session** | S10 (Home), S11 (Action Sheet), S21 (Portion Picker), T01 (Toast) |
| **Most sessions** | S20 (Search), S30 (Favorites Grid) |
| **Weekly** | S40 (Templates), S22 (Manual Entry) |
| **Monthly** | S50 (Profile), S51 (Goals) |
| **Once** | S01 (Login), S02 (Registration), S03 (Onboarding) |

---

## Primary Paths (Happy Paths)

| Flow | Path | Object Journey |
|------|------|----------------|
| **Quick Log (Search)** | Home → Action Sheet → Search → Portion Picker → Home + Toast | User → System Food → Food Log |
| **Quick Log (Favorites)** | Home → Action Sheet → Favorites → Portion Picker → Home + Toast | User → Favorite → Food Log |
| **Manual Entry** | Home → Action Sheet → Manual Entry → Portion Picker → Home + Toast | User → Custom Food → Food Log |
| **Scan Entry** | Home → Action Sheet → Scan → Results → Portion Picker → Home + Toast | User → System Food → Food Log |
| **Template Log** | Home → Action Sheet → Templates → Template Logging → Home + Toast | User → Meal Template → Food Log (multiple) |

---

## Key UX Patterns

| Pattern | Implementation | Supports <30s Goal |
|---------|----------------|-------------------|
| **Hub & Spoke** | All entry methods return to Home | Single mental model |
| **Progressive Disclosure** | Action Sheet → specific method | Reduces cognitive load |
| **Recognition > Recall** | Favorites Grid, Recent searches | Fewer taps |
| **Undo over Confirmation** | Toast with undo vs. confirm dialogs | Faster happy path |
| **Shared Portion Picker** | All paths funnel to S21 | Consistent interaction |

---

## Summary

| Metric | Count |
|--------|-------|
| Objects (OOUX) | 7 |
| Jobs (User Flows) | 10 |
| Screens | 17 |
| Modals/Overlays | 3 (Action Sheet, Profile Switcher, Toast) |
| Shared screens | 1 (Portion Picker serves 4 flows) |

---

**Related Documents:**
- [OOUX Dot Map](./OOUX-dot-map.md)
- [User Flows](../userflows/user-flows-complete.md)
- [IA Map](../ia-map/IA.md)
