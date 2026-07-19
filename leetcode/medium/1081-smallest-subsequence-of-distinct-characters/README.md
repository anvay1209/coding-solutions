# Smallest Subsequence of Distinct Characters

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

Given a string `s`, return  *the  **lexicographically smallest*   *subsequence**  of*  `s`  *that contains all the distinct characters of*  `s`  *exactly once*.

 

 **Example 1:** 

```
Input: s = "bcabc"
Output: "abc"

```

 **Example 2:** 

```
Input: s = "cbacdcbc"
Output: "acdb"

```

 

 **Constraints:** 

- 1 <= s.length <= 1000
- s consists of lowercase English letters.

 

 **Note:**  This question is the same as 316: https://leetcode.com/problems/remove-duplicate-letters/

## Solution

**Language:** C++  
**Runtime:** 0 ms (beats 100.00%)  
**Memory:** 8.6 MB (beats 94.04%)  
**Submitted:** 2026-07-19T12:02:13.087Z  

```cpp
class Solution {
public:
    string smallestSubsequence(string s) {
        vector<int> vis(26), num(26);
        for (char ch : s) {
            num[ch - 'a']++;
        }

        string stk;
        for (char ch : s) {
            if (!vis[ch - 'a']) {
                while (!stk.empty() && stk.back() > ch) {
                    if (num[stk.back() - 'a'] > 0) {
                        vis[stk.back() - 'a'] = 0;
                        stk.pop_back();
                    } else {
                        break;
                    }
                }
                vis[ch - 'a'] = 1;
                stk.push_back(ch);
            }
            num[ch - 'a'] -= 1;
        }
        return stk;
    }
};
```

---

[View on LeetCode](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/)