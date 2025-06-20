---
title : Moore's Voting Algorithm
---

## Problem

To find the majority element in an array. Majority element is the one which appear more than $\lfloor n / 2 \rfloor$ times in an array.

## Algorithm

- If the majority element is `x` then, `count(x) - count(any other element) > 0`.
- Assign `count = 0` and `candidate` which keeps track of majority element.
- Run a loop through array, if we face same element as `candidate`, increase `count` by 1.
- Else, decrease the `count` by 1. 
- If `count` becomes 0, update `candidate` by current element.

## Code 

- Time Complexity = $O(N)$ 
- Space Complexity = $O(1)$

```Cpp
int majorityElement(vector<int>& nums) {
    int n = nums.size();
    int count = 0, candidate = 0;

    for (int i = 0; i < n; i++) {
        if (count == 0) candidate = nums[i];
        if (nums[i] == candidate) {
            count++;
        }
        else {
            count--;
        }
    }

    return candidate;
}
```