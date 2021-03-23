# 🚗 AFM

###### Attentional Factorization Machines:Learning the Weight of Feature Interactions via Attention Networks

###### Publishment:  https://arxiv.org/abs/1708.04617

<img src="https://p26-tt.byteimg.com/origin/pgc-image/6af1bdb39a944a6686a2b9e7ffe23391" width="100%" height="100%" />


## 1.  AFM framework

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/e541890257d44348a7366e5ce7b54ec5" width="90%" height="90%" />

#### 1.1 The Pair-wise Interaction layer ( the same with NFM)

each interacted vector is the element-wise product of two distinct vectors to encode their interaction.

<img src="https://p26-tt.byteimg.com/origin/pgc-image/44304cd874bc41318a35fe7b576790dd" width="50%" height="50%"/>

-  ⊙ denotes the element-wise product of two vectors

-  set of non-zero features in the feature vector **x** be *X* , and the output of the embedding layer be *E* = { **v** *i* **x** *i* }, *i*∈X . 

#### 1.2  The Attention-based Pooling layer

employ the attention mechanism on feature interactions by performing a weighted sum on the interacted vectors.

<img src="https://files.imgdb.cn/tuchuang/2021/03/23/6059d4cf8322e6675c531509.png" width="50%" height="50%" />

 *aij* is the attention score for feature interaction *w*ˆ*ij* , which can be interpreted as the importance of *w*ˆ*ij* in predicting the target. 

 To estimate *aij*:

- learn it by minimizing the prediction loss❌  for features that have never co-occurred in the training data, the attention scores of their interactions cannot be estimated.
- parameterize the attention score with a multi-layer perceptron (*attention network*) ✅
  - The input to the attention network is the interacted vector of two features, which encodes their interaction information in the embedding space.
  - *t* denotes the hidden layer size of the attention network (*attention factor*).
  -  The attention scores are normalized through the softmax function.

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/9f4b4cbb93034a8090b173fd4738a29b" width="50%" height="50%" />



#### 1.3 the Overall Formulation of AFM  Model 

<img src="https://p26-tt.byteimg.com/origin/pgc-image/16e093d55a014aadad2de7957b61e602" width="50%" height="50%" />

