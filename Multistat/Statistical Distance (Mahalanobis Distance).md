$$d_M^2(x, \mu) = (x-\mu)^T \Sigma^{-1}(x-\mu)$$
Squared distance between $x$ and $\mu$ 
Denne distance er anderledes end den geometriske distance (euklidisk).
Man kan se det som, at jo kortere distancen er mellem en observering og middelværdien, jo mere sandsynlig er observeringen.
![[Pasted image 20250911130414.png]]
C er tættere på A, end B.
#### Fordeling af mahalanobis distancer
$$X \sim N_P(\mu, \Sigma) \leftrightarrow d_M^2(x, \mu) \sim \chi^2 $$

#### 100(1-$\alpha$)% Confidence Region of observations
$$d_M^2(x, \mu) = (x-\mu)^T \Sigma^{-1}(x-\mu) \leq \chi^2_{p, \alpha}$$