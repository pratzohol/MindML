---
title: "Erdos Renyl Model"
---

# Erdos Renyl Model : Generating Random Graphs

## 1. Overview

- There are two variants of Erdos Renyl Model:
    - G(n, p) : n nodes, each edge is present with probability p
    - G(n, m) : n nodes, m edges are chosen uniformly at random from the set of all possible edges

- Equivalently, all graphs with n nodes and M edges have equal probability of $p^M (1-p)^{\binom{n}{2}-M}$
- The parameter p in this model can be thought of as a weighting function; as p increases from 0 to 1, the model becomes more and more likely to include graphs with more edges and less and less likely to include graphs with fewer edges.
-  A graph in G(n, p) has on average ${\binom{n}{2}}p$ edges. 
-  The distribution of the degree of any particular vertex is binomial: $P(deg(v)=k)=\binom{n-1}{k}{p^k}(1-p)^{n-1-k}$ 

## 2. References

- https://www.geeksforgeeks.org/erdos-renyl-model-generating-random-graphs/      