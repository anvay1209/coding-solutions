# DSCPP86 - Rating 932

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

### Count number of leaf nodes

Given a tree, find the number of leaf nodes using DFS algorithm.

Write the algorithm forming an adjacency list yourself. In the end, output the number of leaf nodes in the tree.

Hint: Leaf nodes are the nodes which do not have any children. You will need to modify your DFS code to count when you encounter a leaf node.

### Input Format
- The first line of test case contains a single integer $N$, denoting the number of nodes in the tree (the nodes lie in range $[0, N-1]$).
- The next $N-1$ lines contain two integers $a$ and $b$ denoting there is an edge from node $a$ to node $b$.
### Output Format

Output a single integer denoting the number of leaves in the given tree.

### Sample 1:
Input
Output

```
8
0 1
0 2
1 3
1 4
2 5
3 6
5 7
```

```
3
```

### Explanation:

Try to draw the tree on a paper using this testcase.
The leaf nodes are 4, 6 and 7

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T10:00:26.197Z  

```c_cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> adj;
int leafCount = 0;

void dfs(int u) {
    // If the adjacency list is empty, it's a leaf node
    if (adj[u].empty()) {
        leafCount++;
        return;
    }
    
    // Visit all children
    for (int v : adj[u]) {
        dfs(v);
    }
}

int main() {
    int N;
    if (!(cin >> N)) return 0;
    
    // Handle edge case where tree has only 1 node
    if (N == 1) {
        cout << 1 << endl;
        return 0;
    }

    adj.resize(N);
    for (int i = 0; i < N - 1; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
    }

    dfs(0);
    cout << leafCount << endl;

    return 0;
}
```

---

[View on CodeChef](https://www.codechef.com/problems/DSCPP86)