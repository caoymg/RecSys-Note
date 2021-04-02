### *Title: Cross-Domain Recommendation with Adversarial Examples*

###### Authors: Haoran Yan, Pengpeng Zhao, Fuzhen Zhuang, Deqing Wang, Yanchi Liu, Victor S. Sheng

###### Publication: https://dl.acm.org/doi/abs/10.1145/3397271.3401087

###### Note: Yiming Cao



#### **1. Introduction**

- **Cross-domain recommendation** leverages the knowledge from relevant domains to alleviate the data sparsity issue. However, the state-of-the-art cross-domain models are vulnerable to adversarial examples, leading to possibly large errors in generalization.
- Develop a new Adversarial Cross-Domain Network (ACDN), where adversarial examples are dynamically generated to train a deep cross domain recommendation model.



#### 2. **Preliminaries**

**2.1  Notation**

Given a **source domain *S***  and a **target domain *T***  , in which users *U*  are shared, let *IS* and *IT* denote the item sets of  *S*  and  *T* . We define user-item interactions matrix **R** *T*  from user’s implicit feedback in  *T* , where the element *rui* is 1 if user *u* and item *i* have an interaction and 0 otherwise. Similarly, define user-item interactions matrix **R** *S*  from user’s implicit feedback in  *S*.

**2.2 Base Model**

MLP++ is adopted as the base model, which combines two MLPs through sharing the user embedding matrix. 

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/bf8e93deed8040b7b3d5e8cbcc107ea4" width="50%" height="50%" />

The source and target domains are modelled by two neural networks, and the performance can be improved through transferring knowledge between two domains.





#### 3. Methods

**3.1  Adversarial Examples**

define the adversarial perturbations as the model parameter perturbations maximizing the overall loss function:

<img src="https://p26-tt.byteimg.com/origin/pgc-image/71ffba6c09c64a25927df2792c493cd9" width="50%" height="50%" />

- *n* is the perturbations on the embedding parameters 

- *θ emb* = *{* **P** ,  **Q** *t*,  **Q** *s}*

-  *θ f* = *{**θ**ft* *, **θ**fs* *}* is the parameters in output and hidden layers. 

  Essentially, the adversarial perturbations **n** *adv* is a kind of **gradient noise**. 





**3.2 Adversarial Cross-Domain Network**

<img src="https://p26-tt.byteimg.com/origin/pgc-image/6476619227de430f8214d146e7d68895" width="60%" height="60%" />

The objective function of ACDN is defined as follows:

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/4564a487bd1a4775a770184918c55311" width="50%" height="50%" />

The architecture of the proposed model is shown in Fig. 1, which consists of four modules: 

- Input Layer

  First, the Input Layer adopts the one-hot encoding to encode user-item interaction indices.

- Embedding Layer

  Second, the one-hot encodings are embedded into continuous representations and add adversarial perturbations on them to construct adversarial examples in the Embedding Layer.

- Hidden Layers 

  Third, we transform the representations to the final ones in the Hidden Layers.

- Output Layer. 

     Finally, the Output Layer predicts the score with the final representations.





#### 4. Experiments

Table 1 summarizes the statistics of the **two real-world cross-domain datasets**. The first dataset Mobile contains data of user reading news and app installation. The **app installation** and **news reading** are the **target** and **source domain**, respectively. The second dataset Amazon contains the two largest categories, Books and Movies, where Books is the target domain and Movies is the source domain. On the two sparse datasets, we hope to **transfer knowledge form the source domain** to **improve the performance of the target domain recommendation**.

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/6e176114e9bc46e199520e49cc5bd88e" width="50%" height="50%"/>

We use the **leave-one-out method** to evaluate the item recommendation model. We randomly sample one interaction for each user as the validation item to determine the model hyper-parameters. 

For each user, **one interaction** is reserved as the **test item** and **99 items which are not interacted** are randomly sampled as **negative examples**. We **evaluate the model by ranking the 100 items**. We adopt the **Hit Ratio (HR)**, the **Normalized Discounted Cumulative Gain (NDCG)** and the **Mean Reciprocal Rank (MRR)** as the evaluation metrics and cut the ranked list at K = 10. 

- *Baselines*
  - **BPRMF**
  - **MLP**
  - **CMF**
  - **CDCF**
  - **MLP++**
  - **CSN**
  - **CoNet**
  - **SCoNet**

<img src="https://p26-tt.byteimg.com/origin/pgc-image/754c1edbcbc94d2f81ce7d32e0667cd2" width="70%" height="70%"/>
