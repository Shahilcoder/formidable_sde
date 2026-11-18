---
type: entity
area: sde
title: Binary Search Tree
aliases: [Binary Search Tree, BST, BSTs]
tags: [dsa, data-structures, trees, bst, binary-search, recursion]
status: draft
source_count: 1
created: 2026-08-01
updated: 2026-08-01
---

## Summary
A **binary search tree (BST)** is a [[Binary Tree]] carrying one extra promise: for **every** node, all values in its left subtree are smaller and all values in its right subtree are larger. The invariant is **recursive** — it must hold at every node, not just the root — and it is the entire reason a BST can search, insert, and delete in O(log N) on a balanced tree.

## Details

### The invariant
```
        5
      /   \
     1     8
    / \   / \
  -1   3 7   9
```
Every node's left subtree < node < right subtree, all the way down. Two consequences worth memorizing:

1. **Search prunes half the tree at every step** — the tree-shaped analogue of array binary search: compare, then discard one side entirely.
2. **In-order traversal emits values in sorted order.** This is the most-tested BST fact in interviews, and the basis of "validate a BST", "kth smallest element", and "BST → sorted list". See [[Tree Traversal]].

> [!warning] The invariant is subtree-wide, not parent-local
> *Claude addition.* Checking only `left.val < node.val < right.val` at each node is the standard wrong answer to *Validate BST* — it accepts trees where a deep left-subtree node exceeds an ancestor. Correct validation threads a `(min, max)` range down the recursion, or checks that in-order output is strictly increasing.

### Search
```java
// Source — recursive, O(log N) time and O(log N) space on a balanced tree
public static boolean searchBST(TreeNode node, int target) {
    if (node == null) return false;
    if (node.val == target) return true;
    if (target < node.val) return searchBST(node.left, target);
    else return searchBST(node.right, target);
}
```

```cpp
// Claude addition — iterative, O(log N) time and O(1) space.
// A BST search is tail-recursive, so the call stack buys nothing;
// prefer this when space is being graded.
bool searchBST(TreeNode* node, int target) {
    while (node) {
        if (node->val == target) return true;
        node = target < node->val ? node->left : node->right;
    }
    return false;
}
```

### Insert and delete
*Claude addition — the source asserts these are O(log N) average but never shows them.*

**Insert**: walk as if searching, then attach the new node at the `null` you fall off. A fresh node always lands as a leaf.

```cpp
TreeNode* insert(TreeNode* root, int val) {
    if (!root) return new TreeNode(val);
    if (val < root->val) root->left  = insert(root->left,  val);
    else if (val > root->val) root->right = insert(root->right, val);
    return root;                       // equal → no-op (no duplicates)
}
```

**Delete** has three cases, and the third is the one that gets missed:
1. **Leaf** — detach it.
2. **One child** — splice the child into the node's place.
3. **Two children** — replace the value with its **in-order successor** (the leftmost node of the right subtree) or predecessor, then delete *that* node, which by construction has at most one child.

### Complexity
| Operation | Balanced | Unbalanced (degenerate) |
|---|---|---|
| Search / insert / delete — time | **O(log N)** | **O(N)** |
| Recursive space | O(log N) | O(N) |
| Iterative space | O(1) | O(1) |
| In-order traversal | O(N) time | O(N) time |

### Balance is the catch
Nothing in the plain BST definition enforces balance. Insert `1, 2, 3, 4, 5` in order and you get a right-leaning chain — a linked list with extra pointers, O(N) per operation, O(N) stack depth on a recursive search. The O(log N) headline is only true for a **balanced** tree, which is why real systems use self-balancing variants (AVL, red-black — the mechanism behind C++ `std::map`/`std::set` and Java `TreeMap`) rather than a raw BST. This source does not cover them; that gap is flagged on [[Binary Trees & Binary Search Trees]].

### BST vs hashmap
*Claude addition.* A [[Hashmap Lookup Pattern|hashmap]] beats a BST on raw lookup (O(1) vs O(log N)) and is the right default. A BST earns its keep when you need **order**: sorted iteration, range queries, floor/ceiling, predecessor/successor, or kth-smallest — all of which a hash table cannot do without sorting everything first.

## Related
[[Binary Tree]] · [[Tree Traversal]] · [[Heap]] · [[Hashmap Lookup Pattern]] · [[Two Pointer Technique]] · [[DSA Patterns Overview]]

## Sources
- [[Binary Trees & Binary Search Trees]] — the recursive ordering invariant, recursive `searchBST`, balanced vs unbalanced complexity, and in-order-yields-sorted.
