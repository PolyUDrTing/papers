Community Detection in General Hypergraph Via Graph Embedding

- Journal of the American Statistical Association



# Real Data Set

1. 

V: 267 patients

E: 44 categorical features, a hyperedge that contains all the patients sharing the particular feature value.  

Community: 211 vertices come from the abnormal patients and the other 53 ones come from the normal patients.

2. 

V: Mesh terms are annotated.

E: hyperedges are 10,472 papers.

Community:  Neoplasms (C04) and Nerve System Diseases (C10).



# Previous Work

due to the difficulty of lacking an appropriate adjacency tensor for nonuniform hypergraph.

1. SHP converts a nonuniform hypergraph to an incident matrix, and then maximizes the hypergraph associativity or minimizes the normalized hypergraph cut. 

2. WPTG represents the nonuniform hypergraph by a weighted adjacency matrix, and then standard graph community detection methods 

   i. hypergraph adjacency tensor to matrix and thus suffer from information loss

   ii. converting a nonuniform hypergraph to a uniform one by adding null vertices can be a better data processing approach than decom- posing a nonuniform hypergraph into a collection of uniform hypergraphs of different range. 



# Model

1. hypergraph embedding model:

   i. augmentation step: augmentation step introduces only one null vertex rather than multiple ones as suggested in Ouvrard, Goff

   ii. embedding step: extends the latent space model for graph network to general hypergraph network 

2. joint modeling framework is developed for simultaneously conducting hypergraph estimation and community detection.

3. asymptotic consistencies of the proposed method in terms of both hypergraph estimation and community detection in sparse hypergraph network



$$
\theta_{i_{1} \ldots i_{m}}=\log \left(\frac{p_{i_{1} \ldots i_{m}}}{s_{n}-p_{i_{1} \ldots i_{m}}}\right)
$$

$$
p_{i_{1} \ldots i_{m}}=s_{n}\left(1+e^{-\theta_{i_{1} \ldots i_{m}}}\right)^{-1}
$$

HEM: hypergraph embedding model
$$
\Theta=\mathcal{I} \times_{1} \boldsymbol{\alpha} \times_{2} \cdots \times_{m} \boldsymbol{\alpha}
$$

$$
\theta_{i_{1} \ldots i_{m}}=\mathcal{I} \times_{1} \boldsymbol{\alpha}_{i_{1}}^{T} \times_{2} \cdots \times_{m} \boldsymbol{\alpha}_{i_{m}}^{T}
$$

$\alpha=Z C$, HEM reduces to $\Theta=$ $\mathcal{B} \times_{1} Z \times_{2} \cdots \times_{m} Z$ with ${\mathcal{B}=\mathcal{I} \times_{1} C \times_{2} \cdots \times_{m} C \text {, which becomes }}$ an hSBM with membership matrix $Z \in\{0,1\}^{(n+1) \times(K+1)}$ and a transformed core probability tensor $\mathcal{B} \in \mathbb{R}^{(K+1) \times \cdots \times \times(K+1)}$.



# Algorithm

1. 


$$
\mathcal{L}(\boldsymbol{\alpha} ; \mathcal{A})=\frac{1}{\varphi(n, m)} \sum_{\delta_{i_{1}, \ldots_{m}}^{n+1, \text { ord }}=0} L\left(\theta_{i_{1} \ldots i_{m}} ; a_{i_{1} \ldots i_{m}}\right)
$$

$$
\mathcal{L}_{\lambda}(\boldsymbol{\alpha} ; \mathcal{A})=\mathcal{L}(\boldsymbol{\alpha} ; \mathcal{A})+\lambda_{n} J(\boldsymbol{\alpha})
$$
where $\lambda_{n}$ is a positive tuning parameter and
$$
J(\boldsymbol{\alpha})=\min _{Z \in \Gamma, C \in \mathcal{R}^{(K+1) \times r}} \frac{1}{n}\|\boldsymbol{\alpha}-Z C\|_{F}^{2}, C_{K+1}=r^{-1 / 2} \mathbf{1}_{r},
$$
2. 

$\boldsymbol{\alpha}_{1: n}^{(t+1)}=\boldsymbol{\alpha}_{1: n}^{(t)}-\eta_{t} \nabla_{\boldsymbol{\alpha}_{1: n}} \mathcal{L}_{\lambda}^{(t)}\left(\boldsymbol{\alpha}^{(t)}\right)$, where $\eta_{t}>0$ is the learning rate at step $t+1$, and
$$
\begin{aligned}
\nabla_{\boldsymbol{\alpha}_{1: n}} \mathcal{L}_{\lambda}^{(t)}\left(\boldsymbol{\alpha}^{(t)}\right)=& \frac{1}{\varphi(n, m)}\left\langle\mathcal{T} * \Delta, \mathcal{I} \times_{2} \boldsymbol{\alpha} \times_{3} \cdots \times_{m} \boldsymbol{\alpha}\right\rangle_{1: n}^{\{2, \ldots, m\}} \\
&+\frac{2 \lambda_{n}}{n}\left(\boldsymbol{\alpha}-Z^{(t)} C^{(t)}\right)_{1: n}
\end{aligned}
$$
it resembles the K-means formulation for α(t+1)  , and thus a standard K-means algorithm can be employed to solve for Z and C.

