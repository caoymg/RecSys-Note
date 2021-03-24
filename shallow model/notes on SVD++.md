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

Central to most item-oriented approaches is a similarity measure between items. Frequently, it is based on the **Pearson correlation coefficient, *ρij***, which measures the tendency of users to rate items *i* and *j* similarly. An appropriate similarity measure, denoted by ***sij*** , would be a shrunk correlation coefficient:

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

-  typical model 

  - The prediction is done by taking an inner product, i.e.<img src="https://img.imgdb.cn/item/604989075aedab222cca8717.png" width="30%" height="30%" />
    - each user *u* with a user factors vector ***p****u* *∈* R*f* 
    - each item *i* with an item-factors vector ***q****i* *∈* R*f* 
  - model directly only the observed ratings, while avoiding overfitting through an adequate regularized model<img src="https://img.imgdb.cn/item/604989555aedab222ccabc92.png" width="80%" height="80%" />

-  NSVD model

  - avoids explicitly parameterizing each user, but rather models users based on the items that they rated. This way, each item *i* is associated with two factor vectors ***q****i* and ***x****i*. The representation of a user *u* is through the sum:<img src="https://img.imgdb.cn/item/6049ddef5aedab222cf99881.png" width="40%" height="40%" />

  -  so ***r****ui* is predicted as 

   <img src="https://img.imgdb.cn/item/6049e9855aedab222c01926f.png" width="50%" height="50%" />

   - R(*u*) is the set of items rated by user *u*.


- explain ratings by characterizing both products and users on factors automatically inferred from user feedback.

- Latent factor models are generally effective at estimating overall structure that relates simultaneously to most or all items. However, these models are **poor at detecting strong associations among a small set of closely related items**, precisely where neighborhood models do best.

-  typical model 

  - The prediction is done by taking an inner product, i.e.<img src="https://img.imgdb.cn/item/604989075aedab222cca8717.png" width="30%" height="30%" />
    - each user *u* with a user factors vector ***p****u* *∈* R*f* 
    - each item *i* with an item-factors vector ***q****i* *∈* R*f* 
  - model directly only the observed ratings, while avoiding overfitting through an adequate regularized model<img src="https://img.imgdb.cn/item/604989555aedab222ccabc92.png" width="80%" height="80%" />

-  NSVD model

  - avoids explicitly parameterizing each user, but rather models users based on the items that they rated. This way, each item *i* is associated with two factor vectors ***q****i* and ***x****i*. The representation of a user *u* is through the sum:<img src="https://img.imgdb.cn/item/6049ddef5aedab222cf99881.png" width="40%" height="40%" />

  -  so ***r****ui* is predicted as 

    <img src="https://img.imgdb.cn/item/6049e9855aedab222c01926f.png" width="50%" height="50%" />

    - R(*u*) is the set of items rated by user *u*.

## 2. **A new neighborhood model**

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



## **3. Latent Factor Models Revisited**

#### 3.1 Asymmetric-SVD

prediction rule：

<img src="https://img.imgdb.cn/item/604b1f625aedab222cafd932.png" width="50%" height="50%" />

- each item *i* is associated with three factor vectors *q**i**, x**i**, y**i*** *∈* R*f* .
- instead of providing an explicit parameterization for users, we **represent users through the items that they prefer**.

- advantages
  - provides advantages that are usually regarded as belonging to neighborhood models, namely, an **ability to explain recommendations**（does not employ any level of abstraction on the users side. Hence, predictions are a direct function of past users’ feedback）and to **handle new users seamlessly**（Asymmetric-SVD does not parameterize users, we can handle new users as soon as they provide feed back to the system).

learn the values of involved parameters by minimizing the regularized squared error function, employ a simple gradient descent scheme to solve the system.

<img src="https://img.imgdb.cn/item/604b229d5aedab222cb18b83.png" width="50%" height="50%" />

#### 3.2 SVD++📣

as far as integration of implicit feedback is concerned, we could get more accurate results by a more direct modifification.

<img src="https://img.imgdb.cn/item/604b23fb5aedab222cb24c56.png" width="80%" height="80%" />

SVD++ does not offer the previously mentioned benefits of having less parameters / conveniently handling new users / readily explainable results. 

- This is because we do abstract each user with a factors vector. 
- However,  SVD++ is clearly **advantageous** in terms of **prediction accuracy**. Actually, to our best knowledge, its results are more accurate than all previously published methods on the Netflix data.



## 4. **An Integrated Model**

integrate the **neighborhood model** with our most accurate factor model – **SVD++**. A combined model will sum the predictions of (10) and (15), thereby allowing neighborhood and factor models to enrich each other, as follows:

<img src="https://img.imgdb.cn/item/604b25cf5aedab222cb366c3.png" width="70%" height="70%" />

-  *μ*+ *bu* + *bi*, describes general properties of the item and the user, without accounting for any involved interactions.
- next qT(...) provides the interaction between the user profile and the item profile.
- The final “neighborhood tier” contributes fine grained adjustments that are hard to profile.

