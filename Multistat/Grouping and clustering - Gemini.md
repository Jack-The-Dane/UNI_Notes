## date: 2024-10-24 course: [[Multivariate Statistics]] tags: #lecture-notes #clustering #unsupervised-learning #masters #statistics topic: Grouping and clustering of multivariate observations lecture_no: 12

# Lecture 12: Grouping and Clustering

## 1. Introduction

**Context:** Up until now, we've mostly looked at supervised scenarios (regression, discriminant analysis). Today we move to **Unsupervised Learning**.

- **Input:** Data matrix $X$ ($n \times p$).
	
- **Missing:** No response vector $y$ (labels).
    
- **Goal:** Find natural groupings (clusters) in the data such that:
    
    1. **Homogeneity:** Observations _within_ a group are similar.
        
    2. **Separation:** Observations _between_ groups are dissimilar.
        

**Applications:**

- Customer segmentation (marketing).
    
- Genomic data (grouping genes with similar expression profiles).
    
- Image segmentation/compression.
    

## 2. Definition of Distances (Between Observations)

To group things, we need to quantify "similarity" or "dissimilarity" ($d_{ij}$).

### A. Continuous Variables

The standard approach is the **Minkowski metric** ($L_p$ norm):

$$d_{ij} = \left( \sum_{k=1}^p |x_{ik} - x_{jk}|^p \right)^{1/p}$$

- **Euclidean (**$p=2$**):** Standard geometric distance. Most common. $\sqrt{\sum (x_{ik} - x_{jk})^2}$.
    
- **Manhattan (**$p=1$**):** City block distance. Sum of absolute differences.
    

> [!WARNING] Importance of Standardization If variables have different units (e.g., Age in years vs. Income in \$), the variable with the larger variance/scale will dominate the Euclidean distance. **Solution:** Always standardize variables to $Z$-scores (mean 0, var 1) before clustering!

### B. Binary (Indicator) Variables

For categorical data turned into dummies ($0/1$). Let $a$ = number of variables where both $i$ and $j$ are 1. Let $b, c$ = mismatches ($0,1$ or $1,0$). Let $d$ = matches of $0,0$.

1. **Simple Matching Coefficient:** $(a+d) / p$. (Counts both presence and absence as similarities).
    
2. **Jaccard Distance:** Useful for sparse data (asymmetric binary). We don't care if both lack a feature (0-0 matches).
    
    $$D_{Jaccard} = 1 - \frac{a}{a+b+c}$$

### C. Distance Between Variables

Sometimes we want to cluster columns, not rows.

- **Correlation Distance:** $d_{jk} = 1 - r_{jk}$ (or $1 - |r_{jk}|$).
    
- If two variables are highly correlated, distance is close to 0.
    

## 3. Distances Between Clusters (Linkage Metrics)

Once we have distances between points, how do we measure distance between _groups_ of points ($C_1$ and $C_2$)?

| Method               | Definition                                              | Pros/Cons                                                                              |
| -------------------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Single Linkage**   | $d(C_1, C_2) = \min_{i \in C_1, j \in C_2} d_{ij}$      | Nearest neighbors. **Con:** "Chaining" effect (long, stringy clusters).                |
| **Complete Linkage** | $d(C_1, C_2) = \max_{i \in C_1, j \in C_2} d_{ij}$      | Farthest neighbors. **Con:** Sensitive to outliers; tends to force spherical clusters. |
| **Average Linkage**  | Average of all pairwise distances.                      | Robust balance between single and complete.                                            |
| **Ward's Method**    | Minimize the increase in within-cluster variance (ESS). | very popular; produces compact, even-sized clusters.                                   |
| Centroid Linkage     | $d(C1​,C2​)=∣∣\bar{x1}​−\bar{x2}​∣∣$                    | Distance between centroids of clusters                                                 |

> [!EXAMPLE] DEMO: Inter-cluster Linkage Calculation **Scenario:** Cluster A = $\{P_1(0), P_2(2)\}$ Cluster B = $\{P_3(5)\}$ (1D points for simplicity)
> 
> - **Single Linkage:**
>     
>     - Dist($P_1, P_3$) = 5
>         
>     - Dist($P_2, P_3$) = 3
>         
>     - **Result:** $\min(5, 3) = 3$
>         
> - **Complete Linkage:**
>     
>     - **Result:** $\max(5, 3) = 5$
>         
> - **Average Linkage:**
>     
>     - $(5 + 3) / 2 = 4$
>         

## 4. Motivation: Search Algorithms

Why do we need heuristics?

- Total number of ways to partition $n$ items into $k$ clusters follows Stirling numbers of the second kind.
    
- For $n=25$ and $k=5$, there are $\approx 2.4 \times 10^{15}$ possibilities.
    
- **Conclusion:** Brute force is impossible. We need greedy algorithms (Hierarchical) or iterative optimization (K-means).

## 5. Hierarchical Clustering

**Approach:** Agglomerative (Bottom-up). **Input:** Distance Matrix $D$ ($n \times n$).

**Algorithm:**

1. Start with $n$ clusters (each observation is a cluster).
    
2. Find the pair with the smallest distance in $D$.
    
3. Merge them.
    
4. Update $D$ using the Linkage Metric (calculate distance from new merged group to all old groups).
    
5. Repeat until 1 cluster remains.
    

**Visualization:** [[Dendrogram]]. Height of the bar = distance at which merge occurred.

> [!EXAMPLE] DEMO: Hierarchical Clustering Steps **Data Matrix D (Initial):** | | A | B | C | |---|---|---|---| | **A** | 0 | 2 | 6 | | **B** | 2 | 0 | 5 | | **C** | 6 | 5 | 0 |
> 
> **Step 1:** Find min dist. It's $d(A,B) = 2$. **Step 2:** Merge $\{A, B\}$. New cluster is $(AB)$. **Step 3:** Update Distances (Using **Single Linkage**).
> 
> - $d((AB), C) = \min( d(A,C), d(B,C) )$
>     
> - $d((AB), C) = \min( 6, 5 ) = 5$
>     
> 
> **New Matrix:** | | (AB) | C | |---|---|---| | **(AB)**| 0 | 5 | | **C** | 5 | 0 |
> 
> **Step 4:** Merge $((AB), C)$ at height 5. Done.

## 6. Non-Hierarchical Clustering (K-Means)

**Approach:** Partitioning. **Input:** Data Matrix $X$ (raw data), and usually prespecified $K$.

**Algorithm (Lloyd's):**

1. Randomly initialize $K$ centroids.
    
2. **Assignment:** Assign each observation to the nearest centroid (Euclidean distance).
    
3. **Update:** Recalculate centroids (mean of points in the cluster).
    
4. Repeat 2-3 until convergence (centroids stop moving).
    

**Objective Function:** Minimize Within-Cluster Sum of Squares (WCSS).

> [!EXAMPLE] DEMO: K-Means in Python (Conceptual)
> 
> ```
> from sklearn.cluster import KMeans
> import matplotlib.pyplot as plt
> ```

> # Data X: Two distinct blobs
> 
> model = KMeans(n_clusters=2, init='random') model.fit(X)

> # Visualizing the steps:
> 
> # Iteration 1: Centroids are random, partition is messy.
> 
> # Iteration 2: Centroids jump to the center of the mess.
> 
> # Iteration 3: Boundaries adjust.
> 
> # Final: Centroids sit perfectly in the center of the blobs.
> 
> ```
> 
> *Note: K-means assumes clusters are spherical and roughly equal size.*
> ```

## 7. Gaussian Mixture Models (GMM)

**Idea:** K-Means is a "hard" assignment ($x_i$ belongs to $k$). GMM is "soft" (probabilistic). Assume the data is generated by a mixture of $K$ Multivariate Gaussian distributions.

**Parameters per cluster** $k$**:**

1. Mean vector $\mu_k$ (center).
    
2. Covariance matrix $\Sigma_k$ (shape/orientation).
    
3. Mixing probability $\pi_k$ (size).
    

**Algorithm:** Expectation-Maximization (EM).

1. **E-step:** Calculate "responsibilities" (probability that $x_i$ belongs to $k$).
    
2. **M-step:** Update $\mu_k, \Sigma_k, \pi_k$ based on weighted data.
    

> [!EXAMPLE] DEMO: GMM vs K-Means **Scenario:** Data shaped like a stretched oval (ellipsoid).
> 
> - **K-Means:** Will try to fit a circle. It might cut the oval in half if it's too long. Fails to capture the variance structure.
>     
> - **GMM:** Learns the Covariance Matrix $\Sigma$. It adapts the "shape" of the cluster to match the oval.
>     
> - **Result:** GMM fits the data density much better than K-Means for non-spherical clusters.
>     

**MAP Assignment:** To turn soft probabilities into hard clusters for final reporting:

$$C(x_i) = \text{argmax}_k P(C_k | x_i)$$

## 8. Multidimensional Scaling (MDS)

**Problem:** We have high-dimensional data ($p=100$) or just a distance matrix. We can't see the clusters. **Goal:** Map points to 2D or 3D such that the distances in the plot preserve the original distances in $D$ as well as possible.

**Stress Function:** Measures the error between original distances $\delta_{ij}$ and plotted distances $d_{ij}$.

$$Stress = \sqrt{\frac{\sum (d_{ij} - \delta_{ij})^2}{\sum \delta_{ij}^2}}$$

> [!EXAMPLE] DEMO: MDS Visualization Imagine a dataset of distinct cities. We only have the "Flight Time" matrix (Distance).
> 
> 1. **Input:** $D$ (Flight times between London, NY, Tokyo, etc.).
>     
> 2. **MDS Algorithm:** Tries to arrange points on a 2D sheet.
>     
> 3. **Output:** A map where cities close in flight time are physically close.
>     
> 
> _Use in Clustering:_ Run K-means on the full $p$-dimensional data, then project to 2D using MDS to visualize if the clusters look well-separated.

**Summary:**

1. Standardize data first!
    
2. Hierarchical = good for visualization (dendrogram), bad for large $N$.
    
3. K-Means = fast, simple, but assumes spheres.
    
4. GMM = flexible covariance, probabilistic.