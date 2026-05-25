# Healthcare-Data-Privacy-Anonymization-Framework
Evaluating Linkage Attacks, k-Anonymity, and l-Diversity


This repository contains a specialized data privacy and security analysis framework.
The project demonstrates the vulnerabilities of "de-identified" healthcare databases to malicious re-identification methods and evaluates structural mitigation strategies.

## 🔬 Project Overview & Purpose

Modern data privacy requires shifting away from the naive assumption that simply removing direct identifiers (like names) is sufficient to protect patient confidentiality. 

This project is divided into two primary analytical phases:
1. **The Vulnerability Phase:** Implementing a programmatic **Linkage Attack** by merging a simulated "de-identified" public health registry with an open voter database using Quasi-Identifiers (QIs).
2. **The Mitigation Phase:** Evaluating the efficiency of **k-Anonymity** (via data generalization and suppression) and **l-Diversity** in neutralizing re-identification risks and preventing homogeneity attacks.

---

## ⚔️ Phase 1: Linkage Attack Implementation

### ⚙️ Methodology & Quasi-Identifiers (QIs)
The attack was executed programmatically via a Python/Jupyter pipeline by performing a relational join between two primary datasets:
* `PatientsPublic.xlsx` (The allegedly anonymized medical database)
* `VotersPublic.xlsx` (A publicly accessible voter registry)

By isolating **Age** and **Sex** as **Quasi-Identifiers (QIs)**—seemingly unharmful metadata attributes—we mapped intersections between the cohorts to reconstruct the identities of masked profiles.

### 📊 Attack Results & Security Breach Evaluation
* **Total Intersections:** **25 matches** were generated through QI overlapping.
* **Deterministic Re-identification:** **15 unique individuals** were successfully and fully re-identified with absolute confidence, allowing the extraction of their sensitive medical profiles.
* **Case Study (Deterministic Breach):** The combination of a 63-year-old Female profile in both registries yielded a high-confidence match, successfully re-identifying a patient (*Ioanna Christou*) and exposing sensitive clinical diagnoses, including **anemia** and **type 2 diabetes**.
* **Probabilistic Breach:** Even in scenarios where a 1:1 deterministic match was not established, the attack severely degraded anonymity. For example, narrowing down a target profile to a highly dense cohort (e.g., *"Female, 24"*) within a heavily restricted subset compromises the patient's right to total confidentiality.

**Conclusion:** Removing names is an insufficient security practice if the underlying metadata matrix remains unmasked.

---

## 🛡️ Phase 2: Mitigation via k-Anonymity & l-Diversity

To counter the vulnerabilities exposed in Phase 1, a secondary simulation was executed by cross-referencing `VotersPublic.xlsx` against an optimized medical dataset: `PatientsPublickAnon.xlsx`.

### 🗂️ Defense Mechanisms Applied
* **k-Anonymity (Data Generalization & Suppression):** Continuous numeric attributes were converted into structural intervals (e.g., specific ages were generalized into age brackets such as `[50-67]`), and geographic identifiers (ZIP codes) were masked. This structural transformation guarantees that every individual record is statistically indistinguishable from at least $k-1$ other records in the same equivalence class.
* **l-Diversity (Diversity Guarantee):** Applied to ensure that each equivalence class contains a diverse distribution of sensitive attributes (diagnoses), effectively mitigating deterministic inference and neutralizing **Homogeneity Attacks**.

### 🎯 Security Evaluation After Anonymization
The deployment of k-anonymity successfully neutralized all high-confidence re-identification vectors established during the initial linkage attack. 
* *Example:* The profile of *Ioanna Christou*, which was fully compromised in Phase 1, was successfully obscured into a generalized, secure multi-patient cohort of females within the `[50-67]` age group, preventing individual privacy leakage.

"Note: The dataset files (VotersPublic.xlsx, PatientsPublic.xlsx, etc.) are proprietary academic data provided by the University and are not included in this public repository for data privacy reasons."
