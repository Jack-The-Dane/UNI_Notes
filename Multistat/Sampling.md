## Data matrix
$$X \text{(Not population. Matrix of samples)} = \begin{bmatrix}
x_{11} & x_{12} & .. & x_{1p} \\
x_{21} & : & : & : \\
: & : & : & : \\
x_{n1} & .. & .. & x_{np}
\end{bmatrix} = \begin{bmatrix}
x_1^T \\
x_2^T \\
x_3^T \\
x_4^T
\end{bmatrix}$$
n points in p-dimensional space

# Descriptive statistics
### Estimation of moments (mean, variance, covariance)
#### 1st order moment (Mean)
$$\hat{\mu} = \bar{x} = {1 \over n} \sum_{j=1}^{n}x_j$$ 
#### 2nd order moment (Covariance)
$$\hat{\Sigma} = S = {1 \over n-1} \sum_{j=1}^{n}(x_j-\hat{\mu})(x_j-\hat{\mu})^T$$
Covariance values are difficult to interpret, only really useful for the sign of the covariance
#### Correlation Matrix
$$\hat{\rho} = R$$
Values of the correlation matrix should be $-1 \le r_{ij} \le 1$
