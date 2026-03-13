# Kick-off Dedalus (Prototype)

### Project Overview - Dedalus PVS Prototype

- Dedalus: Leading German hospital systems provider (50%+ market share with Orbis software)
- Building PVS (Practice Management System) for MVZs (Medical Care Centers)
  - Similar certifications needed as the other PVS (KVDT, medication, DMP)
  - Wants seamless integration with existing hospital systems
- Demo target: April 21-23 DMEA event
  - Need clickable prototype showing use cases
  - Official announcement of upcoming PVS
  - Design can change post-demo

### Use Cases & Requirements

- Use Case 1: Patient Transfer from Hospital to MVZ
  - Hospital system creates patient profile with administrative data
  - Transfer patient info to PVS for continued treatment
  - Key requirement: Visual distinction between hospital data (read-only) vs PVS data (editable)
  - Patient timeline showing documentation sources with color coding
  - Documentation flows back to hospital system after examination
- Use Case 2: PVS Dashboard for Practice Managers
  - Analytics for efficiency improvements
  - No-show rates, specialty performance, device utilization
  - “Wow effect” showing 23% no-show rate on Tuesday mornings vs MVZ average
  - Single view with expandable details

### Technical Considerations & Constraints

- Desktop web app only (no mobile for now)
- NDA signed - cannot reference previous competitor work or screenshots
- Data model in FHIR format to be provided by Tamara
- Prototype developer may assist (pending Elena confirmation)
- Style guide available but design freedom encouraged
- Focus on efficiency narrative over exact implementation details

