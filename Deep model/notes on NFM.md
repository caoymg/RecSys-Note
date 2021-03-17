#  🚗 **NFM**

##### Neural Factorization Machines for Sparse Predictive Analytics
##### Publication: https://dl.acm.org/doi/abs/10.1145/3077136.3080777
<img src="https://p26-tt.byteimg.com/origin/pgc-image/8f4f8b6ddc284e6398add3d22190d82d" width="100%" height="100%" />

## 1. The NFM model

#### 1.1 Input & Output

Similar to factorization machine, NFM is a general machine learner working with any real valued feature vector. Given a sparse vector **x** ∈ R*n* as input, where a feature value *x* *i* = 0 means the *i*-th feature does not exist in the instance, NFM estimates the target as:

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/b4d59e458dd84d899b79c3760b0d8f14" width="40%" height="40%" />

-  first and second terms are the linear regression part similar to that for FM, which models **global bias of data** and **weight of features**. 
- third term is the core component of NFM for modelling feature interactions, which is a **multi-layered feed forward neural network** as shown in Figure 2.

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/557aa2b450cd466cb2b2b833ef7c791c" width="50%" height="50%" />

#### 1.2 **Embedding Layer**

the embedding layer is a fully connected layer that projects each feature to a dense vector representation.

- only need to include the embedding vectors for non-zero features, *i.e.,* V*x* = {*x* *i* **v** *i* } where *xi* ≠0.
- **rescale an embedding vector by its input feature value**, rather than simply an embedding table lookup, so as to account for the real valued features



#### **1.3 Bi-Interaction Layer**

feed the embedding set V*x* into the Bi-Interaction layer, which is a **pooling operation** that **converts a set of embedding vectors to one vector**:

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/5b5ca31ccf6a448eb40c8bfca83ac5bf" width="30%" height="30%" />

- where  ⊙ denotes the element-wise product of two vectors
-  not introduce extra model parameter, and more importantly, it can be efficiently computed in linear time (*O*(**kN**x ) time), where **N**x denotes the number of non-zero entries in **x**. 



#### 1.4 **Hidden Layers**

By specifying **non-linear activation functions**, such as sigmoid, hyperbolic tangent (tanh), and Rectier (ReLU), the model can **learn higher-order feature interactions** in a **non-linear way**.

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/bb69c944bad3433db7546d9225b88655" width="30%" height="30%" />

#### 1.5 **Prediction Layer.** 

the output vector of the last hidden layer **z** *L* is transformed to the final prediction score.



#### 1.6  **Learning**

1. For regression, a commonly used objective function is the squared loss.
2. For classication task, we can optimize the hinge loss or log loss. 
3. For ranking task, we can optimize pairwise personalized ranking loss  or contrastive max-margin loss.
4.  use mini-batch Adagrad as the optimizer, rather than the vanilla SGD. Its main advantage is that the learning rate can be self adapted during the training phase.

## 2. **EXPERIMENTS**

#### 2.1 experimental settings

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/354f1c3a65ff44aa94bc66284856a0ae" width="50%" height="50%" />

- evaluate with ***root mean square error* (RMSE)**, where a lower RMSE score indicates a better performance. Note that RMSE has been widely used for **evaluating regression tasks** such as **recommendation with explicit ratings**  and **click-through rate prediction**.
- **Baselines**
  - **LibFM**， **HOFM**，**Wide&Deep**，**DeepCross**

#### 2.2 Findings

-  dropout can also be an effective strategy to address overfittng of linear latent-factor models.
- by addressing the internal covariate shift with BN, the model’s generalization ability can be improved.
- best performance is when using one hidden layer only.
  - because the Bi-Interaction layer has encoded informative second-order feature interactions, and based on which, a simple non-linear function is suffcient to capture higher-order interactions. 

