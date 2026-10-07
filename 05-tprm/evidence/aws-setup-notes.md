# AWS Account Security & Cost Controls Setup

**Organization:** Northbridge Health Ltd  
**Cloud Provider:** Amazon Web Services (AWS)  
**Environment:** AWS Free Tier  

## Applied Governance & Security Controls

### 1. Root Account Hardening (ISO 27001 A.5.17 / SOC 2 CC6.1)
* Root account secured with Multi-Factor Authentication (MFA).
* Root account access restricted from daily development and administration.

### 2. IAM Administrative Access (ISO 27001 A.5.15 / SOC 2 CC6.3)
* Created dedicated IAM administrator user (`grc-admin`).
* Enforced MFA hardware/virtual token for `grc-admin`.
* Enforced Principle of Least Privilege baseline.

### 3. Financial Oversight & Cost Safeguards (ISO 27001 A.5.8)
* Configured AWS Zero-Spend / £5 Budget Alert with automated email notifications.
* Mandated Infrastructure-as-Code tear-down protocol (`terraform destroy`) after operational sessions.