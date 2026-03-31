# 🧪 Cheminformatics & Molecular Docking Analysis

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Domain](https://img.shields.io/badge/Domain-Drug%20Discovery-purple)
![ML](https://img.shields.io/badge/ML-Random%20Forest%20%7C%20GBM%20%7C%20AdaBoost-orange)
![Docking](https://img.shields.io/badge/Docking-AutoDock%20Vina-red)

## 📌 Project Overview
This project applies **Cheminformatics** techniques combined with **Machine Learning**
to analyze drug-like molecules, predict molecular properties, and perform
**Molecular Docking** to identify the best drug candidate for protein-ligand interaction.

The entire pipeline goes from raw SMILES strings → descriptor calculation →
ML modeling → drug-likeness filtering → molecular docking.

---

## 💊 Compounds Analyzed
| Compound | Drug-like (Lipinski)? |
|----------|-----------------------|
| Aspirin | ✅ Yes |
| Ibuprofen | ✅ Yes |
| Naproxen | ✅ Yes |
| Celecoxib | ✅ Yes |

---

## 🔬 Complete Project Workflow

### Step 1 — Molecular Descriptor Calculation
- Used **RDKit** and **Mordred** libraries
- Calculated 18+ descriptors per molecule: LogP, MolWt, TPSA,
  HBD, HBA, FractionCSP3, HeavyAtomCount, RingCount, BalabanJ, and more
- Saved descriptor data as CSV

### Step 2 — Fingerprint Generation
- **Morgan Fingerprints** (radius=2, 1024 bits) — captures circular
  structural environment of each atom
- **MACCS Keys** (167 bits) — standard structural keys for drug comparison
- Both fingerprint types saved separately as CSV

### Step 3 — Machine Learning Models
Multiple ML models were trained and compared for **Molecular Weight prediction**:

| Model | MAE | R² Score |
|-------|-----|----------|
| Random Forest | 149.93 | -0.118 |
| Gradient Boosting | 176.84 | -0.459 |
| AdaBoost | 167.53 | -0.512 |
| Ensemble (RF+GB+Ada) | 160.57 | -0.267 |
| RF with GridSearchCV | Optimized | Best Params |

> **Random Forest performed best** among all models and was selected
> for further tuning using GridSearchCV.

### Step 4 — Lipinski's Rule of Five (Drug-likeness Filter)
Applied Lipinski's Rule of Five to filter valid drug candidates:
- Molecular Weight < 500 Da ✅
- H-Bond Donors ≤ 5 ✅
- H-Bond Acceptors ≤ 10 ✅
- LogP ≤ 5 ✅

All 4 compounds passed → selected for docking.

### Step 5 — Molecular Docking (AutoDock Vina)
- Converted molecules to **.pdbqt format** for docking
- Performed docking against target protein receptor
- **Best drug candidate selected** based on lowest binding energy score
- Docking files included in `/docking_files` folder

---

## 📁 Project Structure
```
Cheminformatics-Drug-Discovery/
│
├── CHEMO_INFO_PROJECT.ipynb      ← Main notebook
├── requirements.txt              ← Python dependencies
├── README.md                     ← Project documentation
│
├── docking_files/                ← AutoDock Vina files
│   ├── receptor.pdbqt
│   ├── aspirin.pdbqt
│   ├── ibuprofen.pdbqt
│   ├── naproxen.pdbqt
│   └── celecoxib.pdbqt
```

---

## 🛠️ Tech Stack
| Tool/Library | Purpose |
|-------------|---------|
| RDKit | Molecular descriptor & fingerprint calculation |
| Mordred | Extended molecular descriptors |
| Scikit-learn | ML models (RF, GBM, AdaBoost, Ensemble) |
| XGBoost | Boosting model |
| Pandas / NumPy | Data handling |
| Matplotlib | Visualization |
| AutoDock Vina | Molecular Docking |

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
Cheminformatics with Machine Learning** conducted by **Nyberman**.

This was a **group mini-project** assigned during the course to apply
real-world drug discovery concepts.

### 👥 Project Team
| Name |
|------|
| Tushar Parihar |
| Gargi Durbude |
| Uday Kumar |
