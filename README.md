🧪 Cheminformatics Integrated with Machine Learning












📌 Project Overview

This project integrates Cheminformatics with Machine Learning to analyze drug-like molecules from a curated chemical database.

The workflow includes:

Molecular descriptor calculation
Fingerprint generation
Machine learning-based molecular property prediction
Drug-likeness filtering (Lipinski Rule of Five)
ML-driven compound selection
Molecular docking of the selected compound

⚠️ Key Concept:
This project does not aim to dock all compounds.
Instead, it demonstrates how a trained ML model can be used to identify the most reliable candidate for docking, making the process more efficient and intelligent.

🗄️ Database Used
Property	Details
Database	DrugBank (DrgBnk.sdf)
Type	Small molecule structures
Format	SDF (.sdf)
No. of Structures	200+ bioactive molecules
Description	Curated dataset of drug-like molecules
💊 Initial Candidate Compounds
Compound	SMILES	Actual MW	Predicted MW
Aspirin	CC(=O)OC1=CC=CC=C1C(=O)O	180.159	198.62
Ibuprofen	CC(C)CC1=CC=C(C=C1)C(C)C(=O)O	206.285	215.69
Naproxen	CC@@H
C(=O)O	230.263	225.23
Celecoxib	CC1=CC=C(C=C1)C2=CC(=NN2...)C(F)(F)F	381.379	330.65
🤖 Machine Learning Modeling
Target Variable: Molecular Weight (MolWt)
Dataset Split: 80% Train / 20% Test
Total Molecules: 200+
Models Evaluated
Model	MAE	R² Score	Remarks
Random Forest (RF)	149.93	-0.118	✅ Best performer
Gradient Boosting (GBM)	176.84	-0.459	Less accurate
AdaBoost	167.53	-0.512	Sensitive to noise
Ensemble Model	160.57	-0.267	Moderate performance

✅ Random Forest selected based on best overall performance.

🧠 ML-Based Compound Selection (Core Idea)

The selection of compound for docking was based on prediction accuracy of the trained ML model.

📊 Observation
Compound	Actual MW	Predicted MW	Error
Naproxen	230.263	225.23	Low

👉 Naproxen showed the closest match between actual and predicted molecular weight

🎯 Why Naproxen was Selected?
Indicates high model confidence
Shows better feature representation
Minimizes prediction error
Suitable for reliable downstream analysis
✅ Final Selection

👉 Only Naproxen was selected for docking

✔️ This reflects the project objective:

Using Machine Learning to decide which compound should be taken forward, instead of docking all compounds.

💊 Drug-Likeness Evaluation (Lipinski Rule)

All compounds satisfied:

Molecular Weight < 500 Da
H-Bond Donors ≤ 5
H-Bond Acceptors ≤ 10
LogP ≤ 5

👉 All were drug-like, but final selection was based on ML accuracy

🔩 Molecular Docking
Tool: AutoDock Vina
Ligand Used: Naproxen
Target: Protein receptor
Steps:
Ligand preparation (.pdbqt)
Receptor preparation
Grid box setup
Docking simulation
Binding pose analysis

👉 Docking was performed only on the ML-selected compound (Naproxen)

🔬 Workflow Summary
Descriptor Calculation
Fingerprint Generation
ML Model Training
Model Evaluation
Drug-likeness Filtering
ML-Based Compound Selection
Docking of Selected Compound
📁 Project Structure
Cheminformatics-Drug-Discovery/
│
├── CHEMO_INFO_PROJECT.ipynb
├── requirements.txt
├── README.md
│
└── docking_files/
    ├── receptor.pdbqt
    └── naproxen.pdbqt
🛠️ Tech Stack
RDKit
Mordred
Scikit-learn
XGBoost
Pandas / NumPy
Matplotlib
AutoDock Vina
🚀 How to Run
git clone https://github.com/TusharParihar128/Cheminformatics-Drug-Discovery.git
cd Cheminformatics-Drug-Discovery
pip install -r requirements.txt
jupyter notebook
🙏 Acknowledgement

This project was completed as part of a 1-Month Intensive Course on Cheminformatics with Machine Learning conducted by NyBerMan Bioinformatics (Europe).

👥 Project Team
Name	Affiliation
Tushar Parihar	MSc Bioinformatics, Savitribai Phule Pune University
Gargi Durbude	MSc Biotechnology, MIT-WPU
Uday Kumar Kesarpu	PhD Scholar, IIT Indore
📅 Project Date

January 31, 2025
