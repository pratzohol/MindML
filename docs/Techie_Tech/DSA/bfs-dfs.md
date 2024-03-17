---
title: "BFS & DFS"
tags:
    - Algorithms
    - Graphs
---

# BFS & DFS

## 1. BFS

```cpp
vector<int> BFS(int V, vector<int> adj[]) {
    int visited[V] = {0};
    visited[0] = 1; //start from node 0

    queue<int> q;
    q.push(0);

    vector<int> bfs_nodes;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        bfs.push_back(node);

        for (int nbr : adj[node]) {
            if (!visited[nbr]) {
                visited[nbr] = 1;
                q.push(nbr);
            }
        }
    }
    return bfs_nodes;
}
```

## 2. DFS

```cpp
void dfs(int node, vector<int>& adj[], int visited[], vector<int>& dfs_nodes) {
    visited[node] = 1;
    dfs_nodes.push_back(node);

    for (int nbr : adj[node]) {
        if (!visited[nbr]) {
            dfs (nbr, adj, visited, dfs_nodes);
        }
    }
}
```
```cpp
vector<int> DFS(int V, vector<int> adj[]) {
    int visited[V] = {0};

    vector<int> dfs_nodes;

    dfs(0, adj, visited, dfs_nodes);
    return dfs_nodes;
}
```

## 3. Complexity

- Time Complexity -> $O(V + E)$
- Space Complexity -> $O(V)$
