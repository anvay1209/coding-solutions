# Maximize Active Section with Trade II

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## Problem

You are given a binary string `s` of length `n`, where:

- '1' represents an active section.
- '0' represents an inactive section.

You can perform  **at most one trade**  to maximize the number of active sections in `s`. In a trade, you:

- Convert a contiguous block of '1's that is surrounded by '0's to all '0's.
- Afterward, convert a contiguous block of '0's that is surrounded by '1's to all '1's.

Additionally, you are given a  **2D array**  `queries`, where `queries[i] = [li, ri]` represents a substring `s[li...ri]`.

For each query, determine the  **maximum**  possible number of active sections in `s` after making the optimal trade on the substring `s[li...ri]`.

Return an array `answer`, where `answer[i]` is the result for `queries[i]`.

 **Note** 

- For each query, treat s[li...ri] as if it is augmented with a '1' at both ends, forming t = '1' + s[li...ri] + '1'. The augmented '1's do not contribute to the final count.
- The queries are independent of each other.

 

 **Example 1:** 

 **Input:**  s = "01", queries = [[0,1]]

 **Output:**  [1]

 **Explanation:** 

Because there is no block of `'1'`s surrounded by `'0'`s, no valid trade is possible. The maximum number of active sections is 1.

 **Example 2:** 

 **Input:**  s = "0100", queries = [[0,3],[0,2],[1,3],[2,3]]

 **Output:**  [4,3,1,1]

 **Explanation:** 

- Query [0, 3] → Substring "0100" → Augmented to "101001" Choose "0100", convert "0100" → "0000" → "1111". The final string without augmentation is "1111". The maximum number of active sections is 4.
- Query [0, 2] → Substring "010" → Augmented to "10101" Choose "010", convert "010" → "000" → "111". The final string without augmentation is "1110". The maximum number of active sections is 3.
- Query [1, 3] → Substring "100" → Augmented to "11001" Because there is no block of '1's surrounded by '0's, no valid trade is possible. The maximum number of active sections is 1.
- Query [2, 3] → Substring "00" → Augmented to "1001" Because there is no block of '1's surrounded by '0's, no valid trade is possible. The maximum number of active sections is 1.

 **Example 3:** 

 **Input:**  s = "1000100", queries = [[1,5],[0,6],[0,4]]

 **Output:**  [6,7,2]

 **Explanation:** 

- Query [1, 5] → Substring "00010" → Augmented to "1000101" Choose "00010", convert "00010" → "00000" → "11111". The final string without augmentation is "1111110". The maximum number of active sections is 6.
- Query [0, 6] → Substring "1000100" → Augmented to "110001001" Choose "000100", convert "000100" → "000000" → "111111". The final string without augmentation is "1111111". The maximum number of active sections is 7.
- Query [0, 4] → Substring "10001" → Augmented to "1100011" Because there is no block of '1's surrounded by '0's, no valid trade is possible. The maximum number of active sections is 2.

 **Example 4:** 

 **Input:**  s = "01010", queries = [[0,3],[1,4],[1,3]]

 **Output:**  [4,4,2]

 **Explanation:** 

- Query [0, 3] → Substring "0101" → Augmented to "101011" Choose "010", convert "010" → "000" → "111". The final string without augmentation is "11110". The maximum number of active sections is 4.
- Query [1, 4] → Substring "1010" → Augmented to "110101" Choose "010", convert "010" → "000" → "111". The final string without augmentation is "01111". The maximum number of active sections is 4.
- Query [1, 3] → Substring "101" → Augmented to "11011" Because there is no block of '1's surrounded by '0's, no valid trade is possible. The maximum number of active sections is 2.

 

 **Constraints:** 

- 1 <= n == s.length <= 105
- 1 <= queries.length <= 105
- s[i] is either '0' or '1'.
- queries[i] = [li, ri]
- 0 <= li <= ri < n

## Solution

**Language:** C++  
**Runtime:** 128 ms (beats 64.52%)  
**Memory:** 284.9 MB (beats 19.35%)  
**Submitted:** 2026-07-22T13:39:27.598Z  

```cpp
class SparseTable {
private:
    vector<vector<int>> st;

public:
    SparseTable(const vector<int>& data) {
        st.push_back(data);
        int i = 1, N = st[0].size();
        while (2 * i <= N + 1) {
            const auto& pre = st.back();
            vector<int> cur;
            for (int j = 0; j < N - 2 * i + 1; j++) {
                cur.push_back(max(pre[j], pre[j + i]));
            }
            st.push_back(cur);
            i <<= 1;
        }
    }

    int query(int begin, int end) {
        if (begin > end) {
            return 0;
        }
        int len = end - begin + 1;
        int lg = 0;
        while ((1 << (lg + 1)) <= len) {
            lg++;
        }
        return max(st[lg][begin], st[lg][end - (1 << lg) + 1]);
    }
};

class Solution {
public:
    vector<int> maxActiveSectionsAfterTrade(string s,
                                            vector<vector<int>>& queries) {
        int n = s.length();
        int cnt1 = count(s.begin(), s.end(), '1');

        vector<int> zeroBlocks;
        vector<int> blockLeft;
        vector<int> blockRight;

        int i = 0;
        while (i < n) {
            int st = i;
            while (i < n && s[i] == s[st]) {
                i += 1;
            }
            if (s[st] == '0') {
                zeroBlocks.push_back(i - st);
                blockLeft.push_back(st);
                blockRight.push_back(i - 1);
            }
        }

        int m = zeroBlocks.size();
        if (m < 2) {  // continuous 0 blocks less than 2 segments, return the
                      // answer directly
            return vector<int>(queries.size(), cnt1);
        }
        vector<int> tmpSum(m - 1);
        for (int i = 0; i < m - 1; i++) {
            tmpSum[i] = zeroBlocks[i] + zeroBlocks[i + 1];
        }
        SparseTable st(tmpSum);
        vector<int> ans;

        for (const auto& q : queries) {
            int l = q[0], r = q[1];
            int i = lower_bound(blockRight.begin(), blockRight.end(), l) -
                    blockRight.begin();
            int j = upper_bound(blockLeft.begin(), blockLeft.end(), r) -
                    blockLeft.begin() - 1;

            // at most 1 continuous block of 0s within the substring
            if (i > m - 1 || j < 0 || i >= j) {
                ans.push_back(cnt1);
                continue;
            }

            int firstLen = blockRight[i] - max(blockLeft[i], l) +
                           1;  // actual length of the first consecutive block
                               // of 0s in the substring
            int lastLen = min(blockRight[j], r) - blockLeft[j] +
                          1;  // actual length of the last consecutive block of
                              // 0s in the substring
            // exactly 2 consecutive 0 blocks within the substring
            if (i + 1 == j) {
                int bestGain = firstLen + lastLen;
                ans.push_back(cnt1 + bestGain);
                continue;
            }

            int val1 = firstLen + zeroBlocks[i + 1];
            int val2 = zeroBlocks[j - 1] + lastLen;
            int val3 = st.query(i + 1, j - 2);
            int bestGain = max({val1, val2, val3});
            ans.push_back(cnt1 + bestGain);
        }

        return ans;
    }
};
```

---

[View on LeetCode](https://leetcode.com/problems/maximize-active-section-with-trade-ii/)