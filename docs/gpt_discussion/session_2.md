# Summary of Session 2: Customer Analysis

## Continued Discussion on Customer Analysis

We built upon our previous discussions, focusing particularly on Steps 2 and 3 of Customer Analysis, which involve segmentation and targeting strategies to better understand and cater to the customer base.

### Step 2: Segmentation

#### Understanding the Need for Segmentation
- We recognized that customer needs are heterogeneous and vary widely, necessitating the grouping of customers with similar needs into segments. This approach helps in addressing the specific needs of each group effectively.
- Segmentation involves collecting and analyzing data on customer needs, behaviors, and attitudes. Methods like surveys are traditionally used to gather this data, but more recent approaches include analyzing large-scale behavioral data, provided it is validated accurately.

#### Cluster Analysis
- Cluster analysis is employed to handle scenarios with numerous base variables where simple segmentation is not feasible. It helps in identifying a manageable number of distinct segments by grouping consumers based on similarity in their needs and behaviors.
- The process starts by calculating the distance between each pair of individuals, grouping those that are closest into the same segment. We use various criteria, including managerial judgment and statistical tools like the Elbow plot, to decide the optimal number of segments.

#### Descriptor Variables
- Once segments are defined, we characterize them using descriptor variables which include demographics and other relevant information. For instance, data from social media platforms like Twitter can provide insights into demographics and user engagement levels.
- Understanding these descriptors is crucial for crafting targeted marketing strategies that are tailored to the specific characteristics and preferences of each segment.

### Step 3: Targeting

#### Selection of Target Segments
- The targeting step involves deciding which of the previously identified segments to focus on. This decision is influenced by internal factors and is inherently subjective, often requiring input from both marketing and non-marketing team members.
- We evaluate segments based on several factors including their size, profitability, and growth potential. This helps in assessing the attractiveness of each segment to the firm.

#### Multifactor Targeting Model
- To systematically evaluate and select target segments, we use the Multifactor Targeting Model. This model scores each segment based on its attractiveness and the firm’s ability to serve it, integrating these scores into a comprehensive decision matrix.
- The model reduces subjectivity in segment selection, employing methodologies like the Delphi method to gather consensus among experts.

### Case Study Discussion: Chase Sapphire

#### Overview of the Case
- The discussion revolved around Chase Sapphire's strategy to target affluent and savvy customers, initially with its regular card and subsequently with the Reserve card aimed at younger customers.
- It was important to understand why Chase chose to target this particular group, especially given their lower market share compared to competitors like Amex and the specific spending habits of the target group.

#### Key Takeaways
- The case highlighted the importance of aligning targeting strategies with overall business goals and the potential benefits of focusing on customers who are likely to use multiple products.
- We also considered the economic implications of targeting customers who are typically "transactors," emphasizing the need for strategies that might encourage them to revolve balances under certain conditions.


## Understanding K-Means Clustering

### What is K-Means Clustering?

K-means clustering is a popular unsupervised learning algorithm used to partition a set of data points into K distinct non-overlapping subgroups (clusters), where each data point belongs to only one group. It aims to minimize the variance within each cluster, essentially forming clusters based on the mean distance from the centroid of the data points in each cluster.

### Mathematical Formulation

The objective of k-means clustering is to minimize the within-cluster sum of squares (WCSS), also known as the inertia. The mathematical formulation is:

$$
\min_{S} \sum_{i=1}^{k} \sum_{x \in S_i} \| x - \mu_i \|^2
$$

where $ S = \{S_1, S_2, \ldots, S_k\} $ represents the set of clusters, $ x $ denotes the data points in cluster $ S_i $, and $ \mu_i $ is the centroid of points in $ S_i $.

### Intuition Behind K-Means

The intuition behind k-means clustering is to define clusters such that the total intra-cluster variation (or total within-cluster sum of square) is minimized. The centroids are recalculated iteratively as the mean of the data points assigned to each cluster until convergence is achieved, meaning the centroids no longer change significantly.

### Pros and Cons of K-Means

#### Pros
- **Efficiency**: K-means is generally fast and efficient in terms of computational costs, making it suitable for large datasets.
- **Simplicity**: It is easy to implement and understand.

#### Cons
- **Number of Clusters**: The algorithm requires the number of clusters to be specified in advance.
- **Sensitivity to Outliers**: K-means is sensitive to noise and outliers as these can influence the calculation of centroids.
- **Initialization Sensitivity**: The results of k-means can vary significantly depending on the initial choice of centroids.

### When Does It Fail?

K-means clustering tends to fail in the following scenarios:
- **Non-convex Clusters**: It does not perform well with non-globular (non-convex) cluster shapes.
- **Varying Sizes and Density**: Clusters of varying sizes and different densities can lead to poor clustering performance.

### Example: K-Means Clustering Using Python

Below is a simple example using `numpy` for data generation and `sklearn` for performing k-means clustering:

```python
import numpy as np
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Generate synthetic data
np.random.seed(0)
X = np.vstack((np.random.normal(loc=0.0, scale=1.0, size=(100, 2)),
               np.random.normal(loc=5.0, scale=1.0, size=(100, 2))))

# Apply k-means clustering
kmeans = KMeans(n_clusters=2, random_state=0).fit(X)
labels = kmeans.labels_

# Plotting the results
plt.scatter(X[:, 0], X[:, 1], c=labels, cmap='viridis', marker='o')
centroids = kmeans.cluster_centers_
plt.scatter(centroids[:, 0], centroids[:, 1], c='red', s=200, alpha=0.5)
plt.title("K-Means Clustering Example")
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.show()
```

### Detailed Analysis of K-Means Clustering Example

#### Step-by-Step Walkthrough

1. **Data Generation**:
   - We generate synthetic data using `numpy` to create two distinct groups. Each group is formed using a normal distribution with different means to ensure they are distinguishable.

2. **Applying K-Means**:
   - The `KMeans` class from `sklearn.cluster` is instantiated with `n_clusters=2` to specify that we want to identify two clusters.
   - The `fit` method is used on our dataset `X`, which performs the clustering.

3. **Visualization**:
   - We use `matplotlib.pyplot` to visualize the results. Data points are plotted with colors indicating the cluster assignment (`labels`), which are obtained from `kmeans.labels_`.
   - The centroids, calculated as the mean location of points in each cluster, are highlighted using red markers. These centroids are crucial as they represent the 'center' of each cluster.

#### Interpretation of Results

- The scatter plot visually confirms the effectiveness of k-means in this scenario, as it successfully identifies and segregates the two clusters based on their features.
- The centroids accurately reflect the central points of each cluster, demonstrating how k-means attempts to minimize intra-cluster variance.

### Best Practices and Tips for Using K-Means

1. **Determining the Number of Clusters**:
   - Methods like the Elbow method can be used to estimate the optimal number of clusters by analyzing the rate of decrease in WCSS as the number of clusters increases.

2. **Handling Outliers**:
   - Preprocessing data to remove outliers or using robust scaling methods can help improve the results of k-means clustering.

3. **Choosing Initial Centroids**:
   - Multiple initializations of centroids can be performed to avoid poor clustering due to unfortunate initial centroid positions. Sklearn's KMeans uses multiple centroid seeds by default (`n_init` parameter).

### Limitations and Considerations

While k-means is a powerful tool for clustering, it is not without its limitations. Understanding these can help in choosing the right algorithm for your data:
- **Data Shape and Size**: K-means assumes that clusters are roughly spherical and similar in size. Data that do not meet these assumptions may be poorly clustered.
- **Scalability**: While generally efficient, the computational cost can become prohibitive with very large datasets or a high number of dimensions (features).

### Conclusion

K-means clustering provides a useful framework for understanding groupings in data across various applications. By recognizing its strengths and weaknesses, users can effectively apply k-means to both real-world and theoretical problems in a way that informs decision-making and strategic planning. Its simplicity, coupled with the robustness offered by libraries like `sklearn`, makes it an indispensable tool in the machine learning toolkit.

