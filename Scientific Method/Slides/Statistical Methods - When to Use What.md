
_A concise university-level reference for choosing appropriate statistical analyses, with examples._

---

## How to Choose a Statistical Method (Quick Guide)

Ask these questions in order:

1. **What is your research goal?**
    
    - Compare groups
        
    - Examine relationships
        
    - Predict outcomes
        
    - Reduce dimensions / find structure
        
2. **What is your outcome (dependent variable)?**
    
    - Continuous (e.g. test score, height)
        
    - Categorical (binary, nominal, ordinal)
        
    - Multiple outcomes
        
3. **What are your predictors (independent variables)?**
    
    - Categorical (groups, conditions)
        
    - Continuous
        
    - A mix of both
        
4. **How many outcomes?**
    
    - One → _univariate_
        
    - More than one → _multivariate_
        
5. **Do you meet assumptions?**
    
    - Normality
        
    - Homogeneity of variance/covariance
        
    - Independence
        

---

## Descriptive Statistics (Start Here)

### Mean, Median, Mode

- **Use when**: Summarizing central tendency
    
- **Example**: Average exam score
    

### Standard Deviation / Variance

- **Use when**: Describing variability
    
- **Example**: Spread of reaction times
    

### Correlation (Pearson / Spearman)

- **Use when**: Assessing association between two variables
    
- **Pearson**: Continuous, linear, normal
    
- **Spearman**: Ordinal or non-normal
    
- **Example**: Height vs weight
    

---

## Group Comparison Methods (Univariate)

### Independent Samples _t_-Test

- **Use when**:
    
    - One continuous outcome
        
    - One categorical IV with **two groups**
        
- **Example**: Test scores of online vs in-person students
    

### Paired Samples _t_-Test

- **Use when**:
    
    - Same participants measured twice
        
- **Example**: Pre-test vs post-test anxiety scores
    

### One-Way ANOVA

- **Use when**:
    
    - One continuous outcome
        
    - One categorical IV with **3+ groups**
        
- **Example**: Reaction time across three drug conditions
    

### Two-Way (Factorial) ANOVA

- **Use when**:
    
    - One continuous outcome
        
    - **Two categorical IVs**
        
    - Interested in interaction effects
        
- **Example**: Effect of teaching method and gender on exam scores
    

### Repeated Measures ANOVA

- **Use when**:
    
    - Same subjects measured across 3+ conditions or time points
        
- **Example**: Memory performance measured weekly for a month
    

---

## Group Comparison Methods (Multivariate)

### MANOVA (Multivariate Analysis of Variance)

- **Use when**:
    
    - **Multiple continuous dependent variables**
        
    - One or more categorical IVs
        
- **Why not multiple ANOVAs?**
    
    - Controls Type I error
        
    - Accounts for correlations among outcomes
        
- **Example**: Effect of therapy type on anxiety _and_ depression scores
    

### MANCOVA

- **Use when**:
    
    - MANOVA + continuous covariates
        
- **Example**: Teaching method effects on math and reading scores, controlling for IQ
    

---

## Regression-Based Methods

### Simple Linear Regression

- **Use when**:
    
    - Predicting a continuous outcome from one continuous predictor
        
- **Example**: Predict GPA from study hours
    

### Multiple Linear Regression

- **Use when**:
    
    - Multiple predictors (continuous and/or categorical)
        
- **Example**: Predict salary from education, experience, and gender
    

### Logistic Regression

- **Use when**:
    
    - Binary outcome variable
        
- **Example**: Predict pass/fail from attendance and study time
    

### Multinomial Logistic Regression

- **Use when**:
    
    - Categorical outcome with 3+ categories
        
- **Example**: Predict transport choice (car/bus/train)
    

---

## Non-Parametric Alternatives

_(Use when assumptions of parametric tests are violated)_

### Mann–Whitney U Test

- **Alternative to**: Independent _t_-test
    
- **Example**: Median income between two groups
    

### Wilcoxon Signed-Rank Test

- **Alternative to**: Paired _t_-test
    
- **Example**: Pre/post pain ratings
    

### Kruskal–Wallis Test

- **Alternative to**: One-way ANOVA
    
- **Example**: Satisfaction scores across 4 services
    

### Friedman Test

- **Alternative to**: Repeated Measures ANOVA
    
- **Example**: Rankings across conditions
    

---

## Categorical Data Analysis

### Chi-Square Test of Independence

- **Use when**:
    
    - Two categorical variables
        
- **Example**: Gender × voting preference
    

### Fisher’s Exact Test

- **Use when**:
    
    - Small sample sizes
        
- **Example**: Treatment success × failure (small N)
    

---

## Multivariate & Exploratory Methods

### Principal Component Analysis (PCA)

- **Use when**:
    
    - Reducing many correlated variables into fewer components
        
- **Example**: Socioeconomic status from income, education, occupation
    

### Factor Analysis

- **Use when**:
    
    - Identifying latent constructs
        
- **Example**: Personality traits from questionnaire items
    

### Cluster Analysis

- **Use when**:
    
    - Grouping observations based on similarity
        
- **Example**: Customer segmentation
    

### Discriminant Function Analysis

- **Use when**:
    
    - Predicting group membership from continuous predictors
        
- **Example**: Classifying species from physical measurements
    

---

## Mixed & Advanced Models

### ANCOVA

- **Use when**:
    
    - ANOVA + covariate(s)
        
- **Example**: Teaching method effect controlling for prior knowledge
    

### Mixed-Effects Models

- **Use when**:
    
    - Hierarchical or nested data
        
- **Example**: Students nested within classrooms
    

### Structural Equation Modeling (SEM)

- **Use when**:
    
    - Complex causal models with latent variables
        
- **Example**: Motivation → study behavior → achievement
    

---

## Summary Table (Rule of Thumb)

|Goal|Outcome|Groups|Method|
|---|---|---|---|
|Compare 2 groups|Continuous|2|t-test|
|Compare 3+ groups|Continuous|3+|ANOVA|
|Multiple outcomes|Continuous|Any|MANOVA|
|Predict outcome|Continuous|Any|Regression|
|Binary outcome|Binary|Any|Logistic Regression|
|Non-normal data|Continuous|Any|Non-parametric|

---

## Exam Tip

> **ANOVA = regression with categorical predictors**  
> **MANOVA = multiple ANOVAs analyzed together**

If you're unsure:

- Start with **regression logic**
    
- Count **dependent variables**
    
- Check **measurement scales**
    

---

_Suitable as a one-page exam reference or expandable Obsidian knowledge note._