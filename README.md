# MoleculeNet Benchmark: 8 ML Models on Aqueous Solubility (ESOL)

**Author:** Gunjan Subedi  
**Programme:** Masters in AI for Drug Development *(Independent project developed alongside the programme)*  
**Dataset:** ESOL (Delaney Aqueous Solubility) — MoleculeNet  
**Task:** Regression — Predict log₁₀ aqueous solubility (mol/L)

---

## Overview

This project benchmarks 8 machine learning models on the ESOL (Estimated Solubility) dataset from MoleculeNet — one of the most widely used cheminformatics benchmarks in drug discovery. The goal is to predict the aqueous solubility of drug-like molecules from their chemical structure, a critical property in early-stage drug development.

Molecules are represented using **Morgan Fingerprints (ECFP4, 1024 bits)** computed via RDKit, and the dataset is split using a **scaffold-based strategy** — the industry standard in pharmaceutical machine learning — to ensure the model is evaluated on genuinely unseen chemical scaffolds.

---

## Why Aqueous Solubility Matters

Poor solubility is one of the leading causes of drug candidate failure in development. Being able to predict solubility computationally from molecular structure alone allows medicinal chemists to screen and prioritise compounds before expensive wet lab experiments, making this a high-value task in AI-assisted drug design.

---

## Models Benchmarked

| Model | Type |
|---|---|
| K-Means (k=4) | Clustering (unsupervised) |
| Agglomerative Clustering | Clustering (unsupervised) |
| DBSCAN | Clustering (unsupervised) |
| Gaussian Mixture Model | Clustering (unsupervised) |
| K-Nearest Neighbours (KNN) | Supervised Regression |
| Random Forest | Supervised Regression |
| XGBoost | Supervised Regression |
| Neural Network (PyTorch MLP) | Supervised Regression |

---

## Methodology

| Component | Details |
|---|---|
| Molecular featurisation | Morgan Fingerprints (ECFP4, radius=2, 1024 bits) via RDKit |
| Data splitting | Scaffold split (Bemis-Murcko) — train/val/test on distinct chemical scaffolds |
| Regression metrics | RMSE, MAE, R² |
| Clustering metrics | Silhouette Score, Davies-Bouldin Index |
| Validation | 5-fold cross-validation on all supervised models |
| Neural network | 3-layer MLP with BatchNorm and Dropout (PyTorch) |

## Project Structure
├── ESOL_MoleculeNet_ML_Benchmark.ipynb   # Main benchmark notebook
└── README.md

**Notebook sections:**

1. Install and Import Libraries
2. Dataset: ESOL Aqueous Solubility
3. Cheminformatics: Featurize Molecules with Morgan Fingerprints
4. Exploratory Data Analysis
5. Chemical Space Visualization (PCA of Morgan Fingerprints)
6. Data Splitting: Scaffold Split (Pharma Standard)
7. Model Training and Evaluation (Clustering + Supervised Models + Neural Network)
8. Benchmark Results and Visualization
9. Feature Importance (Random Forest)
10. 5-Fold Cross-Validation
11. Summary and Conclusions

---

## Key Results

- **XGBoost and Random Forest** consistently outperform other models on ECFP4 fingerprints
- **LogP (lipophilicity)** is the most correlated molecular descriptor with solubility — consistent with Lipinski's Rule of Five
- **Scaffold splitting** reveals a meaningful performance gap compared to random splitting, reflecting real-world generalisation challenges
- The **PyTorch MLP** achieves competitive performance with appropriate regularisation (BatchNorm + Dropout)
- **Clustering models** successfully partition chemical space into structurally meaningful groups

---

## Tools and Libraries

| Library | Purpose |
|---|---|
| `RDKit` | Molecular featurisation, Morgan fingerprints, scaffold splitting |
| `PyTorch` | Neural network (MLP) implementation |
| `XGBoost` | Gradient boosted trees |
| `scikit-learn` | KNN, Random Forest, clustering, cross-validation |
| `pandas`, `numpy` | Data manipulation |
| `matplotlib`, `seaborn` | Visualisation |

**Install dependencies:**

```bash
pip install rdkit scikit-learn xgboost torch pandas numpy matplotlib seaborn
```

---

## Dataset

The ESOL (Estimated SOLubility) dataset was introduced by Delaney (2004) and is a gold-standard benchmark in cheminformatics.

| Property | Value |
|---|---|
| Source | Delaney, J. S. (2004). *J. Chem. Inf. Comput. Sci.* |
| Molecules | 1,128 |
| Target | log₁₀(solubility in mol/L) |
| Format | SMILES strings |
| Benchmark suite | MoleculeNet |

---

## References

1. Delaney JS (2004). ESOL: Estimating Aqueous Solubility Directly from Molecular Structure. *J. Chem. Inf. Comput. Sci.*
2. Wu Z et al. (2018). MoleculeNet: A Benchmark for Molecular Machine Learning. *Chemical Science.*
3. Rogers D, Hahn M (2010). Extended-Connectivity Fingerprints. *J. Chem. Inf. Model.*
4. Bemis GW, Murcko MA (1996). The Properties of Known Drugs. *J. Med. Chem.*
5. Chen T, Guestrin C (2016). XGBoost: A Scalable Tree Boosting System. *KDD.*

---

## About

An independent project developed alongside my Masters in AI for Drug Development. It demonstrates end-to-end cheminformatics and machine learning skills — molecular featurisation, scaffold-aware data splitting, multi-model benchmarking, and neural network implementation — directly applicable to computational drug discovery and AI-assisted molecular property prediction roles.
---

## Project Structure
