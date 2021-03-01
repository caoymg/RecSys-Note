### *Title: Deep Adversarial Social Recommendation*

###### Authors: [Wenqi Fan](https://arxiv.org/search/cs?searchtype=author&query=Fan%2C+W), [Tyler Derr](https://arxiv.org/search/cs?searchtype=author&query=Derr%2C+T), [Yao Ma](https://arxiv.org/search/cs?searchtype=author&query=Ma%2C+Y), [Jianping Wang](https://arxiv.org/search/cs?searchtype=author&query=Wang%2C+J), [Jiliang Tang](https://arxiv.org/search/cs?searchtype=author&query=Tang%2C+J), [Qing Li](https://arxiv.org/search/cs?searchtype=author&query=Li%2C+Q)

###### Publication: IJCAI 2019

###### Note: Yiming Cao



#### **1. Introduction**

- one challenge is to learn **separated user representations** in the user-item interactions (item domain) and user-user connections (social domain) while transferring the information from the social domain to the item domain for social recommendation.
- introduce a principled way to transfer users’ information from social domain to item domain using a **bidirectional mapping** method where we cycle information between the two domains to progressively enhance the user representations.
- propose a **deep adversarial social recommender system DASO**, which can harness the power of adversarial learning to learn the bidirectional mappings between the two domains,and ultimately optimize better user and item representations.

#### 2. **Preliminaries**

-  **user-item interactions matrix** **R** *∈* R *N×M*  from user’s implicit feedback, where the *i, j*-th element *ri,j* is 1 if there is an interaction (e.g., clicked/bought) between user *ui* and item *vj* , and 0 otherwise. However,*ri,j* = 1 does not mean user *ui* actually likes item *vj* . Similarly, *ri,j* = 0 does not mean *ui* does not like item *vj* , since it can be that the user *ui* is not aware of the item *vj* . 

- the **social network between users** can be described by a matrix **S** *∈* R *N×N* , where *s**i,j* = 1 if there is a social relation be

  tween user *ui* and user *uj* , and 0 otherwise.

- Given the interaction matrix **R** and the social network **S**, we aim to predict the unobserved entries (i.e., those where *r**i,j* = 0) in **R**.



#### 3. Methods

- *Cyclic User Modeling*

  - non linear mapping operation ( a **M**ulti **L**ayer **P**erceptron), denoted as **h *S→I***, to transfer user’s information from the social domain to the item domain.

  - a bidirectional mapping between these two domains (achieved by including another nonlinear mapping **h *I→S***) is utilized to help cycle the information between them to progressively enhance the user representations in both domains, which has the same network structure as the **h *S→I (MLP)***.

  -  To learn these mappings, we further introduce **cycle reconstruction**.

    -  Its intuition is that transferred knowledge in the target domain should be reconstructed to the original knowledge in the source domain.

      <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/5aeef06d214f450c9e8b7537bb40fd18" width="50%" height="50%" />

- *Item Domain Adversarial Learning*

  - **Discriminator *DI*** aims to distinguish real user-item pairs (i.e., real samples) and the generated high-quality negative samples. The discriminator can be optimized by minimizing the objective in eq. (2) with the generator fixed using stochastic gradient methods.
  - **Generator *GI*** can be viewed in a reinforcement learning setting, where log(1 + *exp*(*f* *D* ( ))) is the reward given to the action “selecting *vi* given a user *ui*” performed according to the policy probability *GI* (*v|ui*).
  - Note that different from the way of optimizing user and item representations with the typical negative sampling on traditional recommender systems, the adversarial learning technique tries to generate “diffificult” and high-quality negative samples to guide the learning of user and item representations.

  <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/f3b252b2fa7f466d8255e35789a8ffe3" width="50%" height="50%" />

- *Social Domain Adversarial Learning*

  - In order to learn better user representations from the social perspective, another adversarial learning is harnessed in the social domain.

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/d29a66cf32cf4fc0819673854aff9ca1" width="50%" height="50%" />

#### 4. Experiments

<img src="https://p26-tt.byteimg.com/origin/pgc-image/7ca3368a39684b9d85f781cc6d5c03c3" width="50%" height="50%" />

- *Evaluation*
  - Precision@K and Normalized Discounted Cumulative Gain (NDCG@K). We set K as 3, 5, and 10. 
- *Baselines*
  - **BPR**,**SBPR** ,**SocialMF**
  - **DeepSoR**
  - **GraphRec**
  - **IRGAN** ( combines two types of models via adversarial training, a generative model that generates items for a user and a discriminative model that determines whether the instance is from real data or generated.)

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/75833228722e46b4bb776446c67aff9f" width="50%" height="50%" />
