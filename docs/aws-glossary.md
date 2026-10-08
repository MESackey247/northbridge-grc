# AWS Cloud Infrastructure & GRC Control Glossary

**Organization:** Northbridge Health Ltd  
**Scope:** AWS Cloud Infrastructure & Service Governance  
**Framework Alignment:** ISO/IEC 27001:2022 (Annex A.8) & SOC 2 Trust Services Criteria  

---

## 1. Governance Overview
Northbridge Health operates a 100% cloud-native SaaS environment hosted on Amazon Web Services (AWS) within the London (`eu-west-2`) region. This document defines the primary AWS services utilized and maps them directly to information security compliance controls.

---

## 2. Core AWS Services & Control Mapping Matrix

### 2.1 Identity and Access Management (AWS IAM)
* **Plain English Definition:** IAM controls authentication (verifying *who* you are) and authorization (verifying *what* you can access) across AWS resources.
* **Northbridge Usage:** IAM enforces Multi-Factor Authentication (MFA), Role-Based Access Control (RBAC), and Least Privilege policies for developers and infrastructure.
* **Control Mapping:**
  * **ISO 27001:2022:** Control A.5.15 (Access Control), Control A.5.17 (Authentication Information)
  * **SOC 2:** CC6.1 (Logical Access), CC6.3 (Principle of Least Privilege)

### 2.2 Simple Storage Service (AWS S3)
* **Plain English Definition:** S3 stores digital files and data objects inside secure, scalable "buckets."
* **Northbridge Usage:** Holds encrypted application logs, database backups, and patient scheduling attachments. Public access is globally blocked at the account level.
* **Control Mapping:**
  * **ISO 27001:2022:** Control A.8.12 (Data Leakage Prevention), Control A.8.13 (Information Backup)
  * **SOC 2:** CC6.6 (Boundary Protection), Availability A1.2 (Data Redundancy)

### 2.3 Virtual Private Cloud (AWS VPC)
* **Plain English Definition:** A private, logically isolated virtual network inside AWS that segregates production databases from public web interfaces.
* **Northbridge Usage:** Ensures production databases containing patient data are housed in private subnets with no direct route to or from the public internet.
* **Control Mapping:**
  * **ISO 27001:2022:** Control A.8.20 (Network Security), Control A.8.22 (Segregation in Networks)
  * **SOC 2:** CC6.6 (Transmission and Boundary Protection)

### 2.4 AWS CloudTrail
* **Plain English Definition:** The central logging service that continuously records every single API call, management console login, and resource modification across the entire AWS account.
* **Northbridge Usage:** Serves as the primary audit log repository for incident investigation, digital forensics, and compliance verification.
* **Control Mapping:**
  * **ISO 27001:2022:** Control A.8.15 (Logging), Control A.8.16 (Monitoring Activities)
  * **SOC 2:** CC7.1 (System Monitoring & Anomaly Detection)

### 2.5 AWS Key Management Service (AWS KMS)
* **Plain English Definition:** A centralized service that manages cryptographic keys used to encrypt and decrypt sensitive data stored across AWS services.
* **Northbridge Usage:** Enforces hardware-backed AES-256 encryption at rest for all S3 buckets, RDS databases, and backup snapshots.
* **Control Mapping:**
  * **ISO 27001:2022:** Control A.8.24 (Use of Cryptography)
  * **SOC 2:** Confidentiality C1.1 (Encryption Standards)