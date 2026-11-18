---
type: source
area: sde
title: Binary Trees & Binary Search Trees
aliases: [Binary Trees & Binary Search Trees, AlgoMap Binary Trees, Greg Hogg Lecture 8]
tags: [dsa, trees, binary-tree, bst, traversal, recursion]
status: draft
source_type: article
url: https://algomap.io/lessons/binary-trees
author: AlgoMap.io / Greg Hogg
raw_path: raw/notes/DSA/Binary Trees and BST.md
ingested: 2026-08-01
created: 2026-08-01
updated: 2026-08-01
---

## TL;DR
AlgoMap's binary-tree lesson: a **binary tree** is a node-based hierarchy where each node has at most two children (left/right), and a **BST** adds the recursive ordering invariant *left subtree < node < right subtree*, which is what buys O(log N) search on a balanced tree. The bulk of the value is the **traversal taxonomy** — DFS in pre/in/post order (stack, explicit or via the call stack) and BFS/level-order (queue) — plus the complexity table for search and traversal. Accompanying Greg Hogg Lecture 8 code (Java) shows recursive pre/in-order, *iterative* pre-order, level-order, generic DFS search, and BST search.

## Key points
- **Structure & terminology.** Node (value + left/right pointers), root, leaf, parent, children, `null`/`None` for an absent child. A binary tree is a specialized **directed graph**.
- **Types named.** *Complete* (all levels full except possibly the last, filled left-to-right), *perfect* (all internal nodes have 2 children, all leaves on the same level), and *BST* (ordering invariant, holding recursively).
- **Two representations.** Linked nodes, or an **array with 1-based indexing**: node `i` has children at `2i` and `2i+1`. This is exactly the layout a [[Heap]] uses.
- **BST invariant → O(log N).** Search halves the space at each step on a balanced tree. Unbalanced, the tree degenerates to a linked list: **O(N)** time and **O(N)** stack space.
- **Traversals.** DFS = pre-order (node, left, right), in-order (left, node, right), post-order (left, right, node); **in-order on a BST emits sorted values**. BFS = level-order, top-to-bottom, queue-driven; the source flags it for layered processing and shortest-path.
- **Complexity table.** General-tree search O(N)/O(N). Balanced BST search O(log N)/O(log N); unbalanced O(N)/O(N). Any traversal (DFS or BFS) O(N) time, O(N) space worst case (call stack or queue).
- **Off-topic code block.** The first snippet is **Lecture 7 array binary search in C++**, not trees — classic target search plus a condition-based "first index where the predicate is true" variant. Noted here, not filed as its own page yet (see Gaps).

## Notable quotes / data
> "A **binary search tree** is a binary tree where the left subtree contains values less than the parent node, and the right subtree contains values greater than the parent node."

> "**Time Complexity (Unbalanced BST):** `O(N)` — resembles a linked list in the worst case."

> "The **height** of a binary tree is defined as the longest path from the root node to any leaf node, counted in terms of nodes... a **leaf** node has a height of 1."

> [!warning] Definition conflict — height
> This source counts height **in nodes** with a leaf at height **1**. The standard (CLRS) definition counts **edges**, making a leaf height **0** and a single-node tree height 0. LeetCode's *Maximum Depth of Binary Tree* counts **nodes**, so it agrees with this source numerically while using the word "depth". Off-by-one bugs live here — always pin down which convention a problem statement means. Recorded on [[Binary Tree]].

## Gaps this source leaves
- Claims BST **insert/delete** are O(log N) average but never shows either. Filled with a labeled addition on [[Binary Search Tree]].
- Describes **post-order** but never codes it. Filled with a labeled addition on [[Tree Traversal]].
- Gives only **recursive** BST search (O(log N) space); the iterative O(1)-space form is a labeled addition on [[Binary Search Tree]].
- Says nothing about **self-balancing** trees (AVL / red-black) — the thing that actually guarantees the O(log N) it advertises. Candidate for the next ingest.
- The C++ **binary search** code deserves its own concept page from a proper binary-search source (target search + the predicate/lower-bound "first true" form).
- All code here is **Java**; the rest of this wiki is C++. Equivalent C++ node definitions added on [[Binary Tree]].

## Touches
[[Binary Tree]] · [[Binary Search Tree]] · [[Tree Traversal]] · [[Stack]] · [[Queue]] · [[Heap]] · [[DSA Patterns Overview]]
