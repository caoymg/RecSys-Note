# 🚗 **SVD++**

##### Factorization Meets the Neighborhood: a Multifaceted Collaborative Filtering Model


## 1. **A new neighborhood model**

- abandon user-specific weights in favor of global weights independent of a specific user. The weight from *j* to *i* is denoted by ***w*** *ij* and will be learnt from the data through optimization.
  - Usually the weights in a neighborhood model represent interpolation coeffi-cients relating unknown ratings to existing ones. 
  - Viewing the **weights** as **global offsets**, rather than as user-specific interpolation coeffificients, emphasizes the **influence of missing ratings**. In other words, a user’s opinion is formed not only by what he rated, but also by what he did not rate. (here we sum over all items rated by *u*, unlike (4) that sums over members of S*k*(*i*; *u*).)

- use implicit feedback, which provide an alternative way to learn user preferences. To this end, we add another set of weights.
- take more risk with well modeled users that provided much input. On the other hand, we are less certain about the modeling of users that provided only a little input, in which case we would like to stay with safe estimates close to the baseline values.
  - many ratings (high *|*R(*u*)*|*) 
  - many implicit feedback (high *|*N(*u*)*|*)

<img src="https://img.imgdb.cn/item/604b1da85aedab222caef29b.png" width="50%" height="50%" />

- model parameters are learnt by solving the **regularized least squares problem**:

<img src="https://img.imgdb.cn/item/604b1de25aedab222caf0ea8.png" width="50%" height="50%" />



## **2. Latent Factor Models Revisited**

#### 2.1 Asymmetric-SVD

prediction rule：

<img src="https://img.imgdb.cn/item/604b1f625aedab222cafd932.png" width="50%" height="50%" />

- each item *i* is associated with three factor vectors *q**i**, x**i**, y**i*** *∈* R*f* .
- instead of providing an explicit parameterization for users, we **represent users through the items that they prefer**.

- advantages
  - provides advantages that are usually regarded as belonging to neighborhood models, namely, an **ability to explain recommendations**（does not employ any level of abstraction on the users side. Hence, predictions are a direct function of past users’ feedback）and to **handle new users seamlessly**（Asymmetric-SVD does not parameterize users, we can handle new users as soon as they provide feed back to the system).

learn the values of involved parameters by minimizing the regularized squared error function, employ a simple gradient descent scheme to solve the system.

<img src="https://img.imgdb.cn/item/604b229d5aedab222cb18b83.png" width="50%" height="50%" />

#### 2.2 SVD++📣

as far as integration of implicit feedback is concerned, we could get more accurate results by a more direct modifification.

<img src="https://img.imgdb.cn/item/604b23fb5aedab222cb24c56.png" width="80%" height="80%" />

SVD++ does not offer the previously mentioned benefits of having less parameters / conveniently handling new users / readily explainable results. 

- This is because we do abstract each user with a factors vector. 
- However,  SVD++ is clearly **advantageous** in terms of **prediction accuracy**. Actually, to our best knowledge, its results are more accurate than all previously published methods on the Netflix data.



## 3. **An Integrated Model**

integrate the **neighborhood model** with our most accurate factor model – **SVD++**. A combined model will sum the predictions of (10) and (15), thereby allowing neighborhood and factor models to enrich each other, as follows:

<img src="https://img.imgdb.cn/item/604b25cf5aedab222cb366c3.png" width="70%" height="70%" />

-  *μ*+ *bu* + *bi*, describes general properties of the item and the user, without accounting for any involved interactions.
- next qT(...) provides the interaction between the user profile and the item profile.
- The final “neighborhood tier” contributes fine grained adjustments that are hard to profile.

