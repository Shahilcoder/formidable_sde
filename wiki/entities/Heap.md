---
type: entity
area: sde
title: Heap
aliases: [Heap, Binary Heap, Priority Queue]
tags: [dsa, data-structures, web-dev, trees]
status: draft
source_count: 2
created: 2026-07-12
updated: 2026-08-01
---

## Summary
A **heap** is a tree-based structure that keeps the min (or max) element at the root, giving O(log n) insert and extract-min/max and O(1) peek. It's the usual implementation of a **priority queue**.

## Details

### Structure
A binary heap is a **complete** [[Binary Tree]] — every level full except possibly the last, which fills left-to-right — which is exactly the shape that makes the **array representation** economical: with 1-based indexing, node `i` has children at `2i` and `2i+1` and its parent at `i/2`. No pointers, no wasted cells. Completeness also pins the height at O(log n), which is where the O(log n) insert/extract comes from.

Note the invariant is **weaker** than a [[Binary Search Tree]]'s: a heap only promises *parent beats child*, with no left-vs-right ordering. So a heap gives you the extreme element in O(1) but cannot do sorted iteration or search in O(log n) — [[Tree Traversal|in-order traversal]] of a heap yields nothing useful.
**Web use case:** serving the highest-priority item first — e.g. a list of people where premium users are bumped to the top of the queue so their work is processed first. Also: top-K queries, scheduling, merging sorted streams, and Dijkstra/A* frontiers.

A priority queue is the abstract "always give me the most important item next" interface; a binary heap is the common concrete data structure behind it.

## Related
[[Queue]] · [[Stack]] · [[Binary Tree]] · [[Binary Search Tree]] · [[Tree Traversal]] · [[DSA for Web Development]]

## Sources
- [[Bare Min DSA for WebDev]] — "list of people objects; someone got premium; put them at top of priority queue."
- [[Binary Trees & Binary Search Trees]] — the complete-binary-tree shape and the 1-based `2i` / `2i+1` array representation a heap is built on.
