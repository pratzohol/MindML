---
title: "MCM DP"
tags:
    - Algorithms
    - Dynamic Programming
---

# Matrix Chain Multiplication (MCM) | DP

## 1. Problem Statement

Given a sequence of matrices, find the most efficient way to multiply these matrices together. The problem is not actually to perform the multiplications, but merely to decide in which order to perform the multiplications.

- Twisted version of this problem is given in [Leetcode | Minimum score triangulation of Polygon](https://leetcode.com/problems/minimum-score-triangulation-of-polygon/)

## 2. Solution

- Time Complexity --> $O(n^3)$
- Memoized with DP

```cpp
int f(vector<int>& arr, int i, int j){
    
    // base condition
    if(i == j)
        return 0;

    int mini = INT_MAX;
    
    // partitioning loop
    for(int k = i; k<= j-1; k++){

        int ans = f(arr,i,k) + f(arr, k+1,j) + arr[i-1]*arr[k]*arr[j];
        mini = min(mini,ans);

    }
    return mini;
}


int matrixMultiplication(vector<int>& arr, int N){
    
    int i =1;
    int j = N-1;
    
    return f(arr,i,j);
    
    
}
```

- Tabulation Method

```cpp linenums="1" hl_lines="8 9 10"
int matrixMultiplication(vector<int>& arr, int N){
    vector<vector<int>> dp(N,vector<int>(N,-1));
    
    for(int i=1; i<N; i++){
        dp[i][i] = 0;
    }
    
    for(int i = N-1; i >= 1; i--){

        for(int j = i+1; j < N; j++){
            
            int mini = INT_MAX;
    
            // partioning loop
            for(int k = i; k<= j-1; k++){

                int ans = dp[i][k]+ dp[k+1][j] + arr[i-1]*arr[k]*arr[j];
                mini = min(mini,ans);

            }
            
            dp[i][j] = mini;
        }
    }
    return dp[1][N-1];
}

```

- For the memoized solution we see that for calculating `f(i, j)` we need to calculate `f(i, k)` and `f(k+1, j)` for all `i <= k < j`. That is for `f(i, k)` part, we need `f(i, i + 1)`, `f(i, i + 2)`, ..., `f(i, j - 1)`. We see that all these values lie in row `i` of the memoization table. Similarly, for `f(k + 1, j)` part, we need `f(i + 1, j)`, `f(i + 2, j)`, ..., `f(j - 1, j)`. We see that all these values lie in column `j` of the memoization table. 
- Specifically, all the entries that is below `f(i, j)` but above `f(j, j)` and to left of `f(i, j)` but just right of `f(i, i)` are the entries that we need to calculate `f(i, j)`.
- Thus, we first iterate `i` from `N- 1` to `1` so that entries below any row are filled and then iterate `j` from `i + 1` to `N - 1` so that entries to the left of any column are filled.
