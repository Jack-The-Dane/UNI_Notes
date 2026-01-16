One-factor multivariate analysis of variance
## Model 
Model with MVN populations: $l=1,\dots,g$
Populations are separated by one factor, the index
All populations should have roughly the same number of observations
Can be used to test several different ways to accomplish the same thing. So can test a new method against all the old methods at once.

## Assumptions
All observations come from multi-variable normally distributed populations.
$$X_{lj} \sim N_{p}(\mu_{l}, \Sigma_{l})$$
We assume homoscedacicity, so:
$$\Sigma_{1} = \Sigma_{2}=\Sigma_{g}$$
Means:
$$\mu_{l} = \mu_{overall} + \tau_{l}$$
$\tau_{l}$ is called the factor effect.

## Hypotheses
$H_{0}$: No factor effect, all means are the same.
$H_{1}$: Significant factor effect, some $\mu_{l}$ is different

### Sample means
Overall:
$$\bar{x} = \frac{1}{n}  $$
## Decomposition ("sum of squares")
$$(X_{lj} - \bar{X}) = (X_{lj}-\bar{X_{l}}) + (X_{l}-\bar{X})$$
SSTotal:
$$\sum_{l=1}^{g} \sum_{j=1}^n (X_{lj}-\bar{X})(X_{lj}-\bar{X})^T = \sum_{l=1}^{g} \sum_{j=1}^n (X_{lj}-\bar{X}_{l})(X_{lj}-\bar{X}_{l})^T + \sum_{l=1}^{g} \sum_{j=1}^n (X_{l}-\bar{X})(X_{l}-\bar{X})^T$$
Left of plus is called SSWithin (Difference between samples and their population mean), right of plus is called SSBetween (Difference between population means and overall mean)

## MANOVA TABEL
$$\begin{bmatrix}
\text{Variation} & SS & df & \hat{\Sigma} \\
\text{between} & SSB & g-1 & S_B = SSB/(g-1) \\
\text{Within} & SSW & n-g & S_W = SSW/(n-g) \\
\text{Total} & SST & n-1 & S_T = SST/(n-1)
\end{bmatrix}$$See MANOVA 1 pdf

### Accept H_0
Model:
$$x_{lj} \sim N_{P}(\mu_{l}, \Sigma)$$
$$\hat{\mu}=\bar{X}$$
$$\hat{\Sigma} = S_{T}$$
### Reject H_0
Model:
$$X_{lj} \sim N_{p}(\mu_{l}, \Sigma)$$
$$\hat{\mu_{l}} = \bar{X_{l}}$$
$$\hat{\Sigma} = S_{W}$$
## Pairwise CI
Between populations $k$ and $l$, variable $i$
To check which population is significantly different, and what variable in that population
CI:
$$\left[ (\bar{X}_{ki}  - \bar{X}_{li}) \pm t_{n-g,{\frac{\alpha}{pg(g-1)}}} \cdot \sqrt{ {\frac{1}{n_{k}}+{\frac{1}{nl}}} } \sqrt{ S_{W,ii} }\right]$$
Number of CI's:
$$\frac{1}{2}g(g-1)p$$If the interval contains zero, it is not significant.

## Model check
Need to check each population separately
Bartlett test for $H_{0}$ (Are all $\Sigma$ the same?)

### Likelihood ratio test statistic
$$LRTS = (n-g)\log(\vert S_{P} \vert)- \sum_{l=1}^g(n_{l}-1)\log(\vert S_{l}\vert)$$
Finite pop correction
$$c=1- \frac{2p^2+3p-1}{6(p+1)(g-1)} \left( \Sigma_{l=1}^g {\frac{1}{n_{l-1}}-{\frac{1}{n-g}}} \right)$$
$$T=c\cdot LRTS \sim \chi^2_{df-df_{0}}$$
Full model: all sigmas are different (g covariance matrices)
H0 model: all sigmas are same (1 covariance matrix)
With
$$p{\frac{p+1}{2}}$$
Unique elements in $\Sigma$
And this number of degrees of freedom in T formula:
$$df-df_{0} = (g-1){\frac{p(p+1)}{2}}$$