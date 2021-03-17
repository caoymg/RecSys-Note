#  🚗 **FM**

##### Factorization Machines

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/59968d5dc1504c7f88f030953078079e" width="50%" height="50%" />

## 1. The NFM model

#### 1.1 Input & Output

Similar to factorization machine, NFM is a general machine learner working with any real valued feature vector. Given a sparse vector **x** ∈ R*n* as input, where a feature value *x* *i* = 0 means the *i*-th feature does not exist in the instance, NFM estimates the target as:

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/b4d59e458dd84d899b79c3760b0d8f14" width="50%" height="50%" />

-  first and second terms are the linear regression part similar to that for FM, which models **global bias of data** and **weight of features**. 
- third term is the core component of NFM for modelling feature interactions, which is a **multi-layered feed forward neural network** as shown in Figure 2.

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/557aa2b450cd466cb2b2b833ef7c791c" width="50%" height="50%" />