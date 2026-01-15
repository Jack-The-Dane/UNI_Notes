## Random Vector
$X = [x_1, x_2]^T$ 
### Simultaneous pdf (probability density function)
$$f(x_1,x_2) = P(X_1=x_1, X_2=x_2)$$

#### Marginal PDF's
$$f(x_1) = \int{f(x_1,x_2) dx_2}$$
or vice versa

#### Mean vector
$$\mu = (E[x_1], E[x_2])^T$$
#### Marginal variances
$$\sigma_1^2 = \sigma_{11} = E[X_1-\mu_1)^2] \ge 0$$
#### Covariance
$$\sigma_{12} = Cov(X_1,X_2) = E[(X_1-\mu_1)(X_2-\mu_2)$$
Can be positive/zero/negative
#### Covariance Matrix
$$\Sigma = \begin{bmatrix}
\sigma_{11} & \sigma_{12} \\
\sigma_{21} & \sigma_{22}
\end{bmatrix}$$
This matrix is symmetric and positive semi-definite

#### Correlation coefficient
$$\rho_{12} = \frac{\sigma_{12}}{\sigma_1 \sigma_2}$$
#### Correlation matrix
$$\rho = \begin{bmatrix}
1 & \rho_{12} \\
\rho_{21} & 1
\end{bmatrix}$$
#### Generalized variance
$$\vert \Sigma \vert = det(\Sigma) = \Pi^{2}_{i=1} \lambda_i$$
The measure of amount of random variance. Smaller values mean more ordered data (higher correlation, either positive or negative). 

# Extending to P dimensions
#### Mean vector
$$\mu = \begin{bmatrix}
\mu_1 \\
: \\
\mu_p
\end{bmatrix}$$
#### Covariance Matrix 
$$\Sigma = E[(X-\mu)(X-\mu)^T]$$
#### Correlation matrix
also extends