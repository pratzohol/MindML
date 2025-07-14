---
title: Disjoint Set Union (DSU)
---

# Disjoint Set Data Structure

## 1. Introduction

Disjoint Set Union or DSU is also called Union Find because of its two main operations.
The basic interface of this data structure consists of only two operations:

- `find_set(v)` - returns the ultimate parent of the set that contains the element `v`. This can be used to check if two elements are part of the same set or not. `a` and `b` are exactly in the same set, if `find_set(a) == find_set(b)`. Otherwise they are in different sets.
- `union_sets(a, b)` - merges two sets (the sets in which the element `a` and element `b` is located)

## 2. Implementation

### 2.1 Union by rank
```cpp
class DSU {
public:
    vector<int> parent, rank;

    // Initialize DSU data structure
    DSU (int n) {
        parent.resize(n);
        rank.resize(n, 0);

        for (int i = 0; i < n; ++i) {
            parent[i] = i;
        }
    }

    // find ultimate parent while doing
    // path compression optimization
    int find_set(int v) {
        if (parent[v] != v) {
            parent[v] = find_set(parent[v]);
        }
        return parent[v];
    }

    // Union by Rank
    void union_sets(int a, int b) {
        a = find_set(a);
        b = find_set(b);

        if (a != b) {
            if (rank[a] < rank[b])
                swap(a, b);

            parent[b] = a;

            if (rank[a] == rank[b]) {
                rank[a]++;
            }
        }
    }
};
```
### 2.2 Union by size

```cpp
class DSU {
public:
    vector<int> parent, size;

    // Initialize DSU data structure
    DSU (int n) {
        parent.resize(n);
        size.resize(n, 0);

        for (int i = 0; i < n; ++i) {
            parent[i] = i;
        }
    }

    // find ultimate parent while doing
    // path compression optimization
    int find_set(int v) {
        if (parent[v] != v) {
            parent[v] = find_set(parent[v]);
        }
        return parent[v];
    }

    // Union by Size
    void union_sets(int a, int b) {
        a = find_set(a);
        b = find_set(b);

        if (a != b) {
            if (size[a] < size[b])
                swap(a, b);

            parent[b] = a;
            size[a] += size[b];
        }
    }
};
```

## 3. Complexity

- Time Complexity -->  $O(1)$
    - If we combine both optimizations - path compression with union by size / rank - we will reach nearly constant time queries.
    - The final amortized time complexity is  $O(\alpha(n))$ , where  $\alpha(n)$  is the inverse Ackermann function, which grows very slowly.
    - It grows so slowly, that it doesn't exceed  $4$  for all reasonable $n$ (approximately  $n < 10^{600}$ .
    - If we only use Path compression, the  $T(n) = O(\log n)$   per call on average.
- Space Complexity -->  $O(n)$