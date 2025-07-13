---
title: "Dijkstra's Algorithm"
---

# Dijkstra's Algo

## 1. Problem Statement

Given a graph and a source vertex in the graph, find shortest paths from source to all vertices in the given graph.

- NOTE : If graph is a **DAG**, then simply do [[topo-sort|Topological Sort]] and store the vertices in a stack. Then pop the vertices from the stack and update the distances of the adjacent vertices.
- This is because to calculate shortest path of any node, we need to calculate the shortest path of all the nodes that come before it. Thus, this automatically calls for topological sorting.

## 2. Solution

- **NOTE:** Dijkstra’s Algorithm is not valid for negative weights or negative cycles.
- A negative cycle is a cycle whose edges are such that the sum of their weights is a negative value.
- Difference between using `sets` and `priority_queues` is that in `sets` we can check if there exists a pair with the same node but a greater distance than the current distance.
- This is not possible in `priority_queues` as we cannot erase a particular element from the queue. Thus, we need to push the same node with a smaller distance and the `priority_queue` will automatically sort it.
- We can use `queues` also but it will be slower than the above two methods.

### 2.1 Using Sets

```cpp
vector<int> dijkstra(int V, vector<vector<int>> adj, int src) {
    // Create a set for storing the nodes as a pair {dist,node}
    set<pair<int,int>> st;

    // Initialising dist list with a large number to
    // indicate the nodes are unvisited initially.
    // This list contains distance from source to the nodes.
    vector<int> dist(V, 1e9);

    st.insert({0, src});

    // Source initialised with dist=0
    dist[src] = 0;

    // Now, erase the minimum distance node first from the set
    // and traverse for all its adjacent nodes.
    while(!st.empty()) {
        auto it = *(st.begin());

        int node = it.second;
        int dis = it.first;
        st.erase(it);

        // Check for all adjacent nodes of the erased
        // element whether the prev dist is larger than current or not.
        for(auto it : adj[node]) {
            int adjNode = it[0];
            int edgW = it[1];

            if(dis + edgW < dist[adjNode]) {
                // erase if it was visited previously at
                // a greater cost.
                if(dist[adjNode] != 1e9)
                    st.erase({dist[adjNode], adjNode});

                // If current distance is smaller,
                // push it into the queue
                dist[adjNode] = dis + edgW;
                st.insert({dist[adjNode], adjNode});
            }
        }
    }
    return dist;
}
```

### 2.2 Using Priority Queues

```cpp
vector<int> dijkstra(int V, vector<vector<int>> adj, int S) {
    // Create a p.q. for storing the nodes as a pair {dist,node}
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // This list contains distance from source to the nodes.
    vector<int> distTo(V, INT_MAX);

    // Source initialised with dist=0.
    distTo[S] = 0;
    pq.push({0, S});

    // Now, pop the minimum distance node first from the min-heap
    // and traverse for all its adjacent nodes.
    while (!pq.empty()) {
        int node = pq.top().second;
        int dis = pq.top().first;
        pq.pop();

        // Check for all adjacent nodes of the popped out
        // element whether the prev dist is larger than current or not.
        for (auto it : adj[node]) {
            int v = it[0];
            int w = it[1];

            if (dis + w < distTo[v]) {
                distTo[v] = dis + w;

                // If current distance is smaller,
                // push it into the queue.
                pq.push({dis + w, v});
            }
        }
    }
    return distTo;
}
```
## 3. Complexity

- Time Complexity --> $O(E*logV)$ if using sets, else $O(E*logE)$ if using min-heap
- Space Complexity --> $O(V)$

