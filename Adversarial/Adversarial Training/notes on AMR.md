### *Title: Adversarial Training Towards Robust Multimedia Recommender System*

###### Authors: Jinhui Tang, Xiaoyu Du, Xiangnan He, Fajie Yuan, Qi Tian, Tat-Seng Chua

###### Publication: https://ieeexplore.ieee.org/abstract/document/8618394

###### Note: Yiming Cao



#### **1. Introduction**

- Multimedia content contains rich visually-relevant signal that can reveal user preference, providing opportunities to improve recommender systems that are typically based on collaborative filtering on user behavior data only.
- Emphasize the vulnerability issue of state-of-the-art multimedia recommender systems due to the use of DNNs for feature learning.
- **Adversarial Multimedia Recommendation (AMR)** is  an adversary which adds perturbations on multimedia content with the aim of maximizing the VBPR loss function. 

#### 2. Methods

##### 2.1  Visual Bayesian Personalized Ranking

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/0b94a8f7c3db4aa4a322b1cf86416774" width="50%" height="50%" />

where the first term p*T*u qi is same as MF to model the collaborative filtering effect, and the second term h*T*u (Eci) models user preference based on the item’s image. 

- pu (qi ) denotes the ID embedding for user u (item i) 
- hu is u’s embedding in the image latent space
- ci denotes the visual feature vector for item i (which is extracted by AlexNet)
-  E converts the visual feature vector to latent space. 

<img src="https://p26-tt.byteimg.com/origin/pgc-image/5a6de5f6fd7f4469b3cad701fe524655" width="50%" height="50%" />





##### 2.2  Adversarial Multimedia Recommendation (AMR)

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/9973df7a06cc4d56a5e1f639c29cff5e" width="60%" height="60%" />

The difference of this visually-aware recommender model with VBPR is that it **associates each user with one embedding vector pu** only, while in VBPR each user has two embedding vectors pu and hu. This simplification is just to **ensure a fair comparison with the conventional MF** model when the embedding size K is set as a same number (i.e., making the models have the same representation ability).

The perturbed model is formulated as:

<img src="https://p26-tt.byteimg.com/origin/pgc-image/0b254e842898469faae6a7dc79abfc92" width="50%" height="50%" />

- Adversary Construction

  Obtain optimal perturbations by maximizing the BPR loss on training data:

  <img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/b91893361e964d6c87b5ab12a2e17428" width="50%" height="50%" />

- Model Optimization

  To make the model less sensitive to the adversarial perturbations, in addition to minimize the original BPR loss, we also minimize the adversary’s objective function.

  <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/53082a70fe4140ef94efe0db05c9825a" width="50%" height="50%" />

- Learning Algorithm

  1. Learning Adversarial Perturbations

     Due to the non-linearity of the objective function  and the 𝜀-constraint in optimization, it is difficult to get the exact solution. As such, we bor

     row the idea from the fast gradient sign method, approximating the objective function by linearizing it around 𝛥; and then, we solve the constrained optimization problem on this approximated linear function.

     <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/d1d934adf328418cb6cf24ca413546f3" width="50%" height="50%" />

  2. Learning Model Parameters

     Since the perturbations D are fixed in this step, it becomes a conventional minimization problem and can be approached with gradient descent.

     <img src="https://p26-tt.byteimg.com/origin/pgc-image/118b1f39c20643438d0cc58703951197" width="50%" height="50%" />



#### 3. Experiments

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/ba22bf7ef0ee402181ffcfada2ff1189" width="60%" height="60%"/>

- evaluate the ranking list using **Hit Ratio (HR)** and **Normalized Discounted Cumulative Gain (NDCG)**. (*HR* is a recall-based metric, measuring whether the testing item is in the top-K list. While *NDCG* is position-sensitive,which assigns higher score to hits at higher positions.)
- *Baselines*
  - Pop
  - MF-BPR
  - MF-eALS
  - DUIF
  - VBPR

