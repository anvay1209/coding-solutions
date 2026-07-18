# DSCPP82 - Rating 932

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

### Implementation - Adjacency List

In this section, we will see the implementation of adjacency list.

The code given on the right forms the adjacency list for the tree given above.
Run the code to see the list formed and check out the difference from the adjacency matrix.

### Input Format
- The first line of input will contain a single integer $N$, denoting the number of nodes in the Tree.
- Then the next N - 1 lines contains two numbers $u_i$ and $v_i$ denoting the i-th edge of the Tree.
### Output Format

Output the final adjacency array.

### Sample 1:
Input
Output

```
6
0 1
0 2
1 3
1 4
2 5
```

```
1 2 
3 4 
5 
```

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T09:58:13.115Z  

```c_cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n;
    if (!(cin >> n)) return 0;
    
    // Adjacency list representation
    vector<int> tree[n];
    
    int u, v;
    for (int i = 0; i < n - 1; i++) {
        cin >> u >> v;
        // Adding edge from u to v
        tree[u].push_back(v);
    }
    
    // Printing only the neighbors as per the required format
    for (int i = 0; i < n; i++) {
        for (int node : tree[i]) {
            cout << node << " ";
        }
        cout << "\n";
    }
    
    return 0;
}
```

---

[View on CodeChef](https://www.codechef.com/problems/DSCPP82)