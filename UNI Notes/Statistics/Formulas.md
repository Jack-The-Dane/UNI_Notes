## 1. Descriptive Statistics

- **Mean (Arithmetic Average)**  
    $$ \bar{x} = \frac{\sum_{i=1}^n x_i}{n} $$  
    where xix_ixi​ represents each value in the dataset and nnn is the number of observations.
    
- **Median**
    
    - If nnn is odd: the middle value.
    - If nnn is even: the average of the two middle values.
- **Mode**
    
    - The most frequently occurring value(s) in a dataset.
- **Range**  
    $$ \text{Range} = \text{Maximum value} - \text{Minimum value} $$
    
- **Variance**
    
    - For a sample:  
        $$ s^2 = \frac{\sum_{i=1}^n (x_i - \bar{x})^2}{n - 1} $$
    - For a population:  
        $$ \sigma^2 = \frac{\sum_{i=1}^N (x_i - \mu)^2}{N} $$
- **Standard Deviation**
    
    - For a sample:  
        $$ s = \sqrt{s^2} $$
    - For a population:  
        $$ \sigma = \sqrt{\sigma^2} $$
- **Coefficient of Variation (CV)**  
    $$ \text{CV} = \frac{\sigma}{\mu} \times 100\% $$
    

---

## 2. Probability

- **Probability of an Event AAA**  
    $$ P(A) = \frac{\text{Number of favorable outcomes}}{\text{Total number of possible outcomes}} $$
    
- **Addition Rule (for two events A and B)**  
    $$ P(A \cup B) = P(A) + P(B) - P(A \cap B) $$
    
- **Multiplication Rule (for two independent events A and B)**  
    $$ P(A \cap B) = P(A) \times P(B) $$
    
- **Conditional Probability**  
    $$ P(A|B) = \frac{P(A \cap B)}{P(B)}, \quad P(B) \neq 0 $$
    

---

## 3. Probability Distributions

- **Binomial Probability**  
    $$ P(X = k) = \binom{n}{k} p^k (1 - p)^{n - k} $$  
    where (nk)=n!k!(n−k)!\binom{n}{k} = \frac{n!}{k!(n - k)!}(kn​)=k!(n−k)!n!​, nnn is the number of trials, ppp is the probability of success, and kkk is the number of successes.
    
- **Poisson Probability**  
    $$ P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!} $$  
    where λ\lambdaλ is the average rate of occurrence, and kkk is the number of occurrences.
    
- **Normal Distribution (Probability Density Function)**  
    $$ f(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}} $$  
    where μ\muμ is the mean and σ\sigmaσ is the standard deviation.
    

---

## 4. Inferential Statistics

- **Z-score (Standard Score)**  
    $$ z = \frac{x - \mu}{\sigma} $$  
    where xxx is an individual value, μ\muμ is the mean, and σ\sigmaσ is the standard deviation.
    
- **Confidence Interval for the Mean (Normal Distribution, Known σ\sigmaσ)**  
    $$ \text{CI} = \bar{x} \pm Z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} $$
    
- **Confidence Interval for the Mean (t-Distribution, Unknown σ\sigmaσ)**  
    $$ \text{CI} = \bar{x} \pm t_{\alpha/2, n-1} \cdot \frac{s}{\sqrt{n}} $$
    
- **Margin of Error**
    
    - For population mean:  
        $$ \text{ME} = Z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} $$
    - For proportion:  
        $$ \text{ME} = Z_{\alpha/2} \cdot \sqrt{\frac{p(1 - p)}{n}} $$
- **Hypothesis Testing (t-test for Mean)**  
    $$ t = \frac{\bar{x} - \mu_0}{\frac{s}{\sqrt{n}}} $$
    

---

## 5. Correlation and Regression

- **Correlation Coefficient (Pearson)**  
    $$ r = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^n (x_i - \bar{x})^2 \sum_{i=1}^n (y_i - \bar{y})^2}} $$
    
- **Simple Linear Regression Equation**  
    $$ y = \beta_0 + \beta_1 x $$  
    where:  
    $$ \beta_1 = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2} $$  
    and  
    $$ \beta_0 = \bar{y} - \beta_1 \bar{x} $$