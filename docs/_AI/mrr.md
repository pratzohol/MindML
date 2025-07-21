---
title: Mean Reciprocal Rank (MRR)
---

# Mean Reciprocal Rank (MRR)

# Definition

MRR is a standard metric in ranking tasks, when there is a single correct answer per query.

For  $N$  queries, let's say you predict  $\text{rank}_i$  for the correct result (one which should ideally be ranked 1). Then, 

\[
\text{MRR} = \frac{1}{N} \sum_{i=1}^{N} \frac{1}{\text{rank}_i} \quad \text{where} \quad \text{MRR} \in [0, 1]
\]
