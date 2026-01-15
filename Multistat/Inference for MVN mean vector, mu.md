$\mu$ is unknown.
# Hypothesis testing
## Model (samples)
$$X_n, ..., X_n \text{ iid (independently identically distributed) } X_j \sim N_p(\mu, \Sigma) \text{ (both unknown)} $$
Perform model check: Scattermatrix and Mahalanobis QQ plot

## Hypothesis (what you want to find out)
$$\text{Null hypothesis: } H_0: \mu = \mu_0$$
Where $\mu_0$ is your postulated mean.
Otherwise:
$$H_1 : \mu \neq \mu_0$$
This is a two sided hypothesis.

## Test statistics
### Step 1 - Estimation of unknown parameters
$\mu$ and $\Sigma$ 
See [Estimation of MVN Parameters](/home/jacob/shared/Obsidian_notes/UNI Notes/Multistat/Estimation of MVN parameters.md)

### Step 2 - Make test statistic (t)
$$1D : t = \frac{\bar{x}- \mu_0}{s/\sqrt{n}} \sim t_{n-1}$$
$$P_D : t^2 = (\bar{x} - \mu_0) \frac{1}{s/n}-(\bar{x} - \mu_0) \sim F_{1,n-1}$$
Hotelling
$$T^2 = (\bar{x} - \mu_0)^T \left({S \over n} \right)^{-1} (\bar{x} - \mu_0)$$
If the sample mean is close to $\mu_0$, you will have a small $T^2$, meaning accept the null hypothesis. Otherwise accept $H_1$.
### Step 3 - Test
$$T_0^2 \rightarrow t_0^2$$
Where $t_0^2$ is your data from before.
Test using TS PDF, using the Fischer distribution $F_{p,n-p}$ , choose an $\alpha$, and use Matlab with $finv(1-\alpha, p, n-p)$
$\alpha$ should probably be either 0.01, 0.05 or 0.10.
*IFF*   $t_0^2 \gt {P(n-1) \over n-P} F_{p,n-p,\alpha}$ reject $H_0$

#### OR Calculate p-value
$$p-value = 1-P(F_{p,n-p} \lt \frac{n-p}{p(n-1)} t_0^2)$$
Use fcdf($\frac{n-p}{p(n-1)} t_0^2$, p, n-p)
if the p-value is low -> reject $H_0$ 
"low" p-value means to compare with an $\alpha$ level, if p $\lt \alpha$ reject $H_0$, otherwise accept $H_1$

# Confidence Region
When in many dimensions, you will have a region instead of an interval.
Region will be in $\mathcal{R}^p$.
$100(1-\alpha)\% CR:$:
$$(\bar{x} - \mu_0)^T \left({S \over n} \right)^{-1} (\bar{x} - \mu_0) \le \frac{n-p}{p(n-1)} F_{p,n-pm, \alpha}$$
This will give a hyper-ellipsoid in P dimensions
# Confidence Intervals
For $\mu$ variables, $\mu_i$, $i=1,...,p$
## Marginal CI's
For $\mu_i$, $i=1,...,p$ 
$$CI_i = \bar{x}_i \pm t_{n-1,\alpha/2} \sqrt{s_i^2 \over n} $$
This has a problem: The overall confidence becomes too low.
If the confidence in all dimensions individually equals 95%, then the overall confidence will be $(1-\alpha)^p$, which is lower than we want.
## Bonferroni CI
For $\mu_i$, $i=1,...,p$ 
when $\alpha \ll 1$:
$$(1-\alpha)^p \approx= 1-\alpha p$$
Choose $\alpha_b = {\alpha \over p}$
$$(1-\alpha_b)^p \approx= 1-\alpha_b p = 1- \alpha$$
$$CI_i = \bar{x}_i \pm t_{n-1,{\alpha /2p}} \sqrt{s_i^2 \over n}$$
## Simultaneous CI's
$$CI_i = \bar{x}_i \pm \sqrt{{P(n-1) \over n-P} F_{p,n-p,\alpha}} \sqrt{s_i^2 \over n}$$


