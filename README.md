# Machine Learning and AI 
in Biomedical Research

**MSc Cancer Genomics and Data Science**
**Queen Mary University of London, 2025–2026**

This repository contains three long answer assignments 
covering supervised classification, unsupervised 
clustering and deep learning applied to cancer 
genomics and pathology imaging. All LAQs include 
biological interpretation and critical discussion 
of model performance.

---

## LAQ 1 — Supervised Classification: 
Random Forest for DLBCL Subtype Prediction

**Files:**
`Ka Yi Chan CAN7035 ML AI LAQ1.Rmd`
`Ka Yi Chan CAN7035 ML AI LAQ2.Rmd`

**Dataset:**
- Training/testing: DLBCL_cohort_2 — gene expression 
  from 350 DLBCL samples (167 ABC, 183 GCB), 
  70/30 train/test split
- Validation: DLBCL_Cohort_1 — 798 DLBCL samples

**Pipeline and findings:**

*Model tuning:* ntree tuned by plotting OOB error vs 
number of trees. OOB error (overall ~2%) stabilised 
after 100 trees for all three error curves (overall, 
ABC false negative, GCB false positive), confirming 
ntree=100 as sufficient.

*Feature selection strategy:*
- Model 1 (all features): 100% training accuracy; 
  perfect confusion matrix (115 ABC, 123 GCB 
  correctly classified)
- Model 2 (top 1,000 features by importance): 
  evaluated against Model 1
- Model 3 (recursive feature elimination to 
  optimal n): minimised OOB while maximising 
  parsimony

*Validation on independent Cohort 1:* Performance 
was poor. Investigation revealed a critical batch 
effect: Cohort 2 expression values ranged 2–10 
whereas Cohort 1 ranged 8–15. This distributional 
mismatch means the model's decision boundaries, 
learned on Cohort 2 scale, were inappropriate for 
Cohort 1, even with ntree increased to 200. Data 
normalisation prior to cross-cohort prediction 
would be required to overcome this.

**Tools:** R, randomForest, caret, Biobase, 
ggplot2, tidyverse, pROC

---

## LAQ 2 — Unsupervised Clustering: 
Molecular Subtype Discovery in ESCC

**File:** `Ka Yi Chan CAN7035 ML AI LAQ2.Rmd`

**Dataset:** Gene expression profiles from 90 
oesophageal squamous cell carcinoma (ESCC) samples 
— 26,540 genes × 90 samples (TCGA)

**Pipeline and findings:**

*Feature selection:* Top 1,500 most variable genes 
selected by Median Absolute Deviation (MAD) to 
reduce noise while preserving biologically 
informative variance.

*NMF cluster number selection (K=2 to 6, 10 runs, 
seed=420):*
- K=4 selected as optimal based on four criteria: 
  cophenetic correlation remained high (stable 
  cluster assignments), dispersion showed recovery 
  at K=4, sparseness peaked at K=4 (samples most 
  distinctly assigned), and silhouette dropped 
  sharply with consensus maps fragmenting beyond K=4
- NMF Brunet algorithm (KL divergence objective) 
  applied at K=4 on 1,500 × 90 matrix
- Top 20 differentially expressed gene signatures 
  extracted per cluster; GSEA performed per cluster 
  to identify upregulated and downregulated pathways

*Consensus clustering (ConsensusClusterPlus, 500 
repetitions, K up to 10):*
- K=4 independently confirmed as optimal
- Cluster membership and pathway enrichment compared 
  between NMF and consensus clustering results

**Tools:** R, NMF, ConsensusClusterPlus, GSEA, 
ggplot2, tidyverse

---

## LAQ 3 — Deep Learning: 
CNN for H&E Pathology Image Classification

**File:** `Ka Yi Chan CAN7035 Assignment LAQ3.ipynb`

**Dataset:** 8 H&E whole slide image files in 
four groups (A1/A2 vs B1/B2 for Model 1; 
C1/C2 vs D1/D2 for Model 2)

**Pipeline:**

*Image preprocessing:*
- Tiled into 100×100 pixel patches using a tissue 
  content threshold of 20% to exclude background 
  and white space
- Tile counts: A1=96, A2=104, B1=108, B2=104, 
  C1=96, C2=108, D1=96, D2=66 good tiles
- 90:10 train/test split with seed=420 
  for reproducibility

*CNN models:*
- Model 1 trained on Groups A vs B
- Model 2 trained on Groups C vs D
- Model 2 achieved 100% accuracy on its 
  own test set

*Cross-testing findings:*
- Model 1 tested on test set 2: accuracy dropped 
  to ~8%, significantly below chance (50%), 
  indicating the model consistently predicted the 
  wrong class — not random but inverted
- Model 2 tested on test set 1: accuracy dropped 
  to 45%, near chance

*Biological interpretation:*
- The 8% accuracy below chance confirms that 
  A/B and C/D represent independent pathological 
  conditions with entirely distinct morphological 
  signatures that do not transfer across models
- Model 2's 100% training accuracy followed by 
  45% cross-test accuracy indicates overfitting — 
  the model memorised dataset-specific features 
  rather than learning generalisable biological 
  markers
- CNN decision boundaries learned for one 
  pathological problem are mathematically 
  irrelevant to a different one; staining 
  variation across slides adds additional noise
- Conclusion: AI models trained for specific 
  pathology tasks are not directly transferable 
  to independent pathological conditions without 
  retraining

**Tools:** Python, TensorFlow/Keras, OpenCV, 
PIL, numpy, pandas, matplotlib

---

## Technologies Used

- **Languages:** R (R Markdown), Python 
  (Jupyter notebook)
- **Key packages:** randomForest, caret, NMF, 
  ConsensusClusterPlus, TensorFlow, Keras, 
  OpenCV, ggplot2, tidyverse, pROC
