### *Title: Enhancing Social Recommendation with Adversarial Graph Convolutional Networks*

###### Authors: Junliang Yu, Hongzhi Yin, Jundong Li, Min Gao, Zi Huang, and Lizhen Cui

###### Publication: IEEE TRANSACTIONS ON KNOWLEDGE AND DATA ENGINEERING 

###### Implementation: https://github.com/hexiangnan/adversarial_personalized_ranking

###### Note: Yiming Cao



#### **1. Introduction**

- failure of social recommender systems
  - (1) A majority of users only have a very limited number of neighbors in social networks and can hardly benefit from social relations;
  - (2) Social relations are noisy but they are indiscriminately used; 
  - (3) Social relations are assumed to be universally applicable to multiple scenarios while they are actually multi-faceted and show heterogeneous strengths in different scenarios.
- design alternative neighborhood generation, neighborhood denoising, and attention-aware social recommendation, which are corresponding solutions to the above three questions, unify and intensify these three components by integrating them into a deep adversarial framework based on GCNs.


#### 2. **Preliminaries**

-  we focus on Top-N recommendation. 
-  *y ui* is either 1 (positive) or 0 (negative or unknown). For each user pair (*u*1*, u*2), *s u1,u2* = 1 indicates that *u*1 follows *u*2 in the social network.
- noted that we work on directed graphs and the relation matrix **S** *∈* R*m**×**m*  is asymmetric.

#### 3. Methods

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/2b6c3e4cb38942f39335e493202cd1ab" width="80%" height="80%" />

- *Alternative Neighborhood Generation*

  - **alternative neighborhood** refers to a group of users who share similar preferences with the specified user.

  - being different from these existing literatures, the high-order in our work means relations beyond pairwise which cannot be captured with the conventional methods such as DFS.

  - focus on **triangular motifs** because of the widespread triadic closure in social networks.

    <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/6425f37878de4a6682d54afd708e9759" width="50%" height="50%" />

-  *Neighborhood Denoising*

  -  The final identified alternative neighborhood should be those users which contribute most to the recommendation task.
  - we use the motif *M*8-induced relations to serve as the reliable part because *M*8-induced relations are a subset of the explicit social relations while they are strengthened by common purchases.
    -  To impose this constraint, we concatenate the motif-based GCN with a fully-connected multi-layer perception (MLP) and make them nearly work as a concrete autoencoder.
  - the GCN is the encoder while the MLP is the decoder.From the perspective of data flflow, the input is the motif-induced adjacency matrix, the learned representation is the output of the concrete selector layer. 

- *Attentive Social Recommendation*

  - perform embedding propagation between both user pairs and user-item pairs.
  -  following the design of LightGCN, we combine different embeddings of different layers to constitute the final embeddings *e∗u* and *e∗i* for model prediction.

-  *Unifying All Modules with Adversarial Training*

  -  select new neighbors that can minimize the gap between the scores of the neighbors and the current user on the items purchased by the current user,which is explained to find neighbors who have the similar preferences with the current user. 
  - maximize this gap because the user herself should show more affection to the purchased item. 

#### 4. Experiments

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/377840eb03614dfbb02bee3d580b57c2" width="50%" height="50%" />

- *Evaluation*
  - To evaluate the performance of all methods, two relevancy-based metrics *Precision@10* and *Recall@10* and one ranking-based metric *NDCG@10* are used. For a fair comparison, we rank all the candidate items to calculate these three metrics.
- *Baselines*
  - Random 
  - BPR 
  - SBPR 
  - IF-BPR 
  - DiffNet++ 
  - RSGAN 
  - LightGCN 

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/ee1b24ba21624a42ba7fb9389c305f72" width="70%" height="70%" />


