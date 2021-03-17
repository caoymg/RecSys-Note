# 🚗 **Wide & Deep Learning**

###### Wide & Deep Learning for Recommender Systems

###### Publishment: https://dl.acm.org/doi/abs/10.1145/2988450.2988454

<img src="https://p26-tt.byteimg.com/origin/pgc-image/0170329c2af44932b39b4067eca441cd" width="100%" height="100%" />

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/facc1647ef2040f58f00f3004daa148e" width="50%" height="50%" />



## 1. The Wide & Deep Learning model

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/4ab71877299e4263bd0f4ec6885306f3" width="80%" height="80%" />

#### 1.1 **The Wide Component**

The wide component is a generalized linear model of the form *y* = **w** *T* **x** + *b*. One of the most important transformations is the *cross-product transformation*, which is defined as:

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/facc1647ef2040f58f00f3004daa148e" width="50%" height="50%"/>

- cki is a boolean variable that is 1 if the i-th feature is part of the k-th transformation φk, and 0 otherwise.

#### 1.2  **The Deep Component**

 each hidden layer computes:

<img src="https://p26-tt.byteimg.com/img/pgc-image/f63a8e63f4234868b5d2d646b2f72bbc~tplv-obj.image" width="50%" height="50%" />

#### **1.3 Joint Training of Wide & Deep Model**

The wide component and deep component are combined using a **weighted sum of their output log odds** as the prediction, which is then fed to one common logistic loss func tion for joint training.

