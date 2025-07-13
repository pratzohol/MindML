---
title: Floyd Warshall Algo
---

## 1. Problem Statement

Given a graph and a source vertex in the graph, find shortest paths between all pair of vertices in the given graph.

## 2. Solution

### 2.1 When to use

- Works for both directed and undirected weighted graphs and can handle negative weight edges.
- Does not work for the graphs with negative cycles.
- Can detect neagtive cycles just like [Bellman Ford Algo](./bellman-ford.md)

### 2.2 Code

- We assume if there is no edge between `i` and `j`, then `matrix[i][j] = 1e8` and `matrix[i][i] = 0`.

```cpp
void floyd_warshall(vector<vector<int>>& matrix) {
    int n = matrix.size();

    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = min(matrix[i][j], matrix[i][k] + matrix[k][j]);
            }
        }
    }

    // To check for negative cycles,
    // if matrix[i][i] is negative then there is a negative cycle present
    for (int i = 0; i < n; i++) {
        if (matrix[i][i] < 0) {
            cout << "Negative cycle found" << endl;
        }
    }
}
```

## 4. Complexity

- Time Complexity --> $O(V^3)$
- Space Complexity --> $O(1)$