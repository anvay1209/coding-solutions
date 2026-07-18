# DSCPP81 - Rating 932

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## Problem

### Implementation - Adjacency Matrix

In this section, we will check out how to implement the adjacency matrix we discussed.

The code given on the right forms the adjacency matrix for the tree given above. Notice how the edges are taken as input and run the code to see the matrix.

### Input Format
- The first line of input will contain a single integer $N$, denoting the number of nodes in the Tree.
- Then the next N - 1 lines contains two numbers $u_i$ and $v_i$ denoting the i-th edge of the Tree.
### Output Format

Output the final adjacency matrix.

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
0 1 1 0 0 0
0 0 0 1 1 0
0 0 0 0 0 1
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T09:56:32.174Z  

```c_cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    // This is our adjacency matrix
    // All the elements are initialized to zero
    vector < vector < int >> adjMatrix(n, vector < int > (n, 0));

    // Take the input for all the edges
    int u, v;
    for (int i = 0; i < n - 1; i++) {
        cin >> u >> v;

        // Adding an edge from u to v
        adjMatrix[u][v] = 1;
    }

    // Printing the adjacency matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << adjMatrix[i][j] << " ";
        }
        cout << "\n";
    }
}
```

---

[View on CodeChef](https://www.codechef.com/problems/DSCPP81)