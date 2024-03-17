---
title: \bigoplus
tags:
    - LaTeX
---

## 1. \bigoplus operator

This operator looks like this $\rightarrow\bigoplus$. In _LaTeX_, we use `$\bigoplus$` for this, and hence, the title name.(since you cannot use _LaTeX_ math mode in title ;-;)

## 2. Definition

$\bigoplus$ is a direct sum operator. I will give an example using graphs to explain this.

- Suppose only the nodes {$v_1$, $v_2$, $v_3$} $\in \mathcal{V}$ are given and I want to construct a subgraph $\mathcal{G}^D$ = ($\mathcal{V}^D$, $\mathcal{E}^D$, $\mathcal{R}^D$) around it by sampling its $k$-hop neighborhood from the graph $\mathcal{G}$.
- Then we find the $k$-hop neighbors of each node $v_m \in \mathcal{V}$, denoted as ($\mathcal{V}_{m}$, $\mathcal{E}_{m}$, $\mathcal{R}_{m}$).
- $(\mathcal{V}_{m}, \mathcal{E}_{m}, \mathcal{R}_{m}) =$ subgraph obtained by sampling $k$-hop neighborhood of the node $v_m \in \mathcal{V} \;\;\; \forall m = 1, 2, 3$.
- Finally, you have sets of vertices, sets of edges and sets of relations. We take union of these sets respectively over $m = 1, 2, 3$ to obtain the desired subgraph $\mathcal{G}^D$.  
- $\mathcal{V}^D = \bigcup_{m=1}^{m=3} \mathcal{V}_{m}$, &ensp; $\mathcal{E}^D = \bigcup_{m=1}^{m=3} \mathcal{E}_{m}$ &ensp; and &ensp; $\mathcal{R}^D = \bigcup_{m=1}^{m=3} \mathcal{R}_{m}$
- This can be equivalently represented as $\mathcal{G}^D = \bigoplus_{m=1}^{m=3} (\mathcal{V}_{m}, \mathcal{E}_{m}, \mathcal{R}_{m})$
