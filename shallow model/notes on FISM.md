# 🚗 FISM

##### Factorization Meets the Neighborhood: a Multifaceted Collaborative Filtering Model

## 1. **Preliminaries**

<img src="https://img.imgdb.cn/item/604c2e4e5aedab222c214f29.png" width="100%" height="100%" />

 two such items can be similar to each other by virtue of another item which is similar to both of them (**transitive relation**).

## 2. FISM (factored item similarity methods)

proposed item-oriented FISM method uses a factored item similarity model similar in spirit to that used by NSVD and SVD++.

FISM employs a **regression approach** based on **structural equation modeling** in which, **unlike NSVD (and SVD++)**, the known rating information for a particular user-item pair (*r ui*) is not used when the rating for that item is being estimated.

- This impacts how the diagonal entries of the item-item similarity matrix corresponding to **S** = **PQ**T influence the estimation of the recommendation score. Diagonal entries in the item similarities matrix correspond to including an item’s own value while computing the prediction for that item. 
- **NSVD** does not exclude the diagonal entries while estimating the ratings during learning and prediction phases.
  - This shortcoming of NSVD impacts the quality of the estimated factors when the number of factors becomes large. 
  - In this case it can lead to rather trivial estimates, in which an item ends up recommending itself.
- while **FISM** explicitly excludes the diagonal entries while estimating. 

In FISM, the **recommendation score** for a user *u* on an unrated item *i* (denoted by ˜*rui*) is calculated as an aggregation of the items that have been rated by *u* with the corresponding product of **pj** latent vectors from **P** and the **qi** latent vector from **Q**.

<img src="https://img.imgdb.cn/item/604c62a65aedab222c3a55c2.png" width="50%" height="50%" />

- *R*+*u* is the set of items rated by user *u*
- **p**j and **q**i are the learned item latent factors
- *n*+*u* is the number of items rated by *u*, and *α* is a user specified parameter between 0 and 1.
- the The term (*n*+*u* ) *-α* is used to control the degree of agreement between the items rated by the user with respect to their similarity to the item whose rating is being estimated respect to their similarity to the item whose rating is being estimated.

developed two different types of FISM models that use **different loss functions** and **associated optimization methods**：

#### **2.1 FISMrmse**

###### squared error loss function

<img src="https://img.imgdb.cn/item/604c68845aedab222c3eb318.png" width="50%" height="50%" />

*R*+*u* *\{**i**}* is the set of items rated by user *u*, excluding the current item *i*, whose value is being estimated. This exclusion is done to conform to regression models based on structural equation modeling. 

In FISMrmse, the matrices **P** and **Q** are learned by minimizing the following **regularized optimization problem**:

<img src="https://img.imgdb.cn/item/604c68ac5aedab222c3efd15.png" width="50%" height="50%" />

#### 2.2 **FISMauc**

###### a ranking loss function based on Bayesian Personalized Ranking (BPR)

<img src="https://img.imgdb.cn/item/604c6aaa5aedab222c40eb7e.png" width="50%" height="50%" />

- This is motivated by the fact that the Top-*N* recommendation problem deals with **ranking the items in the right order**, unlike the rating prediction problem where minimizing the RMSE is the goal.

- the error is computed as the relative difffference between the actual non-zero and zero entries and the difference between their corresponding estimated values.
  - Thus, this loss function focuses not on estimating the right value, but on the ordering of the zero and non-zero values.

In FISMauc, the matrices **P** and **Q** are learned by minimizing the following **regularized optimization problem**:

<img src="https://img.imgdb.cn/item/604c6ac95aedab222c410194.png" width="50%" height="50%" />

