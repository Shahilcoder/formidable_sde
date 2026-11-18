---
type: entity
area: sde
title: Binary Tree
aliases: [Binary Tree, Binary Trees, TreeNode]
tags: [dsa, data-structures, trees, binary-tree, recursion]
status: draft
source_count: 1
created: 2026-08-01
updated: 2026-08-01
---

## Summary
A **binary tree** is a hierarchical structure of **nodes**, each holding a value and at most **two** children — `left` and `right` — either of which may be `null`. It is a restricted **directed graph**: one root, no cycles, one parent per node. Nearly every tree problem is solved by recursing on the two children, which makes binary trees the natural home for divide-and-conquer thinking.

## Details

### Terminology
- **Node** — value + pointers to left/right children.
- **Root** — the topmost node; every other node descends from it.
- **Leaf** — a node with no children.
- **Parent / children** — the node directly above / directly below.
- **`null` (`None`)** — the absence of a child. The base case of essentially every recursive tree function.

### Types
| Type | Property |
|---|---|
| **Complete** | All levels full except possibly the last, which fills left-to-right. |
| **Perfect** | Every internal node has 2 children; all leaves sit on the same level. |
| **[[Binary Search Tree]]** | Recursive ordering invariant: left subtree < node < right subtree. |

*Claude addition:* a **full** (a.k.a. strict) binary tree — every node has either 0 or 2 children — is the fourth term interviewers use, and is not the same as complete.

### Representation
- **Linked structure** — the default: an object/struct per node with two pointers.
- **Array, 1-based indexing** — node at index `i` has children at `2i` and `2i+1` (parent at `i/2`). Compact and pointer-free, but only economical for **complete** trees; a sparse tree wastes cells on nulls. This is exactly how a [[Heap]] is stored.

```java
// Source (Greg Hogg Lecture 8) — Java
static class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}
```

```cpp
// Claude addition — the C++ equivalent, matching the LeetCode signature
// used throughout the rest of this wiki
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```

### Height
The **height** is the longest root-to-leaf path.

> [!warning] Contradiction — how height is counted
> [[Binary Trees & Binary Search Trees]] counts height **in nodes**, so a leaf has height **1** and a single-node tree height 1.
> The standard (CLRS) definition counts **edges**: a leaf has height **0**.
> LeetCode's *Maximum Depth of Binary Tree* counts **nodes** — numerically the source's convention, under the word "depth".
> Neither is wrong; they are different conventions, and mixing them is a classic off-by-one. Pin down which one a problem means before writing the base case (`return 0` vs `return 1` on `null`).

Height is what all the complexity claims hang on: a balanced tree has height O(log N), a degenerate one O(N).

### Searching an unordered binary tree
With no ordering invariant there is nothing to prune, so a search must be prepared to visit every node:

```java
// Source — generic DFS search, O(N) time, O(N) space worst case
public static boolean search(TreeNode node, int target) {
    if (node == null) return false;
    if (node.val == target) return true;
    return search(node.left, target) || search(node.right, target);
}
```

- **Time** O(N) — worst case all nodes visited.
- **Space** O(N) — the recursion stack (or BFS queue) in a degenerate tree; O(log N) if balanced.

Add the ordering invariant and this becomes O(log N) — see [[Binary Search Tree]].

### What builds on binary trees
[[Heap]] (complete binary tree, array-backed), expression/parse trees, decision trees, and — with the ordering invariant — search trees. Beyond that: [[Trie]] (n-ary), segment trees, and general graph traversal, which reuses the [[Tree Traversal]] machinery plus a visited set.

## Related
[[Binary Search Tree]] · [[Tree Traversal]] · [[Stack]] · [[Queue]] · [[Heap]] · [[Trie]] · [[DSA Patterns Overview]]

## Sources
- [[Binary Trees & Binary Search Trees]] — structure, terminology, complete/perfect types, linked vs array representation, node-counted height definition, generic DFS search and its complexities.
