# DSCPP86

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

_Description not available._

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T09:59:22.409Z  

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

[View on CodeChef](https://www.codechef.com/problems/DSCPP86)