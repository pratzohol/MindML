---
title: "Sliding Window"
tags:
    - Algorithms
---

# Sliding Window

## 1. Type 1

For problems in which we can update sliding window based on the conditions in the problem, we maintain two pointers `i` (or start) and `j` (or end). Run a `for` loop on `j`. WHen particular condition is satisfied, update the `i` pointer and the sliding window and add to the `ans` accordingly.

## 2. Type 2

Example problem statement : Given an integer array `nums` and an integer `k`, return the number of **good subarrays** of `nums`.  
A **good array** is an array where the number of different integers in that array is exactly `k`.

Solution : Since, updating sliding window based on this rule seems improbable, we will slightly reformulate the problem as finding subarrays with at most `k` different elements. This way we can find answer simply by `atMost(k) - atMost(k - 1)`.

```cpp
int subarraysWithKDistinct(vector<int>& nums, int k) {
        return atMost(nums, k) - atMost(nums, k - 1);
}

int atMost(vector<int>& nums, int k) {
    int n = nums.size();
    int i = 0, j = 0, ans = 0;

    map<int, int> mp;

    for (int j = 0; j < n; j++) {
        mp[nums[j]]++;

        while (mp.size() > k) {
            if (mp[nums[i]] == 1) mp.erase(nums[i]);
            else mp[nums[i]]--;
            i++;
        }

        ans += j - i + 1;
    }
    return ans;
}
```
