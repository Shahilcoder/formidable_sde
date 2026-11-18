---
type: entity
area: sde
title: Stack
aliases: [Stack, LIFO, LIFO Stack, Call Stack]
tags: [dsa, data-structures, trees, recursion]
status: stub
source_count: 1
created: 2026-08-01
updated: 2026-08-01
---

## Summary
A **stack** is a LIFO (last-in, first-out) structure: push and pop happen at the same end, both O(1), with O(1) peek at the top. It is the LIFO counterpart to [[Queue]].

## Details
**Why it matters for trees:** a stack *is* depth-first search. DFS explores as deep as possible before backtracking, and that backtracking is precisely stack behaviour — either an **explicit** stack in an iterative traversal, or the **implicit call stack** in a recursive one. Recursion and an explicit stack are the same algorithm with different bookkeeping; see [[Tree Traversal]].

```java
// Source — iterative pre-order DFS. Push right before left so left pops first.
java.util.Stack<TreeNode> stack = new java.util.Stack<>();
stack.push(root);
while (!stack.isEmpty()) {
    TreeNode current = stack.pop();
    visit(current);
    if (current.right != null) stack.push(current.right);
    if (current.left  != null) stack.push(current.left);
}
```

That the traversal is O(N) *space* in the worst case is a statement about how deep this stack can get — O(N) for a degenerate tree, O(log N) for a balanced one.

Other standard uses: expression parsing and bracket matching, undo/redo, [[Backtracking]] state, and the monotonic-stack family (next greater element, largest rectangle).

## Related
[[Queue]] · [[Tree Traversal]] · [[Binary Tree]] · [[Backtracking]] · [[DSA for Web Development]]

## Sources
- [[Binary Trees & Binary Search Trees]] — DFS is stack-driven, explicitly or via the recursive call stack; iterative pre-order code.
