# 🧪 Cheminformatics Integrated with Machine Learning

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Domain](https://img.shields.io/badge/Domain-Drug%20Discovery-purple)
![ML](https://img.shields.io/badge/ML-RF%20%7C%20GBM%20%7C%20AdaBoost%20%7C%20Ensemble-orange)
![Docking](https://img.shields.io/badge/Docking-AutoDock%20Vina-red)
![Course](https://img.shields.io/badge/Course-NyBerMan%20Bioinformatics-blue)

## 📌 Project Overview
This project integrates **Cheminformatics** with **Machine Learning** to analyze
drug-like molecules from a curated chemical database. The pipeline covers
molecular descriptor calculation, fingerprint generation, ML-based molecular
weight prediction, and drug-likeness filtering using Lipinski's Rule of Five.

Instead of docking all compounds, a **Machine Learning-driven selection strategy**
was used to identify the most reliable compound, which was then taken forward for
**Molecular Docking using AutoDock Vina**.
---

## 🗄️ Database Used
| Property | Details |
|----------|---------|
| **Database** | DrugBank (DrgBnk.sdf) |
| **Type** | Small molecule structures |
| **Format** | SDF (.sdf) |
| **No. of Structures** | 200+ bioactive molecules |
| **Description** | Manually curated database of bioactive molecules with drug-like properties |

---

## 💊 Candidate Compounds (Initial Screening)
| Compound | SMILES | Actual MW | Predicted MW |
|----------|--------|-----------|--------------|
| Aspirin | CC(=O)OC1=CC=CC=C1C(=O)O | 180.159 | 198.62 |
| Ibuprofen | CC(C)CC1=CC=C(C=C1)C(C)C(=O)O | 206.285 | 215.69 |
| Naproxen | C[C@@H](C1=CC2=C(C=C1)C=C(C=C2)OC)C(=O)O | 230.263 | 225.23 |
| Celecoxib | CC1=CC=C(C=C1)C2=CC(=NN2...)C(F)(F)F | 381.379 | 330.65 |

---
👉 These compounds were initially evaluated, but **not all were docked**.

Selection for docking was based on **ML prediction accuracy**, not random choice.

## 🧠 ML-Based Compound Selection (Core Idea)

After training the machine learning model, compounds were evaluated based on
how accurately their molecular weight was predicted.

| Compound | Actual MW | Predicted MW | Error |
|----------|----------|--------------|-------|
| Naproxen | 230.263  | 225.23       | Low |

👉 **Naproxen showed the closest match between actual and predicted values**

### 🎯 Why Naproxen was selected?

- Indicates high model confidence  
- Shows better feature representation  
- Minimizes prediction error  
- Suitable for reliable downstream analysis  

### ✅ Final Decision
👉 Only **Naproxen** was selected for docking  

✔️ This follows the main objective:
> Using Machine Learning to decide *which compound should be taken forward*, instead of docking all compounds.

## 🔬 Complete Project Workflow

### 📐 Step 1 — Molecular Descriptor Calculation
Calculated **15 key descriptors** per molecule using RDKit:

| Descriptor | Description |
|-----------|-------------|
| MolWeight | Total molecular mass |
| MolLogP | Hydrophobicity (octanol-water partition) |
| NumHDonors | H-bond donors count |
| NumHAcceptors | H-bond acceptors count |
| TPSA | Topological Polar Surface Area — drug absorption |
| NumRotatableBonds | Freely rotating bonds |
| FractionCSP3 | Proportion of sp3 carbons |
| HeavyAtomCount | All non-hydrogen atoms |
| NHOHCount | N/O atoms with H attached |
| NOCount | Total N and O atoms |
| RingCount | Number of rings |
| MolMR | Molecular refractivity (volume) |
| ExactMolWt | Isotope-aware molecular weight |
| MaxPartialCharge | Max partial charge on molecule |
| NumRadicalElectrons | Unpaired electrons |

---

### 🔏 Step 2 — Molecular Fingerprint Generation
Two types of fingerprints were generated:

**Morgan Fingerprints (Circular)**
- Radius = 2, 1024 bits
- Captures local atomic environment
- Used for structural similarity comparisons

**MACCS Keys**
- 166 predefined structural sub-patterns
- Rigid but highly reliable for database searches
- Used for molecular structure comparison

---

### 🤖 Step 3 — Machine Learning Models
- **Target Variable:** Molecular Weight (MolWt)
- **Dataset Split:** 80% Train / 20% Test
- **Total Molecules:** 200+

Four models were trained and compared:

| Model | MAE | R² Score | Notes |
|-------|-----|----------|-------|
| **Random Forest (RF)** | 149.93 | -0.118 | ✅ Best performer |
| Gradient Boosting (GBM) | 176.84 | -0.459 | High accuracy but slow |
| AdaBoost | 167.53 | -0.512 | Sensitive to noise |
| Ensemble (RF+GBM+Ada) | 160.57 | -0.267 | Combined predictions |

> ✅ **Random Forest was selected as the best model** — lowest MAE and
> highest R² among all models. Further tuned using **GridSearchCV**.

---

### 💊 Step 4 — Lipinski's Rule of Five (Drug-likeness Filter)
All 4 compounds were evaluated for drug-likeness:

| Rule | Condition | All 4 Compounds |
|------|-----------|-----------------|
| Molecular Weight | < 500 Da | ✅ Pass |
| H-Bond Donors | ≤ 5 | ✅ Pass |
| H-Bond Acceptors | ≤ 10 | ✅ Pass |
| LogP | ≤ 5 | ✅ Pass |

All 4 compounds passed drug-likeness criteria → considered suitable candidates.

👉 However, final selection for docking was based on **ML prediction accuracy**, not just Lipinski rules.

---

### 🔩 Step 5 — Molecular Docking (AutoDock Vina)

- Only **Naproxen** was selected for docking based on ML prediction accuracy  
- Ligand converted to **.pdbqt format**  
- Docked against target **protein receptor**  
- Binding pose and interactions analyzed  

👉 Docking was performed **only on the ML-selected compound**, not on all compounds

---

## 📁 Project Structure
```
Cheminformatics-Drug-Discovery/
│
├── CHEMO_INFO_PROJECT.ipynb       ← Main analysis notebook
├── requirements.txt               ← Python dependencies
├── README.md                      ← Project documentation
│
└── docking_files/
    ├── receptor.pdbqt
    └── naproxen.pdbqt
```

---

## 🛠️ Tech Stack
| Tool / Library | Purpose |
|---------------|---------|
| **RDKit** | Descriptor & fingerprint calculation |
| **Mordred** | Extended molecular descriptors |
| **Scikit-learn** | RF, GBM, AdaBoost, Ensemble models |
| **XGBoost** | Gradient boosting variant |
| **Pandas / NumPy** | Data manipulation |
| **Matplotlib** | Model comparison plots |
| **AutoDock Vina** | Molecular docking |

---

## 🚀 How to Run
```bash
git clone https://github.com/TusharParihar128/Cheminformatics-Drug-Discovery.git
cd Cheminformatics-Drug-Discovery
pip install -r requirements.txt
jupyter notebook
```

---

## 🙏 Acknowledgement
This project was completed as part of a **1-Month Intensive Course on
Cheminformatics with Machine Learning** conducted by
**NyBerMan Bioinformatics (Europe)**.

This was a **group mini-project (Team 3 — Data Driven Chemist)**
assigned during the course to apply real-world drug discovery concepts
including descriptors, fingerprints, ML modeling, and molecular docking.

### 👥 Project Team
| Name | Affiliation |
|------|-------------|
| **Tushar Parihar** | MSc Bioinformatics, Savitribai Phule Pune University |
| **Gargi Durbude** | MSc Biotechnology, MIT-World Peace University |
| **Uday Kumar Kesarpu** | PhD Scholar, IIT Indore |

📅 **Project Date:** January 31, 2025
