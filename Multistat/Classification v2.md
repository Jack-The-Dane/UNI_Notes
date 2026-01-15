# Lecture Notes: Multivariate Statistics – Classification Models

**Course:** Multivariate Statistics  
**Semester:** MSc, 1st Semester  
**Topic:** Classification Models and Decision Rules  
**Date:** 🗓️ [Insert date]  
**Lecturer:** [Insert name]

---

## 🧩 Model

### Populations and Sample Space
- A **population** represents a group of multivariate observations drawn from a probability distribution.  
  - Example: Two populations, $\pi_1$ and $\pi_2$, each with distributions $f_1(x)$ and $f_2(x)$.
- The **sample space** (Ω) is the set of all possible observation vectors: $x \in \mathbb{R}^p$.
- **Objective:** Given an observation $x$, determine which population it most likely belongs to using a **decision rule**.

---

### Decision Rule and Splitting of Sample Space
- A **decision rule** is a mapping $\delta(x)$ that assigns $x$ to one of the possible classes (populations):
  $$
  \delta(x) =
  \begin{cases}
  \pi_1, & x \in R_1 \\
  \pi_2, & x \in R_2
  \end{cases}
  $$
- The **sample space** is thus split into decision regions $R_1$ and $R_2$.
- The choice of these regions depends on the chosen criterion (e.g., minimizing misclassification probability or cost).

---

### 🧪 DEMO: Two-Population Classification (Case I and II)
- **Case I:** Equal covariance matrices → Linear Discriminant Analysis (LDA)
- **Case II:** Unequal covariance matrices → Quadratic Discriminant Analysis (QDA)

Visual intuition:  
- LDA → linear boundary (straight line or plane).  
- QDA → curved boundary (ellipse, parabola, etc.).

---

### Possible Misclassifications
- **Misclassification:** occurs when a sample from one population is incorrectly assigned to another.  
  - **Type I error:** Classify $x \in \pi_1$ as $\pi_2$  
  - **Type II error:** Classify $x \in \pi_2$ as $\pi_1$

#### Confusion Matrix
| True \ Predicted | π₁ | π₂ |
|------------------:|:--:|:--:|
| π₁               | a  | b  |
| π₂               | c  | d  |

- Diagonal cells = correct classifications  
- Off-diagonal cells = misclassifications

#### Cost Matrix
| Decision → |     π₁     |     π₂     |
| ---------- | :--------: | :--------: |
| True π₁    |     0      | $$C(2,1)$$ |
| True π₂    | $$C(1,2)$$ |     0      |

- $C(2|1)$ = cost of classifying π₁ as π₂  
- $C(1|2)$ = cost of classifying π₂ as π₁  
- Incorporates **asymmetric losses** for wrong decisions.

**Priors:**  
- $P(\pi_1)$, $P(\pi_2)$ = prior probabilities of belonging to each population.

---

## ⚖️ General Classification Criteria (Distribution-Free)

### Expected Cost of Misclassification (ECM)
The **Expected Cost of Misclassification** (ECM) is defined as:

$$
ECM = \sum_{i=1}^{g} \sum_{j \neq i} C(j|i) P(j|i) P(\pi_i)
$$

- It measures the *expected loss* over all possible decisions.  
- The goal of the classifier is to **minimize ECM**.

---

### Minimizing ECM → Splitting of Sample Space → Decision Rule
- The decision rule is found by minimizing the expected cost at each point $x$.
- Decision criterion:
  $$
  \text{Decide } \pi_1 \text{ if } C(2|1) P(\pi_1|x) < C(1|2) P(\pi_2|x)
  $$
- This rule determines how the sample space is split into decision regions.

---

### Special Cases
1. **Equal costs:**  
   When all misclassification costs are the same, minimizing ECM reduces to minimizing the **Total Probability of Misclassification (TPM):**
   $$
   TPM = P(2|1)P(\pi_1) + P(1|2)P(\pi_2)
   $$

2. **Equal costs and priors:**  
   When costs and priors are equal, the decision rule simplifies to the **Maximum Likelihood (ML) rule:**
   $$
   \text{Decide } \pi_1 \text{ if } f_1(x) > f_2(x)
   $$

---

### MAP – Maximum A Posteriori Rule
Using **Bayes’ theorem:**
$$
P(\pi_i | x) = \frac{f_i(x) P(\pi_i)}{f(x)}
$$

- The **MAP rule** assigns $x$ to the population with the highest posterior probability:
  $$
  \delta(x) = \arg\max_i P(\pi_i | x)
  $$
- This generalizes the ML rule by incorporating prior probabilities.
### Soft decision rule:
$$
d = 
\begin{cases}
d_{1}: P(\pi_{1}|x_{0}) > 95\% \\
d_{2}: P(\pi_{2}|x_{0}) > 95\% \\
\text{Otherwise dont classify}
\end{cases}
$$

---

## 🧮 Classification for Two MVN Populations – Case I (LDA)

### Model with Equal Population Covariance Matrices
Assume:
$$
\pi_i: X \sim N_p(\mu_i, \Sigma), \quad i = 1,2
$$

- Both populations share the same covariance matrix $\Sigma$.
- This assumption leads to **linear** decision boundaries.

---

### LDA Decision Rule (Population Version)
$$
\delta(x) =
\begin{cases}
\pi_1, & (\mu_1 - \mu_2)^T \Sigma^{-1}x > k \\
\pi_2, & \text{otherwise}
\end{cases}
$$
where $k$ depends on priors and misclassification costs.

This rule creates a **linear separating hyperplane** between the two populations.

---

### Sample-Based LDA Decision Rule
- Replace unknown parameters with sample estimates:
  - $\mu_i \to \hat{\mu}_i$  
  - $\Sigma \to \hat{\Sigma}$

Decision function:
$$
\delta(x) =
\begin{cases}
\pi_1, & d_1(x) > d_2(x) \\
\pi_2, & \text{otherwise}
\end{cases}
$$

where
$$
d_i(x) = x^T \hat{\Sigma}^{-1} \hat{\mu}_i - \frac{1}{2}\hat{\mu}_i^T \hat{\Sigma}^{-1} \hat{\mu}_i + \ln P(\pi_i)
$$

---

### Alternative Formulation for ML Case (Squared Statistical Distances)
Under equal priors and costs, LDA can be viewed as minimizing **Mahalanobis distance**:
$$
D^2(x, \mu_i) = (x - \mu_i)^T \Sigma^{-1}(x - \mu_i)
$$
→ Choose the class for which $$D^2$$ is smallest.

---

## 🧭 MVN Model Control

### Test for Multivariate Normality (MVN)
Before applying LDA or QDA, the assumption of multivariate normality must be checked.

**Common tests:**
- **Mardia’s test:** based on multivariate skewness and kurtosis.  
- **Henze–Zirkler test:** energy-distance based approach.  
- **Royston test:** multivariate extension of Shapiro–Wilk.

---

### Bartlett Test for Equal Covariance Matrices
- **Null hypothesis:** $$H_0: \Sigma_1 = \Sigma_2$$  
- Tests homogeneity of covariance matrices across populations.
- Sensitive to departures from normality.

---

### Hotelling’s $$T^2$$ Test
Used to test for significant separation between mean vectors:
$$
T^2 = \frac{n_1 n_2}{n_1 + n_2} (\bar{x}_1 - \bar{x}_2)^T S_p^{-1} (\bar{x}_1 - \bar{x}_2)
$$

- $$S_p$$ = pooled covariance matrix.  
- Analogous to the univariate *t*-test but in multivariate space.

---

## 🌀 Classification for Two MVN Populations – Case II (QDA)

### Model with Unequal Population Covariance Matrices
Assume:
$$
\pi_i: X \sim N_p(\mu_i, \Sigma_i)
$$

- Different covariance matrices ⇒ **Quadratic** decision boundaries.
- More flexible than LDA but requires more parameters to estimate.

---

### QDA Decision Rule (Population Version)
$$
\delta(x) =
\begin{cases}
\pi_1, & g_1(x) > g_2(x) \\
\pi_2, & \text{otherwise}
\end{cases}
$$

where
$$
g_i(x) = -\frac{1}{2}\ln|\Sigma_i| - \frac{1}{2}(x - \mu_i)^T \Sigma_i^{-1}(x - \mu_i) + \ln P(\pi_i)
$$

- The decision boundary between classes is **quadratic in x**.

---

### Sample-Based QDA Decision Rule
- Replace parameters with sample estimates $$\hat{\mu}_i$$ and $$\hat{\Sigma}_i$$.
- The rule remains quadratic but becomes data-driven.

---

## 📊 Performance of Classification – Probability of Misclassification

### TPM (Total Probability of Misclassification)
The theoretical overall error rate:
$$
TPM = P(2|1)P(\pi_1) + P(1|2)P(\pi_2)
$$

- Can only be computed if the true distributions are known.

---

### Empirical APER – Apparent Error Rate
Computed using **training data**:
$$
APER = \frac{\text{Number of misclassified training samples}}{n}
$$
- Measures performance on data used to train the model (optimistic estimate).

---

### Estimated AER – Actual Error Rate
Estimated via **cross-validation** (e.g., leave-one-out or k-fold):
- Provides a more **unbiased estimate** of true classification accuracy.
- Reduces overfitting compared to APER.

---

**Summary:**
- **LDA:** Linear boundary, assumes equal covariances.  
- **QDA:** Quadratic boundary, allows unequal covariances.  
- **MAP** and **ML** rules derive from Bayesian principles.  
- Classification accuracy can be evaluated theoretically (TPM) or empirically (APER, AER).

---
