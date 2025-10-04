# DA5401_Assignment05
Abhishek Kumar -  DA25C002
# 🧬 DA5401 A5: Visualizing Data Veracity Challenges in Multi-Label Classification

## 📘 Overview
This assignment explores **data veracity issues** in **multi-label classification** using the **Yeast dataset**, a benchmark dataset in bioinformatics. The goal is to apply **advanced non-linear dimensionality reduction techniques** — **t-SNE** and **Isomap** — to visually examine problems such as **noisy labels**, **outliers**, and **hard-to-learn samples** in real-world gene expression data.

By the end of this notebook, you will understand how data complexity and manifold structure affect the **performance and reliability of classifiers** in biological contexts.

---

## 🎯 Objectives
- Apply **t-SNE** and **Isomap** to visualize the high-dimensional Yeast dataset.
- Identify **data veracity challenges** such as noisy labels, outliers, and overlapping class regions.
- Compare **local vs. global structure preservation** between t-SNE and Isomap.
- Discuss how manifold complexity influences **classification difficulty**.

---

## 🧩 Dataset Description
**Dataset:** Yeast Gene Expression Data  
**Source:** [MULAN Repository – Yeast Dataset](http://mulan.sourceforge.net/datasets-mlc.html)

- **Instances:** 2,417  
- **Features:** 103 continuous gene expression features  
- **Labels:** 14 binary functional categories (multi-label targets)  

Each data point represents an **experiment**, and each label corresponds to a **functional category** (e.g., nucleus, cytoplasm, mitochondria).  
The same protein may belong to multiple categories, making this a **multi-label classification problem**.

---

## ⚙️ Part A: Preprocessing and Setup
### 1. Data Loading
Load the **feature matrix (X)** and the **multi-label target matrix (Y)** from the dataset.  
Perform dimensionality checks to confirm shape and structure.

### 2. Label Simplification
To simplify visualization:
- Select the **two most frequent single-label classes**.
- Include the **most frequent multi-label combination**.
- Assign all other labels to a single “Other” category.

This reduces complexity and creates a **color index** for visualization (`Class1`, `Top_MultiCombo`, `Other`).

### 3. Feature Scaling
Standardize the feature matrix using **Z-score normalization**.  
Scaling ensures that all features contribute **equally** to distance calculations, which is essential for distance-based techniques like **t-SNE** and **Isomap**.

---

## 🌐 Part B: t-SNE and Veracity Inspection
### 1. t-SNE Implementation
Apply **t-Distributed Stochastic Neighbor Embedding (t-SNE)** to reduce X to 2D.  
Experiment with **different perplexity values (5, 30, 50)** to balance **local vs. global** neighborhood preservation.  
Choose the optimal perplexity (≈30) based on cluster clarity and interpretability.

### 2. Visualization
Create a **2D scatter plot** where:
- Each point represents an experiment.
- Color encodes the categorical class (`Class1`, `Top_MultiCombo`, `Other`).

### 3. Veracity Inspection
From the t-SNE plot:
- **Noisy/Ambiguous Labels:** Points of one color embedded inside another cluster (multi-functional genes).  
- **Outliers:** Isolated points or distant micro-clusters (rare or mismeasured samples).  
- **Hard-to-Learn Samples:** Overlapping regions with mixed colors, where simple classifiers would struggle.

---

## 🧭 Part C: Isomap and Manifold Learning
### 1. Isomap Implementation
Apply **Isomap** to project data into 2D space for comparison with t-SNE.  
Explain that:
- **Isomap** preserves **global geometry** (geodesic distances along the manifold).  
- **t-SNE** preserves **local neighborhoods** (pairwise similarities).

### 2. Visualization
Generate 2D Isomap plots for various neighbor sizes (`n_neighbors = 5, 10, 20, 30, 50, 70`).  
Color points using the same scheme as in t-SNE for consistency.

### 3. Comparison and Manifold Analysis
- **Isomap vs. t-SNE:**  
  - Isomap reveals **global continuity** of the data manifold.  
  - t-SNE provides **strong local separability** but arbitrary global layout.  
- **Manifold Curvature:**  
  The Isomap plot shows a **moderately curved manifold**, suggesting nonlinear relationships among features.  
  This curvature explains why **classification is challenging**, as linear models cannot easily separate overlapping regions.

---

## 🧮 Theoretical Insights
| Aspect | **t-SNE** | **Isomap** |
|:-------|:------------|:------------|
| **Preserves** | Local structure (neighborhoods) | Global structure (manifold geometry) |
| **Best for** | Visualizing fine-grained clusters | Understanding overall data topology |
| **Global meaning of distances** | Weak | Strong |
| **Sensitivity** | Perplexity parameter | Number of neighbors |
| **Use case** | Local exploration and anomaly inspection | Manifold structure and global continuity |

---

## 🧠 Interpretation Summary
- **The Yeast dataset** lies on a **nonlinear, moderately curved manifold** — not flat, but continuous.  
- **Isomap** unfolds this structure, revealing how different gene expression profiles relate globally.  
- **t-SNE** exposes local patterns and class overlaps, highlighting where data veracity challenges occur.
- The **complexity of the manifold** corresponds to **classification difficulty**, as overlapping and curved regions reduce separability.

---

## 💡 Key Takeaways
- Scaling and preprocessing are crucial for all distance-based methods.
- t-SNE and Isomap complement each other:
  - t-SNE → Focus on **local clusters**.
  - Isomap → Focus on **global geometry**.
- Data veracity challenges such as **label noise**, **outliers**, and **nonlinear manifolds** significantly impact model performance.
- A **nonlinear classifier** (e.g., Random Forest, SVM-RBF, or Neural Networks) is better suited for such complex biological data.


