# Healthcare-Data-Privacy-Anonymization-Framework
Evaluating Linkage Attacks, k-Anonymity, and l-Diversity


This repository contains a specialized data privacy and security analysis framework.
The project demonstrates the vulnerabilities of "de-identified" healthcare databases to malicious re-identification methods and evaluates structural mitigation strategies.



## 🚀 Project Workflow & Key Steps

### ⚔️ Step 1: The Linkage Attack (Vulnerability Phase)
* **Objective:** Test if removing patient names is enough to protect privacy.
* **Method:** Executed a programmatic join (`pd.merge`) between a "masked" medical dataset (`PatientsPublic.xlsx`) and a public voter registry (`VotersPublic.xlsx`) using **Age** and **Sex** as Quasi-Identifiers (QIs).
* **Result:** Generated **25 matches** and successfully re-identified **15 unique individuals**, exposing sensitive clinical diagnoses (e.g., specific cases of anemia and type 2 diabetes).

### 🛡️ Step 2: k-Anonymity & l-Diversity (Mitigation Phase)
* **Objective:** Neutralize the re-identification risk exposed in Step 1.
* **Method:** Applied the same linkage attack framework against an anonymized dataset (`PatientsPublicKAnon.xlsx`) utilizing data generalization (age brackets like `[50-67]`) and suppression (ZIP code masking).
* **Result:** **Successfully blocked all high-confidence matches.** Patients were structurally obscured inside equivalence classes where each record is indistinguishable from at least $k-1$ others, while $l$-diversity prevented homogeneity attacks.


\"Note: The dataset files (VotersPublic.xlsx, PatientsPublic.xlsx, etc.) are proprietary academic data provided by the University and are not included in this public repository for data privacy reasons.
