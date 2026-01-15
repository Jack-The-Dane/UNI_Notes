Large: $n \gg p$  (Based on Central Limit Theorem)
$$X \sim N_{p}(\mu, \Sigma) \rightarrow d^2(x,\mu) =(x-\mu)^T \Sigma^{-1}(x-\mu) \sim \chi^2_{p}$$
when $n \gg p$, due to to CLT:
$$(\bar{x}-\mu)^T \left( \frac{s}{n} \right)^{-1} (\bar{x} - \mu) \approx \sim \chi^2_{p}$$
Approximate large sample Confidence Interval
$$(\bar{x}-\mu)^T \left( \frac{s}{n} \right)^{-1} (\bar{x} - \mu) \le \chi^2_{p,\alpha}$$
Use chi2inv($1-\alpha, p$)
