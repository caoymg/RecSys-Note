### *Title: Sequential Recommendation with Self-AttentiveMulti-Adversarial Network*

###### Authors: Ruiyang Ren, Zhaoyang Liu, Yaliang Li, Wayne Xin Zhao, Hui Wang, Bolin Ding, and Ji-Rong Wen

###### Publication: [SIGIR '20: Proceedings of the 43rd International ACM SIGIR Conference on Research and Development in Information Retrieval](https://dl.acm.org/doi/proceedings/10.1145/3397271)July 2020 Pages 89–98https://doi.org/10.1145/3397271.3401111

###### Implementation: https://github.com/ReyonRen/MFGAN

###### Note: Yiming Cao



#### **1. Introduction**

- When context information (called *factor*) is involved, model trained with *Maximum Likelihood Estimation (MLE)* is difficult to analyze when and how each individual factor would affect the final recommendation performance. 
- Proposed  **Multi-Factor Generative Adversarial Network (MFGAN)** has two kinds of modules: a **Transformer-based generator** taking user behavior sequences as input to recommend the possible next items, and **multiple factor-specific discriminators** to evaluate the generated sub-sequence from the perspectives of different factors.



#### 2. Methods
<img src="https://p26-tt.byteimg.com/origin/pgc-image/508deb7e2a6c4b88817df503ca2ebde0" width="50%" height="50%" />

- *Components*

  -  **the prediction component (*𝑖.𝑒.* generator *𝐺*)** which is a sequential recommendation model and successively generates the next items based on the current historical sequence. (the generator will not use any context information from the item side. It only makes the prediction conditioned on historical sequence data.)

    -  *Embedding Layer* 
      - item embedding matrix 𝑴 ∈ R |I|×*𝑑*:  project original one-hot representations of items to *𝑑*-dimensional dense representations. 
      - input embedding matrix *𝑬* ∈ R*𝑛*×*𝑑*: given a *𝑛*-length sequence of historical interactions, we apply a look-up operation from *𝑴*  to form the input embedding matrix *𝑬* 
      - learnable position encoding matrix *𝑷* ∈ R*𝑛*×*𝑑*: to enhance the input representations.
      - **input representations 𝑬𝐺** ∈ R*𝑛*×*𝑑* for the generator: summing two embedding matrices: 𝑬𝐺 = *𝑬* + *𝑷*.)
    -  *Self-attention Block*
    -  *Prediction Layer*

    <img src="https://p9-tt-ipv6.byteimg.com/origin/pgc-image/6ed577a0be3d49d08be3cd8d37213ac5" width="50%" height="50%"  />

  - **the evaluation component** that is a set of *𝑚* discriminators {*𝐷*1*,*𝐷*2*, . . . , *𝐷*𝑚} for judging the rationality of generated sequences. Each discriminator performs the judgement from a certain perspective based on the information of some corresponding factor. (*𝑖.𝑒.*, music recommender system: multiple discriminators specially designed with category information, popularity statistics, artist and album of music.)

    - embedding layer

    - one self-attention block

    - the degree of the rationality for the generated recommendation sequence is measured by a Multiple-Layer Perceptron (MLP)

      <img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/af9f66fe5d1f4b55a7ed0c74faf04beb" width="50%" height="50%"  />

- *Overall Procedure*

  - The evaluation results are sent back to the generator to guide the learning of the generator at the next round. Correspondingly, the discriminator is updated by taking the generated sequence and actual sequence (*i.e.,* ground-truth user behaviors) as the training samples for improving its discriminative capacity. 

    <img src="https://p26-tt.byteimg.com/origin/pgc-image/7220700b50a140858543e3f5423a364d" width="50%" height="50%"  />

    

#### 4. Experiments

<img src="https://p26-tt.byteimg.com/origin/pgc-image/9e534640d49447bf96e89b2fd4b324ae" width="50%" height="50%"  />

- evaluate it with **Mean Reciprocal Rank (MRR)**, **top-*𝑘* Normalized Discounted cumulative gain (NDCG@10)** and **Hit Ratio (HR@10)**. For each positive item in the test set, we pair it with 100 sampled items that the user has not interacted with as negative items. 
- *Baselines*
  - **PopRec**
  - **BPR**
  - **FM**
  - **IRGAN** ( combines two types of models via adversarial training, a generative model that generates items for a user and a discriminative model that determines whether the instance is from real data or generated)
  - **FPMC** ( combines Matrix Factorization and Markov Chain, which can simultaneously capture sequential information and long-term user preference)
  - **GRU** (proposes to incorporate additional feature vector as the input of GRU networks, which incorporates auxiliary features to improve sequential recommendation)
  - **SASRec** (It is a next-item sequential recommendation method based on the Transformer architecture, which adaptively considers interacted items for prediction. This method is the state of-the-art baseline for sequential recommendation)

![img](https://p3-tt-ipv6.byteimg.com/origin/pgc-image/63510c6f490446dcba0b59aeafca2fb6)



