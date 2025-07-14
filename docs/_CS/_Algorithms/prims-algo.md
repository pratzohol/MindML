---
title: Prim's Algo (MST)
---

## 1. Problem Statement

Given a weighted, undirected, and connected graph of V vertices and E edges. Find the sum of weights of the edges of the Minimum Spanning Tree.

## 1.1 What is MST ?

A **Spanning tree** is tree-like subgraph consisting of all the vertices in graph. There could be multiple spanning trees. The spanning tree with edges having minimum sum of weights is considered MST.

## 2. Solution

```cpp
vector<vector<int>> prim_mst(int V, vector<vector<int>>& adj){
    // triplets of {edge weight, node, parent}
    // if you just want to find the sum, use pair<int, int>
    priority_queue<vector<int>, vector<vector<int>>, greater<vector<int>>> pq;
    pq.push({0, 0, -1});

    vector<int> vis(V, 0);

    // stores min sum of MST
    int sum = 0;
    // edges of MST in form of {u, v, wt}
    vector<vector<int>> ans;

    while (!pq.empty()) {
        auto it = pq.top();
        pq.pop();

        int wt = it[0];
        int node = it[1];
        int parent = it[2];

        if (vis[node] == 1) continue;

        // add it to the mst
        vis[node] = 1;
        sum += wt;
        if (parent != -1) {
            ans.push_back({node, parent, wt});
        }

        for (auto it : adj[node]) {
            int nbr = it[0];
            int w = it[1];
            if (!vis[nbr]) {
                pq.push({w, nbr, node});
            }
        }
    }

    // returns edges of MST
    return ans;
}
```

## 4. Complexity

- Time Complexity --> $O(E \log E)$
- Space Complexity --> $O(E + V)$