# 🧬 Classifying Leukemia Subtypes Using Gene Expression and Machine Learning

This project explores how machine learning can classify **acute lymphoblastic leukemia (ALL)** and **acute myeloid leukemia (AML)** using gene expression data from microarray experiments, originally published by Golub et al. (1999). The dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/crawford/gene-expression).

---

## 📁 Dataset Summary

- **Samples**: 72 total  
  - 38 training  
  - 34 independent test (held out for evaluation)
- **Features**: 7,129 gene expression values per sample
- **Target**: Leukemia subtype (ALL vs AML)

---

## 🧪 Methodology Overview

### 1. **Preprocessing**
- Removed non-expression “call” columns
- Transposed and merged data with subtype labels
- Standardized expression values (where needed)
- Selected top 500 genes by variance for model input

### 2. **Dimensionality Reduction**
- **PCA** used for exploratory analysis
- PC1 and PC2 captured ~33% of variance
- Partial clustering of ALL vs AML in PC space

---

## 🤖 Model Comparison

| Model                         | Features Used            | Accuracy | AML F1 | Notes |
|------------------------------|--------------------------|----------|--------|-------|
| **Logistic Regression (PCA)**| Top 10 PCs               | 82.4%    | 0.73   | Simple, interpretable baseline |
| **XGBoost (no regularization)** | Top 500 genes         | 91.2%    | 0.90   | Overfit to single gene (Gene 4846) ⚠️ |
| **XGBoost (regularized)**    | Top 500 genes + tuning   | 91.2%    | 0.90   | More stable, still few dominant genes |
| ✅ **Random Forest (best)**   | Top 500 genes            | 91.2%    | 0.90   | Balanced feature importances ✅ |

---

## 🌟 Final Model: Random Forest

- Test accuracy: **91.2%**
- Used top 500 most variable genes
- Distributed importance across 20+ genes

### 🔬 Top Genes by Importance (Random Forest)

| Rank | Gene Index | Importance |
|------|------------|------------|
| 1    | 2120       | 0.04740    |
| 2    | 4846       | 0.04567    |
| 3    | 6217       | 0.04365    |
| 4    | 2591       | 0.03948    |
| 5    | 759        | 0.03766    |
| ...  | ...        | ...        |

---

## 🧠 Insights

- Feature selection is **essential**: top 500 genes outperformed full set
- PCA was useful for **visualization**, not prediction
- Tree-based models (Random Forest, XGBoost) **generalize better** than linear models
- Regularization is critical to prevent **XGBoost overfitting**

---

## 🚀 Future Enhancements

- Annotate top genes via GeneCards / NCBI
- Apply **SHAP** or permutation-based interpretation
- Extend to **multi-class cancer classification**
- Build a **Streamlit dashboard** or deploy via Flask

---

## 📚 Reference

> Golub, T. R., et al. (1999). *Molecular classification of cancer: class discovery and class prediction by gene expression monitoring*. *Science*, 286(5439), 531–537.
