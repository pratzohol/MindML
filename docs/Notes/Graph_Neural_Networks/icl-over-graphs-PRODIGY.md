---
title: "ICL : PRODIGY"
tags:
    - Prompting
    - ICL
    - Graphs
---

# ICL over Graphs : PRODIGY

In this note, I will cover the following paper ["PRODIGY : Enabling in-context learning over graphs"](https://arxiv.org/abs/2305.12600).

_**NOTE**_ : Definition of [[in-context-learning|In-context Learning (ICL)]] is already covered.


## 1. Introduction

We can easily infer that the in-context learning is a novel and one of the most intriguing capabilities of language models. However, how to enable in-context learning over graphs is still an unexplored question.

An in-context learner for graphs should be able to solve novel tasks on novel graphs. For example, give music product recommendations on Spotify when being trained on Amazon purchasing graph.

## 2. Challenges
1. How to formulate and represent node-, edge- and graph-level tasks over graphs with a _unified task representation_ that allows the model to solve diverse tasks without the need for retraining or parameter tuning.
2. How to design model architecture and pre-training objectives that enable in-context learning capabilities across _diverse tasks_ and _diverse graphs_ in the unified task representation.
3. Existing _graph pre-training methods_ only aim to learn good graph encoder and require fine-tuning to adapt to different tasks, while existing _meta-learning methods_ over graphs only aim to generalize across tasks within same graph.

```
Achieving in-context learning requires generalizing across different graphs and tasks 
without fine-tuning or parameter tuning.
```

### 2.1. How to tackle this?

The general approach presented to solve these problems as described in this paper is :

- **_Prompt Graph_** : It provides a way to unify the representation of node-, edge- and graph-level tasks over graphs. It has prompt examples, queries and connected with additional label nodes as shown in Figure below.

    ![Figure 1](../../assets/Notes/Graph_Neural_Networks/icl-over-graphs-prodigy-1.png)

    - This is an example of in-context few shot prompting over graphs for edge classification.
    - (A) Given source graph $\mathcal{G}$, we provide prompt examples $\mathcal{S}$ and queries $\mathcal{Q}$. $\mathcal{S}$ consist of input head and tail nodes and their labels.
    - (B) For each data-point in $\mathcal{S}$ and $\mathcal{Q}$, we construct its _Data graph_ $\mathcal{G}^D$ using the source graph $\mathcal{G}$.
    - (C) Then, we create *Task graph* to capture connection between each data-point and label. We learn embedding to represent Data graph as nodes $v_x$ for each data-point. There are label nodes $v_y$ for each y $\in \mathcal{Y}$. Each data-point is connected to every label nodes. For data-points in $\mathcal{S}$, each edge is marked by a boolean value, $\texttt{T}$ for true label and $\texttt{F}$ for others. 

- **_PRODIGY_** : **Pr**etraining **O**ver **D**iverse **I**n-Context **G**raphs S**y**stems, which is a framework for pre-training in-context learner over prompt graphs.
    - PRODIGY designs both model architecture and pre-training objectives with in-context task formulation over prompt graph.
    - Model architecture uses GNN to learn embeddings of node/edge representations and an attention mechanism for message passing over prompt graph.

## 3. In-Context Learning over Graphs

### 3.1. Classification Tasks

- Graph is defined as $\mathcal{G} = (\mathcal{V}, \mathcal{E}, \mathcal{R})$ where $\mathcal{V}$ is set of nodes, $\mathcal{E}$ is set of edges and $\mathcal{R}$ is set of relations. An edge $e = (u, r, v) \in \mathcal{E}$ consists of two nodes $u$, $v$ and a relation $r \in R$.
- Levels of classification :
    - Node-level : Given set of classes $\mathcal{Y}$, predict class label $y \in \mathcal{Y}$ for each node $v \in \mathcal{V}$. Hence, $\mathcal{X} = V$.
    - Edge-level : Predict label of potential edges formed by any pair of nodes, i.e., $\mathcal{X} = V \times V$. A common special case is that classes are same as the relations, i.e., $\mathcal{Y} = \mathcal{R}$.
    - Graph-level : Predict label on sub-graphs, i.e., input consists of nodes and edges both.
- Since, we want uniform formulation for different levels of tasks, we define space of input $\mathcal{X}$ consists of graphs, i.e., $x_i \in \mathcal{X}$ where $x_i = (\mathcal{V}_i, \mathcal{E}_i, \mathcal{R}_i)$.
    - For node-level classification, $|\mathcal{V}_i| = 1$ and $|\mathcal{E}_i| = 0$
    - For edge-level classification, $|\mathcal{V}_i| = 2$ and $|\mathcal{E}_i| = 0$
    (Since, we are predicting label of potential edges, we don't have any edges in the input, and instead input consists of pair of nodes)
### 3.2. Few-shot Prompting

- For a _k_-shot prompt with downstream _m_-way classification tasks with $|\mathcal{Y}| = m$ classes, we use small number of input-label pairs $\mathcal{S} = \{(x_i, y_i)\}_{i=1}^{m \cdot k}$ as _prompt examples_. Here, we have _k_ samples for each label (class) $y_i \in \mathcal{Y}$.
- Set of queries $\mathcal{Q} = \{x_i\}_{i=1}^n$ is also sampled. We want to predict labels for each query $x_i \in \mathcal{Q}$.
- _Important_ difference between graphs and language models w.r.t. prompting is that the source graph $\mathcal{G}$ contains information about the input, and hence, we need to include $\mathcal{G}$ in the prompt.

## 4. PRODIGY (Solution)

### 4.1. Prompt Graph Representation

Given the information as a prompt, the pre-trained model should be able to directly output the predicted labels for the queries via in-context learning. Thus, to formulate information as unified and efficient form of input, this paper proposes their _in-context task formulation prompt graph_.

Prompt graph consists of both Data Graph and Task Graph. 

1. **_Data graph_** : We perform _contextualization_ of each data-point in $\mathcal{S}$ and $\mathcal{Q}$ using source graph $\mathcal{G}$. We want to have more information about the data-point $x_i = (\mathcal{V}_i, \mathcal{E}_i, \mathcal{R}_i)$ without having to represent the whole source graph $\mathcal{G}$.
    - Intuitively, it makes sense to sample a $k$-hop neighborhood to construct data graph $\mathcal{G}^D$.
    - Formally, $\mathcal{G}_i^D = (\mathcal{V}_i^D, \mathcal{E}_i^D, \mathcal{R}_i^D) \sim \bigoplus_{j = 0}^ k \texttt{Neighbor} (\mathcal{V}_i, \mathcal{G}, j)$, where $\texttt{Neighbor}$ is a function which returns exact $j$-hop neighborhood of each node in $\mathcal{V}_i$ in $\mathcal{G}$.
    - NOTE : $\bigoplus$ ([[bigoplus|\bigoplus]]) is a direct sum operator.
    - _Input Node Set_ : For the data graph $\mathcal{G}^D$, the nodes in $\mathcal{V}_i$ (before contextualization) correspond to this set. For node classification, it is a single target node whereas for link prediction it is a pair of nodes.

1. **_Task graph_** : After contextualizing each data-point to a data graph $\mathcal{G}^D$, we then construct task graph $\mathcal{G}^T$ to better capture the connection and relationship among the inputs and the labels.
    - For each data graph $\mathcal{G}_i^D$, we represent the input as _data node_ $v_{x_i}$.
    - For each label $y_i \in \mathcal{Y}$, we represent the label as _label node_ $v_{y_i}$.
    - So, overall task graph contains $m \cdot k + n$ _data nodes_ and $m$ _label nodes_. ($m \cdot k$ _prompt examples_ and $n$ _queries_)
    - For the query set, we add single directional edge from each label node to each query data node.
    - For prompt examples, each data node is connected to every label node via bidirectional edges, where edge with true labels are marked as $\texttt{T}$ and rest are marked as $\texttt{F}$.

> It is also possible to extend prompt graph to non-classification tasks and free-form text prompting. For example, for numerical regression and other free-form generation tasks (e.g. text generation), one can extend our task graph to contain _vector values_ on the _edges_ to represent $y_i$.

What I understood is that they don't mean that by just extending vector values on edges can solve the problem of numerical regression and free-form generation tasks. They mean that by adding vector values on edges, we can represent different prediction tasks. Suppose, an edge has vector {1, 0} then it means that for task1, it is true and for task2, it is false. So, we can have multiple tasks on the same prompt graph.

### 4.2. Pre-training

We need a pre-training strategy that can pre-train a generalizable model capable of in-context learning. We assume access to pre-train graph $\mathcal{G}_\texttt{pretrain}$ which is independent of of source graph $\mathcal{G}$ for downstream task. Prompt examples and queries are sampled from $\mathcal{G}$ and model is trained on $\mathcal{G}_\texttt{pretrain}$ which we want to be generalizable to a graph $\mathcal{G}$. 

#### 4.2.1. Message Passing Architecture over Prompt Graph

1. **_Data Graph Message Passing_** : We use MP (message passing) GNN $M_\texttt{D}$ that learns node embeddings $E$ for nodes in each $\mathcal{G}^D$.  
Here, $d$ is the embedding dimension and $\mathcal{G}^D$ is the whole data graph and not individual data graph for each data-point. $M_D$ can be implemented using GCN or GAT.

    $$E \in \mathbb{R}^{|\mathcal{V}^D| \times d} = M_D (\mathcal{G}^D)$$

    To get single embedding $G_i$ of each data graph, we aggregate the node embeddings using some pooling function.

    - For node classification, pooling updates the node representation of _single input node_ $\mathcal{V}_i$, for prediction.

        $$G_i = E_{\mathcal{V}_i}$$

    - For link prediction, we concatenate the embeddings of the _pair of input nodes_, as well as max pooling over all node embeddings (including input pair of nodes, I think) with an additional linear layer to convert the embedding size back to $d$.

        $$G_i = W^T(E_{v_1 \in \mathcal{V}_i} || E_{v_2 \in \mathcal{V}_i} || max(E_i)) + b$$

        where || represents concatenation, $W \in \mathbb{R}^{3d \times d}$ is learnable weight matrix and $b$ is learnable bias.

    **_NOTE_** : After performing this step, we get the embedding of data nodes $v_x$ in the task graph $\mathcal{G}^T$. So, we can say that the task graph $\mathcal{G}^T$ is now contextualized.

1. **_Task Graph Message Passing_** : In previous step, there is no communication between $\mathcal{S}$ and $\mathcal{Q}$. So, we do this via message over task graph $\mathcal{G}^T$. Using the connections in the task graph, we want to update the node embeddings of _data nodes_ and _label nodes_.

    The initial embedding of data node $v_{x_i}$ is $G_i$ and the embedding of label node $v_{y_i}$ can either be initialized with random Gaussian or  using some additional information available about the labels.

    Each edge has two binary features $e_{ij}$ that indicates  
    1) whether edge comes from an example or query, and
    2) the edge type, i.e, $\texttt{T}$ or $\texttt{F}$.

    So, we apply another GNN $M_\texttt{T}$ to update the node embeddings of task graph $\mathcal{G}^T$. 

    $$H = M_T (\mathcal{G}^T)$$

    For $M_T$, attention based GNN was used, where each nodes perform attention to other nodes at each layer.

    ```
    The goal of this step is to learn a better representation of the label nodes using
    the support examples and propagate label information back to the support and query
    graph representation for a more task-specific graph representation.
    ```

#### 4.2.2. In-context Pre-training Objectives

##### Pre-training Task Generation

##### Prompt Graph generation with augmentation

##### Pre-training Loss

[//begin]: # "Autogenerated link references for markdown compatibility"
[in-context-learning|In-context Learning (ICL)]: ../Miscellaneous/in-context-learning "In-context Learning (ICL)"
[bigoplus|\bigoplus]: ../Maths/bigoplus "\bigoplus"
[//end]: # "Autogenerated link references"
