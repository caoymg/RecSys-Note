### *Title: Adversarial Collaborative Auto-encoder for Top-N Recommendation*

###### Authors: Feng Yuan, Lina Yao, Boualem Benatallah

###### Publication: https://ieeexplore.ieee.org/abstract/document/8851902

###### Note: Yiming Cao



#### **1. Introduction**

- Most of the state-of-the-art deep learning-based recommendation models assume that user feedbacks are noise-free, on which the neural networks (NN) are trained.

- This work focus on utilizing the nonlinearity of NNs and adversarial training. 

- the first attempt to combine adversarial learning with neural networks for item

  recomendation tasks.



#### 2. **Preliminaries**

**2.1  Collaborative Denoising Auto-encoders**

CDAE utilizes a DAE to learn the distributed embedding vectors of users and items, **p** *u* *∈* R*K*  and **q** *i* *∈* R*K* respectively. 

The predictions for user *u* on the item set *I* are collected in a vector **ˆy** *u* as:

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/2059b930861d44a39c63371d6622dc12" width="50%" height="50%" />

-  **W** **1** *,***W** **2**, **b** **1**, **b** **2**  are encoder and decoder weights and biases
- **p** *u* *∈* R*K*  is the embedding vector for user *u*. 
- *h*(*·*) and *f*(*·*) are activation functions.
-  **y**˜*u* *∈* R*I* is a noise-corrupted version of **y** *u* *∈* R*I* (the original preference vector of user *u* in *Y*).

CDAE exerts the noises randomly on the input data to train a robust set of parameters, which makes it less effective.



#### 3. Methods

**3.1   The Impact of Internal Noises**

The noises are added on different positions as follows:

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/28220fbe75154451b36787636940d1b4" width="50%" height="50%" />

conduct the experiments on a pre-trained CAE model using two datasets: MovieLens-1M, and FilmTrust. Model performance is evaluated by HR on the hold-out testing dataset. Sigmoid functions are employed with the cross-entropy loss due to the binary nature of the input ratings.

- To summarize, both types of noises(Gaussian noise/adversarial noise) pose a more deterimental impact when they are added on encoder or decoder weights.Encoder weight perturbations are less harmful and CAE is more robust against Gaussian noise .

Choose to add adversarial noises on the **encoder/decoder weights** to make the performance degradation as large as possible



**3.2 Adversarial Collaborative Auto-encoder**

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/15d25e1bd7e341c1b95b0b685aeec0a7" width="60%" height="60%" />

employ **multiple adversarial regularizers** and train the model in a minimax manner:

<img src="https://p26-tt.byteimg.com/origin/pgc-image/643fb34749884fc48a7307788a548609" width="60%" height="60%" />

<img src="https://p26-tt.byteimg.com/origin/pgc-image/9eea480c9f29403ca53e4f8326d08a46" width="60%" height="60%" />

-  *loss* *NN* denotes the loss function of NN without adversarial training. 
- Θ is the set of model parameters 
- *S* is the total number of possible ways to add adversarial noises.
-  *λ* *i* controls the noise impact from the *i*-th source. 
- *n* *i* denotes the noise from source *i*.



##### 3.3 Optimization for ACAE

1) pre-training CAE to get optimal parameters Θ; 

2) re-training the above model by iterativelymaximizing (Eq. (3)) and minimizing the loss (Eq. (6)).

Employ mini-batch gradient descent to optimize relevant parameters. 

- pre-training: a fixed learning rate

- adversarial training: Adagrad (adaptively change the learning rate for fine parameter tuning)

#### 4. Experiments

Table 1 summarizes the statistics of the **two real-world cross-domain datasets**. The first dataset Mobile contains data of user reading news and app installation. The **app installation** and **news reading** are the **target** and **source domain**, respectively. The second dataset Amazon contains the two largest categories, Books and Movies, where Books is the target domain and Movies is the source domain. On the two sparse datasets, we hope to **transfer knowledge form the source domain** to **improve the performance of the target domain recommendation**.

<img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/9e2a116886fd432fb12f84ababfe84cf" width="60%" height="60%" />

We use the **leave-one-out method** to evaluate the item recommendation model. We randomly sample one interaction for each user as the validation item to determine the model hyper-parameters. 

For each user in the dataset, we leave out the lastest user-item interaction and randomly select 200 unrated items to form the testing set. The rest interactions form the training set. For those datasets without timestamp information, such as

FilmTrust, we randomly select one interaction for each user.

 We adopt the **Hit Ratio (HR@5)** and the **Normalized Discounted Cumulative Gain (NDCG@5)** . 

- *Baselines*
  - ItemPop
  - MF-BPR
  - CDAE
  - NeuMF
  - AMF

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/3138cff1c473417ebe57b4e229136f0f" width="100%" height="100%"/>

