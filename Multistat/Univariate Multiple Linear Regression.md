## Model
$$Y = \beta_{0} + \beta_{1}z_{1} +\dots+\beta_{r}z_{r}+\epsilon$$
Matrix form:
$$Y = Z \beta + \epsilon$$
Y = Response variable, measured random
$z_{1}\dots z_{r}$ are predictor variables
$\beta_{0},\dots,\beta_{r}$  Are regression coeffs (Marginal slopes), they are unknown, but have a certain value (deterministic), which is what we are trying to find 
$\epsilon$ = error term, random

$$Y_{j} = \beta_{0} + \beta_{1} z_{j1} + \dots + \beta_{r}z_{jr} + \epsilon_{j}$$
Assumptions:
No distribution is assumed
Mean error is 0 ($E[\epsilon_{j}] = 0$)
Homoscedastisity is assumed ($V[\epsilon_{j}] = \sigma^2$ (constant))
$$
\begin{bmatrix}
Y_1 \\
Y_2 \\
: \\
Y_n
\end{bmatrix}
 = 
\begin{bmatrix}
1 & z_{11} & z_{12} & \dots & z_{1r} \\
1 &  &  &  &  \\
1 &  &  &  &  \\
1 &  &  &  & 
\end{bmatrix}
\begin{bmatrix}
\beta_0 \\
\beta_1 \\
: \\
\beta_r
\end{bmatrix}
+
\begin{bmatrix}
\epsilon_1 \\
\epsilon_2 \\
: \\
\epsilon_r
\end{bmatrix}
$$

## Least Squares optimization
Residuals:
$$\hat{\epsilon_{j}} = Y_{j} - \hat{Y}_{j} = Y_{j}-z_{j} \hat{\beta}$$
Sum of squared errors:
$$SSE = \sum_{j=1}^n \hat{\epsilon}_{j}^2 = \hat{\epsilon}^T\hat{\epsilon}$$
Minimize SSE:
$$\hat{\beta}_{LS} = (z^Tz)^{-1}z^TY$$
$(z^Tz)^{-1}z^T$ Is the pseudo-inverse

Fitted responses:
$$\hat{Y} = z \hat{\beta} = z(z^Tz)^{-1}z^T Y = HY$$
$z(z^Tz)^{-1}z^T$ Is the projection matrix $H$
Residuals:
$$\hat{\epsilon} = Y - \hat{Y} = (I-H)Y$$
## Moments
for $\hat{\beta}$
$$E[\hat{\beta}] = E[(z^Tz)^{-1}z^TY] = (z^Tz)^{-1}z^Tz \cdot \beta$$
This means that $\beta$ is unbiased
$$cov[\hat{\beta}] = (z^Tz)^{-1}z^T cov[Y] z(z^Tz)^{-1} = \sigma^2 (z^Tz)^{-1}$$

Estimate $\sigma^2$
$$\hat{\sigma}^2 = \frac{SSE}{df} = \frac{{\sum_{j=1}^n \hat{\epsilon}_{j}^2}}{df} = \frac{SSE}{n-(r+1)}$$
## Measure of model fit
$R^2$
$$\sum_{j=1}^n (Y_{j}-\hat{Y})^2 (SST) = \sum_{j=1}^n (Y_{j}-\hat{Y_{j}})^2 (SSE)+ \sum_{j=1}^n (\hat{Y_{j}}-\bar{Y})^2 (SSR)$$
$$R^2 = \frac{SSR}{SST} = 1 - \frac{SSE}{SST}$$
$$R^2_{adj} = 1 - \frac{\frac{SSE}{(n-(r+1)}}{\frac{SST}{(n-1)}}$$
For a good fit $R^2 \geq 75\%$

## Inference on beta
CR, CI's and $H_{0}$ tests
Assumption on distribution

$$\epsilon \sim N_{m}(0,\sigma^2 I)$$
$$Y \sim N_{m}(z\beta, \sigma^2I)$$
$$\hat{\beta} \sim N_{r+1}(\beta, \sigma^2(z^Tz)^{-1})$$
$$\hat{\sigma}^2 = \frac{SSE}{n-(r+1)} \sim \frac{\sigma^2}{n-(r+1)} \chi^2_{n-(r+1)}$$
## CR for beta
$$x \sim N_{p}\left( \mu, \Sigma \right) \rightarrow (x-\mu)^T \Sigma^{-1}(x-\mu) \sim \chi^2_{p}$$
$$\hat{\beta} \rightarrow (\hat{\beta}-\beta)^T \frac{z^Tz}{\sigma^2(r+1)}(\hat{\beta}-\beta) \sim \frac{\chi^2_{r+1}}{r+1}$$
$$\frac{\hat{\sigma}^2}{\sigma^2} = \frac{SSE}{\sigma^2(n-(r+1))} \sim \frac{1}{n-(r+1)} \chi^2_{n-(r+1)}$$$$(\hat{\beta}-\beta)^T \frac{z^Tz}{\hat{\sigma^2}(r+1)}(\hat{\beta}-\beta) \sim F_{r+1, n-(r+1)}$$
This is the test statistic for beta $\uparrow$
100(1-$\alpha$)% CR for $\beta$
$$(\hat{\beta}-\beta)^T \frac{z^Tz}{\hat{\sigma^2}(r+1)}(\hat{\beta}-\beta)  \leq F_{r+1, n-(r+1), \alpha}$$
## Bonferroni CI's (r+1 of them)
$$\hat{\beta_{i}} \pm t_{n-(r+1), \frac{\alpha}{2(r+1)}} \cdot \sqrt{ (\hat{\sigma^2}(z^Tz)^{-1})_{ii} } \hat{\beta_{i}}$$
$$(\hat{\beta}-\beta_{0})^T \frac{z^Tz}{\hat{\sigma^2}(r+1)}(\hat{\beta}-\beta_{0}) \leq F_{r+1, n-(r+1), \alpha}$$
## Model simplification
Can it be done with less predictor variables
$$ \beta = 
\begin{bmatrix}
\beta_(1) \\
\beta_(2)
\end{bmatrix}
$$
$\beta_{1}$ are the important beta variables
$\beta_{2}$ are beta variables that we think we might be able to remove, without making the model worse.
$$H_{0} : \beta_{(2)} =? 0$$
Extra Sum of Squares:
$$ESS(\beta_{(1)}\rightarrow \beta) = SSR(\beta) - SSR(\beta_{(1)}) = SSE(\beta_{(1)}) - SSE(\beta)$$
Test statistic:
$$F_{0} = \frac{\Delta SSR / (\Delta df)}{\hat{\sigma^2}} = \frac{SSR(\beta)-(SSR(\beta_{(1)}) / (r-q))}{\hat{\sigma^2}}$$
$$F_{0} \sim F_{r-q, n-(r+1)}$$
Reject $H_{0}$ when:
$$F_{0} \leq F_{r-q, n-(r+1), \alpha}$$
Special case $q = 0$: If this hypothesis is true, your model is not significant and does not make sense to use.

## Model check
Assumptions:
Variance is constant
Errors are independent
Errors are normally distributed

Do a check for multivariate normal distribution on errors
Check for independence and homoscedasticity
Plot the error for each variable, there shouldnt be any meaningful pattern
Plot the errors against their respective response variable, there again should not be a pattern. The magnitude of errors should not increase with amplitudes of response
