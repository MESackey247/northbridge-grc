# Three Lines of Defence (3LoD) Framework

Northbridge Health Ltd uses the **Three Lines of Defence** model to distribute risk management and governance responsibilities across the business.
subgraph SecondLine [2nd Line of Defence: Oversight & Compliance]
    GRC[GRC / Information Security Team]
    Risk[Risk Management]
end

subgraph ThirdLine [3rd Line of Defence: Independent Assurance]
    Audit[Internal & External Audit]
end

Dev -->|Executes Controls| GRC
IT -->|Executes Controls| GRC
GRC -->|Defines Policies & Monitors| Dev
GRC -->|Defines Policies & Monitors| IT
Audit -->|Independently Assesses| FirstLine
Audit -->|Independently Assesses| SecondLine
## Responsibilities Breakdown
* **1st Line (Tech & Ops):** Implements technical controls (e.g., AWS IAM, software patching)[cite: 1].
* **2nd Line (GRC):** Defines governance policies, conducts risk assessments, and tracks compliance[cite: 1].
* **3rd Line (Audit):** Provides independent assurance to senior leadership and regulators[cite: 1].