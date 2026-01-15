Using maximum likelihood estimation

Given n samples, iid and MVN distributed.
$H_{0}: \mu =? \mu_{0}$
$H_{1} \ne \mu_{0}$
Full model (unconstrained):
$$L(\mu,\Sigma) = P(\text{given obs:} \mu, \Sigma) = \Pi_{j=1}^pf(x_{i} \vert \mu_{i}, \Sigma_{i})$$
$H_{0}$ Model (constrained):
$$L_{0}(\mu=\mu_{0}, \Sigma) = P(\text{given obs:} \mu=\mu_{0}, \Sigma)$$
Likelihood Ratio:
$$\Lambda = \frac{\max L_{0}(\mu=\mu_{0}, \Sigma)}{\max L(\mu, \Sigma)}$$
If $\Lambda$ is close to 1, accept $H_{1}$
If $\Lambda$ is close to 0, accept $H_{0}$

$$\Lambda = \frac{\vert \hat \Sigma \vert }{\vert \hat \Sigma_{0} \vert}  = \frac{{1 \over n} \sum_{j=1}^{n}(X_j-\bar X)(X_j - \bar X)^T}{{1 \over n} \sum_{j=1}^{n}(X_j-\mu_{0})(X_j - \mu_{0})^T}$$

$$TS = -2\log{\Lambda} =\sim \chi^2_{df-df_{0}}$$
Reject $H_{0}$ if:
$$-2\log \Lambda \ge \chi^2_{p,\alpha}$$
