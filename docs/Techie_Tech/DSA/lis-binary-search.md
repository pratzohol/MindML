---
title: "LIS | Binary Search"
tags:
    - Algorithms
    - Dynamic Programming
---

# Longest Increasing Subsequence (LIS) | Binary Search

## 1. Problem Statement

Given an unsorted array of integers, find the length of longest increasing subsequence.

## 2. Solution

- [Using DP in $O(n^2)$ time](https://takeuforward.org/data-structure/printing-longest-increasing-subsequence-dp-42/)
- To do this problem in $O(n*logn)$ time, following algo is used :
    
    - Initialize a `temp` array.
    - Push the first element of the `arr` to `temp`.
    - Iterate over the next elements.
    - In every iteration, if `arr[i]` is greater than the last element of the `temp` array simply push it to the `temp` array.
    - Else, just find the `lower_bound` index of that element in the `temp` array (say `ind`). Then simply initialize `temp[ind] = arr[i]`.
    - Maintain a `len` variable to calculate the length of the `temp` array in the iteration itself.

```cpp
int longestIncreasingSubsequence(int arr[], int n){
    
    vector<int> temp;
    temp.push_back(arr[0]);
    
    int len = 1;
    
    for(int i=1; i<n; i++){
        if(arr[i]>temp.back()){
           // arr[i] > the last element of temp array 
           
           temp.push_back(arr[i]);
           len++;
           
        } 
        else{
	// replacement step
            int ind = lower_bound(temp.begin(),temp.end(),arr[i]) - temp.begin();
            temp[ind] = arr[i];
        }
        
    }
    
    return len;
}
```

## 3. References

1. [Strivers DSA sheet | DP-43 | LIS-Binary Search](https://takeuforward.org/data-structure/longest-increasing-subsequence-binary-search-dp-43/)