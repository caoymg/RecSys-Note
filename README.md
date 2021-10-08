# RecSys-Note
- [🚗 1. fundamental part of RS](#---1-fundamental-part-of-rs)
  * [notes on shallow model](#notes-on-shallow-model)
    + [notes on AMF](#notes-on-amf)
    + [notes on SVD++](#notes-on-svd--)
    + [notes on FISM](#notes-on-fism)
  * [notes on deep model](#notes-on-deep-model)
    + [notes on FM](#notes-on-fm)
    + [notes on NFM](#notes-on-nfm)
    + [notes on Wide&Deep](#notes-on-wide-deep)
    + [notes on Deep Crossing](#notes-on-deep-crossing)
    + [notes on NCF](#notes-on-ncf)
- [🚗 2. adversarial training (by adding adversarial perturbations)](#---2-adversarial-training--by-adding-adversarial-perturbations-)
    + [paper notes on APR](#paper-notes-on-apr)
    + [paper notes on SACRA](#paper-notes-on-sacra)
- [🚗 3. adversarial learning (generative adversarial network -- using a generator and a discriminator)](#---3-adversarial-learning--generative-adversarial-network----using-a-generator-and-a-discriminator-)
    + [paper notes on APOIR](#paper-notes-on-apoir)
    + [paper notes on Cascading DQN](#paper-notes-on-cascading-dqn)
    + [paper notes on DASO](#paper-notes-on-daso)
    + [paper notes on ESRF](#paper-notes-on-esrf)
    + [paper notes on Geo-ALM](#paper-notes-on-geo-alm)
    + [paper notes on LARA](#paper-notes-on-lara)
    + [paper notes on MFGAN](#paper-notes-on-mfgan)





#### 🚗 1. fundamental part of RS

##### notes on shallow model 
###### notes on AMF
###### notes on SVD++
###### notes on FISM
<img src="https://p3-tt-ipv6.byteimg.com/img/pgc-image/6e6a47ae8a6947e2acd65e98dd352287~tplv-obj.image" width="100%" height="100%" />

##### notes on deep model 
###### notes on FM
###### notes on NFM
###### notes on Wide&Deep
###### notes on Deep Crossing
###### notes on NCF

<img src="https://p26-tt.byteimg.com/img/pgc-image/ccc5cb22247f4eba8fa16c2c4399355a~tplv-obj.image" width="100%" height="100%" />

#### 🚗 2. adversarial training (by adding adversarial perturbations)
###### paper notes on APR 
- Title:Adversarial Personalized Ranking for Recommendation[🌟first train MF with BPR, and then further optimize it under APR framework]
###### paper notes on SACRA
- Title: Adversarial Learning to Compare: Self-Attentive Prospective Customer Recommendation in Location based Social Networks[🌟prospective customer recommendation, recommend by making comparisons among users’ historical check-ins with adversarial training]

#### 🚗 3. adversarial learning (generative adversarial network -- using a generator and a discriminator)
###### paper notes on APOIR
- Title: Adversarial Point-of-Interest Recommendation[🌟geographical and social influence are also incorporated]
###### paper notes on Cascading DQN
- Title: Generative Adversarial User Model for Reinforcement Learning Based Recommendation System[🌟Using the estimated user behavior model φ and the corresponding reward function r as the simulation environment, then use reinforcement learning to obtain a recommendation policy.]
###### paper notes on DASO
- Title: Deep Adversarial Social Recommendation[🌟bidirectional mappings between the user-item interactions (item domain) and user-user connections (social domain)]
###### paper notes on ESRF
- Title: Enhancing Social Recommendation with Adversarial Graph Convolutional Networks[🌟alternative neighborhood generation, neighborhood denoising, and attention-aware social recommendation, GCN based]
###### paper notes on Geo-ALM
- Title: Geo-ALM: POI Recommendation by Fusing Geographical Information and Adversarial Learning Mechanism[🌟fuse geographical features with generative adversarial networks(GAN)]
###### paper notes on LARA
- Title: LARA: Attribute-to-feature Adversarial Learning for New-item Recommendation[🌟aim to optimize a matching problem between existing users and a virtual user profile generated from attributes of the targeting new-item(item cold-start problem)]
###### paper notes on MFGAN
- Title: Sequential Recommendation with Self-AttentiveMulti-Adversarial Network[🌟a Transformer-based generator taking user behavior sequences as input to recommend the possible next items, multiple factor-specific discriminators to evaluate the generated sub-sequence from the perspectives of different factors]
