---

**Prototype Use Cases**

**Target vision for DMEA (MVZ focus)**  
“The PVS that masters MVZ complexity – intelligent, connected, scalable.”

**Typical MVZ pain points:**

* multiple locations  
* multiple specialties  
* changing practitioners  
* centralized control vs. decentralized work

---

## **Usecase 1: Medical Use Case – Integrated Patient Pathway HIS ↔ MVZ (PVS)**

### **Initial Situation**

An adult patient presents independently at the emergency department of a hospital with acute, but not immediately life-threatening symptoms. The objective is seamless, cross-sector care with optimal use of inpatient and outpatient resources.

---

## **Demo Workflow**

### **1\. Patient admission at the hospital**

The patient presents at the emergency department.

Administrative steps:

* Patient is registered in the HIS / Triage software

* Capture of:

  * Demographic data

  * Insurance status

  * Known pre-existing conditions (if available)

  * Consents (data usage, data sharing)

Clinical initial presentation (example):

* Symptoms:

  * Increasing right lower abdominal pain for 3 days

  * Subfebrile temperature

  * Nausea, no vomiting

* Vital signs:

  * stable

  * no signs of shock

* Initial assessment (e.g. Manchester Triage System):

  * Urgency level: yellow

---

### **2\. Initial medical assessment (triage / screening)**

Performed by a physician or qualified nursing staff.

Assessment:

* No immediate need for inpatient treatment

* Further outpatient diagnostic clarification indicated

* Suspected diagnosis:

  * e.g. appendicitis vs. inflammatory bowel disease

➡️ Decision to refer the patient to a connected MVZ (e.g. surgery / radiology / internal medicine)

---

### **3\. Consent and transfer of the patient record**

* The patient provides digital or written consent for data transfer

* Relevant information is selectively extracted from the HIS:

  * Medical history

  * Vital signs

  * Laboratory results (if already available)

  * Initial assessment / suspected diagnosis

➡️ Transfer to the PVS of the MVZ

---

### **4\. Sharing the patient record with the MVZ**

* The patient record is transferred to the PVS in a structured and audit-proof manner

* Use of standardized interfaces (e.g. HL7 / FHIR)

---

### **5\. Opening the patient record in the PVS**

* The treating physician in the MVZ opens the transferred record directly within the local system

* No media disruption, no duplicate data entry

---

### **6\. Clear visual separation of data**

Within the PVS, a clear distinction is made between:

* External patient record (hospital data)

  * read-only

  * visually highlighted

* Own MVZ documentation

  * editable

  * legally independent

➡️ Increased patient safety and legal clarity

---

### **7\. Automated data exchange between HIS and PVS**

* Synchronization of relevant information:

  * Appointment status

  * Findings

  * Diagnostic requests

* Event-driven updates (e.g. CT completed)

---

### **8\. Referral for CT examination at the hospital**

Based on the clinical assessment in the MVZ:

* Indication:

  * Exclusion or confirmation of appendicitis

* Digital referral back to the hospital

* No paper-based referral required

---

### **9\. Intelligent appointment and resource planning**

The system automatically considers:

* Medical specialty

  * e.g. radiology

* Provider availability

* Device availability

  * CT capacity

* Location and utilization levels

  * avoidance of peak times

➡️ Automatic assignment of the optimal CT appointment

---

### **10\. Optional teaser: digital patient engagement**

* The patient receives in advance:

  * Digital consent and information forms

  * Medical history questionnaires

* Upload of documents directly to the appointment

➡️ Time savings on site, improved data quality

---

### **11\. CT examination and documentation in the HIS**

* CT examination is performed at the hospital

* Radiological reporting by a radiologist

* Structured report documented in the HIS

➡️ Automatic transfer of the CT report to the MVZ PVS

---

### **12\. Follow-up treatment at the MVZ**

* The MVZ receives the CT report in real time

* Medical evaluation:

  * e.g. uncomplicated appendicitis

* Treatment decision:

  * conservative outpatient treatment or

  * planned inpatient admission

---

### **13\. Documentation of findings and case closure**

* Complete documentation in the PVS:

  * Diagnosis

  * Treatment recommendation

  * Further procedure

* Optional:

  * Feedback to the hospital

  * Entry into a shared patient record

---

## **MVZ Value Proposition**

* Reduction of idle times

  * through intelligent appointment control

* Fewer incorrect bookings

  * due to automated resource logic

* Improved utilization of expensive resources

  * especially CT / MRI

* Higher quality of care

  * through complete, up-to-date patient data

* Improved patient satisfaction

  * fewer waiting times, fewer duplicate examinations

**Why it’s strong for DMEA**

* classic MVZ problem  
* immediately explainable visually (calendar \+ utilization)  
* clear differentiation from single-practice PVS

**Technically realistic**

* ✔ rule-based, no AI strictly required  
* ✔ data can be simulated  
* ✔ focus on orchestration, not billing

---

## **Use Case 2: Smart PVS Dashboard for MVZ Operational Control**

### **Purpose**

The Smart PVS Dashboard provides MVZ management and site leadership with a **real-time, consolidated overview of operational performance** across all locations, specialties, practitioners, and key resources.  
 Its goal is not documentation, but **early detection of inefficiencies and actionable steering insights**.

---

## **Actors**

* MVZ Management

* Site / Practice Managers

* (Optional) Medical Directors

---

## **Preconditions**

* Multiple MVZ locations are active in the system

* Appointment, treatment, and resource usage data is available (simulated or historical)

* Rule-based and/or lightweight model-based analytics are enabled

---

## **Demo Flow**

### **1\. Entry Point: Smart PVS Dashboard**

The user opens the **Smart PVS Dashboard** from the PVS start screen.

The dashboard aggregates operational KPIs across the entire MVZ network and visualizes them using a **traffic-light logic** (red / yellow / green) to allow immediate interpretation.

---

### **2\. High-Level Operational Overview**

The dashboard displays key insights at a glance:

* 🔴 **Location B: High no-show rate**  
   Location B is highlighted in red, indicating a critical deviation from the MVZ average.

* 🟡 **Specialty X: Above-average treatment duration**  
   Specialty X is marked in yellow, suggesting a potential efficiency issue but not an acute risk.

* 🟢 **Device Y: Underutilized**  
   Device Y is shown in green, signaling unused capacity that could be leveraged elsewhere.

Each indicator is clickable and leads to a more detailed breakdown.

---

### **3\. Drill-Down: Pattern Detection & Context**

When the user clicks on **Location B**, the dashboard reveals:

* No-show rates by:

  * weekday

  * time of day

  * specialty

* Comparison with other locations

The system highlights a detected pattern:

**“Tuesday mornings show a 23% higher no-show rate compared to the MVZ average.”**

This insight is generated using **rule-based thresholds or simple statistical models**, not text generation.

---

### **4\. Practitioner-Level Insights**

Switching to the **Practitioner View**, the dashboard shows anonymized or named performance metrics (depending on role permissions).

Example insight:

**“Practitioner A requires an average of 8 minutes longer per treatment than the specialty benchmark.”**

Additional context is displayed:

* case mix similarity

* room and device usage

* comparison to peers within the same specialty

The dashboard clearly indicates that this is **not a quality judgment**, but an operational observation.

---

### **5\. Resource & Capacity Optimization**

In the **Resource Utilization** section, the system shows:

* Device Y (e.g., imaging equipment) with low utilization

* Available appointment slots at Location C

The dashboard generates a concrete recommendation:

**“Available capacity at Location C could absorb appointment demand from Location B.”**

This recommendation is based on:

* geographic proximity

* compatible specialties

* device availability

* historical patient flow

---

### **6\. Actionability (Optional in Demo)**

For the prototype, the dashboard may visually suggest next steps, such as:

* adjusting appointment templates

* redistributing slots across locations

* introducing reminder workflows for high-risk time slots

No actions are executed automatically—**the dashboard supports decision-making, not automation**.

---

## **Business Value for MVZ**

* Early detection of operational bottlenecks

* Reduced no-show rates through targeted intervention

* Better utilization of expensive resources

* Data-driven steering instead of gut feeling

---

## **Why This Works Well as a Prototype**

* No medical text generation

* No NLP pipelines

* No regulatory gray areas

* Insights are transparent and explainable

* Data and logic can be fully simulated

---

## **Short trade fair pitch (30 seconds)**

“Dedalus is the PVS for MVZs.  
We manage appointments, resources, and patient information across locations—  
and for the first time give MVZ leadership real operational transparency.  
Less chaos, better utilization, better care.”

