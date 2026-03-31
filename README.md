# 🧪 Cheminformatics & Molecular Docking Analysis

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Domain](https://img.shields.io/badge/Domain-Drug%20Discovery-purple)
![ML](https://img.shields.io/badge/ML-Random%20Forest-orange)

## 📌 Project Overview
This project applies **Cheminformatics** techniques to analyze drug-like
molecules and perform **Molecular Docking** to study protein-ligand interactions.
Lipinski's Rule of Five was used to filter valid drug candidates.

---

## 💊 Compounds Analyzed
| Compound | SMILES | Valid Drug? |
|----------|--------|-------------|
| Aspirin | CC(=O)OC1=CC=CC=C1C(=O)O | ✅ Yes |
| Ibuprofen | CC(C)CC1=CC=C... | ✅ Yes |
| Naproxen | C[C@@H](C1=CC2=... | ✅ Yes |
| Celecoxib | CC1=CC=C(C=C1)... | ✅ Yes |

---

## 🔍 Project Workflow
1. **Molecular Descriptor Calculation** – Using RDKit & Mordred
2. **Fingerprint Generation** – Morgan & MACCS fingerprints
3. **Lipinski's Rule of Five** – Drug-likeness filtering
4. **ML Model** – Random Forest Regressor for Molecular Weight prediction
5. **Molecular Docking** – AutoDock Vina with .pdbqt files

---

## 🛠️ Tech Stack
- Python 3.10
- RDKit, Mordred
- Pandas, NumPy, Scikit-learn
- AutoDock Vina (for docking)

---

## 🚀 How to Run
```bash
git clone https://github.com/TusharParihar128/Cheminformatics-Drug-Docking.git
cd Cheminformatics-Drug-Docking
pip install -r requirements.txt
jupyter notebook
```

---

## 🎓 Acknowledgement

This project was completed as part of a **1-Month Intensive Course on
Cheminformatics with Machine Learning** conducted by **Nyberman**.

This was a **group mini-project** assigned during the course to apply
cheminformatics concepts including molecular descriptors, fingerprints,
Lipinski's Rule of Five, and molecular docking.

### 👥 Project Team
| Name |
|------|
| Tushar Parihar |
| Gargi Durbude |
| Uday Kumar |

---

## 👤 Author
**Tushar Parihar**
- GitHub: [@TusharParihar128](https://github.com/TusharParihar128)
