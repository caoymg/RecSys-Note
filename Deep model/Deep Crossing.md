# 🚗 **Deep Crossing**

###### Deep Crossing: Web-Scale Modeling without Manually Crafted Combinatorial Features

###### Publishment: https://dl.acm.org/doi/abs/10.1145/2939672.2939704

<img src="https://p1-tt-ipv6.byteimg.com/img/pgc-image/36073ff73ce84bbf9e0bbdbe8f1c3a52~tplv-obj.image" width="100%" height="100%" />

<img src="https://p6-tt-ipv6.byteimg.com/img/pgc-image/33280dd49c1a4b2e865ec4314931b5f7~tplv-obj.image" width="50%" height="50%" />



## 1. Model Architecture

<img src="https://p26-tt.byteimg.com/img/pgc-image/5dcf399d20334437b91094f6ecc1ede9~tplv-obj.image" width="50%" height="50%" />

#### 1.1 **Embedding and Stacking Layers**

The embedding layer consists of a single layer of a neural network, with the general form:

<img src="https://p1-tt-ipv6.byteimg.com/img/pgc-image/95e48effce4b42a5a58ac4a89f3d55c8~tplv-obj.image" width="50%" height="50%"/>

- *j* indexes the individual feature,
- **X** *Ij* *∈* R*nj* is the input feature
- W is an *mj* *×* *nj* matrix
-  b*∈* R*nj*
- **X** *Oj* is the embedded feature. When *mj* *< nj* , embedding is used to reduce the dimensionality of the input feature. 
- The per element max operator is usually referred to as a *rectified linear unit* (ReLU) in the context of neural networks.

 The output features are then stacked (concatenated) into one vector as the input to the next layer:

<img src="https://p6-tt-ipv6.byteimg.com/img/pgc-image/3e1426f6bfb74ae5bac2edf07ed3f39f~tplv-obj.image" width="50%" height="50%" />

#### **1.2 Residual Layers**

Deep Crossing uses a slightly modified Residual Unit that doesn’t use convolutional kernels.

<img src="https://p6-tt-ipv6.byteimg.com/img/pgc-image/33280dd49c1a4b2e865ec4314931b5f7~tplv-obj.image" width="50%" height="50%" />

