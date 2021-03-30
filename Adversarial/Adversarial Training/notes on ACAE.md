### *Title: Adversarial Collaborative Neural Network for Robust Recommendation*

###### Authors: Feng Yuan, Lina Yao, Boualem Benatallah

###### Publication: https://dl.acm.org/doi/abs/10.1145/3331184.3331321

###### Note: Yiming Cao



#### **1. Introduction**

- In real-world applications, user's feedbacks are possibly contaminated by imperfect user behaviours, posing challenges on the design of robust recommendation methods. 
- propose a general adversarial training framework for  neural network(NN)-based recommendation models and apply the approach on the collaborative auto-encoder model, improving both the model robustness and the overall performance.



#### 2. Methods

##### **2.1  Adversarial Noises**

define the adversarial noises as the model parameter perturbations maximizing the overall loss function.

<img src="https://img.imgdb.cn/item/606321f48322e6675c585abd.png" width="50%" height="50%" />

-  *ϵ* controls the noise level. 
- ∥·∥ denotes the *L*2 norm. 
- Θ is the model parameters.

The above noise is further served as the opponent factor in the minimax game of the training procedure. In general, the noise can be added in various ways, resulting in a generic loss function:

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/f90dfa0bce89449aa163c7101f8012f8" width="50%" height="50%" />

- *loss ORG* denotes the loss function of the original model without adversarial training. 
- Θ is the set of model parameters.
- *S* is the total number of ways to add the noises. 
- *λi* controls the noise impact from the *i*-th source. 
- ***Ni* denotes the noise from source *i***.

##### 2.2 ACAE Model

By adding noise only on encoder/decoder weights and setting all other noise sources to zero, we arrive at the ACAE model.

- When added on the **encoder or decoder weights**, the adversarial noise poses more detrimental impacts.
-  can be explained by noticing the number of entries in the encoder or decoder weights is much larger than that of other positions, such as user embeddings P.

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/51a3d43e0b6849aa9f957acfeb41f811" width="70%" height="70%" />

Limitation: ACAE only utilizes one parameter *ϵ* to control all noise sources.

##### 2.3  fine-grained ACAE(FG-ACAE)

To benefit more from the adversarial training, further insert noises in a fine-grained manner.

Shown in figure 1, **noise terms** are **controlled separately** using **different coefficients**, so that for those positions which are less affected by the adversarial noise, a larger noise coefficient should be applied. 

In addition, FG-ACAE concatenate two **additional noise vectors** on the **first hidden layer**, after which a fully-connected layer is employed to **mix the noise**.

In FG-ACAE, *ϵ* is still in effect, as a general noise level control. 

employ cross-entropy loss function:  *loss CE* = *y* log *σ*(*y*ˆ) − (1- *y*) log (1- *σ*(*y*ˆ)) due to the binary nature of the input data. 

Inserting these conditions into Eq. (3), we have the following loss function:

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/0154d50268a745138e7051dd7bdadced" width="60%" height="60%" />





<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/0154d50268a745138e7051dd7bdadced" width="60%" height="60%" />





#### 3. Experiments

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/ca4a44ab756e4d61b5a41fda6b05fa71" width="40%" height="40%"/>

- The **accuracy** is reported to compare the classification performance of all models. For the comparison of the robustness, following the previous work [Daniel Zügner and Stephan Günnemann. 2019. Certifiable Robustness and Robust Training for Graph Convolutional Networks. In *KDD*. 246–256.],  display **the average of instances’ largest *𝑞*** that they can be certifiably robust. This metric is referred as **avg-max *𝑞*.**
- *Baselines*
  -  **ItemPop**
  - **MF-BPR**
  - **CDAE**
  - **JRL**
  - **NeuMF**
  - **ConvNCF**
  -  **AMF**

