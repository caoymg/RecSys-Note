# 🚗 NCF

###### **Neural Collaborative Filtering**

###### Publishment: https://dl.acm.org/doi/abs/10.1145/3038912.3052569

<img src="https://img.imgdb.cn/item/60549ac4524f85ce293b7bd9.png" width="100%" height="100%" />



## 1.  NCF framework

<img src="https://camo.githubusercontent.com/f6837a03f5f20d88b2cb523ad24dc6a039a47eef1108c7244143a76b075c98ae/68747470733a2f2f696d672e696d6764622e636e2f6974656d2f3630353439633832353234663835636532393363373936632e706e67" width="60%" height="60%" />

#### 1.1 MF's limitation caused by using an inner product

Despite the effectiveness of MF for collaborative filtering, it is well-known that its performance can be hindered by the simple choice of the interaction function — inner product. For example, for the task of rating prediction on explicit feedback, it is well known that the performance of the MF model can be improved by incorporating user and item bias terms into the interaction function

<img src="https://img.imgdb.cn/item/60549c69524f85ce293c6b1a.png" width="50%" height="50%"/>

#### 1.2  **Generalized Matrix Factorization (GMF)**

Intuitively, if we use an identity function for **a** *out*  and enforce **h** to be a uniform vector of 1, we can exactly recover the MF model.

<img src="https://p9-tt-ipv6.byteimg.com/img/pgc-image/b60af0df8868468986934c1798d0d5b3~tplv-obj.image" width="50%" height="50%" />

-  user latent vector **pu** and item latent vector **qi**
- **a** *out* denotes the activation function 
- **h** edge denotes weights of the output layer

#### 1.3 Fusion of GMF and MLP

allow GMF and MLP to learn separate embeddings, and combine the two models by concatenating their last hidden layer.

<img src="https://img.imgdb.cn/item/6054a08e524f85ce293f27fd.png" width="50%" height="50%" />
