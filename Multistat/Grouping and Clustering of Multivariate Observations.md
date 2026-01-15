# Lecture 12 — Grouping and Clustering of Multivariate Observations
_Multivariate Statistics (MSc, Semester 1)_

---

## 1. Introduction

### **Problem Statement**
- For multivariate datasets, we want to **identify natural groupings** (clusters).
- Clustering attempts to detect structure **without predefined labels** → *unsupervised learning*.

### **Purpose and Applications**
- Reduce dimensional complexity.
- Reveal latent subgroups.
- Applications:
  - Bioinformatics (e.g., gene expression clustering)
  - Marketing: customer segmentation
  - Pattern recognition
  - Recommender systems
  - Anomaly/outlier detection

---

## 2. Distances Between Observations

Clustering performance depends heavily on how we measure **similarity**.

### **Continuous Variables**
- **Euclidean distance**:  
  $d(\mathbf{x}_i,\mathbf{x}_j)=\sqrt{\sum_k (x_{ik}-x_{jk})^2}$
- **m-norm / Lp distance**:  
  $d_m(\mathbf{x}_i,\mathbf{x}_j)=\left(\sum_k |x_{ik}-x_{jk}|^m \right)^{1/m}$
  - Special cases:
    - $m=1$: Manhattan  
    - $m=2$: Euclidean  
    - $m\to\infty$: Chebyshev
- **Standardization**
  - Important when variables have different scales.
  - Typically convert $X \to Z$ using z-scores.

### **Binary (Indicator) Variables**
- Based on matches/mismatches:
  - **Jaccard similarity** (ignores double zeros):  
    $J = \dfrac{\text{matches on 1}}{\text{matches on 1} + \text{mismatches}}$
  - **Simple matching coefficient** (includes 0–0 matches):  
    $S = \dfrac{\text{matches}}{\text{total}}$

### **Distances Between Variables**
- Usually measured via correlation:
  - Distance = $1 - r$ or sometimes $\sqrt{2(1-r)}$.

---

## 3. Distances Between Clusters: Linkage Metrics

Used in hierarchical clustering to decide which clusters to merge.

### **Common Linkage Methods**
- **Single linkage**: minimum pairwise distance  
- **Complete linkage**: maximum pairwise distance  
- **Average linkage**: mean pairwise distance  
- **Centroid linkage**: distance between means  
- **Ward’s method**: minimizes increase in within-cluster variance

**DEMO:** Inter-cluster linkage behavior

---

## 4. Motivation: Need for Search Algorithms
- The number of ways to cluster $n$ observations grows extremely fast → linked to **Bell numbers**.
- Exhaustive search is impractical.
- Therefore clustering relies on **heuristic / greedy** algorithms.

---

## 5. Hierarchical Clustering (Using Distance Matrix $D$)

### **Procedure**
1. Compute distance matrix $D$.
2. Start with each observation as its own cluster.
3. Iteratively merge clusters using linkage rule.
4. Produce a **dendrogram**.

### **Properties**
- Does **not** require selecting number of clusters beforehand.
- Sensitive to noise and outliers.
- Computationally expensive for large $n$.

**DEMO:** Hierarchical clustering and dendrogram interpretation

---

## 6. Non-Hierarchical Clustering (Using Data Matrix $X$ or $Z$)

### **K-Means Clustering**
- Objective: minimize within-cluster sum of squares  
  $ \sum_{k=1}^K \sum_{i \in C_k} \|\mathbf{x}_i - \boldsymbol{\mu}_k\|^2 $
- Algorithm:
  1. Initialize $K$ centroids.
  2. Assign each observation to nearest centroid.
  3. Recompute centroids.
  4. Repeat until convergence.

### **Properties**
- Fast, scalable.
- Assumes spherical, compact clusters.
- Must specify $K$ in advance.

**DEMO:** K-means clustering

---

## 7. Clustering Using Gaussian Mixture Models (GMM)

### **Introduction**
- Model data as:  
  $ p(\mathbf{x}) = \sum_{k=1}^K \pi_k \, \mathcal{N}(\mathbf{x} \mid \boldsymbol{\mu}_k, \Sigma_k) $
- Parameters estimated via **Expectation–Maximization (EM)**.

### **Posteriors & MAP Assignment**
- Posterior cluster probability:  
  $ p(k \mid \mathbf{x}_i) = \dfrac{\pi_k \, \mathcal{N}(\mathbf{x}_i \mid \boldsymbol{\mu}_k, \Sigma_k)}{\sum_{j=1}^K \pi_j \, \mathcal{N}(\mathbf{x}_i \mid \boldsymbol{\mu}_j, \Sigma_j)} $
- **MAP (maximum a posteriori)** cluster assignment:  
  $ \hat{z}_i = \arg\max_k p(k \mid \mathbf{x}_i) $

### **Advantages**
- Can model clusters with different shapes/sizes (via $\Sigma_k$).
- Provides soft, probabilistic assignments.

**DEMO:** GMM clustering

---

## 8. Multidimensional Scaling (MDS) and Visualization

### **Purpose**
- Reduce high-dimensional data to 2D/3D while preserving distances.

### **Key Idea**
- Given distance matrix $D$, find coordinates in low dimension that minimize distortion.

### **Applications**
- Visual exploration of cluster structure.
- Detect cluster overlap or separation.

**DEMO:** MDS example

---

## End of Lecture Notes
