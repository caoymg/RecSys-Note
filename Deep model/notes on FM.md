#  🚗 **FM**

##### Factorization Machines

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/59968d5dc1504c7f88f030953078079e" width="100%" height="100%" />

## 1. The FM model

#### 1.1 Input & Output

Assume we have the transaction data of a movie review system. The system records which user u ∈ U rates a movie (item) i ∈ I at a certain time t ∈ R with a rating r ∈ {1, 2, 3, 4, 5}. An example for a prediction task using this data, is to estimate **a function yˆ** that predicts the rating behaviour of a user for an item at a certain point in time.

feature vectors:

<img src="https://p26-tt.byteimg.com/origin/pgc-image/33c56e6081f94a49b1a1b5992b27b010" width="50%" height="50%" />



#### 1.2 Factorization Machine Model

In the ordinary linear model, we all consider each feature independently, and do not consider the **relationship between features**. But in fact, there may be some correlation between features.
In the case of **sparse data**, there will be very few samples satisfying the non-zero cross-term(The crossover is meaningful only if neither [xi] nor [xj] is zero.). When there are insufficient training samples, it is easy to lead to insufficient and inaccurate training of parameters. Then, the training problem of **cross-term parameters can be approximated by matrix factorization**. 

- The model equation for a factorization machine of *degree d = 2* is defined as:

<img src="https://p26-tt.byteimg.com/origin/pgc-image/705ec78697a943d4bd1a5c0a77e243fe" width="50%" height="50%" />

- *d-way Factorization Machine*

  <img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/8f3cf6a755a04a7ab48d4486e60ce1bd" width="50%" height="50%" />

The factorization machine models **all nested variable interactions** (comparable to a polynomial kernel in SVM), but uses a **factorized parametrization** instead of a dense parametrization like in SVMs.

