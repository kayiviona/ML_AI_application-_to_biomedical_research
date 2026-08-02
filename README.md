Machine Learning and AI in Biomedical Research

MSc Cancer Genomics and Data Science
Queen Mary University of London, 2025–2026

This repository contains the coursework assignment from the Machine Learning and AI in Biomedical Research module. 
The module covers supervised and unsupervised machine learning and deep learning methods applied to cancer 
genomics and pathology imaging data.

---

LAQ 1 — Supervised Classification: 
Random Forest for DLBCL Subtype Prediction

Files:
`Ka Yi Chan CAN7035 ML AI LAQ1.Rmd`
`Ka Yi Chan CAN7035 ML AI LAQ2.Rmd`

Dataset:
- Training/testing: DLBCL_cohort_2 — gene expression profiles from 350 DLBCL samples (167 Activated B 
  Cell-like, 183 Germinal Centre B Cell-like)
- Validation: DLBCL_Cohort_1 — 798 DLBCL samples

Methods:
- Random forest classifier for cell-of-origin prediction with 70/30 training/testing split
- Model tuning — optimisation of number of trees and mtry parameter to minimise out-of-bag (OOB) error
- Three-stage feature selection:
  - Full feature model (all genes)
  - Top 1000 most important features
  - Recursive feature elimination to find optimal gene number
- Model evaluation at each stage: OOB error, Type I error, Type II error, ROC curves
- Independent cohort validation on DLBCL_Cohort_1

Tools: R, randomForest, ggplot2, pROC

---

LAQ 2 — Unsupervised Clustering: Molecular Subtype Discovery in ESCC

File: `Ka Yi Chan CAN7035 ML AI LAQ2.Rmd`

Dataset: Gene expression profiles from 90 oesophageal squamous cell carcinoma (ESCC) samples

Methods:
- Non-negative matrix factorisation (NMF) for unsupervised molecular subtype discovery with 
  optimal cluster number selection
- Top 20 gene signatures per cluster identified by differential expression against all other clusters
- Gene Set Enrichment Analysis (GSEA) to identify most upregulated and downregulated pathways 
  per cluster
- Consensus clustering using ConsensusClusterPlus as an independent validation approach
- Comparative analysis of cluster membership and pathway findings between NMF and consensus 
  clustering methods

Tools: R, NMF, ConsensusClusterPlus, GSEA, ggplot2

---

LAQ 3 — Deep Learning: CNN for H&E Pathology Image Classification

File: `Ka Yi Chan CAN7035 Assignment LAQ3.ipynb`

Dataset: 8 H&E whole slide image files divided into two groups:
- Group A vs B (Model 1)
- Group C vs D (Model 2)

Methods:
- Image preprocessing — tiling into 100×100 pixel patches with 90:10 train/test split
- Two convolutional neural network (CNN) models built independently for each image group
- Model performance evaluation: training and validation accuracy for each model
- Cross-testing: Model 1 applied to test set 2 and Model 2 applied to test set 1 to assess 
  generalisation across image groups
- Interpretation of cross-model performance differences

Tools: Python, TensorFlow/Keras, matplotlib

---

Technologies Used

- Languages: R (R Markdown), Python (Jupyter notebook)
- Key packages: randomForest, pROC, NMF, ConsensusClusterPlus, GSEA, TensorFlow, 
  Keras, ggplot2, matplotlib
