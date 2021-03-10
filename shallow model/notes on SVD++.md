# 2. 🚗 **SVD++**

##### Factorization Meets the Neighborhood: a Multifaceted Collaborative Filtering Model

## 2.1 **Preliminaries**
#### 2.1.1 Baseline estimates

A baseline estimate for an unknown rating *r ui* is denoted by ***b ui*** and accounts for the user and item effects

<img src="https://img.imgdb.cn/item/604874915aedab222c3bd690.png" width="50%" height="50%" />

- *bu* indicate the observed deviations of user *u*, from the average.
-  *bi* indicate the observed deviations of item *i*, from the average.

 In order to estimate *bu* and *bi* one can solve the least squares problem,  the first term strives to find *bu*’s and *bi*’s that **fit the given ratings**. The **regularizing term** avoids overfitting by **penalizing the magnitudes of the parameters** :

<img src="https://img.imgdb.cn/item/604874b95aedab222c3becbd.png" width="50%" height="50%" />

🟩 In order to establish recommendations, CF systems need to compare fundamentally different objects: items against users. There are two primary approaches to facilitate such a comparison, which constitute the two main disciplines of CF: *the neighborhood approach* and *latent factor models*.

#### 2.1.2 Neighborhood models

- these methods transform users to the item space by viewing them as baskets of rated items. 
- Neighborhood models are most effective at detecting very localized relationships. They rely on a few signifificant neighborhood relations, often **ignoring the vast majority of ratings by a user**.

Central to most item-oriented approaches is a similarity measure between items. Frequently, it is based on the **Pearson correlation coeffificient, *ρij*** ❓💬, which measures the tendency of users to rate items *i* and *j* similarly. An appropriate similarity measure, denoted by ***sij*** , would be a shrunk correlation coefficient:

<img src="https://img.imgdb.cn/item/60487d345aedab222c411bfe.png" width="50%" height="50%" />

- *nij* denotes the number of users that rated both *i* and *j*. 
- A typical value for *λ*2 is 100.

**Our goal is to predict *rui* **– the unobserved rating by user *u* for item *i*. Using the similarity measure, we identify the *k* items rated by *u*, which are most similar to *i*. **This set of *k* neighbors is denoted by S*k*(*i*; *u*)**. The predicted value of *rui* is taken as a **weighted average** of the ratings **of neighboring items**, while adjusting for user and item effects through the baseline estimates:

<img src="https://img.imgdb.cn/item/60487d685aedab222c4136f2.png" width="50%" height="50%" />

- these methods are not justified by a formal model.

- also questioned the suitability of a similarity measure that isolates the relations between two items, without analyzing the interactions within the full set of neighbors. 
- the fact that interpolation weights in (3) sum to one forces the method to fully rely on the neighbors even in cases where neighborhood information is absent 

a more accurate neighborhood model, which overcomes these difficulties, need to compute the ***interpolation weights*** θu*ij* (estimating all inner products between item ratings):

<img src="https://img.imgdb.cn/item/60487dc75aedab222c417187.png" width="50%" height="50%" />

#### Latent factor models

- explain ratings by characterizing both products and users on factors automatically inferred from user feedback.
- Latent factor models are generally effective at estimating overall structure that relates simultaneously to most or all items. However, these models are **poor at detecting strong associations among a small set of closely related items**, precisely where neighborhood models do best.

❓💬In order to combat overfitting the sparse rating data, models are regularized so estimates are shrunk towards baseline defaults. Regularization is controlled by constants which are denoted as: *λ*1*, λ*2*,...* Exact values of these constants are determined by cross validation. As they grow, regularization becomes heavier.

## 2.2 **Probabilistic Matrix Factorization (PMF)**

Suppose we have M movies, N users, and integer rating values from 1 to K1. Let Rij represent the rating of user i for movie j, U ∈ RD×N and V ∈ RD×M be latent user and movie feature matrices, with column vectors Ui and Vj representing user-specific and movie-specific latent feature vectors respectively. 

基础PMF模型, 使用如下两个假设:

(1) the observation noise 观测噪声（观测评分矩阵R 和近似评分矩阵R^之差）为高斯分布
(2) movie and user features 用户属性U 和电影属性V 均为高斯分布

由于模型性能是通过计算测试集上的均方根误差(RMSE)来衡量的，我们首先采用带有高斯观测噪声的概率线性模型 Since model performance is measured by computing the root mean squared error (RMSE) on the test set, we first adopt a probabilistic linear model with Gaussian observation noise.
We define the conditional distribution(条件分布) over the observed ratings as

  <img src="https://p26-tt.byteimg.com/origin/pgc-image/5315d4be56b0487792d927d5d276d22b" width="50%" height="50%" />

- N (x|µ, σ2) is the probability density function(概率密度函数) of the Gaussian distribution with mean(均值) µ and variance(方差) σ2

- Iij is the indicator function(指标函数) that is equal to 1 if user i rated movie j and equal to 0 otherwise. 


place **zero-mean spherical Gaussian priors(零均值球面高斯先验)** on **user** and **movie feature vectors**:

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/4475b390e8a34c5a8c2e9c69effd7542" width="50%" height="50%" />


The log of the **posterior distribution** over the **user** and **movie features** is given by

<img src="https://inews.gtimg.com/newsapp_ls/0/13255827617/0" width="50%" height="50%" />

- C is a constant that does not depend on the parameters.


Maximizing the log-posterior(对数后) over movie and user features with hyperparameters (i.e. the observation noise variance and prior variances) kept fixed is equivalent to **minimizing the sum-of-squared-errors objective function with quadratic regularization terms(最小化含有二次正则化项的误差平方和目标函数)**:

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/11428fd10d86432895e8c4d54ea04c4e" width="50%" height="50%" />

- λU denotes the Frobenius norm(Frobenius范数)
- A local minimum of the objective function(目标函数的局部最小值) given by Eq. 4 can be found by performing gradient descent in U and V .
- Note that this model can be viewed as a **probabilistic extension of the SVD model**, since if all ratings have been observed, the objective given by Eq. 4 reduces to the SVD objective in the limit of prior variances going to infinity.

the dot product between user- and movie-specific feature vectors is passed through the logistic function g(x) = 1/(1 + exp(−x)), which bounds the range of predictions(限制预测的范围)
<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/419d5121d51248ddab50aaecdc03e9fe" width="50%" height="50%" />

We map the ratings 1, ..., K to the interval [0, 1] using the function t(x) = (x − 1)/(K − 1), so that the range of valid rating values matches the range of predictions our model makes. Minimizing the objective function given above using steepest descent takes time linear in the number of observations. 

## 1.3 **Probabilistic Matrix Factorization (PMF)**
Regularization parameters such as λU and λV defined above provide a more flexible approach to regularization.

As shown above, the problem of **approximating a matrix** in the L2 sense by a product of two low-rank matrices that are **regularized by penalizing their Frobenius norm** can be viewed as **MAP estimation in a probabilistic model with spherical Gaussian priors on the rows of the low-rank matrices**.通过两个以处罚Frobenius范数的方式正则化的低秩的矩阵的乘积近似一个矩阵的问题可以被看作是在低秩矩阵的行上含有球形高斯先验的概率模型中的MAP估计。

The complexity of the model is controlled by the hyperparameters: the noise variance σ 2 and the the parameters of the priors（先验参数） (σ 2 U and σ 2 V above). 

Introducing **priors for the hyperparameters** and **maximizing the log-posterior of the model over both parameters and hyperparameters** allows model complexity to be controlled automatically based on the training data. Using spherical priors for user and movie feature vectors in this framework leads to the standard form of PMF with λU and λV chosen automatically. 

 This approach to regularization allows us to use methods that are **more sophisticated than the simple penalization of the Frobenius norm of the feature matrices**. 🎯For example, we can use priors with diagonal or even full covariance matrices as well as adjustable means for the feature vectors. Mixture of Gaussians priors can also be handled quite easily.

<img src="https://p26-tt.byteimg.com/origin/pgc-image/a6533075f675460ca82f568841a5edc4" width="50%" height="50%" />

where ΘU and ΘV are the hyperparameters for the priors over user and movie feature vectors respectively and C is a constant that does not depend on the parameters or hyperparameters.



## 1.4 **Constrained PMF**

introduce an additional way of **constraining user-specific feature vectors** that has a strong effect on infrequent users (Once a PMF model has been fitted, users with very few ratings will have feature vectors that are close to the prior mean).

 Let W ∈ RD×M be a latent similarity constraint matrix. We define the feature vector for user i as:

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/371778adc27a4eaa8228a5c155f005b0" width="50%" height="50%"  />

- I is the observed indicator matrix with Iij taking on value 1 if user i rated movie j and 0 otherwise. 
- the i th column of the **W matrix** captures the effect of a **user having rated** a particular movie has on the **prior mean of the user’s feature vector**. ➡️  users that have seen the same (or similar) movies will have **similar prior distributions** for their **feature vectors**. 
- Yi can be seen as the offset added to the mean of the prior distribution to get the feature vector Ui for the user i. 
- In the unconstrained PMF model Ui and Yi are equal because the prior mean is fixed at zero. 

the conditional distribution over the observed ratings as

<img src="https://p26-tt.byteimg.com/origin/pgc-image/7d0cd930330348638d6fb194a1a4a81e" width="55%" height="55%" />

regularize the **latent similarity constraint matrix W** by placing a zero-mean spherical Gaussian prior on it

<img src="https://img.imgdb.cn/item/6048290c5aedab222c086c9f.png" width="50%" height="50%" />

As with the PMF model, maximizing the log-posterior is equivalent to minimizing the sum-of-squared errors function with quadratic regularization terms

<img src="https://img.imgdb.cn/item/60482a2d5aedab222c090143.png" width="55%" height="55%" />

- λY = σ 2/σ2 Y  
- λV = σ 2/σ2 V 
- λW = σ 2/σ2 W 

We can then perform gradient descent in Y , V , and W to minimize the objective function given by Eq. 10.