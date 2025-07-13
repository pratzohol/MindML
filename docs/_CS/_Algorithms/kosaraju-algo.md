---
title: Kosaraju's Algo
---

# Kosaraju's Algorithm

## 1. Problem Statement

Find Strongly Connected Components (SCCs) in a directed graph.

## 1.1 Strongly Connected Components (SCCs)

In a directed graph, a Strongly Connected Component is a subset of vertices where every vertex is reachable from each other.


## 2. Solution

```cpp
vector<vector<int>> kosaraju_scc(int V, vector<vector<int>> adj) {
    vector<int> vis(V, 0);
    stack<int> st;
    for (int i = 0; i < V; i++) {
        if (!vis[i]) {
            dfs(i, vis, adj, st);
        }
    }

    vector<vector<int>> adjT(V, vector<int>());
    for (int i = 0; i < V; i++) {
        vis[i] = 0;
        for (auto it : adj[i]) {
            adjT[it].push_back(i);
        }
    }

    vector<vector<int>> scc;
    while (!st.empty()) {
        int node = st.top();
        st.pop();
        if (!vis[node]) {
            vector<int> scc_i;
            dfs3(node, vis, adjT, scc_i);
            scc.push_back(scc_i);
        }
    }
    return scc;
}

void dfs(int node, vector<int> &vis, vector<vector<int>>& adj, stack<int> &st) {
    vis[node] = 1;
    for (auto it : adj[node]) {
        if (!vis[it]) {
            dfs(it, vis, adj, st);
        }
    }
    st.push(node);
}

void dfs3(int node, vector<int> &vis, vector<vector<int>>& adjT, vector<int>& scc_i) {
        vis[node] = 1;
        scc_i.push_back(node);

        for (auto it : adjT[node]) {
            if (!vis[it]) {
                dfs3(it, vis, adjT, scc_i);
            }
        }
    }
```

## 4. Complexity

- Time Complexity --> $O(V + E)$
- Space Complexity --> $O(V + E)$

