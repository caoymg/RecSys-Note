# 🚗 NGCF

###### Neural Graph Collaborative Filtering

###### Publishment:  http://182.150.59.104:8888/https/77726476706e69737468656265737421f4fb0f9d243d265f6c0f/doi/abs/10.1145/3331184.3331267

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/468a910045484d5d9e505afc4ac3a13e" width="100%" height="100%" />


## 1.  NGCF framework

<img src="https://p1-tt-ipv6.byteimg.com/origin/pgc-image/7f60f687884c48f6a02e8bb1a65c4eac" width="60%" height="60%" />

#### 1.1 **Embedding Propagation Layers**（**First-order Propagation**）

**Basis**：the interacted items provide direct evidence on a user’s preference; analogously, the users that consume an item can be treated as the item’s features and used to measure the collaborative similarity of two items.  

**major operations**: *message construction* and *message aggregation*.

**Message Construction**. For a connected user-item pair (*u*,*i*), the message from *i* to *u*:

<img src="https://p26-tt.byteimg.com/origin/pgc-image/ad2cddc35e904bdc99de61dbf9e2c9db" width="50%" height="50%"/>

- W1, W2  are the trainable weight matrices to distill useful information for propagation (*d*′ is the transformation size) 

- Distinct from conventional graph convolution networks that consider the contribution of e*i* only, here additionally encode the interaction between e*i* and e*u* into the message being passed via e*i* ⊙ e*u* （⊙ denotes the element-wise product.）
- *pui* as the graph Laplacian norm (N*u* and N*i* denote the first-hop neighbors of user *u* and item *i*)



**Message Aggregation**. In this stage,  aggregate the messages propagated from *u*’s neighborhood to refine *u*’s representation.

<img src="https://p26-tt.byteimg.com/origin/pgc-image/59b690165a9f47a6ad009549a30d6fa7" width="50%" height="50%" />

- e(1)*u* denotes the representation of user *u* obtained after the first embedding propagation layer.
- activation function of LeakyReLU allows messages to encode both positive and small negative signals. 
- Note that in addition to the messages propagated from neighbors N*u* , we take the self-connection of *u* into consideration: **m*u*←*u* = W1e*u*** , which retains the information of original features (W1 is the weight matrix shared with the one used in Equation (3)). 

#### 1.2  **Embedding Propagation Layers**（**High-order Propagation**）

By stacking *l* embedding propagation layers, a user (and an item) is capable of receiving the messages propagated from its *l*-hop

neighbors.

<img src="https://p26-tt.byteimg.com/origin/pgc-image/2baddd141b5d46ed938b9f16bc3f5c6f" width="50%" height="50%" />

 in the *l*-th step, the representation of user *u* is recursively formulated as:

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/030c7c7712d945e3bb221e1e612fd9ac" width="50%" height="50%" />

wherein the messages being propagated are defined as follows:

<img src="https://p3-tt-ipv6.byteimg.com/origin/pgc-image/90963b3710a4473a9698c886cb9a16d1" width="50%" height="50%" />

- W(*l*) 1 , W(*l*) 2 , ∈ R *dl* ×*dl-1* are the trainable transformationmatrices (*dl* is the transformation size)
- e(*l-1* )*i* is the item representation generated from the previous message-passing steps,memorizing the messages from its (*l*-1)-hop neighbors. 

#### **1.3 Propagation Rule in Matrix Form**

the matrix form of the layer-wise propagation rule (equivalent to Equations (5) and (6))

<img src="https://p26-tt.byteimg.com/origin/pgc-image/b30aaec56da94e67b34ce7a778a7e4ad" width="50%" height="50%" />

- E(*l*) ∈ R(*N* +*M*)×*dl* are the representations for users and items obtained after *l* steps of embedding propagation. 
- E (0) is set as E at the initial message-passing iteration
-  I denote an identity matrix. 
- L represents the Laplacian matrix for the user-item graph, which is formulated as:

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/f75c543fd10646b89414132f2a99f1eb" width="40%" height="40%" />

- R ∈ *RN* ×*M* is the user-item interaction matrix

- 0 is all zero matrix
- A is the adjacency matrix  
- D is the diagonal degree matrix


## 2. Light GCN framework

<img src="https://p26-tt.byteimg.com/origin/pgc-image/ed9d3f83defa46aa8724d8e535eee28e" width="50%" height="50%" />

LightGCN adopts the **simple weighted sum aggregator** and **abandon** the use of *feature transformation* and *nonlinear activation*. 

The graph convolution operation (a.k.a., propagation rule) in LightGCN is defined as

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/b56fc14844d8459aa29f254983d0e8d2" width="50%" height="50%" />

*Matrix Form*

<img src="https://p6-tt-ipv6.byteimg.com/origin/pgc-image/1f4cae65f885493d8dcd58e2d60e72b0" width="50%" height="50%" />
