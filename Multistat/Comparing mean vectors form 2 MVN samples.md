## Paired test
Requires each test object split in 2 parts
Uses the same test population for both test scenarios. This is the best way to do it, if possible.

### Pairwise observations
$$(X_{1j}, X_{2j},\ j=1,\dots ,n)$$
$$X_{1j} \sim N_{p}(\mu_{1}, \Sigma_{1})$$
$$X_{2j} \sim N_{p}(\mu_{2}, \Sigma_{2})$$
#### Difference model
$$D_{j} = X_{1j} - X_{2j} \sim N_{p}(\mu_{1}-\mu_{2}, \Sigma_{d})$$

#### Hypothesis testing
$H_{0}$: 
$$\delta = \mu_{1} - \mu_{2} =? \ \delta_{0} \text{ (often zero)}$$
$H_{1}$: $\delta \neq \delta_{0}$
#### Estimates
$$\hat{\mu_{1}-\mu_{2}} = \bar{D} = \frac{1}{n} \sum_{j=1}^{n} \sim N_{p}\left( \mu_{1}-\mu_{2}, \frac{\Sigma_{d}}{n} \right)$$
$$\Sigma_{d} = S_{d} = \frac{1}{n-1} \sum_{j=1}^{n} (D_{j}-\bar{D})(D_{j}-\bar{D})^T$$
### Hotelling T² Test Statistic
$$T^2 = (\bar{D} - (\mu_{1} - \mu_{2}))^T \frac{S_{d}}{n}^{-1}(\bar{D}-(\mu_{1}-\mu_{2})) \sim \frac{p(n-1)}{n-p} F_{p,n-p}$$
#### Test
$$T^2_{0} = (\bar{D}-\delta_{0})^T\frac{S_{d}}{n}^{-1}(\bar{D}- \delta_{0}) \sim \frac{p(n-1)}{n-p} F_{p,n-p}$$

Reject $H_{0}$ IFF:
$$t^2_{0} \gt \frac{p(n-1)}{n-p} F_{p,n-p, \alpha}$$
P-value:
$$P = P(\frac{p(n-1)}{n-p} F_{p,n-p, \alpha} \gt t_{0}^2)$$
### Confidence region
$100(1-\alpha)\%$ CR for $\mu_{1}-\mu_{2}$
$$T^2 \le \frac{p(n-1)}{n-p} F_{p,n-p, \alpha}$$

### Confidence Intervals
### Bonferroni CI
$$ i,\dots, p:\ \ \ \ \left[ \bar{D_{i}} \pm t_{n-1, \frac{\alpha}{2p}} \cdot \sqrt{ S_{\frac{D_{jii}}{n}} } \right] \text{THIS IS AN INTERVAL}$$
THIS IS AN INTERVAL, - FOR LOWER VALUE, + FOR UPPER VALUE

## Non-paired
Always possible
$$X_{1j} \sim N_{p}(\mu_{1}, \Sigma_{1}), j= 1,\dots, n_{1}$$
$$X_{2j} \sim N_{p}(\mu_{2}, \Sigma_2), j=1,...,n_{2}$$
The two samples dont need to have the same number of samples, but they should be balanced
### Hypothesis
Same as with paired

### Estimates
$$\hat{\mu_{1}} = \bar{X_{1}} \sim N_{p}(\mu_{1}, \Sigma_{1})$$
$$\hat{\mu_{2}} = \bar{X_{2}} \sim N_{p}(\mu_{2}, \Sigma_{2})$$
### Estimation of Sigma
#### Case 1 - Homoscedasticity
$$\Sigma_{1} = \Sigma_{2}$$
Test with Bartlett test (comes later)
$$S_{1} = \frac{1}{n-1} \sum (X_{1j} - \bar{X_{1}})(X_{1j} - \bar{X_{1}})^T$$
$$S_{2} = \text{ Same but with 2}$$
Pooled estimate:
$$\hat{\Sigma} =S_{p} = \frac{ (n_{1}-1)S_{1}+(n_{2}-1)S_{2}}{n_{1}+n_{2}-2}$$
##### Hotelling T² Test Statistic
$$T^2 = ((X_{1}-X_{2}) - (\mu_{1}-\mu_{2}))^T \left[ S_{p} \left( \frac{1}{n_{1}}  + \frac{1}{n_{2}} \right) \right] ^{-1} ((\bar{X_{1}} - \bar{X_{2}})-(\mu_{1}-\mu_{2})) \sim \frac{p(n_{1}+n_{2}-2)}{n_{1}+n_{2}-p-1} F_{p,n_{1}+n_{2}-p-1}$$
##### Test
Reject $H_{0}$ IFF: 
$$t^2_{0} \gt \frac{p(n_{1}+n_{2}-2)}{n_{1}+n_{2}-p-1} F_{p,n_{1}+n_{2}-p-1, \alpha}$$
##### Confidence region
$$T^2 \le \frac{p(n_{1}+n_{2}-2)}{n_{1}+n_{2}-p-1} F_{p,n_{1}+n_{2}-p-1, \alpha}$$
##### Bonferroni Confidence Interval
$$\left[ \bar{X_{1i}} - \bar{X_{2i}} \pm t_{n-1, \frac{\alpha}{2p}} \cdot  \sqrt{ S_{pi i }\left( \frac{1}{n_{1}} + \frac{1}{n_{2}} \right) } \right]$$



#### Case 2
$$\Sigma_{1} \ne \Sigma_{2}$$
Only large sample approximation is possible
$$n_{1}, n_{2} \gg p$$
##### Test Stat
$$T^2 = ((\bar{X_{1}} - \bar{X_{2}} ) - (\mu_{1} - \mu_{2}) )^T \left(  \frac{S_{1}}{n_{1}} + \frac{S_{2}}{n_{2}} \right) ^{-1} ((\bar{X_{1}} - \bar{X_{2}}) - (\mu_{1}-\mu_{2}))$$
$$T^2 \sim \chi^2_{p}$$
With that info you can do tests, Confidence region and Confidence interval

### Bartlett test (Box's M-test)
Test for Homoscedasticity
$$X_{1j} \sim N_{p}(\mu_{1}, \Sigma_{1})$$
$$X_{2j} \sim N_{p}(\mu_{2}, \Sigma_{2})$$
$H_{0}$:
$$\Sigma_{1} =? \Sigma_{2}$$
$H_{1}$:
$$\Sigma_{1} \ne \Sigma_{2}$$
#### Full model
$$\Sigma_{1} \ne \Sigma_{2}$$
Likelihood function: 
$$L(\Sigma_{1}, \Sigma_{2})$$
#### Constrained model
$$\Sigma_{1} = \Sigma_{2}$$
Likelihood function:
$$L_{H_{0}}(\Sigma)$$
#### Likelihood ratio
$$\Lambda = \frac{max(\Sigma) L_{H_{0}}(\Sigma)}{max(\Sigma_{1},\Sigma_{2})L(\Sigma_{1}, \Sigma_{2})}$$
$$0 \le \Lambda \le 1$$
$$-2\log(\Lambda) = (n_{1}-n_{2}-2)\log(\det(S_{p}))-(n_{1}-1)\log(\det(S_{1})) - (n_{2}-1)\log(\det(S_{2}))$$
Finite Population Correction
$$C = 1 - $$
