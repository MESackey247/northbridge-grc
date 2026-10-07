# Data Protection Impact Assessment (DPIA)

**System Name:** AI Patient Triage & Scheduling Subsystem  
**Data Controller:** Northbridge Health Ltd  
**Data Protection Officer (DPO):** dpo@northbridgehealth.co.uk  
**Regulatory Framework:** UK GDPR / Data Protection Act 2018 (ICO Oversight)  
**Assessment Date:** Q4 2026  

---

## 1. Executive Summary & Processing Scope

Northbridge Health Ltd provides a cloud-native SaaS platform designed to streamline patient scheduling and initial clinical triage for NHS trusts and private clinics across the UK. 

This DPIA evaluates the **AI-Assisted Patient Triage Module**, which processes patient-submitted symptoms and triage notes using natural language models to suggest appointment urgency levels.

---

## 2. Lawful Basis for Processing (UK GDPR Articles 6 & 9)

### Article 6 Basis (Standard Personal Data)
* **Article 6(1)(b) - Contract:** Necessary for the performance of a contract between Northbridge Health and healthcare providers to deliver appointment scheduling.
* **Article 6(1)(f) - Legitimate Interests:** Necessary to maintain platform operational security and system reliability.

### Article 9 Condition (Special Category Health Data)
* **Article 9(2)(h) - Health & Social Care:** Processing is necessary for the management of health or social care systems and services provided by qualified healthcare practitioners.

---

## 3. Data Inventory & Data Flow Map

| Data Category | Specific Data Elements | Sensitivity | Storage Location | Retention Period |
| :--- | :--- | :--- | :--- | :--- |
| **Identity Data** | Patient Name, DOB, NHS Number, Email, Phone | High (PII) | AWS RDS (UK Region, Encrypted) | Duration of care contract + 8 years |
| **Health Data** | Reported symptoms, triage severity flags, medical notes | Critical (Special Category) | AWS RDS (UK Region, Encrypted) | Duration of care contract + 8 years |
| **Technical Telemetry** | IP Address, login timestamps, device user-agent | Low / Operational | AWS CloudWatch (UK Region) | 90 days |

### Data Flow Overview
1. **Ingestion:** Patient inputs symptom data via TLS 1.3 encrypted HTTPS connection to AWS VPC.
2. **Processing:** API feeds anonymized prompt inputs (stripped of direct identifiers) to internal machine learning triage logic.
3. **Storage:** Encrypted at rest using AES-256 keys managed via AWS KMS in the London (`eu-west-2`) region.
4. **Access:** Restricted to authorized clinic staff via Role-Based Access Control (RBAC) and Multi-Factor Authentication (MFA).

---

## 4. Key Privacy Risks & Mitigation Controls

| Risk ID | Risk Description | Severity (Pre-Mitigation) | Mitigation Controls Implemented | Severity (Post-Mitigation) |
| :--- | :--- | :--- | :--- | :--- |
| **PR-01** | Unauthorized access to special category patient health records | High | Enforced MFA, RBAC, AWS VPC isolation, and quarterly access reviews (`01-governance/access-control-policy.md`). | **Low** |
| **PR-02** | Exposure of PII/Health data to external LLM or AI model training | High | Strict zero-retention API configurations; AI models are trained solely on synthetic/anonymized data (`01-governance/ai-acceptable-use-policy.md`). | **Low** |
| **PR-03** | Patient data stored or transferred outside the UK/EEA | High | Regional binding enforced: All primary DBs and backups locked to AWS London (`eu-west-2`) (`01-governance/scope.md`). | **Low** |
| **PR-04** | Inability to comply with UK GDPR Subject Access Requests (SAR) or Erasure | Medium | Automated database query scripts for data export and compliance-approved soft/hard deletion pipelines. | **Low** |

---

## 5. Individual Data Subject Rights (UK GDPR)

Northbridge Health supports healthcare clients in fulfilling data subject rights:
* **Right of Access (SAR):** Automated tools generate structured JSON/PDF exports of patient history within 5 business days.
* **Right to Erasure (Right to be Forgotten):** API endpoints support cryptographically verified erasure requests while maintaining regulatory audit logs.
* **Right to Object to Automated Decision-Making (Art. 22):** The triage algorithm provides *decision-support recommendations only*. Final clinical decisions always require human review by qualified healthcare personnel.

---

## 6. DPO Approval & Sign-Off

* **DPO Recommendation:** Approved. The processing implements appropriate technical and organizational measures (TOMs) to safeguard patient privacy.
* **ICO Consultation Required:** No (Residual risk is low post-mitigation).
* **Next Review Date:** Annual or prior to any major AI model architecture change.