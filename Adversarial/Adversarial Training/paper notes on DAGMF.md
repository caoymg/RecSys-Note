### *Title: Directional Adversarial Training for Recommender Systems*

###### Authors: **Yangjun Xu, **Liang Chen**, **Fenfang Xie**, **Weibo Hu**,**Jieming Zhu**,**Chuan Chen**,**Zibin Zheng

###### Publication: http://chenliang.tech/homepagefiles/paper/ECAI_2.pdf

###### Note: Yiming Cao



#### **1. Introduction**

- Adversarial training allows the model to consider more unseen space around *x*, thus encouraging the local smoothness among similar examples and further pushing the model towards better generalization.
- The maximum direction perturbation may move the embedding vector of example *x* close to the examples with different labels(dissimilar examples) or even non-existing examples.
- This work develop the Directional Adversarial Training (DAT) strategy by explicitly injecting the collaborative signal into the perturbation process. That is, both users and items are perturbed towards their similarneighbours in the embedding space with proper restriction.
  

#### 2. **Preliminaries**

- Problem Definition

Input:  two feature vectors that describe user *u* and item *i*. In this paper, the feature input vector is a binary sparse vector by one-hot encoding the identity of a user or an item.
Output: the predicted preference score of user *u* on item *i*

    

#### 3. Methods

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/b90a281275d8426f935ac1fc052be0fe" width="100%" height="100%" />

-  Given a user *u*, we make it perturb towards Top-K nearest neighbours in the embedding space based on pre-trained model parameters. 
-  Meanwhile, the perturbation direction of an observed item *i* and an unobserved item *j* will be perturbed towards the other observed items in the small circle and unobserved items in the large circle, respectively.
-  In this way, the information of similar examples will flow between each other, which explicitly injects the collaborative signal into adversarial learning process.
1. Randomly sample examples (u, i, j) from D
2. Calculating the direction vector. d ← Equation (9)<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/16bd9a766d6344ca901159c90b57c0ff" width="50%" height="50%" />

3. Calculating the worst case weights. wdadv ← Equation (12)<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/02b6d638c6004e4f83bcf0c9ca5b135c" width="50%" height="50%" />
4. Constructing direction adversarial perturbation. ∆(w) ← Equation (10)<img src="https://img.imgdb.cn/item/605e9ae18322e6675c0108c0.png" width="50%" height="50%" />
5. Optimizing model parameters<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/363776e8a35f427f8a2bf43772697501" width="50%" height="50%" />

#### 4. Experiments

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/9c99b72a192f46849893d6767249c581" width="40%" height="40%"/>

- evaluate the ranking list using **Hit Ratio (HR)** and**Normalized Discounted Cumulative Gain (NDCG)**. (*HR* is a recall-based metric, measuring whether the testing item is in the top-K list. While *NDCG* is position-sensitive,which assigns higher score to hits at higher positions.)

- *Baselines*
  - **ItemPop**
  - **MF-BPR**
  - **GMF**
  - **AGMF**( constructed by encoding the GMF into the adversarial training for the recommendation (APR))
  - **NGCF**
  - **IRGAN** ( combines two types of models via adversarial training, a generative model that generates items for a user and a discriminative model that determines whether the instance is from real data or generated.)

<img src="https://p26-tt.byteimg.com/origin/pgc-image/754c1edbcbc94d2f81ce7d32e0667cd2" width="70%" height="70%"/>

