### *Title: Certifiable Robustness to Discrete Adversarial Perturbations for Factorization Machines*

###### Authors: Yang Liu, Xianzhuo Xia, Liang Chen, Xiangnan He, Carl Yang, Zibin Zheng

###### Publication: https://dl.acm.org/doi/abs/10.1145/3397271.3401087

###### Note: Yiming Cao



#### **1. Introduction**

- propose the first method for the certifiable robustness of factorization machines with respect to the **discrete perturbation on input features**.
- To enhance the FM’s robustness against such perturbations, a robust training procedure is presented whose core idea is to **increase the number of instances that are certifiably robust.**



#### 2. **Preliminaries**

The **existing robust factorization machine** considers the environmental noise in user signals. They model such noise by associating an uncertainty vector (e.g. Gaussian distribution) on the input features and seek a solution that remains feasible for all possible perturbations on input features via minimizing the worst-case loss.

However, there are two limitations:

- **Neglecting inputs’ discrete property.** the worst-case loss they minimize is insufficient to model the real worst-case perturbation.
- **Lacking the robustness certificate.** 

**2.1 Problem Formulation**

- model the recommendation problem as binary classification (the label is {1, -1}) whose input data is binary. The perturbation we considered is to change the 0 components of input features to 1 which is closer to the reality.

- Since the fields of input features usually contain specific semantics, directly modifying the fields may change the semantics of the instance. 

  - focus on **perturbing users’ historical items**. That is, the perturbed user-item interactions are injected into the input features.

-  the problem is defined as:

  Problem 1. *Given a trained FM* *𝑓𝜃* *, a target instance 𝒙, and a perturbation space P*𝑞*(*𝒙*)*, check whether all *𝒙*ˆ ∈ P*𝑞* (*𝒙*) *belong to the same class of* *𝒙.*

- To check whether a perturbed instance *𝒙*ˆ ∈ P*𝑞* (*𝒙*) is still classified to the same class, the margin *𝛿* defined as follows between its and the true predicted result is required to be computed.

  <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/49f793c35a4543ddb0f68368f64b646e" width="50%" height="50%" />

  <img src="https://p26-tt.byteimg.com/origin/pgc-image/70d89a01c22f4bd2b27d298a2822d006" width="66%" height="66%" />

#### 3. Methods

**3.1 Non-robust Certificates**

the traditional FM model is vulnerable to discrete adversarial perturbations.

-  adopt a **greedy algorithm** to compute the **worst-case of 𝛿** : sequentially modify the most promising components following a local optimal strategy. Since only one component is modified each time, the value of feature interactions of the perturbation vector itself is its self-interaction term.

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/13c9c533bdfd48b497d65c649a139b05" width="60%" height="60%" />



**3.2 Robust Certificates**

To certificate the robustness of an instance whose predicted label is -1, we derive an upper bound of *𝛿* reached by all possible perturbations. Similarly, for the instance whose predicted label is 1, the lower bound of *𝛿* is derived.

To compute the bound, the calculation of equation (5) is divided into two sub-problems. 

Although the solutions of the first and second sub-problem may be different which means such a prediction may not exist, the robustness of the instance can be verified since the bound is worse than the worst-case can be achieved. 

<img src="https://img.imgdb.cn/item/606284088322e6675ca88482.png" width="60%" height="60%" />



**3.3 Robust Training**



<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/dcbd28048c2249a0a06c65829e27972c" width="50%" height="50%" />

- D is the set of all labeled instances. 
- *𝑦𝑠* is the label of the instance *𝒙𝑠*. 

<img src="https://p26-tt.byteimg.com/origin/pgc-image/6af184d3b5c34ccaa5452b0f5858a514" width="50%" height="50%" />

- *𝑓𝜃* (*𝒙𝑠*) + *𝑏*(*𝒙𝑠*) is the bound of prediction under the worst case perturbation. 
- The perturbation space is P*𝑞* (*𝒙𝑠*) where *𝑞* is a hyper-parameter needed to be tuned.

To perform robust training, the model is first trained according to the equation (12) until convergence. Then we train the model using the equation (13) until convergence.

#### 4. Experiments

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/9c99b72a192f46849893d6767249c581" width="40%" height="40%"/>

- The **accuracy** is reported to compare the classification performance of all models. For the comparison of the robustness, following the previous work [Daniel Zügner and Stephan Günnemann. 2019. Certifiable Robustness and Robust Training for Graph Convolutional Networks. In *KDD*. 246–256.],  display **the average of instances’ largest *𝑞*** that they can be certifiably robust. This metric is referred as **avg-max *𝑞*.**
- *Baselines*
  - **MF**
  - **RFM-1 **( state-of-the-art robust factorization machine which forces the model to make right prediction under the continuous noise.)
  - **RFM-2**

<img src="https://p26-tt.byteimg.com/origin/pgc-image/754c1edbcbc94d2f81ce7d32e0667cd2" width="70%" height="70%"/>