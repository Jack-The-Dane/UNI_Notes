Observations $X_1, X_2 ... X_n$ iid, $X_j \sim N_p(\mu, \Sigma)$

## Maximum likelihood estimation
likelihood function (gives PDF values)
$$L(\mu, \Sigma) = 'P(\text{Given obs}\vert \mu, \Sigma)'$$
We want to maximise this function:
$$\hat \mu_{ML} = \bar X = {1 \over n} \sum_{j=1}^{n}{x_j} \sim N_p(\mu, {\Sigma \over n}) \text{   Obtained by mean(X) in Matlab} $$
$$\hat \Sigma_{ML} = {1 \over n} \sum_{j=1}^{n}(X_j-\bar X)(X_j - \bar X)^T$$
$$S = \hat \Sigma = {1 \over n-1} \sum_{j=1}^{n}(X_j-\bar X)(X_j - \bar X)^T \text{ Obtained by cov(X) in Matlab}$$
$$E[S] = \Sigma$$

