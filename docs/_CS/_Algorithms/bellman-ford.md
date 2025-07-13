---
title: Bellman Ford Algo
---

# Bellman Ford Algorithm

## 1. Problem Statement

Given a graph and a source vertex in the graph, find shortest paths from source to all vertices in the given graph.

## 2. Solution

### 2.1 When to use

- Dijkstra's algo fails if graph contains negative edges or negative cycle.
- Bellman-Ford works well if the graph contains negative edges.
- It is also able to detect if any negative cycle is present in the graph.
* Bellman ford works with directed graphs. For undirected graphs, convert it to directed graph first.

### 2.2 Code

```cpp
vector<int> bellman_ford(int V, vector<vector<int>>& edges, int src) {
	vector<int> dist(V, 1e8);
	dist[src] = 0;

    vector<int> parent(V);
    for (int i = 0; i < V; i++) {
        parent[i] = i;
    }

	// Relaxation of all the edges V times, not (V - 1) as we
    // need one additional relaxation to detect negative cycle
	for (int i = 0; i < V; i++) {
		for (vector<int> edge : edges) {
			int u = edge[0];
			int v = edge[1];
			int wt = edge[2];
			if (dist[u] != 1e8 && dist[u] + wt < dist[v]) {

                // If this is the Vth relaxation, then there is
                // a negative cycle
                if(i == V - 1)
                    return {-1};

                // Update shortest distance to node v
                dist[v] = dist[u] + wt;
                parent[v] = u;
            }
		}
	}

    return dist;
}
```

## 4. Complexity

- Time Complexity --> $O(V*E)$
- Space Complexity --> $O(V)$

