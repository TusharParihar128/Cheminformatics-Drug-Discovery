# 🧪 Cheminformatics Integrated with Machine Learning

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Domain](https://img.shields.io/badge/Domain-Drug%20Discovery-purple)
![ML](https://img.shields.io/badge/ML-RF%20%7C%20GBM%20%7C%20AdaBoost%20%7C%20Ensemble-orange)
![Docking](https://img.shields.io/badge/Docking-AutoDock%20Vina-red)
![Course](https://img.shields.io/badge/Course-NyBerMan%20Bioinformatics-blue)

## 📌 Project Overview

This project integrates **Cheminformatics** with **Machine Learning** to analyze drug-like molecules from a curated chemical database.

The pipeline includes:

- Molecular descriptor calculation
- Molecular fingerprint generation
- Machine learning-based property prediction
- Drug-likeness evaluation (Lipinski Rule of Five)
- Rational compound selection using ML
- Molecular docking of selected candidate

⚠️ **Key Idea of the Project:**  
Instead of docking all compounds, this project focuses on using a trained ML model to identify the most reliable compound for docking.

---

## 🗄️ Database Used

| Property | Details |
|----------|---------|
| **Database** | DrugBank (DrgBnk.sdf) |
| **Type** | Small molecule structures |
| **Format** | SDF (.sdf) |
| **No. of Structures** | 200+ bioactive molecules |
| **Description** | Curated dataset of drug-like molecules used for ML modeling and analysis |

---

## 💊 Candidate Compounds (Initial Screening)

| Compound | SMILES | Actual MW | Predicted MW |
|----------|--------|-----------|--------------|
| Aspirin | CC(=O)OC1=CC=CC=C1C(=O)O | 180.159 | 198.62 |
| Ibuprofen | CC(C)CC1=CC=C(C=C1)C(C)C(=O)O | 206.285 | 215.69 |
| Naproxen | C[C@@H](C1=CC2=C(C=C1)C=C(C=C2)OC)C(=O)O | 230.263 | 225.23 |
| Celecoxib | CC1=CC=C(C=C1)C2=CC(=NN2...)C(F)(F)F | 381.379 | 330.65 |

---

## 🤖 Machine Learning Modeling

**Target Variable:** Molecular Weight (MolWt)  
**Dataset Split:** 80% Training / 20% Testing  
**Total Molecules:** 200+

### Models Evaluated

| Model | MAE | R² Score | Remarks |
|-------|-----|----------|---------|
| **Random Forest (RF)** | 149.93 | -0.118 | ✅ Best performer |
| Gradient Boosting (GBM) | 176.84 | -0.459 | Slower, less accurate |
| AdaBoost | 167.53 | -0.512 | Sensitive to noise |
| Ensemble Model | 160.57 | -0.267 | Moderate performance |

✅ **Random Forest selected** based on lowest error and comparatively better generalization.

---

## 🧠 ML-Based Compound Selection (Core Contribution)

After model training, compound selection was performed based on **prediction reliability**.

### 📊 Key Observation

| Compound | Actual MW | Predicted MW | Error |
|----------|-----------|--------------|-------|
| Naproxen | 230.263 | 225.23 | **Low** |

👉 **Naproxen** showed the closest agreement between actual and predicted values.

### 🎯 Selection Rationale
- Accurate prediction indicates strong model confidence
- Lower error implies better feature representation
- Reliable compounds are better suited for downstream validation (docking)

### ✅ Final Decision
**Only Naproxen was selected for docking.**

✔️ This follows the core principle:  
*"Use Machine Learning to guide experimental selection rather than blindly screening all compounds."*

---

## 💊 Drug-Likeness Evaluation (Lipinski Rule)

All candidate compounds satisfied:

| Rule | Condition | Status |
|------|-----------|--------|
| Molecular Weight | < 500 Da | ✅ Pass |
| H-Bond Donors | ≤ 5 | ✅ Pass |
| H-Bond Acceptors | ≤ 10 | ✅ Pass |
| LogP | ≤ 5 | ✅ Pass |

👉 Ensuring all compounds are drug-like, but selection was based on **ML accuracy**, not just rules.

---

## 🔩 Molecular Docking

| Tool Used | AutoDock Vina |
|-----------|---------------|
| Ligand | Naproxen |
| Target | Protein receptor (prepared in .pdbqt format) |

**Process:**
- Ligand preparation
- Grid box definition
- Docking simulation
- Binding pose analysis

👉 Docking was performed **only on the ML-selected compound (Naproxen)**.

---

## 🔬 Complete Workflow
┌─────────────────────────┐
│ Descriptor Calculation │ ← RDKit
│ (15 key descriptors) │
└────────────┬────────────┘
↓
┌─────────────────────────┐
│ Fingerprint Generation │ ← Morgan + MACCS
│ (Morgan + MACCS Keys) │
└────────────┬────────────┘
↓
┌─────────────────────────┐
│ ML Model Training & │ ← Random Forest
│ Evaluation │ (Best performer)
└────────────┬────────────┘
↓
┌─────────────────────────┐
│ Drug-likeness Filtering │ ← Lipinski Rule
└────────────┬────────────┘
↓
┌─────────────────────────┐
│ ML-Based Compound │ ← Naproxen selected
│ Selection │ (Lowest prediction error)
└────────────┬────────────┘
↓
┌─────────────────────────┐
│ Docking of Selected │ ← AutoDock Vina
│ Compound │
└─────────────────────────


---

## 📁 Project Structure
Cheminformatics-Drug-Discovery/
│
├── CHEMO_INFO_PROJECT.ipynb ← Main analysis notebook
├── requirements.txt ← Python dependencies
├── README.md ← Documentation
│
└── docking_files/
├── receptor.pdbqt
└── naproxen.pdbqt


---

## 🛠️ Tech Stack

| Tool / Library | Purpose |
|---------------|---------|
| **RDKit** | Descriptor & fingerprint calculation |
| **Mordred** | Advanced molecular descriptors |
| **Scikit-learn** | ML modeling (RF, GBM, AdaBoost) |
| **XGBoost** | Gradient boosting |
| **Pandas / NumPy** | Data processing |
| **Matplotlib** | Visualization |
| **AutoDock Vina** | Molecular docking |

---

## 🚀 How to Run

```bash
git clone https://github.com/TusharParihar128/Cheminformatics-Drug-Discovery.git
cd Cheminformatics-Drug-Discovery
pip install -r requirements.txt
jupyter notebook

🙏 Acknowledgement
This project was completed as part of a 1-Month Intensive Course on Cheminformatics with Machine Learning conducted by NyBerMan Bioinformatics (Europe).

This was a group mini-project (Team 3 — Data Driven Chemist) focused on applying real-world drug discovery techniques.

👥 Project Team
Name	Affiliation
Tushar Parihar	MSc Bioinformatics, Savitribai Phule Pune University
Gargi Durbude	MSc Biotechnology, MIT-WPU
Uday Kumar Kesarpu	PhD Scholar, IIT Indore
📅 Project Date: January 31, 2025


✅ Done! Copy this entire block from the first line to the last line and paste directly into your README.md file on GitHub.
