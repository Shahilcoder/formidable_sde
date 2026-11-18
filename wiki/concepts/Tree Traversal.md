---
type: concept
area: sde
title: Tree Traversal
aliases: [Tree Traversal, DFS, BFS, Depth-First Search, Breadth-First Search, Level Order Traversal, Pre-order, In-order, Post-order]
tags: [dsa, trees, traversal, recursion, dfs, bfs]
status: draft
source_count: 1
created: 2026-08-01
updated: 2026-08-01
---

## Summary
**Tree traversal** is the act of visiting every node exactly once, and the *order* you choose is the whole game — most tree problems are "pick the right traversal, do one line of work per node". Two families: **DFS** (depth-first — go deep, then backtrack; driven by a [[Stack]], explicit or the call stack) in three orders, and **BFS** (breadth-first / level-order — go wide, level by level; driven by a [[Queue]]).

## Details

### Choosing a traversal
| Order | Visit sequence | Reach for it when |
|---|---|---|
| **Pre-order** | node → left → right | You need the node *before* its children: copy/clone a tree, serialize it, print a directory listing top-down. |
| **In-order** | left → node → right | The tree is a [[Binary Search Tree]] — this emits **sorted** values. Validate-BST, kth-smallest, BST→list. |
| **Post-order** | left → right → node | You need children's results *before* the node: compute height/size, delete/free a tree bottom-up, evaluate an expression tree, any subtree-aggregate DP. |
| **Level-order (BFS)** | level by level, top-down | The problem mentions *levels*, *depth*, *widths*, or *shortest path*: level averages, right-side view, minimum depth, zigzag. |

The mnemonic: **pre / in / post** names *when the node itself is visited* relative to its two subtrees. The left-before-right part never changes.

### DFS — recursive
```java
// Source (Greg Hogg Lecture 8)
public static void preOrder(TreeNode node) {
    if (node == null) return;      // base case: the null child
    System.out.println(node);      // visit
    preOrder(node.left);
    preOrder(node.right);
}

public static void inOrder(TreeNode node) {
    if (node == null) return;
    inOrder(node.left);
    System.out.println(node);      // visit moves between the two calls
    inOrder(node.right);
}
```

```cpp
// Claude addition — post-order, which the source describes but never codes.
// Same shape; the visit simply moves after both recursive calls.
void postOrder(TreeNode* node) {
    if (!node) return;
    postOrder(node->left);
    postOrder(node->right);
    cout << node->val << '\n';
}
```

All three are one function with the `visit` line slid to a different position. That's the entire difference.

### DFS — iterative, with an explicit stack
```java
// Source — iterative pre-order.
// Push right BEFORE left, because a stack reverses: left must pop first.
public static void preOrderIterative(TreeNode node) {
    if (node == null) return;
    java.util.Stack<TreeNode> stack = new java.util.Stack<>();
    stack.push(node);
    while (!stack.isEmpty()) {
        TreeNode current = stack.pop();
        System.out.println(current);
        if (current.right != null) stack.push(current.right);
        if (current.left  != null) stack.push(current.left);
    }
}
```

*Claude note:* iterative **pre-order** is the easy one — it's the only order where a plain push-both-children loop works, because the node is visited on the way *down*. Iterative in-order and post-order need extra state (a "descend left, then pop" loop, or a visited flag / reversed-pre-order trick). If an interviewer asks for "iterative traversal" unqualified, pre-order is the one to volunteer.

### BFS — level order, with a queue
```java
// Source — level-order traversal
public static void levelOrder(TreeNode node) {
    if (node == null) return;
    java.util.Queue<TreeNode> queue = new java.util.LinkedList<>();
    queue.add(node);
    while (!queue.isEmpty()) {
        TreeNode current = queue.poll();
        System.out.println(current);
        if (current.left  != null) queue.add(current.left);
        if (current.right != null) queue.add(current.right);
    }
}
```

Structurally identical to iterative DFS with the [[Stack]] swapped for a [[Queue]] — LIFO goes deep, FIFO goes wide. That one-word swap is the whole distinction.

*Claude addition:* this flat version loses level boundaries. To process **one level at a time** (the form most BFS problems actually want), snapshot the queue size at the top of each round and consume exactly that many nodes:

```cpp
while (!q.empty()) {
    int sz = q.size();               // everything currently queued = one level
    for (int i = 0; i < sz; ++i) {
        TreeNode* cur = q.front(); q.pop();
        /* ...work for this level... */
        if (cur->left)  q.push(cur->left);
        if (cur->right) q.push(cur->right);
    }
    /* ...end of level: record average / last node / depth++... */
}
```

### Complexity
- **Time: O(N)** for every traversal — each node is visited exactly once, regardless of order.
- **Space: O(N)** worst case, but for *different reasons*: DFS holds a stack as deep as the tree's **height** (O(N) degenerate, O(log N) balanced); BFS holds a queue as wide as the widest **level** (up to ~N/2 leaves in a perfect tree).
- Practical consequence: on a **deep, narrow** tree prefer BFS; on a **wide, bushy** tree prefer DFS.

### Beyond trees
The same two loops traverse a general graph — add a **visited set** so cycles don't trap you, and BFS gains its headline property: on an unweighted graph it finds **shortest paths**. When this wiki takes on graphs, DFS and BFS will split out into their own pages; while the material is tree-only, it lives here.

## Related
[[Binary Tree]] · [[Binary Search Tree]] · [[Stack]] · [[Queue]] · [[Backtracking]] · [[Heap]] · [[DSA Patterns Overview]]

## Sources
- [[Binary Trees & Binary Search Trees]] — the DFS/BFS split, all three DFS orders, recursive pre/in-order, iterative pre-order, level-order code, and traversal complexities.
