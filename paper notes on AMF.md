### *Title: Adversarial Personalized Ranking for Recommendation*

###### Authors: Xiangnan He, Zhankui He, Xiaoyu Du, Tat-Seng Chua

###### Publication: [SIGIR '18: The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval](https://dl.acm.org/doi/proceedings/10.1145/3209978)June 2018 Pages 355–364https://doi.org/10.1145/3209978.3209981

###### Implementation: https://github.com/hexiangnan/adversarial_personalized_ranking

###### Note: Yiming Cao



#### **1. Introduction**

- Optimizing MF with BPR leads to a recommender model that is highly vulnerable to adversarial perturbations on its model parameters, which implies the possibly large error in generalization.

- Proposed a new optimization framework, namely **Adversarial Personalized Ranking(APR)** which enhances the pairwise ranking method BPR by performing adversarial training (**by adding adversarial perturbations on the embedding vectors of users and items**).

- The whole framework of APR can be optimized with the standard stochastic gradient descent. Derived the APR solver for MF and term the method as **Adversarial Matrix Factorization(AMF)** 

  

#### 2. **Preliminaries**

- MF-BPR is Vulnerable to Adversarial Noises
  
  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/1fa1b49fb52643258db8cf58ef37c64a" width="60%" height="60%" />
  
  - **eq(1) objective function of BPR:** can be interpreted as a classifier — given a triplet (*u*,*i*, *j*), it determines whether (*u*,*i*) should have a higher score than (*u*, *j*).  A positive instance of (*u*,*i*, *j*) means that *y*ˆ*ui* should be larger than*y*ˆ*uj* as much as possible to get the correct label of +1; and a negative instance can be seen as having a label of 0.
  
  - **eq(2) adversarial perturbations:** aim to maximize the objective function of BPR
  
  - **eq(3) optimal Δ:** As MF is a bilinear model and BPR objective function involves nonlinear operations, it is intractable to get exact maximization with respect to Δ. we approximate the objective function by linearizing it round Δ. 
  
    

#### 3. Methods

- Adversarial Personalized Ranking

  <img src="https://p26-tt.byteimg.com/origin/pgc-image/307e67995f504c668514d6f60bb09c65" width="60%" height="60%"/>

  - **eq(4) objective function of APR:** the adversarial term LBPR (D |Θ + Δ*adv* ) -- regularizing the model by stabilizing the classification function in BPR (also called *adversarial regularizer* and use *λ* to control its strength).
  -  **eq(5) training process of APR:** the intermediate variable Δ maximizes the objective function to beminimized by Θ (minx-game)
  -  the model parameters **Θ are initialized by optimizing BPR** , rather than randomly initialized. (the adversarial perturbations are only reasonable and necessary to add when the model parameters start to overfit the data.) 

- Adversarial Matrix Factorization

  - first train MF with BPR, and then further optimize it under APR framework.

    <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/ac46bf24662d4aacafda4346eea78bd6" width="60%" height="60%"/>



#### 4. Experiments

<img src="https://p26-tt.byteimg.com/origin/pgc-image/90ddb1a6f00545b6b2fe1781ec0d5183" width="60%" height="60%"/>

- evaluate the ranking list using **Hit Ratio (HR)** and**Normalized Discounted Cumulative Gain (NDCG)**. (*HR* is a recall-based metric, measuring whether the testing item is in the top-K list. While *NDCG* is position-sensitive,which assigns higher score to hits at higher positions.)

- *Baselines*
  - **ItemPop**
  - **MF-BPR**
  - **CDAE**
  - **NeuMF**(combines MF and multi-layer perceptrons(MLP) to learn the user-item interaction function)
  - **IRGAN** ( combines two types of models via adversarial training, a generative model that generates items for a user and a discriminative model that determines whether the instance is from real data or generated.)

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/4f880952aee347ab9c2305b08aae12d8" width="60%" height="60%"/>

- APR  outperforms BPR with a relative improvement of **11.2% on average** and achieves state-of-the-art performance for item recommendation.
