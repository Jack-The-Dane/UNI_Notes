---
course: "[[Multivariate Statistical Analysis]]"
date: 2025-11-20
tags:
  - uni/masters/semester1
  - statistics/classification
  - math/linear-algebra
type: lecture-note
---

# Classification & Discriminant Analysis

## 1. General Classification Criteria (Distribution Free)

**Goal:** Assign observation vector $\mathbf{x}$ to one of $g$ populations ($G_1, \dots, G_g$).
**Priors:** $p_i = P(G_i)$ (Probability that an observation belongs to group $i$).

### A. ECM (Expected Cost of Misclassification)
We aren't just minimizing errors; we are minimizing the **cost** of errors.

> [!INFO] Definition: Cost Function
> $C(k|i) =$ Cost of assigning object to group $k$ when it actually belongs to group $i$.
> * Usually $C(i|i) = 0$ (no cost for being right).

**Formula for ECM:**
$$
ECM = \sum_{i=1}^{g} p_i \times \sum_{k=1}^{g} P(k|i) \times C(k|i)
$$

### B. The Decision Rule (Minimizing ECM)
To minimize ECM, we partition the sample space into regions $R_1, \dots, R_g$.

**Rule:** Assign $\mathbf{x}$ to Group $k$ if:
$$
\sum_{i=1, i\neq k}^{g} p_i f_i(\mathbf{x}) C(k|i) < \sum_{i=1, i\neq j}^{g} p_i f_i(\mathbf{x}) C(j|i) \quad \forall j \neq k
$$
*(Interpretation: Assign to the group where the weighted cost of being wrong is lowest).*
Different formula:
$$k = argmin_{1,\dots,g} \left( \sum_{i=1, i \ne k}^{g} p_{i}f_{i}(x_{i})c(k|i) \right)$$
### C. Special Cases

| Case | Assumption | Objective | Rule Name |
| :--- | :--- | :--- | :--- |
| **1** | Equal Costs | Minimize **TPM** (Total Prob. of Misclassification) | TPM Rule |
| **2** | Equal Costs + Equal Priors | Maximize Density | **ML Rule** (Max Likelihood) |

**The MAP Rule (Maximum A Posteriori):**
Using [[Bayes Theorem]]:
$$
P(G_k|\mathbf{x}) = \frac{f_k(\mathbf{x}) p_k}{\sum f_i(\mathbf{x}) p_i}
$$
> [!TIP] Connection
> The **MAP Rule** (pick highest posterior) is mathematically equivalent to minimizing TPM.

---

## 2. Classification for MVN Populations (QDA)

**Assumption:** Data in each group follows a [[Multivariate Normal Distribution]]: $\mathbf{x} \sim N_p(\boldsymbol{\mu}_i, \boldsymbol{\Sigma}_i)$.

### A. General Case: Unequal Covariances
If $\boldsymbol{\Sigma}_i \neq \boldsymbol{\Sigma}_j$, the decision boundary is **Quadratic** (curved).

### B. QDA Decision Rule (Population)
Assign to group $k$ that maximizes the **Quadratic Score**:

$$
d_k^Q(\mathbf{x}) = -\frac{1}{2} \ln|\boldsymbol{\Sigma}_k| - \frac{1}{2}(\mathbf{x} - \boldsymbol{\mu}_k)^T \boldsymbol{\Sigma}_k^{-1} (\mathbf{x} - \boldsymbol{\mu}_k) + \ln p_k
$$

> [!NOTE] Key Component
> The term $(\mathbf{x} - \boldsymbol{\mu}_k)^T \boldsymbol{\Sigma}_k^{-1} (\mathbf{x} - \boldsymbol{\mu}_k)$ is the squared **[[Mahalanobis Distance]]**.

### C. Sample-Based QDA
Since we don't know parameters, estimate them:
* $\boldsymbol{\mu}_i \rightarrow \bar{\mathbf{x}}_i$
* $\boldsymbol{\Sigma}_i \rightarrow \mathbf{S}_i$ (Sample covariance)
* $p_i \rightarrow \hat{p}_i = n_i / n_{total}$

---

## 3. Classification for MVN Populations (LDA)

**Assumption:** **Homoscedasticity** (Equal Covariance Matrices).
$$
\boldsymbol{\Sigma}_1 = \boldsymbol{\Sigma}_2 = \dots = \boldsymbol{\Sigma}_{pooled}
$$

### A. The Simplification
The quadratic terms cancel out. The boundary becomes a **Hyperplane** (Linear).

### B. LDA Decision Rule
Maximize the **Linear Score**:
$$
d_k^L(\mathbf{x}) = \boldsymbol{\mu}_k^T \boldsymbol{\Sigma}^{-1} \mathbf{x} - \frac{1}{2}\boldsymbol{\mu}_k^T \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}_k + \ln p_k
$$

### C. Sample-Based LDA
Use the **Pooled Covariance Matrix**:
$$
\mathbf{S}_{pooled} = \frac{\sum (n_i - 1)\mathbf{S}_i}{\sum n_i - g}
$$
* **Pros:** More degrees of freedom, stable for small $n$.
* **Cons:** High bias if covariances are actually different.

![[lda_qda_comparison.png]]
*(Insert the plot generated in class here)*

---

## 4. MVN Model Control

Always check assumptions before trusting the model.

1.  **Test for MVN Samples:**
    * **Chi-Square Plot:** Plot squared Mahalanobis distances $d_j^2$ against $\chi^2$ quantiles. Should be linear.
2.  **[[Bartlett Test]] (or Box's M):**
    * $H_0: \boldsymbol{\Sigma}_1 = \dots = \boldsymbol{\Sigma}_g$
    * > [!WARNING]
    * > Bartlett's test is extremely sensitive to non-normality.
3.  **[[MANOVA]]:**
    * $H_0: \boldsymbol{\mu}_1 = \dots = \boldsymbol{\mu}_g$
    * If we fail to reject, groups aren't separated enough to classify.

---

## 5. Performance: Error Rates

### A. APER (Apparent Error Rate)
* **Method:** Train on $X$, Test on $X$.
* **Metric:** Confusion Matrix $\rightarrow n_{miss}/n_{total}$.
* **Problem:** Optimistically biased (underestimates error).

### B. AER (Actual Error Rate) estimation
* **Method:** Cross-Validation (Lachenbruch's Holdout / Leave-One-Out).
    1.  Remove $\mathbf{x}_j$.
    2.  Train on $n-1$.
    3.  Classify $\mathbf{x}_j$.
* **Result:** Nearly unbiased estimate of true error.

---
#review #todo
- [ ] Review the derivation of the QDA score from the density function.
- [ ] Implement LOOCV in Python for the next assignment.