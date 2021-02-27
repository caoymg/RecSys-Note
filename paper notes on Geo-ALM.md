### *Title: Geo-ALM: POI Recommendation by Fusing Geographical Information and Adversarial Learning Mechanism*

###### Authors: Wei Liu, Zhi-Jie Wang, Bin Yao and Jian Yin

###### Publication: [SIGIR '18: The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval](https://dl.acm.org/doi/proceedings/10.1145/3209978)June 2018 Pages 355–364https://doi.org/10.1145/3209978.3209981

###### Implementation: https://github.com/hexiangnan/adversarial_personalized_ranking

###### Note: Yiming Cao



#### **1. Introduction**

- The negative samples in ranking pairs are obtained randomly, which may fail to leverage “critical” negative samples in the model training. On the other hand, most of previous works did not exploit geographical information comprehensively, which may also affect the performance.

- Fuse **geographical features** with **generative adversarial networks(GAN)** to achieve Point-of Interest (POI) recommendation.

  

#### 2. **Preliminaries**

- For a user *ui* , its visited POIs are usually called the **positive samples**. The unvisited POIs are usually called the **negative samples**.

- To leverage the missing data to learn user’s preference between visited POIs and unvisited POIs, a representative method is the **pairwise ranking**, the ranking loss function is based on **maximum likelihood estimation**. The model can distinguish positive sample from most of negative samples (see the right part). With random sampling, it is hard to choose the critical negative samples (see the ones in the red circle). Moreover, without geographical information *GI*, similar sample vectors may be hard to differentiate, e.g., the ones in the red circle. Yet, with *GI*, it is easier to distinguish them (see the black dot).

  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/3ab7ae6888394a078934df8001b5d014" alt="img" style="zoom:50%;" />



#### 3.Methods

-  *The Discriminator Module*

  - essentially, it is a maximum likelihood estimate problem: make the probability,  *f* *θ*(*vj* *> vj'* *|**u**i*), as maximal as possible.

  - different from the previous models whose negative samples are obtained by randomly sampling from the whole POI set *V* , our discriminator uses the negative samples *vj'* picked by the *generator*.

  - fuse geographical information into the discriminator:  The POI feature →*vj* depicts the user’s preference to POI. The region feature → *Rvj* can characterize the sketch of the POIs in the corresponding region, its dot product with user’s embedding can depict user’s geographical and general preference to the region.

    <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/c9cfb10f1031457b9345452f25c8bbe1" alt="img" style="zoom:67%;" />

  - inspired by the Skip-gram model, we exploit the geographical correlation to enhance the prior knowledge.

- *The Generator Module*

  - the essence of the generative module is to provide the discriminator with high-quality negative samples, which helps the discriminator improve the training performance. 

  - For a newly generated negative pair (*ui* *, vj'* ) together with the positive pair (*ui* *, vj* ), the reward function calculated by the discriminator is defifined as

    <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/9bc5f0a4d2224db88e0f02eea8b406be" alt="img" style="zoom:67%;" />

#### 4. Experiments

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/923cfa1f6046409099bb38d1e6458bba" alt="img" style="zoom:50%;" />

- *Evaluation*

  - where L denotes the top-*n* POIs recommended by the model for user *u*, T denotes the POI set that user *u* really visited.

  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/b560dc9bc51f43b7b76d58443d087eac" alt="img" style="zoom:50%;" />

- *Baselines*

  - **BPR**
  - **IRenMF**
  - **Rank-GeoFM **(a ranking-based MF model that learns users’ preference rankings for POIs, and includes the geographical influence of neighboring POIs)
  - **PACE** (alleviates data scarcity via smoothing among neighboring POIs, and it treats the geographical context by regularizing POI feature, based on context graphs)
  -  **GeoIE** (exploits geographical information by asymmetry and high variation geographical influence, and constructs a cross-entropy object function to learn model parameters)

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/3856b260d2814bad96f2a890a300acf2" alt="img" style="zoom:50%;" />

