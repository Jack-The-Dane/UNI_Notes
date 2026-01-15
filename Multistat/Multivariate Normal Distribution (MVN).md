## 1D
$$X \sim N(\mu, \sigma^2) $$
$\sim$ betyder "distributed over", så det her er X distribueret over en Normal distribution med gennemsnit $\mu$, og standart deviation $\sigma$.
$$f(x) \frac{1}{\sqrt{2\pi} \sigma} e^{-{1\over 2} \frac{(x-\mu)}{\sigma}^2} $$
### Standard Normal
$$Z \sim N(0,1)$$
$$f(z) = {1 \over \sqrt{2\pi}} e^{-{1 \over 2}z^2}$$
gennemsnit 0, std 1
## Multi dimensional (pD)
pD exponent:
$$-{1\over 2} (x - \mu)^T \Sigma^{-1}(x - \mu)$$
pdf:
$$f(x) = 2\pi ^{-p/2} \vert \Sigma \vert ^{1/2} e^{-{1\over2}(x-\mu)^T \Sigma^{-1}(x-\mu)} $$
### Notation
$$X \sim N_p(\mu, \Sigma)$$
gennemsnit $\mu$, covariance matrix $\Sigma$ 

## Constant Density Contours
$$(x-\mu)^T\Sigma^{-1}(x-\mu) = Constant = c $$
Dette er en formel på såkaldt "Quadratic form" $A^TBA$ . Den kan producere parabolas, hyperbolas, ellipses, afhængigt af matricen $B$.
$\Sigma$ er en positiv semidefinite matrix, med eigen værdier lig med eller over 0, så den vil altid producere ellipsoids. 
Når p=2, ellipses
Når p=3, ellipsoids
Når p>3, hyper-ellipsoids.

ellipserne vil være centreret omkring $x=\mu$, i p dimensioner.
Retningsvektorerne i ellipsen bestemmes af eigenvektorerne i $\Sigma$.
Half-axis length af retningsvektorerne bestemmes af eigenværdierne af $\Sigma$. -> $\sqrt{c}\sqrt{\lambda_i}, i=1,...,p$ 

### EVD
$$\Sigma = P \Lambda P^T$$
