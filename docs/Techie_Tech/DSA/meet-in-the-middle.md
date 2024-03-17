---
title: "Meet in the Middle"
tags:
    - Algorithms
---

# Meet in the Middle

##  1. <a name='Whatisthis'></a> What is this?
Meet in the middle is a search technique which is used when the input is small but not as small that brute force can be used. Like divide and conquer it splits the problem into two, solves them individually and then merge them. But we can’t apply meet in the middle like divide and conquer because we don’t have the same structure as the original problem.

For subset problems, reduce time complexity from $O(2^n)$ to $O(2^{n/2}*n)$.

##  2. <a name=''></a> How to use it?

- _Problem statement_ :

    You are given an integer array `nums` of `2 * n` integers. You need to partition nums into two arrays of length `n` to minimize the absolute difference of the sums of the arrays. To partition `nums`, put each element of `nums` into one of the two arrays.

    Return the **minimum** possible absolute difference.

- _Solution_ :

    - Partition the array into two halves of size `n / 2` each.
    - Pre-compute the sum of all possible subsets / subsequences corresponding to length `i` in `sum1[i]` for left half. `i` varies from `0` to `n / 2`. Similarly for the right half.
    - Now to make subset of size `n / 2`, we take subset of length `i` from left size and `n / 2 - i` from right side.
    - Thus, we iterate over `i = 0 to i = n / 2` and for each `sum1[i]`, we first sort the `sum2[n / 2 - i]` and use lower bound to find the closest value to `totSum / 2`. (`totSum` is sum of all the elements of the array)
    - Time complexity is $O(2 * 2 ^ {n / 2})$ for finding every subset sum and $O(log (2^{n / 2})) = O(n / 2)$ for binary search. Thus, total time complexity is $O(2^{n / 2} * n)$.

##  3. <a name='References'></a> References

- [Meet in the Middle - GeeksforGeeks](https://www.geeksforgeeks.org/meet-in-the-middle/)
- [Partition Array Into Two Arrays to Minimize Sum Difference - Leetcode](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/solutions/2850095/c-first-timers-explanation-meet-in-middle-simplest-code/)
