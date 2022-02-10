# cross-validation

cross-validation works by splitting the data into multiple parts, or folds, holding out one fold at a time as a test set, fitting the model on the remaining folds and computing its error on the held-out fold, and finally averaging the errors across all folds to obtain the cross-validation error. 



# Limitation for graphs

low rank



# Idea

The two crucial parts of edge cross-validation are splitting node pairs at random and applying low-rank matrix completion to obtain a full matrix Â

Treating the network after removing the entries of A for some node pairs as a partially observed network, we apply low-rank matrix completion to complete the network and then fit the relevant model. This reconstructed network has the same rate of concentration around the true model as the full network adjacency matrix, allowing for valid analysis. 

imputation accuracy is not the primary goal; we expect, and in fact need, noisy versions of A.



# Algorithm

<font size=4>Step 1. Select the rank $\hat{K}$ for matrix completion, either from prior knowledge or using the model-free cross-validation procedure in $\S$ 3.1.</font>

<font color=Blue>Remark 1. the rank of M itself is directly associated with the model to be selected</font>

<font size=4>Step 2 . For $m=1, \ldots, N$ :</font>
(a) Randomly choose a subset of node pairs $\Omega \subset \mathcal{V} \times \mathcal{V}$ by selecting each pair independently with probability $p$.
(b) Apply a low-rank matrix completion algorithm to $(A, \Omega)$ to obtain $\hat{A}$ with rank $\hat{K}$.

<font color=Blue>Remark 3. An alternative to matrix completion is to simply replace all the held-out entries
with zeros</font>
$$
\hat{A}=S_{H}\left(\frac{1}{p} P_{\Omega} A, \hat{K}\right)
$$
where $S_{H}\left(P_{\Omega} A, \hat{K}\right)$ denotes the rank- $\hat{K}$ truncated singular value decomposition of a matrix $P_{\Omega} A$; that is, if the singular value decomposition of $P_{\Omega} A$ is $P_{\Omega} A=U D V^{\mathrm{T}}$ where $D=$ $\operatorname{diag}\left(\sigma_{1}, \ldots, \sigma_{n}\right)$ with $\sigma_{1} \geqslant \sigma_{2} \geqslant \cdots \geqslant \sigma_{n} \geqslant 0$, then $S_{H}\left(P_{\Omega} A, \hat{K}\right)=U D_{\hat{K}} V^{\mathrm{T}}$ where $D_{\hat{K}}=\operatorname{diag}\left(\sigma_{1}, \ldots, \sigma_{\hat{K}}, 0, \ldots, 0\right)$

<font color=Blue>Theorem 1 essentially indicates that ||Â − M || ≈ ||A − M ||</font>

(c) For each of the candidate models $q=1, \ldots, Q$, fit the model on $\hat{A}$ and evaluate its loss $L_{q}^{(m)}$ by averaging the loss function $L$ with the estimated parameters over the held-out $\operatorname{set} A_{i j},(i, j) \in \Omega^{\mathrm{c}}$.

<font size=4>Step 3. Let $L_{q}=\sum_{m=1}^{N} L_{q}^{(m)} / N$ and return $\hat{q}=\arg \min _{q} L_{q}$, the best model from set $\mathcal{C}$.</font>
$$
\sum(i, j) \in \Omega^{\mathrm{c}}\left(A_{i j}-\hat{A}_{i j}\right)^{2}
$$

<font color=Blue>picking the most
frequent selection is more robust to different tasks</font>

# Examples

1. rank selection

2. Model selection for block models

