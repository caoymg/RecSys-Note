### *Title: LARA: Attribute-to-feature Adversarial Learning for New-item Recommendation*

###### Authors: Changfeng Sun, Han Liu, Meng Liu, Zhaochun Ren, Tian Gan, Liqiang Nie

###### Publication: [WSDM '20: Proceedings of the 13th International Conference on Web Search and Data Mining](https://dl.acm.org/doi/proceedings/10.1145/3336191)January 2020 Pages 582–590https://doi.org/10.1145/3336191.3371805

###### Implementation: https://github.com/changfengsun/LARA

###### Note: Yiming Cao



#### **1. Introduction**

- aim to optimize a matching problem between existing users and a virtual user profile generated from attributes of the targeting new-item( item cold-start problem). 
- to generate the representation of the user who likes the new item, we design a generative model with multigenerators to generate user profiles from different perspectives of the new item, respectively.
-  the generated user is the most appropriate user for the given item. Afterwards, a discriminator is introduced to distinguish the real user profile and the generated profile.

#### 2. **Preliminaries**

- *Problem Formulation*
  -  in the item cold-start scenario, given a new item *It*  with *k* attributes, we aim to generate the representation of the user who likes the new item according to its attributes, *i.e.*, *ut* ∈ R*k* 
  - *ut* is a user-attribute interaction vector, where the *i*-th element reflects if the user has interaction with the *i*-th attribute of the item.

#### 3. Methods

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/68af02c5016c4eeb95cd07caa7e9b82f" width="50%" height="50%" />

- *Generative Model*
  - Firstly, each attribute *ac i* of the conditional item is assigned to a special generator *дi* , which accepts the mission to **generate the profile of the latent user from a certain perspective**.
  - Afterwards, a neural network *G* is employed to incorporate all generated user profile vectors and output the completely generative user feature vector.

-  *Discriminative Model*

  - The goal of the discriminator is to distinguish the (**u**+, *I* *c* ) pair from the other two kinds of pairs as much as possible.

    <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/046e9102b5f24c0fad7bf954e615d36d" width="50%" height="50%"/>

- *Overall Objective*

  - Compared with existing GAN-based recommendation methods, our method introduce third kind of training tuples, consisting of a conditional item and **a false user** who is uninterested in the conditional item. The reason of introducing this term is that the observed ground truth relevant user-item tuples can **only make the generative user approximate the right users** for conditional item, nevertheless, the observed ground truth ill-suited user-item tuples can **turn the generative user away from the false users** for conditional item. 

  

#### 4. Experiments

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/563dff06c0114306b518dcead6d3c6d8" width="50%" height="50%"/>

- *Evaluation*

  -  employ precision (P@K), mean average precision (M@K), and normalized discounted cumulative gain (NDCG@K) as

    the evaluation metrics 

- *Baselines*

  - **UserPop**
  - **BPR-kNN**
  - **LCE**(combines both the content and the collaborative information.)
  - **NFM**(enhances factorization machines by modelling higher-order and non-linear feature interactions.)
  - **DNN**

  <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/70307eab285d4367afb7260259613a7e" width="80%" height="80%" />


