### *Title: Generative Adversarial User Model for Reinforcement Learning Based Recommendation System*

###### Authors: **Xinshi Chen, Shuang Li, Hui Li, Shaohua Jiang, Yuan Qi, Le Song**

###### Publication: *Proceedings of the 36th International Conference on Machine Learning*, PMLR 97:1052-1061, 2019.

###### Note: Yiming Cao



#### **1. Introduction**

- develop a **generative adversarial network** to imitate user behavior dynamics and learn her reward function.
- develop a novel **Cascading DQN algorithm** to obtain a combinatorial recommendation policy which can handle a large number of candidate items eficiently.

#### 2. **Preliminaries**

- **Environment** *(a logged online user)*, **State** *( an ordered sequence of a user’s historical clicks)*  and **State Transition** *(a user behavior model which returns the transition probability for **s** t+1 given previous state **s** t and the set of items At displayed by the system)* are associated with the user, **Action** *(a subset of k items chosen by the recommender from It to display to the user)* and  **Policy** are associated with the recommendation system, and **Reward Function** is associated with both of them. 
-  the value of the reward is determined by the user’s state and the clicked item once the item occurs in the display set *A*.

#### 3. Methods

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/14577004dc4744afbf855d8477135e93" alt="img" style="zoom:80%;" />

-  Using the estimated **user behavior model *φ*** and the corresponding **reward function *r*** as the **simulation environment**, then use **reinforcement learning** to obtain a **recommendation policy**.

- *Generative Adversarial User Model*

  - represent the state **s**t  as an embedding of the historical sequence of items clicked by the user before session *t*, define the reward function *r*(**s**t, **a**t) based on the state and the embedding of the current action **a**t.
  - state embedding function *h*(*·*)
    - a simple and effective position weighting scheme. Let W ∈ R*m**×**n* be a matrix where the number of rows *m* corresponds to a fixed number of historical steps, and each column corresponds to one set of importance weights on positions. Then the embedding function *h* *∈* R *dn×*1 can be designed as **s**t = *h*(F) := *vec*[ *σ* (FW + B),  where  vec[·] turns the input matrix into a long vector by concatenating the matrix columns. 
    - one can also use an LSTM to capture the history. However, the advantage of the position weighting scheme is that the history embedding is produced by a shallow network. It is more effificient for forward-computation and gradient backpropagation.
  - **reward *rθ*** will extract some statistics from both real user actions and model user actions, and try to magnify their difference (or make their negative gap larger). In contrast, the **user model *φα*** will try to make the difference smaller, and hence more similar to the real user behavior.

- *Cascading RL Policy for Recommendation*

  <img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/cf90fc23c58240c992847ee2b52d05ed" alt="img" style="zoom:50%;" />

  - an item put in different combinations can have different probabilities of being clicked, which is indicated by the user model and is in line with reality. Thus, the optimal policy for recommendation in Eq. (7) will be very expensive to compute. 
  - To address this challenge, we will design not just one but **a set of *k* related Q-functions** which will be used in a cascading fashion for finding the maximum in Eq. (7).

#### 4. Experiments

- *Dataset*
  - (1) MovieLens  (2) LastFM  (3) Yelp  (4) Taobao  (5) YooChoose  (6) Ant Financial

- *Predictive Performance of User Model*

  - *Evaluation*
    - Top-*k* precision (Prec@*k*) is employed as the evaluation metric. It is the proportion of top-*k* ranked items at each page view that are actually clicked by the user, averaged across test page views and users.
  - *Baselines*
    - IKNN, S-RNN, SCKNNC, XGBOOST, DFM, W&D-LR, W&D-CCF

  ![img](https://p6-tt-ipv6.byteimg.com/origin/pgc-image/476890110fb14496ac43dee2709867e9)

- *Recommendation Policy Based on User Model*

  - *Evaluation*

    - 1. Cumulative reward 

      - For each recommendation action, we can observe a user’s behavior and compute her reward *r*(st, at) using the test model.

    - 2.  CTR (click through rate)

      - the ratio of the number of clicks and the number of steps it is run. 

  - *Baselines*

    - W&D-LR, W&D-CCF,GAN-Greedy

    <img src="https://p26-tt.byteimg.com/origin/pgc-image/9c627e48bc7e4acd91005536edd720a3" alt="img" style="zoom:50%;" />

  

-  *User Model Assisted Policy Adaptation*
  - how the CTR increases as each policy interacts with and adapts to users over time. 
  - The results show that the CDQN policy pre-trained over a GAN user model can quickly achieve a high CTR even when it is applied to a new set of users 



