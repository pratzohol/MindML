---
title: "Topological Sort"
tags:
    - Algorithms
    - Graphs
---

# Topological Sort

## 1. Definition

- In topological sorting, node `u` will always appear before node `v` if there is a directed edge from node `u` towards node `v`, i.e., `u` -> `v`.
- This is only possible for _Directed Acyclic Graphs_ (**DAGs**).

## Using DFS

```cpp
void dfs(int node, int vis[], stack<int> &st, vector<int> adj[]) {
    vis[node] = 1;
    for (auto it : adj[node]) {
        if (!vis[it]) dfs(it, vis, st, adj);
    }
    st.push(node);
}

vector<int> topoSort(int V, vector<int> adj[]) {
    int vis[V] = {0};
    stack<int> st;

    for (int i = 0; i < V; i++) {
        if (!vis[i]) {
            dfs(i, vis, st, adj);
        }
    }

    vector<int> ans;
    while (!st.empty()) {
        ans.push_back(st.top());
        st.pop();
    }
    return ans;
}
```

- This Algorithm assumes that graph is DAG.

## Using BFS (Kahn's Algorithm)

```cpp
vector<int> findOrder(int n, vector<vector<int>>& adj) {
    vector<int> indegree(n, 0);

    for (int i = 0; i < n; i++) {
        for (int j : adj[i]) {
            indegree[j]++;
        }
    }

    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) q.push(i);
    }

    vector<int> ans;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        ans.push_back(node);

        for (int nbr : adj[node]) {
            if (--indegree[nbr] == 0) {
                q.push(nbr);
            }
        }
    }

    return (ans.size() == n) ? ans : vector<int>(); //check if there's a cycle
}
```
