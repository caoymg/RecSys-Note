### *Title: Geo-ALM: POI Recommendation by Fusing Geographical Information and Adversarial Learning Mechanism*

###### Authors: Liu, Wei & Wang, Zhi-Jie & Yao, Bin & Yin, Jian.

###### Publication: IJCAI 2019

###### Note: Yiming Cao



#### **1. Introduction**

- The negative samples in ranking pairs are obtained randomly, which may fail to leverage “critical” negative samples in the model training. On the other hand, most of previous works did not exploit geographical information comprehensively, which may also affect the performance.

- Fuse **geographical features** with **generative adversarial networks(GAN)** to achieve Point-of Interest (POI) recommendation.

  

#### 2. **Preliminaries**

- For a user *ui* , its visited POIs are usually called the **positive samples**. The unvisited POIs are usually called the **negative samples**.

- To leverage the missing data to learn user’s preference between visited POIs and unvisited POIs, a representative method is the **pairwise ranking**, the ranking loss function is based on **maximum likelihood estimation**. The model can distinguish positive sample from most of negative samples (see the right part). With random sampling, it is hard to choose the critical negative samples (see the ones in the red circle). Moreover, without geographical information *GI*, similar sample vectors may be hard to differentiate, e.g., the ones in the red circle. Yet, with *GI*, it is easier to distinguish them (see the black dot).

  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/3ab7ae6888394a078934df8001b5d014" height="50%" width="50%" />



#### 3.Methods

-  *The Discriminator Module*

  - essentially, it is a maximum likelihood estimate problem: make the probability,  *f* *θ*(*vj* *> vj'* *|**u**i*), as maximal as possible.

  - different from the previous models whose negative samples are obtained by randomly sampling from the whole POI set *V* , our discriminator uses the negative samples *vj'* picked by the *generator*.

  - fuse geographical information into the discriminator:  The POI feature →*vj* depicts the user’s preference to POI. The region feature → *Rvj* can characterize the sketch of the POIs in the corresponding region, its dot product with user’s embedding can depict user’s geographical and general preference to the region.

    <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/c9cfb10f1031457b9345452f25c8bbe1" height="50%" width="50%" />

  - inspired by the Skip-gram model, we exploit the geographical correlation to enhance the prior knowledge.

- *The Generator Module*

  - the essence of the generative module is to provide the discriminator with high-quality negative samples, which helps the discriminator improve the training performance. 

  - For a newly generated negative pair (*ui* *, vj'* ) together with the positive pair (*ui* *, vj* ), the reward function calculated by the discriminator is defifined as

    <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/9bc5f0a4d2224db88e0f02eea8b406be" height="50%" width="50%" />

#### 4. Experiments

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/923cfa1f6046409099bb38d1e6458bba" height="50%" width="50%" />

- *Evaluation*

  - where L denotes the top-*n* POIs recommended by the model for user *u*, T denotes the POI set that user *u* really visited.

  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/b560dc9bc51f43b7b76d58443d087eac" height="50%" width="50%"** />

- *Baselines*

  - **BPR**
  - **IRenMF**
  - **Rank-GeoFM **(a ranking-based MF model that learns users’ preference rankings for POIs, and includes the geographical influence of neighboring POIs)
  - **PACE** (alleviates data scarcity via smoothing among neighboring POIs, and it treats the geographical context by regularizing POI feature, based on context graphs)
  -  **GeoIE** (exploits geographical information by asymmetry and high variation geographical influence, and constructs a cross-entropy object function to learn model parameters)

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/3856b260d2814bad96f2a890a300acf2" height="50%" width="50%" />

