# 🚗 **SVD++**

##### Factorization Meets the Neighborhood: a Multifaceted Collaborative Filtering Model

## 1 **Preliminaries**
#### 1.1 Baseline estimates

A baseline estimate for an unknown rating *r ui* is denoted by ***b ui*** and accounts for the user and item effects

<img src="https://img.imgdb.cn/item/604874915aedab222c3bd690.png" width="50%" height="50%" />

- *bu* indicate the observed deviations of user *u*, from the average.
-  *bi* indicate the observed deviations of item *i*, from the average.

 In order to estimate *bu* and *bi* one can solve the least squares problem,  the first term strives to find *bu*’s and *bi*’s that **fit the given ratings**. The **regularizing term** avoids overfitting by **penalizing the magnitudes of the parameters** :

<img src="https://img.imgdb.cn/item/604874b95aedab222c3becbd.png" width="50%" height="50%" />

🟩 In order to establish recommendations, CF systems need to compare fundamentally different objects: items against users. There are two primary approaches to facilitate such a comparison, which constitute the two main disciplines of CF: *the neighborhood approach* and *latent factor models*.

#### 1.2 Neighborhood models

- these methods transform users to the item space by viewing them as baskets of rated items. 
- Neighborhood models are most effective at detecting very localized relationships. They rely on a few signifificant neighborhood relations, often **ignoring the vast majority of ratings by a user**.

Central to most item-oriented approaches is a similarity measure between items. Frequently, it is based on the **Pearson correlation coeffificient, *ρij*** ❓💬, which measures the tendency of users to rate items *i* and *j* similarly. An appropriate similarity measure, denoted by ***sij*** , would be a shrunk correlation coefficient:

<img src="https://img.imgdb.cn/item/60487d345aedab222c411bfe.png" width="50%" height="50%" />

- *nij* denotes the number of users that rated both *i* and *j*. 
- A typical value for *λ*2 is 100.

**Our goal is to predict *rui* **– the unobserved rating by user *u* for item *i*. Using the similarity measure, we identify the *k* items rated by *u*, which are most similar to *i*. **This set of *k* neighbors is denoted by S*k*(*i*; *u*)**. The predicted value of *rui* is taken as a **weighted average** of the ratings **of neighboring items**, while adjusting for user and item effects through the baseline estimates:

<img src="https://img.imgdb.cn/item/60487d685aedab222c4136f2.png" width="50%" height="50%" />

- these methods are not justified by a formal model.

- also questioned the suitability of a similarity measure that isolates the relations between two items, without analyzing the interactions within the full set of neighbors. 
- the fact that interpolation weights in (3) sum to one forces the method to fully rely on the neighbors even in cases where neighborhood information is absent 

a more accurate neighborhood model, which overcomes these difficulties, need to compute the ***interpolation weights*** θu*ij* (estimating all inner products between item ratings):

<img src="https://img.imgdb.cn/item/60487dc75aedab222c417187.png" width="50%" height="50%" />

#### Latent factor models

- explain ratings by characterizing both products and users on factors automatically inferred from user feedback.
- Latent factor models are generally effective at estimating overall structure that relates simultaneously to most or all items. However, these models are **poor at detecting strong associations among a small set of closely related items**, precisely where neighborhood models do best.

❓💬In order to combat overfitting the sparse rating data, models are regularized so estimates are shrunk towards baseline defaults. Regularization is controlled by constants which are denoted as: *λ*1*, λ*2*,...* Exact values of these constants are determined by cross validation. As they grow, regularization becomes heavier.

