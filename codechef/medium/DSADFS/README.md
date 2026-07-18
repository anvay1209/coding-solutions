# DSADFS

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

### Depth First Search

Depth-First Search (DFS) is a tree traversal algorithm that explores as far as possible along each branch before backtracking. It starts at the root and systematically explores the tree by going as deep as possible along each branch before backtracking.

Here's a more detailed explanation of DFS:

- Start at the Source: Begin the traversal from the root node.
- Visit and Print: Visit the source node and print it.
- Explore Children: Move to an unvisited child of the node and repeat steps 2 and 3.
- Backtrack: If all children of this node are visited, backtrack to a neighboring unvisited node.
- Continue Until All Nodes Are Visited: Repeat steps 3 - 4 until all vertices have been visited.

DFS is often implemented using a recursive approach or a stack data structure.

### Video Explanation

Check this pseudo code for DFS:

```
void dfs(int node){
    // print node or do anything with it...
    for(int child: tree[node]){ // tree is stored as adjacency list
        dfs(child);
    }
}

```

### Task
- Given a tree with $N$ vertices and $N - 1$ edges, rooted at node number $1$.
- Output the nodes while traversing the tree in DFS order.
### Input Format
- The first line of the input contains a single integer $N$ — the number of vertices.
- The next $N - 1$ lines describe the edges. The $i$-th of these $N - 1$ lines contains two space-separated integers $u_i$ and $v_i$, denoting a bidirectional edge between $u_i$ and $v_i$.
### Output Format

Output $N$ integers on the same line - the vertices of the given tree in DFS order if we start traversing from the root node 1.

### Constraints
- $1 \leq N \leq 100000$
- $1 \leq u_i, v_i \leq N$
### Sample 1:
Input
Output

```
10
1 2
1 5
1 9
2 3
3 4
5 6
6 7
5 8
9 10
```

```
1 2 3 4 5 6 7 8 9 10 

```

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T09:58:41.003Z  

```c_cpp
#include <bits/stdc++.h>
using namespace std;

const int maxx = 100005;
vector<int> tree[maxx];

void dfs(int node) {
    cout << node << " ";

    for (auto i : tree[node]) {
        dfs(i);
    }
}

int main() {
    int n;
    cin >> n;

    int u, v;
    for (int i = 0; i < n - 1; i++) {
        cin >> u >> v;
        tree[u].push_back(v);
    }

    // Start DFS from the root node
    dfs(1);
}
```

---

[View on CodeChef](https://www.codechef.com/problems/DSADFS)