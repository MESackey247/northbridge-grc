# SOC 2 Type II Trust Services Criteria (TSC) Mapping

**Organization:** Northbridge Health Ltd  
**System Name:** Northbridge Patient Scheduling & Triage Platform  
**Audit Standard:** AICPA SOC 2 Type II (Trust Services Criteria)  
**In-Scope Categories:** Security (Common Criteria), Availability, Confidentiality, Privacy  

---

## 1. Executive Summary & Audit Mapping Strategy

To streamline audit execution and reduce operational overhead, Northbridge Health maps its existing **ISO 27001:2022 ISMS** controls and **Internal Governance Policies** directly to the **AICPA SOC 2 Trust Services Criteria (TSC)**. 

This mapping serves as the primary evidence index for external auditors during annual SOC 2 Type II evaluation windows.

---

## 2. Common Criteria (CC-Series) Mapping

### CC1.0: Control Environment (Governance & Oversight)
| SOC 2 Criteria ID | Criteria Description | Northbridge Implementation | Primary Evidence Artifact |
| :--- | :--- | :--- | :--- |
| **CC1.1** | Commitment to integrity and ethical values | Mandatory Employee Code of Conduct and annual policy sign-offs | `01-governance/acceptable-use-policy.md` |
| **CC1.2** | Board/Executive security oversight | Board-level quarterly risk reviews and ISMS leadership approval | `01-governance/3lod.md` |
| **CC1.3** | Management establishes structures and reporting lines | Implementation of the Three Lines of Defence (3LoD) governance model | `01-governance/3lod.md` |

### CC2.0: Communication and Information
| SOC 2 Criteria ID | Criteria Description | Northbridge Implementation | Primary Evidence Artifact |
| :--- | :--- | :--- | :--- |
| **CC2.1** | Internal security policy communication | Security policies published centrally; mandatory onboarding training | `01-governance/acceptable-use-policy.md` |
| **CC2.2** | External communication regarding security & privacy | Public ISMS scope statement and patient privacy disclosures | `01-governance/scope.md` |

### CC6.0: Logical and Physical Access Controls
| SOC 2 Criteria ID | Criteria Description | Northbridge Implementation | Primary Evidence Artifact |
| :--- | :--- | :--- | :--- |
| **CC6.1** | Logical access security against unauthorized entry | Mandatory Multi-Factor Authentication (MFA) and SSO across all systems | `01-governance/access-control-policy.md` |
| **CC6.2** | User registration, modification, and revocation | Automated identity provisioning and immediate access revocation upon offboarding | `01-governance/access-control-policy.md` |
| **CC6.3** | Principle of least privilege enforcement | Role-Based Access Control (RBAC) and quarterly privilege access reviews | `01-governance/access-control-policy.md` |
| **CC6.6** | Data boundary and transmission protection | TLS 1.3 encryption in transit, AWS VPC isolation, and public S3 bucket blocking | `01-governance/scope.md`, `03-compliance/soa.csv` |
| **CC6.8** | Protection against malicious code | Managed Endpoint Detection & Response (EDR) enforced on corporate laptops | `01-governance/acceptable-use-policy.md` |

### CC7.0: System Operations & Incident Management
| SOC 2 Criteria ID | Criteria Description | Northbridge Implementation | Primary Evidence Artifact |
| :--- | :--- | :--- | :--- |
| **CC7.1** | Vulnerability scanning and infrastructure monitoring | Automated CI/CD dependency scanning, AWS GuardDuty, and CloudTrail auditing | `02-risk/register.csv`, `03-compliance/soa.csv` |
| **CC7.2** | Anomaly detection and security incident evaluation | Real-time security alerts configured for unauthorized API calls or logins | `02-risk/register.csv` |
| **CC7.3** | Incident response and escalation procedures | Formal Incident Response Plan with defined severity levels and reporting SLAs | `01-governance/scope.md`, `02-risk/methodology.md` |

### CC8.0: Change Management
| SOC 2 Criteria ID | Criteria Description | Northbridge Implementation | Primary Evidence Artifact |
| :--- | :--- | :--- | :--- |
| **CC8.1** | Code change authorization, testing, and deployment | Mandatory peer-reviewed Pull Requests (PRs) and isolated DEV/PROD environments | `01-governance/access-control-policy.md` |

---

## 3. Additional In-Scope Trust Services Categories

### Availability (A1.0)
* **A1.1 / A1.2 Capacity & Redundancy:** AWS Multi-AZ auto-scaling deployments and continuous database backups to satisfy our 99.9% uptime SLA (`02-risk/register.csv`).

### Confidentiality (C1.0)
* **C1.1 Data Classification & Encryption:** Patient records and PII encrypted at rest using AES-256 and restricted via RBAC (`01-governance/scope.md`).

### Privacy (P1.0 - P8.0)
* **P1.1 / P3.1 Data Minimization & UK GDPR Compliance:** Strict health data processing boundaries, anonymized telemetry, and AI input safeguards (`01-governance/scope.md`, `01-governance/ai-acceptable-use-policy.md`).

---

## 4. Continuous Control Monitoring & Audit Cadence

Northbridge Health maintains SOC 2 compliance through recurring operational cadences:
1. **Monthly:** Review vulnerability scan outputs and cloud configuration alerts.
2. **Quarterly:** Conduct IAM access review audits across AWS, GitHub, and Google Workspace.
3. **Annually:** Engage an independent CPA firm for a SOC 2 Type II audit report and third-party penetration testing.