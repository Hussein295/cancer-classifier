# 🧬 Multi-Cancer Type Classifier from Gene Expression Profiles

![Python](https://img.shields.io/badge/Python-3.11-blue)
![XGBoost](https://img.shields.io/badge/XGBoost-99.4%25_Accuracy-green)
![SHAP](https://img.shields.io/badge/Explainability-SHAP-orange)
![Data](https://img.shields.io/badge/Data-TCGA_via_cBioPortal-red)

An end-to-end machine learning pipeline that classifies **5 cancer types** from 
RNA-seq gene expression profiles using real TCGA patient data. Achieves **99.4% 
accuracy** with XGBoost and uses SHAP to reveal the biological drivers behind 
every prediction.

---

## 🎯 Project Highlights

- **Real clinical data:** 792 patient samples across 5 cancer types from TCGA 
  via cBioPortal REST API
- **Biologically validated results:** SHAP analysis independently rediscovered 
  known clinical markers (CDX2 for colorectal, NKX2-1 for lung, FLT1 for kidney)
- **Production-quality pipeline:** Modular notebooks, cached intermediate results, 
  reproducible splits
- **Full explainability:** Per-prediction gene-level explanations using SHAP 
  TreeExplainer

---

## 📊 Results

| Model | Test Accuracy | CV Accuracy (5-fold) |
|---|---|---|
| XGBoost | **99.4%** | 98.86% ± 1.01% |
| Random Forest | 98.1% | 99.12% ± 0.95% |

### UMAP — 5 Cancer Types Separate Cleanly
![UMAP](outputs/figures/03_umap.png)

### SHAP — Genes Driving Each Prediction
![SHAP](outputs/figures/09_shap_bar.png)

### Confusion Matrix
![Confusion](outputs/figures/07_confusion_matrices.png)

---

## 🗂️ Project Structure

```
cancer-classifier/
├── data/
│   ├── raw/              ← TCGA expression data (fetched via API)
│   └── processed/        ← Cleaned, normalized dataset
├── notebooks/
│   ├── 01_data_acquisition.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_eda_umap.ipynb
│   ├── 04_modeling.ipynb
│   └── 05_shap.ipynb
├── outputs/
│   ├── figures/          ← All plots
│   └── models/           ← Saved XGBoost + RF models
├── requirements.txt
└── README.md
```

---

## 🧬 Cancer Types

| Abbreviation | Cancer Type | Samples |
|---|---|---|
| BRCA | Breast Invasive Carcinoma | 199 |
| LUAD | Lung Adenocarcinoma | 133 |
| KIRC | Kidney Renal Clear Cell Carcinoma | 198 |
| LGG | Brain Lower Grade Glioma | ~200 |
| COAD | Colon Adenocarcinoma (COADREAD) | 62 |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| `pandas` / `numpy` | Data manipulation |
| `scikit-learn` | ML pipeline, evaluation |
| `xgboost` | Primary classifier |
| `umap-learn` | Dimensionality reduction |
| `shap` | Model explainability |
| `matplotlib` / `seaborn` | Visualization |
| `cBioPortal REST API` | TCGA data acquisition |

---

## 🚀 How to Reproduce

**1. Clone the repo:**
```bash
git clone https://github.com/YOUR_USERNAME/cancer-classifier.git
cd cancer-classifier
```

**2. Create environment:**
```bash
conda create -n cancer_clf python=3.11 -y
conda activate cancer_clf
pip install -r requirements.txt
```

**3. Run notebooks in order:**
```
01_data_acquisition.ipynb   ← fetches data from cBioPortal API (~15 min)
02_preprocessing.ipynb      ← cleans and normalizes data
03_eda_umap.ipynb           ← exploratory analysis and UMAP
04_modeling.ipynb           ← trains and evaluates models
05_shap.ipynb               ← SHAP explainability analysis
```

---

## 🔬 Key Biological Findings

SHAP analysis revealed the model independently rediscovered clinically 
validated cancer biomarkers:

- **CDX2** — dominant COAD driver (SHAP +4.0); used clinically to diagnose 
  colorectal cancer from biopsies
- **NKX2-1/TTF-1** — top LUAD driver; the primary immunohistochemical marker 
  for lung adenocarcinoma
- **FLT1** — top KIRC driver; reflects VHL→HIF1A→VEGF signaling axis 
  characteristic of clear cell kidney cancer
- **FOXA1** — key BRCA driver; pioneer transcription factor for luminal 
  breast epithelial identity
- **SOX2** — LGG signal via low expression; reflects differentiated glial 
  tumor phenotype

---

## 📄 Data Source

Data accessed via the 
[cBioPortal REST API](https://www.cbioportal.org/api/swagger-ui/index.html) 
from The Cancer Genome Atlas (TCGA). Data is not included in this repository 
due to size — run `01_data_acquisition.ipynb` to fetch it automatically.