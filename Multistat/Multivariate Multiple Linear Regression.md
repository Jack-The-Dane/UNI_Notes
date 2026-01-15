- Vector response (Multiple responses, Y vector)
- Common set of predictor variables, z's
Response variable:
$$Y_{i} = \beta_{0i}+ \beta_{1i}z_{1} + \dots + \beta_{ri}z_{i} + \epsilon_{i}$$
Observation:
$$Y_{ji} = \beta_{0i}+ \beta_{1i}z_{ji} + \dots + \beta_{ri}z_{jr} + \epsilon_{ji}$$

General model:
$$Y = Z \beta + \epsilon$$
## Assumptions on errors:
$$E[\epsilon_{ji}] = 0$$
(Mean error is zero)

Error vectors are independent between observations, but might be correlated within each error vector. (Row vector in error matrix)
Covariance between all error vectors should be constant, and covariance matrix is $m\cdot m$

## Estimate beta
Again estimated by Least Squares, but now $\beta$ is a matrix
$$\beta_{LS} = (z^Tz)^{-1}z^TY$$
Fitted observations:
$$\hat{Y} = z \hat{\beta} = z(z^Tz)^{-1}z^T Y = HY$$
Residuals (estimated errors):
$$\hat{\epsilon} = Y - \hat{Y}$$
"Sum of Squares" decomposition:
$$(Y - \bar{Y})^T(Y - \bar{Y}) (SST) = \hat{\epsilon}^T\hat{\epsilon} (SSE) + (\hat{Y} - \bar{Y})^T(\hat{Y} - \bar{Y}) (SSRegression)$$
SSE elements should be small compared to the others for a good fit
$$\hat{\Sigma} = \frac{SSE}{df} = \frac{SSE}{n-(r+1)}$$
## Moments for beta
$$E[\hat{\beta}] = \beta$$
(Unbiased)
$$Cov(\beta(:,i)) = \sigma^2_{i}(z^Tz)^{-1}$$
## Inference on estimates
**New Assumption on error:** 
Errors:
$$\epsilon(j,:) \sim N_{m}(0, \Sigma)$$
(Sigma constant)
$$Y(j,:) \sim N_{m}(Z\beta, \Sigma)$$
$$\beta(:,i) \sim N_{r+1}(\beta(:,i), \sigma^2_{i}(z^Tz)^{-1})$$
## Model check
MVN model check for residual vectors
$$\hat{\epsilon}(j,:)$$
There are n of them, do scatter matrix and mahalanobis QQ-plot for each

Univariate check for $\hat{\epsilon}(:,i)$
- Check for independence
- Check for constant variance
Must be done m times (Once for each variable)

## Inference for beta(:,i)
like UMLR:
- CR for $\beta$
- Bonferroni CI's
- Model simplification

## Simultaneous Check for Model Simplification
Can we remove some predictor variables, without making the model worse?

Same as univariate, split up beta matrix:
$$\beta = \begin{bmatrix}
\beta_1 \\
\beta_2
\end{bmatrix}$$

Cant do exact test, due to matrices, so we use Likelihood Ratio principle

Calculate SSE for both full model and reduced model

$$\hat{\Sigma}_{ML} = \frac{\hat{\epsilon}^T\hat{\epsilon}}{n}$$
$$\hat{\Sigma}_{ML, reduced} = \frac{\hat{\epsilon}_{reduced}^T\hat{\epsilon}_{reduced}}{n}$$
Then compare the two covariance matrices. If they contain almost the same values, we can believe that the reduced model is accurate.
Likelihood ratio test:
$$\Lambda = \left( \frac{\vert \hat{\Sigma}_{ML} \vert}{\vert \hat{\Sigma}_{ML, reduced} \vert} \right)^{n/2}$$
If $\Lambda$ is close to 0, reject model simplification.
If it is close to 1, accept simplification (or whatever the hypothesis is)

### Large sample approximate result
$$ -2\log \Lambda = -n\log\left( \frac{\vert \hat{\Sigma}_{ML} \vert}{\vert \hat{\Sigma}_{ML, reduced} \vert} \right) \sim \chi^2_{df-df_{reduced}}$$
(approximately distributed)
A small improvement could be made:
$$-(n-(r+1)-\frac{m-r+q+1}{2})\log\left( \frac{\vert \hat{\Sigma}_{ML} \vert}{\vert \hat{\Sigma}_{ML, reduced} \vert} \right) \sim \chi^2_{m(r-q)}$$
