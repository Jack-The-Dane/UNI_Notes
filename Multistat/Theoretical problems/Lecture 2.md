## Problem 2.3
![[Pasted image 20250917203829.png]]
$$X = \begin{bmatrix}
X_1 \\
X_2
\end{bmatrix}$$
$$X \sim \mathcal{N} \left( \mu = \begin{bmatrix}
\mu_1 \\
\mu_2
\end{bmatrix}, \Sigma = \begin{bmatrix}
\sigma_1^2 & \sigma_{12} \\
\sigma_{12} & \sigma_2^2
\end{bmatrix} \right)$$
PDF:
$$f_X(x) = \frac{1}{2 \pi \sqrt{\sigma_1^2 \sigma_2^2 - \sigma_{12}^2}} \cdot \exp \left( -\frac{1}{2} \frac{\sigma_2^2(x_1-\mu_1)^2 - 2 \sigma_{12}(x_1-\mu_1)(x_2 - \mu_2) + \sigma_1^2(x_2 - \mu_2)^2}{\sigma_1^2 \sigma_2^2 - \sigma_{12}^2} \right)$$
Mahalanobis quadratic form:
$$d_M^2(x, \mu) = (x-\mu)^T \Sigma^{-1}(x-\mu)$$
$$d_M^2(x, \mu) = x_{1}\,\left(\overline{x_{1}}-\overline{x_{2}}+3\right)-\left(x_{2}-3\right)\,\left(\overline{x_{1}}-2\,\overline{x_{2}}+6\right)$$
$$d_M^2(x, \mu) = 3\,x_{1}+{\left|x_{1}\right|}^2-x_{1}\,\overline{x_{2}}-\frac{\left(x_{2}-3\right)\,\left(-2\,{\left|x_{2}\right|}^2+6\,x_{2}+x_{2}\,\overline{x_{1}}\right)}{x_{2}}$$
50% confidence ellipsis:
$$d_M^2(x, \mu) = (x-\mu)^T \Sigma^{-1}(x-\mu) \leq \chi^2_{p, \alpha}$$
$$3\,x_{1}+{\left|x_{1}\right|}^2-x_{1}\,\overline{x_{2}}-\frac{\left(x_{2}-3\right)\,\left(-2\,{\left|x_{2}\right|}^2+6\,x_{2}+x_{2}\,\overline{x_{1}}\right)}{x_{2}} \le \chi^2_{p,0.5}$$