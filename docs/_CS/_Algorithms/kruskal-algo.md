---
title: Kruskal's Algo (MST)
---

## 1. Problem Statement

Given a weighted, undirected, and connected graph of V vertices and E edges. Find the sum of weights of the edges of the Minimum Spanning Tree.

### 1.1 What is MST ?

A **Spanning tree** is tree-like subgraph consisting of all the vertices in graph. There could be multiple spanning trees. The spanning tree with edges having minimum sum of weights is considered MST.

## 2. Solution

- We need to use [DSU](../disjoint-set.md) data structure to check whether two nodes are in the same path or not.

```cpp
int spanningTree(int V, vector<vector<int>>& adj){

        vector<vector<int>> edges;
        for (int i = 0; i < V; i++) {
            for (auto it : adj[i]) {
                int nbr = it[0];
                int wt = it[1];
                int node = i;

                edges.push_back({wt, node, nbr});
            }
        }
        sort(edges.begin(), edges.end());

        DSU dsu(V);

        //mst sum
        int sum = 0;
        for (auto it : edges) {
            int wt = it[0]
            int u = it[1];
            int v = it[2];

            if (dsu.find_set(u) != dsu.find_set(v)) {
                // To store MST edges
                // just add (u, v) to a vector
                sum += wt;
                dsu.union_sets(u, v);
            }
        }

        return sum;
    }
```

## 4. Complexity

- Time Complexity --> $O(E \log E)$
- Space Complexity --> $O(E + V)$