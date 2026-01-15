# Lecture Notes: Multivariate Statistics – Classification Models

**Course:** Multivariate Statistics  
**Semester:** MSc, 1st Semester  
**Topic:** Classification Models and Decision Rules  
**Date:** 🗓️ [Insert date]  
**Lecturer:** [Insert name]

---

## 🧩 Model

### Populations and Sample Space
- **Population:** A group of observations drawn from a probability distribution.  
  - Example: Two populations \( $\pi_1$ \) and \( $\pi_2$ \) with distributions \( $f_1(x)$ \) and \($f_2(x)$ \).
- **Sample space (Ω):** The set of all possible outcomes or observation vectors \( $x \in \mathbb{R}^p$ \).
- **Goal:** Assign an observation \( $x$ \) to one of the populations based on a *decision rule*.

---

### Decision Rule and Splitting of Sample Space
- **Decision rule:** Function \( $\delta(x)$ \) mapping \( $x$ \) to one of the populations.
$$
  \delta(x) = 
  \begin{cases} 
  \pi_1, & x \in R_1 \\
  \pi_2, & x \in R_2
  \end{cases}
  $$
- **Splitting of sample space:** Divide Ω into decision regions \( $R_1$ \) and \( $R_2$ \).
- $R_1$ and $R_{2}$ should have no elements in common

---

### 🧪 DEMO: Two-Population Classification (Case I and II)
- **Case I:** Equal covariance matrices → Linear Discriminant Analysis (LDA).
- **Case II:** Unequal covariance matrices → Quadratic Discriminant Analysis (QDA).

---

### Possible Misclassifications
- Misclassification occurs when an observation is assigned to the wrong population.
- Two types:
  - Type I error: Classify \( $x \in \pi_1$ \) as \($\pi_2$ \)
  - Type II error: Classify \( $x \in \pi_2$ \) as \( $\pi_1$ \)

#### Confusion Matrix
| True \ Predicted | π₁ | π₂ |
|------------------:|:--:|:--:|
| π₁               | a  | b  |
| π₂               | c  | d  |

#### Cost Matrix
| Decision → |   π₁   |   π₂   |
| ---------- | :----: | :----: |
| True π₁    |   0    | C(2,1) |
| True π₂    | C(1,2) |   0    |

C Is the cost function for predicting the wrong classification. 
- **Priors:** Prior probabilities \( $P(\pi_1)$ \) and \( $P(\pi_2)$ \).

---

## ⚖️ General Classification Criteria (Distribution-Free)

### Expected Cost of Misclassification (ECM)
$$
ECM = \sum_{i=1}^{g} \sum_{j \neq i} C(j|i) P(j|i) P(\pi_i)
$$
- **Goal:** Choose decision rule that *minimizes ECM*.

---

### Minimizing ECM → Splitting of Sample Space → Decision Rule
- Decision boundaries determined by comparing expected costs:
  $$
  \text{Decide } \pi_1 \text{ if } C(2|1) P(\pi_1|x) < C(1|2) P(\pi_2|x)
  $$

---

### Special Cases
- **Equal costs:**  
  ⇒ Minimize **Total Probability of Misclassification (TPM)**  
  \[
  TPM = P(\text{error}) = P(2|1)P(\pi_1) + P(1|2)P(\pi_2)
  \]
- **Equal costs and priors:**  
  ⇒ **Maximum Likelihood (ML) Rule:**  
  \[
  \text{Decide } \pi_1 \text{ if } f_1(x) > f_2(x)
  \]

---

### MAP – Maximum A Posteriori Rule
- Based on **Bayes’ theorem:**
  \[
  P(\pi_i | x) = \frac{f_i(x) P(\pi_i)}{f(x)}
  \]
- **MAP rule:** Choose the class with the highest posterior probability:
  \[
  \delta(x) = \arg\max_i P(\pi_i | x)
  \]

---

## 🧮 Classification for Two MVN Populations – Case I (LDA)

### Model with Equal Population Covariance Matrices
\[
\pi_i: X \sim N_p(\mu_i, \Sigma), \quad i=1,2
\]
- Equal covariance → linear decision boundary.

---

### LDA Decision Rule (Population Version)
\[
\delta(x) = 
\begin{cases} 
\pi_1, & (\mu_1 - \mu_2)^T \Sigma^{-1}x > k \\
\pi_2, & \text{otherwise}
\end{cases}
\]
where \( k \) depends on priors and costs.

---

### Sample-Based LDA Decision Rule
- Replace parameters \( \mu_i \) and \( \Sigma \) with sample estimates \( \hat{\mu}_i \), \( \hat{\Sigma} \).
- Decision function:
  \[
  \delta(x) = 
  \begin{cases}
  \pi_1, & d_1(x) > d_2(x) \\
  \pi_2, & \text{otherwise}
  \end{cases}
  \]
  where  
  \[
  d_i(x) = x^T \hat{\Sigma}^{-1} \hat{\mu}_i - \frac{1}{2}\hat{\mu}_i^T \hat{\Sigma}^{-1} \hat{\mu}_i + \ln P(\pi_i)
  \]

---

### Alternative Formulation for ML-Case (Squared Statistical Distances)
- Equivalent to minimizing **Mahalanobis distance**:
  \[
  D^2(x, \mu_i) = (x - \mu_i)^T \Sigma^{-1}(x - \mu_i)
  \]

---

## 🧭 MVN Model Control

### Test for MVN Samples
- **Goal:** Verify multivariate normality assumption.
- **Common tests:**
  - Mardia’s test (skewness & kurtosis)
  - Henze–Zirkler test
  - Royston test

---

### Bartlett Test for Equal Covariance Matrices
- **Null hypothesis:** \( H_0: \Sigma_1 = \Sigma_2 \)
- Sensitive to deviations from normality.

---

### Hotelling’s \( T^2 \) Test
- Tests significant difference between mean vectors of populations.
  \[
  T^2 = \frac{n_1 n_2}{n_1 + n_2} (\bar{x}_1 - \bar{x}_2)^T S_p^{-1} (\bar{x}_1 - \bar{x}_2)
  \]
- Analogous to univariate *t*-test.

---

## 🌀 Classification for Two MVN Populations – Case II (QDA)

### Model with Unequal Population Covariance Matrices
\[
\pi_i: X \sim N_p(\mu_i, \Sigma_i)
\]
- Decision boundary becomes **quadratic**.

---

### QDA Decision Rule (Population Version)
\[
\delta(x) = 
\begin{cases}
\pi_1, & g_1(x) > g_2(x) \\
\pi_2, & \text{otherwise}
\end{cases}
\]
where  
\[
g_i(x) = -\frac{1}{2}\ln|\Sigma_i| - \frac{1}{2}(x - \mu_i)^T \Sigma_i^{-1}(x - \mu_i) + \ln P(\pi_i)
\]

---

### Sample-Based QDA Decision Rule
- Replace parameters with sample estimates \( \hat{\mu}_i, \hat{\Sigma}_i \).

---

## 📊 Performance of Classification – Probability of Misclassification

### TPM (Total Probability of Misclassification)
- Theoretical, requires knowledge of true distributions:
  \[
  TPM = P(2|1)P(\pi_1) + P(1|2)P(\pi_2)
  \]

---

### Empirical APER – Apparent Error Rate
- Computed using **training data** confusion matrix:
  \[
  APER = \frac{\text{# of misclassified training samples}}{n}
  \]

---

### Estimated AER – Actual Error Rate
- Estimated via **cross-validation**:
  - Leave-one-out (LOOCV)
  - k-fold cross-validation

---

**Summary:**
- LDA → linear boundaries (equal covariances).  
- QDA → quadratic boundaries (unequal covariances).  
- MAP and ML rules stem from Bayesian principles.  
- Classification accuracy measured by TPM, APER, AER.

---
