# BFS

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

### Breadth First Search

In BFS algorithm, we focus on traversing the tree "breadth-wise", i.e, the traversal begins at the root as usual, but instead of traversing a single branch till full depth, we traverse the nodes of all branches according to level. The nodes in the next level are traversed only after all the nodes at the current level/depth have been traversed.

BFS is commonly implemented using a queue data structure, and it's often used for problems where the goal is to find the shortest path or to visit all nodes at a given depth in the tree.

- Start by selecting root as the starting point of the traversal.
- Create a queue and add the starting node to it.
- While the queue is not empty, repeat the following steps: Remove a node from the queue and process it (e.g., print its value). Mark the node as visited and remove it from the queue Retrieve all adjacent nodes of the node being processed. For each of these nodes, if it has not been visited yet, add it to the queue.
- Continue the process until the queue is empty.

BFS guarantees that it visits all vertices at the current level before moving on to the next level, ensuring that it explores the tree in a breadth-first fashion. This property is useful in various applications, such as finding the shortest path.

### Video Explanation

See the BFS traversal of the following tree:

### Task
- Given a tree with $N$ vertices and $N - 1$ edges, rooted at node number $1$.
- Output the nodes while traversing the tree in BFS order.
### Input Format
- The first line of the input contains single integer $N$ — the number of vertices.
- The next $N - 1$ lines describe the edges. The $i$-th of these $N - 1$ lines contains two space-separated integers $u_i$ and $v_i$, denoting a bidirectional edge between $u_i$ and $v_i$.
### Output Format

Output $N$ integers on the same line - the vertices of the given tree in BFS order.

### Constraints
- $1 \leq N \leq 100000$
- $1 \leq u_i, v_i \leq N$
### Sample 1:
Input
Output

```
10
1 2
1 3
1 4
2 5
5 9
3 6
3 7
6 10
4 8
```

```
1 2 3 4 5 6 7 8 9 10 

```

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T09:59:19.845Z  

```c_cpp
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100005;
vector<int> tree[MAX];

void bfs(int root) {
    queue<int> q;

    q.push(root);

    while (!q.empty()) {
        int node = q.front();
        q.pop();

        cout << node << " ";

        for (auto child : tree[node]) {
            q.push(child);
        }
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

    bfs(1);

    return 0;
}
```

---

[View on CodeChef](https://www.codechef.com/problems/BFS)