### 1. 🚗 Probabilistic Matrix Factorization (PMF) model基于概率的矩阵分解模型
1.1 **Preliminaries**
#### low-dimensional factor models

- The idea behind such models is that attitudes or preferences of a user are determined by a small number of unobserved factors

- for N users and M movies, the N ×M preference matrix R is given by the product of an N ×D user coefficient matrix U T and a D × M factor matrix V. Training such a model amounts to finding the best rank(秩)-D approximation to the observed N × M target matrix R under the given loss function.

#### probabilistic factor-based models

- can be viewed as graphical models in which hidden factor variables have directed connections to variables that represent user ratings.
- The major drawback of such models is that exact inference is intractable, which means that potentially slow or inaccurate approximations are required for **computing the posterior distribution(后验概率，知果求因)** over hidden factors in such models.这类模型的主要缺点是很难进行精确的推断，这意味着在计算此类模型中隐藏因素的后验分布时，需要潜在的缓慢或不准确的近似。

#### Singular Value Decomposition (SVD)

- SVD finds the approximation matrix Rˆ = U *T* V of the given rank which minimizes the sum-squared distance to the target matrix R. 

- Since most real-world datasets are sparse, most entries in R will be missing. In those cases, the sum-squared distance is computed only for the observed entries of the target matrix R.

- Seemingly minor modification results in a difficult **non-convex optimization problem** which cannot be solved using standard SVD implementations.这个看似很小的修改导致了一个困难的非凸优化问题，而这个问题无法用标准的SVD实现来解决。

  （凸优化任何局部最优解即为全局最优解。由于这个性质，只要设计一个较为简单的局部算法，例如贪婪算法（Greedy Algorithm）或梯度下降法（Gradient Decent），收敛求得的局部最优解即为全局最优。而非凸优化问题被认为是非常难求解的，因为可行域集合可能存在无数个局部最优点，通常求解全局最优的算法复杂度是指数级的。）

- Instead of constraining the rank of the approximation matrix Rˆ = U T V , i.e. the number of factors, [10] proposed penalizing the norms of U and V . Learning in this model, however, requires solving a **sparse semi-definite program (SDP) 半正定规划**, making this approach infeasible for datasets containing millions of observations.惩罚U和V的范数，而不是限制近似矩阵Rˆ= U T V的秩，即因子的数量。然而，在这个模型中学习需要求解一个稀疏半定程序(SDP)，这使得这种方法对于包含数百万个观测数据集不可行。

⬆️none of these methods have proved to be particularly successful for two reasons. 

- First, none of the above-mentioned approaches, except for the matrix-factorization-based ones, scale well to large datasets.
- Second, most of the existing algorithms have trouble making accurate predictions for users who have very few ratings

A common practice in the collaborative filtering community is to **remove all users with fewer than some minimal number of ratings（删除所有评级数少于最低线的用户）**.



#### Probabilistic Matrix Factorization (PMF)

Suppose we have M movies, N users, and integer rating values from 1 to K1. Let Rij represent the rating of user i for movie j, U ∈ RD×N and V ∈ RD×M be latent user and movie feature matrices, with column vectors Ui and Vj representing user-specific and movie-specific latent feature vectors respectively. 

基础PMF模型, 使用如下两个假设:

(1) 观测噪声（观测评分矩阵R 和近似评分矩阵R ^之差）为高斯分布
(2) 用户属性U 和电影属性V 均为高斯分布

由于模型性能是通过计算测试集上的均方根误差(RMSE)来衡量的，我们首先采用带有高斯观测噪声的概率线性模型 Since model performance is measured by computing the root mean squared error (RMSE) on the test set we first adopt a probabilistic linear model with Gaussian observation noise. We define the conditional distribution over the observed ratings as

![img](https://p26-tt.byteimg.com/origin/pgc-image/5315d4be56b0487792d927d5d276d22b)

- N (x|µ，σ2)是均值为µ，方差为σ2的高斯分布的概率密度函数  N (x|µ, σ2) is the probability density function of the Gaussian distribution with mean µ and variance σ2

- Iij是用户i评价电影j时等于1，否则等于0的指标函数 Iij is the indicator function that is equal to 1 if user i rated movie j and equal to 0 otherwise. 



在用户和电影特征向量上放置了零均值球面高斯先验: place **zero-mean spherical Gaussian priors** on **user** and **movie feature vectors**:

![img](https://p1-tt-ipv6.byteimg.com/origin/pgc-image/4475b390e8a34c5a8c2e9c69effd7542)



用户特征和电影特征的后验分布的对数为The log of the **posterior distribution** over the **user** and **movie features** is given by


![img](https://inews.gtimg.com/newsapp_ls/0/13255827617/0)

- C is a constant that does not depend on the parameters.



在保持固定的超参数(即观测噪声方差和先验方差)下，最大化电影和用户特征的对数后验等价于使用二次正则化项使误差平方和最小:   Maximizing the log-posterior over movie and user features with hyperparameters (i.e. the observation noise variance and prior variances) kept fixed is equivalent to minimizing the sum-of-squared-errors objective function with quadratic regularization terms:


![img](https://p9-tt-ipv6.byteimg.com/origin/pgc-image/11428fd10d86432895e8c4d54ea04c4e)

- λU表示Frobenius范数 λU denotes the Frobenius norm
- 通过对U和V进行梯度下降，可以找到由式4给出的目标函数的局部最小值。 A local minimum of the objective function given by Eq. 4 can be found by performing gradient descent in U and V .
- 请注意，该模型可以被视为SVD模型的概率扩展，因为如果观察到所有评级，则在先验方差趋于无穷大的极限下，Eq. 4给出的目标将减少为SVD目标. Note that this model can be viewed as a **probabilistic extension of the SVD model**, since if all ratings have been observed, the objective given by Eq. 4 reduces to the SVD objective in the limit of prior variances going to infinity.

在我们的实验中, 没有使用一个简单的linear-Gaussian模型来预测有效评级的范围以外的值 In our experiments, instead of using a simple linear-Gaussian model, which can make predictions outside of the range of valid rating values

用户和电影的特征向量之间的点积通过逻辑函数g (x) = 1 / (1 + exp(−x))，实现边界范围的预测 the dot product between user- and movie-specific feature vectors is passed through the logistic function g(x) = 1/(1 + exp(−x)), which bounds the range of predictions

![img](https://p1-tt-ipv6.byteimg.com/origin/pgc-image/419d5121d51248ddab50aaecdc03e9fe)

We map the ratings 1, ..., K to the interval [0, 1] using the function t(x) = (x − 1)/(K − 1), so that the range of valid rating values matches the range of predictions our model makes. Minimizing the objective function given above using steepest descent takes time linear in the number of observations. 


