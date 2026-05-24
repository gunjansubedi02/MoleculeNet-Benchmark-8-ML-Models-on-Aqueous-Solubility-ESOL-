MoleculeNet Benchmark: 8 ML Models on Aqueous Solubility (ESOL)
Author: Gunjan Subedi
Programme: Masters in AI for Drug Development (Independent project developed alongside the programme)
Dataset: ESOL (Delaney Aqueous Solubility) — MoleculeNet
Task: Regression — Predict log10 aqueous solubility (mol/L)

Overview
This project benchmarks 8 machine learning models on the ESOL (Estimated Solubility) dataset from MoleculeNet — one of the most widely used cheminformatics benchmarks in drug discovery. The goal is to predict the aqueous solubility of drug-like molecules from their chemical structure, a critical property in early-stage drug development.
Molecules are represented using Morgan Fingerprints (ECFP4, 1024 bits) computed via RDKit, and the dataset is split using a scaffold-based strategy — the industry standard in pharmaceutical machine learning — to ensure the model is evaluated on genuinely unseen chemical scaffolds.

Why Aqueous Solubility Matters
Poor solubility is one of the leading causes of drug candidate failure in development. Being able to predict solubility computationally from molecular structure alone allows medicinal chemists to screen and prioritise compounds before expensive wet lab experiments, making this a high-value task in AI-assisted drug design.

Models Benchmarked
ModelTypeK-Means (k=4)Clustering (unsupervised)Agglomerative ClusteringClustering (unsupervised)DBSCANClustering (unsupervised)Gaussian Mixture ModelClustering (unsupervised)K-Nearest Neighbours (KNN)Supervised RegressionRandom ForestSupervised RegressionXGBoostSupervised RegressionNeural Network (PyTorch MLP)Supervised Regression

Methodology

Molecular featurisation: Morgan Fingerprints (ECFP4, radius=2, 1024 bits) via RDKit
Data splitting: Scaffold split (Bemis-Murcko) — train/val/test on distinct chemical scaffolds
Evaluation metrics: RMSE, MAE, R² (regression); Silhouette Score, Davies-Bouldin Index (clustering)
Validation: 5-fold cross-validation on all supervised models
Neural network: 3-layer MLP with BatchNorm and Dropout (PyTorch)


Project Structure

ESOL_MoleculeNet_ML_Benchmark.ipynb — Main benchmark notebook
README.md — This file

Notebook sections:

Install and Import Libraries
Dataset: ESOL Aqueous Solubility
Cheminformatics: Featurize Molecules with Morgan Fingerprints
Exploratory Data Analysis
Chemical Space Visualization (PCA of Morgan Fingerprints)
Data Splitting: Scaffold Split (Pharma Standard)
Model Training and Evaluation (Clustering + Supervised Models + Neural Network)
Benchmark Results and Visualization
Feature Importance (Random Forest)
5-Fold Cross-Validation
Summary and Conclusions


Key Results

XGBoost and Random Forest consistently outperform other models on ECFP4 fingerprints
LogP (lipophilicity) is the most correlated molecular descriptor with solubility — consistent with Lipinski's Rule of Five
Scaffold splitting reveals a meaningful performance gap compared to random splitting, reflecting real-world generalisation challenges
The PyTorch MLP achieves competitive performance with appropriate regularisation (BatchNorm + Dropout)
Clustering models successfully partition chemical space into structurally meaningful groups


Tools and Libraries

Python 3.x
RDKit — molecular featurisation, Morgan fingerprints, scaffold splitting
PyTorch — neural network (MLP) implementation
XGBoost — gradient boosted trees
scikit-learn — KNN, Random Forest, clustering models, cross-validation
pandas, numpy — data manipulation
matplotlib, seaborn — visualisation

Install dependencies: pip install rdkit scikit-learn xgboost torch pandas numpy matplotlib seaborn

Dataset
The ESOL (Estimated SOLubility) dataset was introduced by Delaney (2004) and is a gold-standard benchmark in cheminformatics. It contains 1,128 drug-like molecules with experimentally measured aqueous solubility values (log mol/L) represented as SMILES strings.
PropertyValueSourceDelaney, J. S. (2004). J. Chem. Inf. Comput. Sci.Molecules1,128Targetlog10(solubility in mol/L)FormatSMILES stringsBenchmark suiteMoleculeNet

References

Delaney JS (2004). ESOL: Estimating Aqueous Solubility Directly from Molecular Structure. J. Chem. Inf. Comput. Sci.
Wu Z et al. (2018). MoleculeNet: A Benchmark for Molecular Machine Learning. Chemical Science.
Rogers D, Hahn M (2010). Extended-Connectivity Fingerprints. J. Chem. Inf. Model.
Bemis GW, Murcko MA (1996). The Properties of Known Drugs. J. Med. Chem.
Chen T, Guestrin C (2016). XGBoost: A Scalable Tree Boosting System. KDD.


About
An independent project developed alongside my Masters in AI for Drug Development. It demonstrates end-to-end cheminformatics and machine learning skills — molecular featurisation, scaffold-aware data splitting, multi-model benchmarking, and neural network implementation — directly applicable to computational drug discovery and AI-assisted molecular property prediction roles.
