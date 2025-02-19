---
title: "Max area Histogram"
---

# Max area Histogram

## 1. Problem Statement

Given an array of integers heights representing the histogram’s bar height where the width of each bar is 1 return the area of the largest rectangle in histogram.

## 2. Solution

### 2.1 Brute Force 

```cpp
int largestarea(int arr[], int n) {
  int maxArea = 0;

  for (int i = 0; i < n; i++) {

    int minHeight = INT_MAX;

    for (int j = i; j < n; j++) {
      minHeight = min(minHeight, arr[j]);
      maxArea = max(maxArea, minHeight * (j - i + 1));
    }
    
  }
  return maxArea;
}
```

- Time complexity is $O(n^2)$

### 2.2 Using stack to find the next smaller element

- This will be a two pass algorithm and time complexity will be $O(n)$



```cpp

```