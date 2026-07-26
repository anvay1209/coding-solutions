# Maximum Product of Three Numbers

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

Given an integer array `nums`,  *find three numbers whose product is maximum and return the maximum product*.

 

 **Example 1:** 

```
Input: nums = [1,2,3]
Output: 6

```

 **Example 2:** 

```
Input: nums = [1,2,3,4]
Output: 24

```

 **Example 3:** 

```
Input: nums = [-1,-2,-3]
Output: -6

```

 

 **Constraints:** 

- 3 <= nums.length <= 104
- -1000 <= nums[i] <= 1000

## Solution

**Language:** C++  
**Runtime:** 11 ms (beats 37.37%)  
**Memory:** 31.5 MB (beats 46.18%)  
**Submitted:** 2026-07-26T08:05:37.735Z  

```cpp
class Solution {
public:
    int maximumProduct(vector<int>& A) {
        ranges::sort(A);
        return max(
            A.back() * A[A.size() - 2] * A[A.size() - 3],
            A.back() * A.front() * A[1]
        );
    }
};
```

---

[View on LeetCode](https://leetcode.com/problems/maximum-product-of-three-numbers/)