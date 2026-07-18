# BSTMAX

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem

### Find maximum node in BST

Given a binary search tree, find the maximum/largest node in it.

For eg., the maximum node in the given BST is 7.

### Input Format
- The first line of the input contains s single integer $N$ — the number of nodes in the binary search tree.
- Next $N - 1$ lines contain three space separated characters $p_i, c_i, R_i$, describing the tree with edge informations - $p_i$ is an integer denoting the parent node of the $i$th edge, $c_i$ is child node, and the letter $R_i$ denotes whether the child is left child or right child, it's value is L if $c_i$ is left child of $p_i$, else R.
### Output Format

Output on a single line - the the maximum node value of the given BST.

### Constraints
- $1 \leq N \leq 10000$
- $1 \leq p_i, c_i \leq 100000$
- $R_i$ = L or R
- All $p_i$'s and $c_i$'s are distinct.
### Sample 1:
Input
Output

```
7 
4 2 L
4 6 R
2 3 R
2 1 L
6 5 L
6 7 R
```

```
7
```

## Solution

**Language:** c_cpp  
**Runtime:** N/A  
**Memory:** N/A  
**Submitted:** 2026-07-18T08:56:35.825Z  

```c_cpp
class Solution {
public:
    int maxNodeInBST(Node* root) {
        while (root->right != NULL) {
            root = root->right;
        }

        return root->val;
    }
};
```

---

[View on CodeChef](https://www.codechef.com/problems/BSTMAX)