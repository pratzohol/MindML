---
title: Kadane's Algorithm
---

## Problem 

Given an integer array `nums`, find the subarray with the largest sum, and return its sum. [(Detailed solution)](https://leetcode.com/problems/maximum-subarray/solutions/1595195/c-python-7-simple-solutions-w-explanation-brute-force-dp-kadane-divide-conquer)

## Algorithm 

- `curr_sum` will store the maximum subarray sum ending at i.
- `max_sum` stores the maximum sum we have seen till now.
- If `curr_sum` is negative, then there is no need to include it and we can just take `nums[i]`, otherwise we add `nums[i]` to the `curr_sum`.
- At each step, we take max of `curr_sum` and `max_sum` to store the maximum subarray sum we have seen till now.

## Code

- Time Complexity = $O(N)$
- Space Complexity = $O(1)$

```Cpp
int maxSubArray(vector<int>& nums) {
    int max_sum = -1e5;
    int curr_sum = 0;

    for (int i = 0; i < nums.size(); i++) {
        curr_sum = max(nums[i], nums[i] + curr_sum);
        max_sum = max(max_sum, curr_sum);
    }

    return max_sum;
}
```